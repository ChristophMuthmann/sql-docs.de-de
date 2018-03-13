---
title: "Verbindungs-Manager für mehrere Flatfiles | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53e7c263916e9a07504fea6b9756f034e8e570fd
ms.sourcegitcommit: 657d18fc805512c9574b2fe7451310601b9d78cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2018
---
# <a name="multiple-flat-files-connection-manager"></a>Verbindungs-Manager für mehrere Flatfiles
  Mit einem Verbindungs-Manager für mehrere Flatfiles kann ein Paket auf Daten in mehreren Flatfiles zugreifen. Eine Flatfilequelle kann beispielsweise einen Verbindungs-Manager für mehrere Flatfiles verwenden, wenn sich der Datenflusstask in einem Schleifencontainer wie dem For-Schleifencontainer befindet. In jeder Schleife des Containers werden von der Flatfilequelle Daten vom nächsten Dateinamen geladen, der vom Verbindungs-Manager für mehrere Flatfiles bereitgestellt wird.  
  
 Wenn Sie einem Paket einen Verbindungs-Manager für mehrere Flatfiles hinzufügen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Verbindung für mehrere Flatfiles aufgelöst wird, die Eigenschaften im Verbindungs-Manager für mehrere Flatfiles festlegt und der **Connections** -Sammlung des Pakets die Verbindung für mehrere Flatfiles hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **MULTIFLATFILE**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen Verbindungs-Manager für mehrere Flatfiles zu konfigurieren:  
  
-   Geben Sie die Dateien, das Gebietsschema und die Codepage an, die Sie verwenden möchten. Mithilfe des Gebietsschemas werden gebietsschemabezogene Daten interpretiert, wie z. B. Datumsangaben, und mithilfe der Codepage werden Zeichenfolgendaten in Unicode-Daten konvertiert.  
  
-   Geben Sie das Dateiformat an. Sie können ein Format mit Trennzeichen, fester Breite oder rechtem Flatterrand verwenden.  
  
-   Geben Sie eine Kopfzeile, eine Datenzeile und Spaltentrennzeichen an. Spaltentrennzeichen können auf Dateiebene festgelegt und auf Spaltenebene überschrieben werden.  
  
-   Zeigen Sie an, ob die erste Zeile in den Dateien Spaltennamen enthalten.  
  
-   Geben Sie ein Textqualifiziererzeichen an. Für jede Spalte kann die Erkennung eines Textqualifizierers konfiguriert werden.  
  
