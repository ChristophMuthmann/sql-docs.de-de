---
title: "Excel-Ziel | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.exceldest.f1"
helpviewer_keywords: 
  - "Ziele [Integration Services], Excel"
  - "Excel [Integration Services]"
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# Excel-Ziel
  Das Excel-Ziel lädt Daten in Arbeitsblätter oder Bereiche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappen.  
  
## Zugriffsmodi  
 Das Excel-Ziel stellt drei verschiedene Datenzugriffsmodi zum Laden von Daten bereit:  
  
-   Eine Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung. Bei der Abfrage kann es sich um eine parametrisierte Abfrage handeln.  
  
> [!IMPORTANT]  
>  In Excel entspricht ein Arbeitsblatt oder ein Bereich einer Tabelle oder Sicht. In den Listen der verfügbaren Tabellen im Quellen-Editor und Ziel-Editor für Excel werden nur vorhandene Arbeitsblätter (identifiziert durch das an den Arbeitsblattnamen angefügte $-Zeichen, wie z. B. Sheet1$) und benannte Bereiche (identifiziert durch das Fehlen des $-Zeichens, wie z. B. MyRange) angezeigt.  
  
## Überlegungen zur Verwendung  
 Der Excel-Verbindungs-Manager verwendet den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für Jet 4.0 und den unterstützenden Excel-ISAM-Treiber (Indexed Sequential Access Method, indizierte sequenzielle Zugriffsmethode), um sich mit Excel-Datenquellen zu verbinden und diese zu lesen und in sie zu schreiben.  
  
 In vielen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikeln ist das Verhalten dieses Anbieters und Treibers dokumentiert. Diese Artikel beziehen sich zwar nicht speziell auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder die Vorgängerversion Data Transformation Services, aber Sie sollten bestimmte Verhaltensweisen kennen, die zu unerwarteten Ergebnissen führen können. Allgemeine Informationen zu Verwendung und Verhalten des Excel-Treibers finden Sie unter [SO WIRD'S GEMACHT: Verwenden von ADO mit Excel-Daten von Visual Basic oder VBA](http://support.microsoft.com/kb/257819).  
  
 Die folgenden Verhaltensweisen des im Excel-Treiber enthaltenen Jet-Anbieters können zu unerwarteten Ergebnissen führen, wenn Daten in ein Excel-Ziel gespeichert werden.  
  
-   **Speichern von Textdaten**. Wenn der Excel-Treiber Textdatenwerte in ein Excel-Ziel speichert, wird vor den Text jeder Zelle das einfache Anführungszeichen (') gesetzt, um sicherzustellen, dass die gespeicherten Werte als Textwerte interpretiert werden. Wenn Sie andere Anwendungen verwenden bzw. entwickeln, die die gespeicherten Daten lesen oder verarbeiten, kann eine spezielle Verarbeitung des vor jedem Textwert gesetzten einfachen Anführungszeichens erforderlich sein.  
  
     Informationen dazu, wie Sie das Einschließen des einfachen Anführungszeichens vermeiden, finden Sie in diesem Blogpost: [Single quote is appended to all strings when data is transformed to excel when using Excel destination data flow component in SSIS package](http://go.microsoft.com/fwlink/?LinkId=400876)(Einzelnes Anführungszeichen wird an alle Zeichenfolgen angehängt, wenn Daten für Excel umgewandelt werden und die Excel-Ziel-Datenflusskomponente in SSIS verwendet wird), auf msdn.com.  
  
-   **Speichern von Memodaten (ntext)** Zum erfolgreichen Speichern von Zeichenfolgen mit mehr als 255 Zeichen in einer Excel-Spalte muss der Treiber den Datentyp der Zielspalte als **memo** und nicht als **string**erkennen. Wenn die Zieltabelle bereits Datenzeilen enthält, müssen die ersten Zeilen, die vom Treiber als Stichprobe genommen werden, mindestens eine Instanz eines Werts mit mehr als 255 Zeichen in der Memospalte enthalten. Wenn die Zieltabelle während des Paketentwurfs oder zur Laufzeit erstellt wird, muss die CREATE TABLE-Anweisung als Datentyp für die Memospalte LONGTEXT (oder eines der Synonyme) verwenden.  
  
-   **Datentypen**. Der Excel-Treiber erkennt nur einen begrenzten Satz von Datentypen. Beispielsweise werden alle numerischen Spalten als Werte mit doppelter Genauigkeit (DT_R8) interpretiert, und alle Zeichenfolgenspalten (außer Memospalten) werden als Unicode-Zeichenfolgen mit 255 Zeichen (DT_WSTR) interpretiert. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden die Excel-Datentypen folgendermaßen zugeordnet:  
  
    -   Numerisch – Gleitkommawert mit doppelter Genauigkeit (DT_R8)  
  
    -   Währung – Währung (DT_CY)  
  
    -   Boolesch – Boolesch (DT_BOOL)  
  
    -   Datum/Uhrzeit – **datetime** (DT_DATE)  
  
    -   Zeichenfolge – Unicode-Zeichenfolge, Länge 255 (DT_WSTR)  
  
    -   Memo – Unicode-Textstream (DT_NTEXT)  
  
-   **Datentyp- und Längenkonvertierungen**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden Datentypen nicht implizit konvertiert. Daher müssen Sie eventuell die Transformationen für abgeleitete Spalten und für die Datenkonvertierung verwenden, um Excel-Daten vor dem Laden in ein Nicht-Excel-Ziel explizit zu konvertieren bzw. um Nicht-Excel-Daten vor dem Laden in ein Excel-Ziel zu konvertieren. In diesem Fall kann es nützlich sein, das erste Paket mit dem Import/Export-Assistenten zu erstellen, mit dem die Konfiguration notwendiger Konvertierungen vorgenommen wird. Im Folgenden finden Sie einige Beispiele für ggf. erforderliche Konvertierungen:  
  
    -   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und Nicht-Unicode-Zeichenfolgenspalten mit bestimmten Codepages.  
  
    -   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten anderer Längen.  
  
    -   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderer Typen.  
  
## Konfiguration des Excel-Ziels  
 Das Excel-Ziel verwendet einen Excel-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle. Dieser Verbindungs-Manager gibt die zu verwendende Arbeitsmappendatei an. Weitere Informationen finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 Das Excel-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Ziel-Editor für Excel** festlegen können:  
  
-   [Ziel-Editor für Excel &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/excel-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für Excel &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/excel-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für Excel &#40;Seite Fehlerausgabe&#41;](../../integration-services/data-flow/excel-destination-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält alle Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Verwandte Aufgaben  
  
-   [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Verwandte Inhalte  
  
-   Blogeintrag [Excel in Integration Services, Part 1 of 3: Connections and Components](http://go.microsoft.com/fwlink/?LinkId=217674)auf dougbert.com  
  
-   Blogeintrag [Excel in Integration Services, Part 2 of 3: Tables and Data Types](http://go.microsoft.com/fwlink/?LinkId=217675)auf dougbert.com.  
  
-   Blogeintrag [Excel in Integration Services, Part 3 of 3: Issues and Alternatives](http://go.microsoft.com/fwlink/?LinkId=217676)auf dougbert.com.  
  
## Siehe auch  
 [Excel-Quelle](../../integration-services/data-flow/excel-source.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)   
 [Arbeiten mit Excel-Dateien mit dem Skripttask](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  