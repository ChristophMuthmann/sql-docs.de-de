---
title: Excel-Ziel | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 69a0a8b907fcb45cf6ecd0576fb6fba04775d237
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="excel-destination"></a>Excel-Ziel
  Das Excel-Ziel lädt Daten in Arbeitsblätter oder Bereiche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappen.  
  
## <a name="access-modes"></a>Zugriffsmodi  
 Das Excel-Ziel stellt drei verschiedene Datenzugriffsmodi zum Laden von Daten bereit:  
  
-   Eine Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung. Bei der Abfrage kann es sich um eine parametrisierte Abfrage handeln.  
  
> [!IMPORTANT]  
>  In Excel entspricht ein Arbeitsblatt oder ein Bereich einer Tabelle oder Sicht. In den Listen der verfügbaren Tabellen im Quellen-Editor und Ziel-Editor für Excel werden nur vorhandene Arbeitsblätter (identifiziert durch das an den Arbeitsblattnamen angefügte $-Zeichen, wie z. B. Sheet1$) und benannte Bereiche (identifiziert durch das Fehlen des $-Zeichens, wie z. B. MyRange) angezeigt.  
  
## <a name="usage-considerations"></a>Überlegungen zur Verwendung  
 Der Excel-Verbindungs-Manager verwendet den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für Jet 4.0 und den unterstützenden Excel-ISAM-Treiber (Indexed Sequential Access Method, indizierte sequenzielle Zugriffsmethode), um sich mit Excel-Datenquellen zu verbinden und diese zu lesen und in sie zu schreiben.  
  
 In vielen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikeln ist das Verhalten dieses Anbieters und Treibers dokumentiert. Diese Artikel beziehen sich zwar nicht speziell auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder die Vorgängerversion Data Transformation Services, aber Sie sollten bestimmte Verhaltensweisen kennen, die zu unerwarteten Ergebnissen führen können. Allgemeine Informationen zu Verwendung und Verhalten des Excel-Treibers finden Sie unter [SO WIRD'S GEMACHT: Verwenden von ADO mit Excel-Daten von Visual Basic oder VBA](http://support.microsoft.com/kb/257819).  
  
 Die folgenden Verhaltensweisen des im Excel-Treiber enthaltenen Jet-Anbieters können zu unerwarteten Ergebnissen führen, wenn Daten in ein Excel-Ziel gespeichert werden.  
  
-   **Speichern von Textdaten**. Wenn der Excel-Treiber Textdatenwerte in ein Excel-Ziel speichert, wird vor den Text jeder Zelle das einfache Anführungszeichen (') gesetzt, um sicherzustellen, dass die gespeicherten Werte als Textwerte interpretiert werden. Wenn Sie andere Anwendungen verwenden bzw. entwickeln, die die gespeicherten Daten lesen oder verarbeiten, kann eine spezielle Verarbeitung des vor jedem Textwert gesetzten einfachen Anführungszeichens erforderlich sein.  
  
     Informationen dazu, wie Sie das Einschließen des einfachen Anführungszeichens vermeiden, finden Sie in diesem Blogpost: [Single quote is appended to all strings when data is transformed to excel when using Excel destination data flow component in SSIS package](http://go.microsoft.com/fwlink/?LinkId=400876)(Einzelnes Anführungszeichen wird an alle Zeichenfolgen angehängt, wenn Daten für Excel umgewandelt werden und die Excel-Ziel-Datenflusskomponente in SSIS verwendet wird), auf msdn.com.  
  
-   **Speichern von Memodaten (ntext)** Zum erfolgreichen Speichern von Zeichenfolgen mit mehr als 255 Zeichen in einer Excel-Spalte muss der Treiber den Datentyp der Zielspalte als **memo** und nicht als **string**erkennen. Wenn die Zieltabelle bereits Datenzeilen enthält, müssen die ersten Zeilen, die vom Treiber als Stichprobe genommen werden, mindestens eine Instanz eines Werts mit mehr als 255 Zeichen in der Memospalte enthalten. Wenn die Zieltabelle während des Paketentwurfs oder zur Laufzeit erstellt wird, muss die CREATE TABLE-Anweisung als Datentyp für die Memospalte LONGTEXT (oder eines der Synonyme) verwenden.  
  
-   **Datentypen**. Der Excel-Treiber erkennt nur einen begrenzten Satz von Datentypen. Beispielsweise werden alle numerischen Spalten als Werte mit doppelter Genauigkeit (DT_R8) interpretiert, und alle Zeichenfolgenspalten (außer Memospalten) werden als Unicode-Zeichenfolgen mit 255 Zeichen (DT_WSTR) interpretiert. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden die Excel-Datentypen folgendermaßen zugeordnet:  
  
    -   Numerisch – Gleitkommawert mit doppelter Genauigkeit (DT_R8)  
  
    -   Währung – Währung (DT_CY)  
  
    -   Boolesch – Boolesch (DT_BOOL)  
  
    -   Datum/Uhrzeit –     **datetime** (DT_DATE)  
  
    -   Zeichenfolge – Unicode-Zeichenfolge, Länge 255 (DT_WSTR)  
  
    -   Memo – Unicode-Textstream (DT_NTEXT)  
  
-   **Datentyp- und Längenkonvertierungen**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden Datentypen nicht implizit konvertiert. Daher müssen Sie eventuell die Transformationen für abgeleitete Spalten und für die Datenkonvertierung verwenden, um Excel-Daten vor dem Laden in ein Nicht-Excel-Ziel explizit zu konvertieren bzw. um Nicht-Excel-Daten vor dem Laden in ein Excel-Ziel zu konvertieren. In diesem Fall kann es nützlich sein, das erste Paket mit dem Import/Export-Assistenten zu erstellen, mit dem die Konfiguration notwendiger Konvertierungen vorgenommen wird. Im Folgenden finden Sie einige Beispiele für ggf. erforderliche Konvertierungen:  
  
    -   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und Nicht-Unicode-Zeichenfolgenspalten mit bestimmten Codepages.  
  
    -   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten anderer Längen.  
  
    -   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderer Typen.  
  
## <a name="configuration-of-the-excel-destination"></a>Konfiguration des Excel-Ziels  
 Das Excel-Ziel verwendet einen Excel-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle. Dieser Verbindungs-Manager gibt die zu verwendende Arbeitsmappendatei an. Weitere Informationen finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 Das Excel-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält alle Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Blogeintrag [Excel in Integration Services, Part 1 of 3: Connections and Components](http://go.microsoft.com/fwlink/?LinkId=217674)auf dougbert.com  
  
-   Blogeintrag [Excel in Integration Services, Part 2 of 3: Tables and Data Types](http://go.microsoft.com/fwlink/?LinkId=217675)auf dougbert.com.  
  
-   Blogeintrag [Excel in Integration Services, Part 3 of 3: Issues and Alternatives](http://go.microsoft.com/fwlink/?LinkId=217676)auf dougbert.com.  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Ziel-Editor für Excel (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für Excel** können Sie Informationen zur Datenquelle angeben und eine Vorschau der Ergebnisse anzeigen. Das Excel-Ziel lädt Daten in ein Arbeitsblatt oder einen benannten Bereich einer [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappe.  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft des Excel-Ziels ist nicht im **Ziel-Editor für Excel**verfügbar, kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Darüber hinaus sind bestimmte Optionen für schnelles Laden nur im Dialogfeld **Erweiterter Editor**verfügbar. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Excel-Ziel von [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Excel-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Excel-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Excel-Verbindungs-Manager** eine neue Verbindung.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Tabelle oder Sicht|Lädt Daten aus einem Arbeitsblatt oder dem benannten Bereich einer Excel-Datenquelle.|  
|Variable für Tabellenname oder Sichtname|Geben Sie den Namen des Arbeitsblatts oder Bereichs in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL-Befehl|Lädt Daten mithilfe einer SQL-Abfrage in das Excel-Ziel.|  
  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Dropdownliste das Excel-Ziel aus. Wenn die Liste leer ist, klicken Sie auf **Neu**.  
  
 **Neu**  
 Klicken Sie auf **Neu** , um das Dialogfeld **Tabelle erstellen** zu öffnen. Wenn Sie auf **OK**klicken, erstellt das Dialogfeld die Excel-Datei, auf die der **Excel-Verbindungs-Manager** zeigt.  
  
 **Vorhandene Daten anzeigen**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
> [!WARNING]  
>  Wenn der ausgewählte **Excel-Verbindungs-Manager** auf eine nicht vorhandene Excel-Datei zeigt, wird beim Klicken auf diese Schaltfläche eine Fehlermeldung angezeigt.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Liste der in der Datenquelle verfügbaren Objekte den Namen des Arbeitsblatts oder des benannten Bereichs aus.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen des Arbeitsblatts oder des benannten Bereichs enthält.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken. Wahlweise können Sie auch nach der Datei suchen, die den Abfragetext enthält, indem Sie auf **Durchsuchen**klicken.  
  
 **Abfrage erstellen**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
## <a name="excel-destination-editor-mappings-page"></a>Ziel-Editor für Excel (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für Excel** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten in der Tabelle Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten in der Tabelle Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigen Sie die in obiger Tabelle ausgewählten Eingabespalten an. Die Zuordnungen können Sie mithilfe der Liste **Verfügbare Eingabespalten**ändern.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, und ob sie zugeordnet sind.  
  
## <a name="excel-destination-editor-error-output-page"></a>Ziel-Editor für Excel (Seite Fehlerausgabe)
  Auf der Seite **Erweitert** in **Ziel-Editor für Excel** können Sie die Optionen für die Fehlerbehandlung angeben.  
  
### <a name="options"></a>enthalten  
 **Eingabe oder Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für Excel** im Knoten **Verbindungs-Manager**ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Description**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="see-also"></a>Siehe auch  
 [Excel-Quelle](../../integration-services/data-flow/excel-source.md)   
 [Integrationsservices &#40; SSIS &#41; Variablen](../../integration-services/integration-services-ssis-variables.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)   
 [Working with Excel Files with the Script Task](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