-   Legen Sie Eigenschaften wie z. B. den Namen, den Datentyp und die maximale Breite für einzelne Spalten fest.  
  
 Wenn der Verbindungs-Manager für mehrere Flatfiles auf mehrere Dateien verweist, werden die Pfade der Dateien durch einen senkrechten Strich (|) getrennt. Die **ConnectionString** -Eigenschaft des Verbindungs-Managers hat folgendes Format:  
  
 \<*Pfad*>|\<*Pfad*>  
  
 Mehrere Dateien können Sie auch mithilfe von Platzhalterzeichen angeben. Wenn z.B. auf alle Textdateien auf Laufwerk C verwiesen werden soll, kann der Wert der **ConnectionString** -Eigenschaft auf C:\\*.txt festgelegt werden.  
  
 Falls ein Verbindungs-Manager für Flatfiles auf mehrere Dateien verweist, müssen alle Dateien das gleiche Format aufweisen.  
  
 Der Verbindungs-Manager für mehrere Flatfiles legt die Länge von Zeichenfolgenspalten standardmäßig auf 50 Zeichen fest. Sie können im Dialogfenster **Verbindungs-Manager-Editor für mehrere Flatfiles** Beispieldaten auswerten und automatisch die Länge dieser Spalten ändern, um zu vermeiden, dass Daten abgeschnitten werden oder die Spaltenbreite überschritten wird. Es sei denn, Sie ändern die Spaltenlänge in einer Flatfilequelle oder in einer Transformation. Dann bleibt die Spaltenlänge der Zeichenfolgenspalte im gesamten Datenfluss gleich. Wenn diese Spalten Zielspalten zugeordnet sind, die schmaler sind, werden in der Benutzeroberfläche Warnungen angezeigt. Darüber hinaus können aufgrund der abgeschnittenen Daten zur Laufzeit Fehler angezeigt werden. Sie können im Verbindungs-Manager für Flatfiles, in der Flatfilequelle oder in einer Transformation die Größe der Spalten auf die Größe der Zielspalten ändern. Legen Sie zum Ändern der Länge von Ausgabespalten auf der Registerkarte **Eingabe- und Ausgabeeigenschaften** im Dialogfeld **Erweiterter Editor** die **Length** -Eigenschaft der Ausgabespalte fest.  
  
 Wenn Sie die Spaltenlängen im Verbindungs-Manager für mehrere Flatfiles aktualisieren, nachdem Sie die Flatfilequelle, die den Verbindungs-Manager verwendet, hinzugefügt und geändert haben, ist das manuelle Ändern der Ausgabespaltengröße in der Flatfilequelle nicht erforderlich. Wenn Sie das Dialogfeld **Flatfilequelle** öffnen, stellt die Flatfilequelle eine Option zum Synchronisieren der Spaltenmetadaten bereit.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Konfiguration des Verbindungs-Managers für mehrere Flatfiles  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Verbindungs-Manager-Editor für mehrere Flatfiles (Seite Allgemein)
  Um eine Gruppe von Dateien im selben Datenformat auszuwählen und das entsprechende Datenformat anzugeben, verwenden Sie im Dialogfeld **Verbindungs-Manager-Editor für mehrere Flatfiles** die Seite **Allgemein** . Durch eine Verbindung für mehrere Flatfiles kann von einem Paket eine Verbindung zu einer Gruppe von Textdateien im selben Format hergestellt werden.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Verbindung für mehrere Flatfiles im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Die bewährte Methode ist hierbei, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Dateinamen**  
 Geben Sie den Pfad und den Dateinamen ein, die für die Verbindung für mehrere Flatfiles verwendet werden sollen. Verwenden Sie zum Angeben mehrerer Dateien Platzhalterzeichen, wie in „C:\\*.txt“, oder verwenden Sie den senkrechten Strich (|), um die verschiedenen angegebenen Dateinamen voneinander zu trennen. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
 **Durchsuchen**  
 Wechseln Sie in das Verzeichnis mit den Dateinamen, die bei der Verbindung für mehrere Flatfiles verwendet werden sollen. Sie können mehrere Dateien auswählen. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
 **Gebietsschema**  
 Geben Sie den Ort an, um Informationen zu Bestellungen und zur Datums- und Zeitkonvertierung bereitzustellen.  
  
 **Unicode**  
 Gibt an, ob Unicode verwendet werden soll. Bei Verwendung von Unicode wird keine Codepage angegeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Gibt an, ob die Datei Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet. Alle Dateien müssen dasselbe Datenformat aufweisen.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Die Trennung von Spalten erfolgt durch Trennzeichen. Welche Trennzeichen dies sind, wird auf der Seite **Spalten** angegeben.|  
|Feste Breite|Die Spalten weisen eine feste Breite auf, die auf der Seite **Spalten** durch Ziehen der Markierungslinien angegeben wird.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das auf der Seite **Spalten** angegebene Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Gibt die zu verwendenden Textqualifizierer an. Sie können beispielsweise angeben, dass Text in Anführungszeichen eingeschlossen werden soll.  
  
 **Kopfzeilentrennzeichen**  
 Wählen Sie aus einer Liste mit Trennzeichen für Kopfzeilen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Kopfzeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Kopfzeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Kopfzeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Kopfzeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Kopfzeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Kopfzeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Kopfzeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Kopfzeilen dient ein senkrechter Strich.|  
  
 **Auszulassende Kopfzeilen**  
 Geben Sie nach Möglichkeit die Anzahl der auszulassenden Kopfzeilen an.  
  
 **Spaltennamen in der ersten Datenzeile**  
 Gibt an, ob in der ersten Datenzeile Spaltennamen erwartet werden bzw. bereitzustellen sind.  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>Verbindungs-Manager-Editor für mehrere Flatfiles (Seite Spalten)
  Verwenden Sie den Knoten **Spalten** im Dialogfeld **Verbindungs-Manager-Editor für mehrere Flatfiles** , um die Zeilen- und Spalteninformationen anzugeben und eine Vorschau der ersten ausgewählten Datei anzuzeigen.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Verbindung für mehrere Flatfiles im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Es ist eine bewährte Methode, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und einfacher zu verwalten sind.  
  
### <a name="flat-file-format-dynamic-options"></a>Flatfileformat (dynamische Optionen)  
  
#### <a name="format--delimited"></a>Format = Mit Trennzeichen  
 **Zeilentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Zeilentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Zeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Zeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Zeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Zeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Zeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Zeilen dient ein senkrechter Strich.|  
  
 **Spaltentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Spaltentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Spalten dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Spalten dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Spalten dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Spalten dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Spalten dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Spalten dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Spalten dient ein senkrechter Strich.|  
  
 **Spalten zurücksetzen**  
 Entfernt alle bis auf die ursprünglichen Spalten, wenn Sie auf **Spalten zurücksetzen**klicken.  
  
