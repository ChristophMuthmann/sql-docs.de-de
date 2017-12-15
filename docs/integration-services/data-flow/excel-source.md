---
title: Excel-Quelle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: "60"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 61e28171171a822f25da6979340785bc5c114e1c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="excel-source"></a>Excel-Quelle
  Die Excel-Quelle extrahiert Daten aus Arbeitsblättern oder Bereichen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappen.  
  
 Die Excel-Quelle stellt vier verschiedene Datenzugriffsmodi zum Extrahieren von Daten bereit:  
  
-   Eine Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung. Bei der Abfrage kann es sich um eine parametrisierte Abfrage handeln.  
  
-   Die Ergebnisse einer SQL-Anweisung, die in einer Variablen gespeichert werden.  
  
> [!IMPORTANT]  
>  In Excel entspricht ein Arbeitsblatt oder ein Bereich einer Tabelle oder Sicht. Die Liste verfügbarer Tabellen im Quellen-Editor und Ziel-Editor für Excel zeigt vorhandene Arbeitsblätter (gekennzeichnet durch das an den Arbeitsblattnamen angefügte $-Zeichen, wie z. B. Sheet1$) und benannte Bereiche (gekennzeichnet durch das Fehlen des $-Zeichens, wie z. B. MyRange) an. Weitere Informationen finden Sie im Abschnitt mit Überlegungen zur Verwendung.  
  
 Die Excel-Quelle verwendet einen Excel-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle. Dieser Verbindungs-Manager gibt die zu verwendende Arbeitsmappendatei an. Weitere Informationen finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 Die Excel-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="usage-considerations"></a>Überlegungen zur Verwendung  
 Der Excel-Verbindungs-Manager verwendet den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für Jet 4.0 und den unterstützenden Excel-ISAM-Treiber (Indexed Sequential Access Method, indizierte sequenzielle Zugriffsmethode), um sich mit Excel-Datenquellen zu verbinden und diese zu lesen und in sie zu schreiben.  
  
 In vielen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikeln ist das Verhalten dieses Anbieters und Treibers dokumentiert. Diese Artikel beziehen sich zwar nicht speziell auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder die Vorgängerversion Data Transformation Services, aber Sie sollten bestimmte Verhaltensweisen kennen, die zu unerwarteten Ergebnissen führen können. Allgemeine Informationen zu Verwendung und Verhalten des Excel-Treibers finden Sie unter [SO WIRD'S GEMACHT: Verwenden von ADO mit Excel-Daten von Visual Basic oder VBA](http://support.microsoft.com/kb/257819).  
  
 Die folgenden Verhaltensweisen des Jet-Anbieters mit dem Excel-Treiber können zu unerwarteten Ergebnissen führen, wenn Daten aus einer Excel-Datenquelle gelesen werden.  
  
-   **Datenquellen**. Die Quelle von Daten in einer Excel-Arbeitsmappe kann ein Arbeitsblatt sein, an das das $-Zeichen angefügt werden muss (z. B. Sheet1$), oder ein benannter Bereich (z. B. MyRange). In einer SQL-Anweisung muss der Name eines Arbeitsblatts mit Trennzeichen versehen sein (z. B. [Sheet1$]), um Syntaxfehler durch das $-Zeichen zu vermeiden. Der Abfrage-Generator fügt diese Trennzeichen automatisch hinzu. Wenn Sie ein Arbeitsblatt angeben, liest der Treiber den zusammenhängenden Zellenblock ab der ersten nicht leeren Zelle in der linken oberen Ecke des Arbeitsblatts oder Bereichs. Deshalb sind leere Zeilen in den Quelldaten oder eine leere Zeile zwischen Titel- oder Kopfzeilen und den Datenzeilen nicht zulässig.  
  
-   **Fehlende Werte**. Der Excel-Treiber liest eine bestimmte Anzahl von Zeilen (standardmäßig 8 Zeilen) in der angegebenen Quelle, um den Datentyp jeder Spalte zu ermitteln. Wenn eine Spalte offensichtlich gemischte Datentypen enthält, insbesondere eine Mischung aus numerischen Daten und Textdaten, entscheidet der Treiber zugunsten des Mehrheitsdatentyps und gibt in Zellen mit Daten des anderen Datentyps NULL-Werte zurück. (In einer unentschiedenen Situation hat der numerische Datentyp Vorrang.) Die meisten Zellenformatierungsoptionen im Excel-Arbeitsblatt scheinen keinen Einfluss auf diese Datentypfestlegung zu haben. Sie können dieses Verhalten des Excel-Treibers ändern, indem Sie den Importmodus angeben. Um den Importmodus anzugeben, fügen Sie **IMEX=1** dem Wert für erweiterte Eigenschaften in der Verbindungszeichenfolge des Excel-Verbindungs-Managers im Fenster **Eigenschaften** hinzu. Weitere Informationen finden Sie unter [PRB: Mithilfe von DAO OpenRecordset als NULL zurückgegebene Excel-Werte](http://support.microsoft.com/kb/194124)(maschinelle Übersetzung).  
  
-   **Abgeschnittener Text**. Wenn der Anbieter bestimmt, dass eine Excel-Spalte Textdaten enthält, wählt der Treiber den Datentyp (string- oder memo-Datentyp) auf Basis des längsten Werts, der als Stichprobe genommenen wird. Wenn der Treiber in den als Stichprobe genommenen Zeilen keine Werte mit mehr als 255 Zeichen findet, wird die Spalte nicht als Memospalte, sondern als Zeichenfolgenspalte mit 255 Zeichen behandelt. Deshalb können Werte, die länger als 255 Zeichen sind, abgeschnitten werden. Um Daten aus einer Memospalte ohne das Abschneiden von Daten zu importieren, müssen Sie sicherstellen, dass die Memospalte mindestens eine der als Stichprobe genommenen Zeilen einen Wert mit mehr als 255 Zeichen enthält, oder Sie müssen die vom Treiber als Stichprobe genommene Zeilenanzahl erhöhen, um solch eine Zeile einzuschließen. Sie können die Zeilenanzahl in der Stichprobe steigern, indem Sie den Wert von **TypeGuessRows** unter dem Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** erhöhen. Weitere Informationen finden Sie unter [PRB: Übertragung von Daten aus Jet 4.0 OLEDB-Quelle schlägt mit Pufferüberlauffehler fehl](http://support.microsoft.com/kb/281517).  
  
-   **Datentypen**. Der Excel-Treiber erkennt nur einen begrenzten Satz von Datentypen. Beispielsweise werden alle numerischen Spalten als Werte mit doppelter Genauigkeit (DT_R8) interpretiert, und alle Zeichenfolgenspalten (außer Memospalten) werden als Unicode-Zeichenfolgen mit 255 Zeichen (DT_WSTR) interpretiert. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden die Excel-Datentypen folgendermaßen zugeordnet:  
  
    -   Numerisch – Gleitkommawert mit doppelter Genauigkeit (DT_R8)  
  
    -   Währung – Währung (DT_CY)  
  
    -   Boolesch – Boolesch (DT_BOOL)  
  
    -   Datum/Uhrzeit – **datetime** (DT_DATE)  
  
    -   Zeichenfolge – Unicode-Zeichenfolge, Länge 255 (DT_WSTR)  
  
    -   Memo – Unicode-Textdatenstrom (DT_NTEXT)  
  
-   **Datentyp- und Längenkonvertierungen**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden Datentypen nicht implizit konvertiert. Daher müssen Sie u. U. die Transformationen für abgeleitete Spalten oder für die Datenkonvertierung verwenden, um Excel-Daten vor dem Laden in ein Nicht-Excel-Ziel explizit zu konvertieren bzw. um Nicht-Excel-Daten vor dem Laden in ein Excel-Ziel zu konvertieren. In diesem Fall kann es nützlich sein, das erste Paket mit dem Import/Export-Assistenten zu erstellen, mit dem die Konfiguration notwendiger Konvertierungen vorgenommen wird. Im Folgenden finden Sie einige Beispiele für ggf. erforderliche Konvertierungen:  
  
    -   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und Nicht-Unicode-Zeichenfolgenspalten mit bestimmten Codepages  
  
    -   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten unterschiedlicher Länge  
  
    -   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderen Typs  
  
## <a name="excel-source-configuration"></a>Konfiguration der Excel-Quelle  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält alle Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Informationen zum Durchlaufen einer Gruppe von Excel-Dateien finden Sie unter [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Quellen-Editor für Excel (Seite Verbindungs-Manager)
  Mithilfe des Knotens **Verbindungs-Manager** im Dialogfeld **Quellen-Editor für Excel** können Sie eine [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappe für die Quelle auswählen. Die Excel-Quelle liest Daten aus einem Arbeitsblatt oder dem benannten Bereich einer vorhandenen Arbeitsmappe.  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft der Excel-Quelle ist nicht im **Quellen-Editor für Excel**verfügbar, kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt Excel-Quelle von [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Excel-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Excel-Verbindungs-Manager** eine neue Verbindung.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Wert|Description|  
|-----------|-----------------|  
|Tabelle oder Sicht|Ruft Daten aus einem Arbeitsblatt oder dem benannten Bereich einer Excel-Datei ab.|  
|Variable für Tabellenname oder Sichtname|Geben Sie den Namen des Arbeitsblatts oder Bereichs in einer Variablen an.<br /><br /> **Relevante Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL-Befehl|Ruft mithilfe einer SQL-Abfrage Daten aus einer Excel-Datei ab. |  
|SQL-Befehl aus Variable|Gibt den SQL-Abfragetext in einer Variablen an.|  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Liste der in der Excel-Arbeitsmappe verfügbaren Objekte den Namen des Arbeitsblatts oder des benannten Bereichs aus.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen des Arbeitsblatts oder des benannten Bereichs enthält.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text der SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken. Wahlweise können Sie auch nach der Datei mit dem Abfragetext suchen, indem Sie auf **Durchsuchen**klicken.  
  
 **Parameter**  
 Wenn Sie eine parametrisierte Abfrage eingeben und im Abfragetext ? als Parameterplatzhalter verwenden, können Sie den Paketvariablen mithilfe des Dialogfelds **Abfrageparameter festlegen** Abfrageeingabeparameter zuordnen.  
  
 **Build query**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Datenzugriffsmodus = SQL-Befehl aus Variable  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Text für die SQL-Abfrage enthält.  
  
## <a name="excel-source-editor-columns-page"></a>Quellen-Editor für Excel (Seite Spalten)
  Mithilfe der Seite **Spalten** des Dialogfelds **Quellen-Editor für Excel** können Sie jeder externen (Quell-)Spalte eine Ausgabespalte zuordnen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren externen Spalten an. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden.  
  
 **Externe Spalte**  
 Zeigt die externen (Quell-)Spalten in der Reihenfolge an, in der sie von dem Task gelesen werden. Sie können die Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der oben besprochenen Tabelle löschen. Wählen Sie anschließend die externen Spalten in einer anderen Reihenfolge aus der Liste aus.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
## <a name="excel-source-editor-error-output-page"></a>Quellen-Editor für Excel (Seite Fehlerausgabe)
  Mithilfe der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für Excel** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.  
  
### <a name="options"></a>enthalten  
 **Eingabe oder Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für Excel** auf der Seite **Verbindungs-Manager**ausgewählt wurden.  
  
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
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Blogeintrag [Importing data from 64-bit Excel in SSIS](http://go.microsoft.com/fwlink/?LinkId=217673)(Importieren von Daten aus 64-Bit-Excel in SSIS) auf hrvoje.piasevoli.com  
  
-   Blogeintrag [Excel in Integration Services, Part 1 of 3: Connections and Components](http://go.microsoft.com/fwlink/?LinkId=217674)auf dougbert.com  
  
-   Blogeintrag [Excel in Integration Services, Part 2 of 3: Tables and Data Types](http://go.microsoft.com/fwlink/?LinkId=217675)auf dougbert.com.  
  
-   Blogeintrag [Excel in Integration Services, Part 3 of 3: Issues and Alternatives](http://go.microsoft.com/fwlink/?LinkId=217676)auf dougbert.com.  
  
  
