---
title: "Verbindungs-Manager-Editor f&#252;r mehrere Flatfiles (Seite Erweitert) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.multifile.advanced.f1"
helpviewer_keywords: 
  - "Verbindungs-Manager-Editor für mehrere Flatfiles"
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# Verbindungs-Manager-Editor f&#252;r mehrere Flatfiles (Seite Erweitert)
  Legen Sie mithilfe der Seite **Erweitert** im Dialogfeld **Verbindungs-Manager-Editor für mehrere Flatfiles** Eigenschaften wie den Datentyp und Trennzeichen für jede einzelne Spalte in den Textdateien fest, mit denen der Verbindungs-Manager für Flatfiles eine Verbindung herstellt.  
  
 Standardmäßig beträgt die Länge von Zeichenfolgenspalten 50 Zeichen. Sie können Beispieldaten auswerten und die Länge dieser Spalten automatisch ändern, um zu verhindern, dass Daten abgeschnitten werden oder extrem breite Spalten entstehen. Sie können darüber hinaus andere Metadaten aktualisieren, um Kompatibitlität mit Zielspalten zu aktivieren. Sie können beispielsweise den Datentyp einer Spalte, die nur ganzzahlige Daten enthält, in einen numerischen Datentyp ändern, z. B. DT_I2.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für den Verbindungs-Manager für mehrere Flatfiles im Workflow an. Der eingegebene Name wird im Bereich **Verbindungs-Manager** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers angezeigt.  
  
 **Description**  
 Beschreiben Sie den Verbindungs-Manager. Die bewährte Methode ist hierbei, den Verbindungs-Manager zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Konfigurieren Sie die Eigenschaften für jede Spalte.**  
 Wählen Sie eine Spalte im linken Bereich, um im rechten Bereich ihre Eigenschaften anzuzeigen. In der folgenden Tabelle werden die Datentypeigenschaften beschrieben. Einige der aufgeführten Eigenschaften können nur für einige Flatfileformate konfiguriert werden.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**ColumnType**|Gibt an, ob eine Spalte getrennt ist, eine feste Breite hat bzw. einen unregelmäßigen rechten Rand aufweist. Diese Eigenschaft ist schreibgeschützt. Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen abgeschlossen.|  
|**OutputColumnWidth**|Gibt an, welcher Wert als Anzahl von Bytes gespeichert werden soll; bei Unicode-Dateien wird dieser Wert als Zeichenanzahl angezeigt. Im Datenflusstask dient dieser Wert dem Festlegen der Breite der Ausgabespalte für die Flatfilequelle.<br /><br /> Hinweis: Im Objektmodell heißt diese Eigenschaft MaximumWidth.|  
|**DataType**|Wählen Sie eine Option aus der Liste der verfügbaren Datentypen aus. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Gibt an, ob Textdaten mit einem Textqualifiziererzeichen gekennzeichnet werden:<br /><br /> **True**: Die Textdaten in der Flatfile sind gekennzeichnet.<br /><br /> **False**: Die Textdaten in der Flatfile sind nicht gekennzeichnet.|  
|**Name**|Geben Sie einen Spaltennamen an. Standardwert ist eine nummerierte Liste mit Spalten; Sie können jedoch einen eindeutigen, beschreibenden Namen auswählen.|  
|**DataScale**|Gibt die Skala numerischer Daten an. Skala heißt in diesem Fall die Anzahl der Dezimalstellen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Wählen Sie eine Option aus der Liste der verfügbaren Spaltentrennzeichen aus. Dabei sollten Sie Spaltentrennzeichen auswählen, deren Auftreten als Zeichen im Text unwahrscheinlich ist. Bei Spalten fester Breite wird dieser Wert ignoriert.<br /><br /> **{CR}{LF}** – Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.<br /><br /> **{CR}** – Als Trennzeichen für Spalten dient ein Wagenrücklauf.<br /><br /> **{LF}** – Als Trennzeichen für Spalten dient ein Zeilenvorschub.<br /><br /> **Semikolon {;}** – Als Trennzeichen für Spalten dient ein Semikolon.<br /><br /> **Doppelpunkt {:}** – Als Trennzeichen für Spalten dient ein Doppelpunkt.<br /><br /> **Komma {,}** – Als Trennzeichen für Spalten dient ein Komma.<br /><br /> **Tabulator {t}** – Als Trennzeichen für Spalten dient ein Tabulator.<br /><br /> **Senkrechter Strich {&#124;}** – Als Trennzeichen für Spalten dient ein senkrechter Strich.|  
|**DataPrecision**|Gibt die Präzision numerischer Daten an. Präzision heißt in diesem Fall die Anzahl der Stellen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Gibt an, welcher Wert als Anzahl von Bytes gespeichert werden soll; bei Unicode-Dateien wird dieser Wert als Zeichenanzahl angezeigt. Bei mit Trennzeichen versehenen Spalten wird dieser Wert ignoriert.<br /><br /> **Hinweis:** Im Objektmodell heißt diese Eigenschaft ColumnWidth.|  
  
 **Neu**  
 Durch Klicken auf **Neu** fügen Sie eine neue Spalte hinzu. Die neue Spalten wird beim Klicken auf **Neu** standardmäßig am Ende der Liste hinzugefügt. Ferner sind für die Schaltfläche folgende, über die Dropdownliste auswählbare Optionen verfügbar.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Spalte hinzufügen**|Fügt am Ende der Liste eine neue Spalte hinzu.|  
|**Einfügen vor**|Fügt vor der ausgewählten Spalte eine neue Spalte ein.|  
|**Einfügen nach**|Fügt nach der ausgewählten Spalte eine neue Spalte ein.|  
  
 **Delete**  
 Wählen Sie eine Spalte aus, und entfernen Sie sie dann, indem Sie auf **Löschen** klicken.  
  
 **Typen vorschlagen**  
 Im Dialogfeld **Spaltentypen vorschlagen** können Sie die Beispieldaten in der ersten ausgewählten Datei auswerten, um Vorschläge für den Datentyp und die -länge der einzelnen Spalten zu erhalten. Weitere Informationen finden Sie unter [Referenz zur Benutzeroberfläche des Dialogfelds „Spaltentypen vorschlagen“](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Spalten“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Verbindungs-Manager-Editor für mehrere Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  