#### <a name="format--fixed-width"></a>Format = Feste Breite  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilenbreite**  
 Geben Sie erst die Länge der Zeile an, bevor Sie einzelnen Spalten Trennzeichen hinzufügen. Sie können auch die vertikale Linie im Vorschaufenster verschieben, um das Zeilenende zu kennzeichnen. Der Wert der Zeilenbreite wird automatisch aktualisiert.  
  
 **Spalten zurücksetzen**  
 Entfernt alle bis auf die ursprünglichen Spalten, wenn Sie auf **Spalten zurücksetzen**klicken.  
  
#### <a name="format--ragged-right"></a>Format = Rechter Flatterrand  
  
> [!NOTE]  
>  Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.  
  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Zeilentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Zeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Zeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Zeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Zeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Zeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Zeilen dient ein senkrechter Strich.|  
  
 **Spalten zurücksetzen**  
 Entfernt alle bis auf die ursprünglichen Spalten, wenn Sie auf **Spalten zurücksetzen**klicken.  
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Verbindungs-Manager-Editor für mehrere Flatfiles (Seite Erweitert)
  Legen Sie mithilfe der Seite **Erweitert** im Dialogfeld **Verbindungs-Manager-Editor für mehrere Flatfiles** Eigenschaften wie den Datentyp und Trennzeichen für jede einzelne Spalte in den Textdateien fest, mit denen der Verbindungs-Manager für Flatfiles eine Verbindung herstellt.  
  
 Standardmäßig beträgt die Länge von Zeichenfolgenspalten 50 Zeichen. Sie können Beispieldaten auswerten und die Länge dieser Spalten automatisch ändern, um zu verhindern, dass Daten abgeschnitten werden oder extrem breite Spalten entstehen. Sie können darüber hinaus andere Metadaten aktualisieren, um Kompatibitlität mit Zielspalten zu aktivieren. Sie können beispielsweise den Datentyp einer Spalte, die nur ganzzahlige Daten enthält, in einen numerischen Datentyp ändern, z. B. DT_I2.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>enthalten  
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
 Durch Klicken auf **Neu**fügen Sie eine neue Spalte hinzu. Die neue Spalten wird beim Klicken auf **Neu** standardmäßig am Ende der Liste hinzugefügt. Ferner sind für die Schaltfläche folgende, über die Dropdownliste auswählbare Optionen verfügbar.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Spalte hinzufügen**|Fügt am Ende der Liste eine neue Spalte hinzu.|  
|**Einfügen vor**|Fügt vor der ausgewählten Spalte eine neue Spalte ein.|  
|**Einfügen nach**|Fügt nach der ausgewählten Spalte eine neue Spalte ein.|  
  
 **Delete**  
 Wählen Sie eine Spalte aus, und entfernen Sie sie dann, indem Sie auf **Löschen**klicken.  
  
 **Typen vorschlagen**  
 Im Dialogfeld **Spaltentypen vorschlagen** können Sie die Beispieldaten in der ersten ausgewählten Datei auswerten, um Vorschläge für den Datentyp und die -länge der einzelnen Spalten zu erhalten. Weitere Informationen finden Sie unter [Referenz zur Benutzeroberfläche des Dialogfelds „Spaltentypen vorschlagen“](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>Verbindungs-Manager-Editor für mehrere Flatfiles (Seite Vorschau)
  Auf der Seite **Vorschau** des Dialogfelds **Verbindungs-Manager-Editor für mehrere Flatfiles** können Sie den Inhalt der ersten ausgewählten Quelldatei anzeigen, der in die von Ihnen definierten Spalten unterteilt ist.  
  
 Weitere Informationen zum Verbindungs-Manager für mehrere Flatfiles finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Verbindung für mehrere Flatfiles im Workflow an. Der eingegebene Name wird im Bereich **Verbindungs-Manager** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Es ist eine bewährte Methode, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Auszulassende Datenzeilen**  
 Geben Sie an, wie viele Zeilen am Anfang von Flatfiles ausgelassen werden sollen.  
  
 **Vorschau der Zeilen**  
 Zeigen Sie Beispieldaten in der ersten ausgewählten Flatfile an, die entsprechend den von Ihnen gewählten Optionen in Spalten und Zeilen unterteilt sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Flatfilequelle](../../integration-services/data-flow/flat-file-source.md)   
 [Flatfileziel](../../integration-services/data-flow/flat-file-destination.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
