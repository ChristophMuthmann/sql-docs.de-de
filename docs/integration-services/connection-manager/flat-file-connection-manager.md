---
title: "Verbindungs-Manager für Flatfiles | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
caps.latest.revision: "49"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 29a1b62455247f2ba3cbcb17fafb6f0f78865230
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="flat-file-connection-manager"></a>Verbindungs-Manager für Flatfiles
  Mit einem Verbindungs-Manager für Flatfiles kann ein Paket auf Daten in einer Flatfile zugreifen. Beispielsweise können die Flatfilequellen und -ziele Verbindungs-Manager für Flatfiles zum Extrahieren und Laden von Daten verwenden.  
  
 Der Verbindungs-Manager für Flatfiles kann nur auf eine einzige Datei zugreifen. Wenn Sie auf mehrere Dateien verweisen möchten, verwenden Sie anstelle eines Verbindungs-Managers für Flatfiles einen Verbindungs-Manager für mehrere Flatfiles. Weitere Informationen finden Sie unter [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Spaltenlänge  
 Der Verbindungs-Manager für Flatfiles legt die Länge von Zeichenfolgenspalten standardmäßig auf 50 Zeichen fest. Sie können im Dialogfenster **Verbindungs-Manager-Editor für Flatfiles** Beispieldaten auswerten und automatisch die Länge dieser Spalten ändern, um zu vermeiden, dass die Daten abgeschnitten werden oder die Spaltenbreite überschritten wird. Es sei denn, Sie ändern danach die Spaltenlänge in einer Flatfilequelle oder in einer Transformation. Dann bleibt die Spaltenlänge der Zeichenfolgenspalte im gesamten Datenfluss gleich. Wenn diese Zeichenfolgenspalten Zielspalten zugeordnet sind, die schmaler sind, werden in der Benutzeroberfläche Warnungen angezeigt. Darüber hinaus können aufgrund der abgeschnittenen Daten zur Laufzeit Fehler auftreten. Um Fehler bzw. das Abschneiden von Daten zu vermeiden, können Sie im Verbindungs-Manager für Flatfiles, in der Flatfilequelle oder in einer Transformation die Größe der Spalten auf die Größe der Zielspalten ändern. Legen Sie zum Ändern der Länge von Ausgabespalten auf der Registerkarte **Eingabe- und Ausgabeeigenschaften** im Dialogfeld **Erweiterter Editor** die **Length** -Eigenschaft der Ausgabespalte fest.  
  
 Wenn Sie die Spaltenlängen im Verbindungs-Manager für Flatfiles aktualisieren, nachdem Sie die Flatfilequelle, die den Verbindungs-Manager verwendet, hinzugefügt und geändert haben, ist das manuelle Ändern der Ausgabespaltengröße in der Flatfilequelle nicht erforderlich. Wenn Sie das Dialogfeld **Flatfilequelle** öffnen, stellt die Flatfilequelle eine Option zum Synchronisieren der Spaltenmetadaten bereit.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Konfiguration des Verbindungs-Managers für Flatfiles  
 Wenn Sie einem Paket einen Verbindungs-Manager für Flatfiles hinzufügen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Flatfileverbindung aufgelöst wird, die Eigenschaften der Flatfileverbindung festlegt und der **Connections** -Sammlung des Pakets den Verbindungs-Manager für Flatfiles hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **FLATFILE**festgelegt.  
  
 Standardmäßig sucht der Verbindungs-Manager für Flatfiles immer nach einem Zeilentrennzeichen in Daten ohne Anführungszeichen und startet eine neue Zeile, wenn ein Zeilentrennzeichen gefunden wird. Dadurch kann der Verbindungs-Manager für Flatfiles Dateien mit Zeilen, in denen Spaltenfelder fehlen, ordnungsgemäß analysieren.  
  
 In einigen Fällen wird die Paketleistung verbessert, wenn Sie diese Funktion deaktivieren. Sie können diese Funktion deaktivieren, indem Sie die Eigenschaft für den Verbindungs-Manager für Flatfiles von **AlwaysCheckForRowDelimiters**auf **False**festlegen.  
  
 Es gibt folgende Möglichkeiten, um den Verbindungs-Manager für Flatfiles zu konfigurieren:  
  
-   Geben Sie die Datei, das Gebietsschema und die Codepage an, die Sie verwenden möchten. Mithilfe des Gebietsschemas werden gebietsschemabezogene Daten interpretiert, wie z. B. Datumsangaben, und mithilfe der Codepage werden Zeichenfolgendaten in Unicode-Daten konvertiert.  
  
-   Geben Sie das Dateiformat an. Sie können ein Format mit Trennzeichen, fester Breite oder rechtem Flatterrand verwenden.  
  
-   Geben Sie eine Kopfzeile, eine Datenzeile und Spaltentrennzeichen an. Spaltentrennzeichen können auf Dateiebene festgelegt und auf Spaltenebene überschrieben werden.  
  
-   Zeigen Sie an, ob die erste Zeile in der Datei Spaltennamen enthält.  
  
-   Geben Sie ein Textqualifiziererzeichen an. Für jede Spalte kann die Erkennung eines Textqualifizierers konfiguriert werden.  
  
     Die Verwendung eines Qualifiziererzeichens zum Einbetten eines Qualifiziererzeichens in eine qualifizierte Zeichenfolge wird durch den Verbindungs-Manager für Flatfiles unterstützt. Eine doppelte Instanz eines Textqualifizierers wird als literale, einzelne Instanz dieser Zeichenfolge interpretiert. Ist der Textqualifizierer beispielsweise ein einfaches Anführungszeichen, und die Eingabedaten sind 'abc', 'def', 'g'hi', so sind die Ausgabedaten abc, def, g'hi. Eine Instanz eines Textqualifizierers, die in eine qualifizierte Zeichenfolge eingebettet ist, verursacht jedoch den Fehler DTS_E_PRIMEOUTPUTFAILED in der Flatfilequelle.
  
-   Legen Sie Eigenschaften wie z. B. den Namen, den Datentyp und die maximale Breite für einzelne Spalten fest.  
  
 Sie können die ConnectionString-Eigenschaft für den Verbindungs-Manager für Flatfiles festlegen, indem Sie einen Ausdruck im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]angeben. Um einen Überprüfungsfehler zu vermeiden, gehen Sie wie folgt vor.  
  
-   Wenn Sie einen Ausdruck verwenden, um die Datei anzugeben, fügen Sie einen Dateipfad im Feld **Dateiname** unter **Verbindungs-Manager-Editor für Flatfiles**hinzu.  
  
-   Legen Sie die Eigenschaft **DelayValidation** im Verbindungs-Manager für Flatfiles auf **True**fest.  
  
 Sie können einen Ausdruck verwenden, um einen Dateinamen zur Laufzeit zu erstellen, indem Sie den Verbindungs-Manager für Flatfiles mit dem Flatfileziel verwenden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>Verbindungs-Manager-Editor für Flatfiles (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Verbindungs-Manager-Editor für Flatfiles** wählen Sie eine Datei und ein Dateiformat aus. Eine Flatfileverbindung ermöglicht das Herstellen einer Verbindung von einem Paket zu einer Textdatei.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Flatfileverbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Es ist eine bewährte Methode, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und einfacher zu verwalten sind.  
  
 **Dateiname**  
 Geben Sie den Pfad und den Dateinamen ein, die für die Flatfileverbindung verwendet werden sollen.  
  
 **Durchsuchen**  
 Suchen Sie den Dateinamen, der für die Flatfileverbindung verwendet werden soll.  
  
 **Gebietsschema**  
 Gibt das Gebietsschema für die Bereitstellung sprachspezifischer Informationen für das Bestellen sowie für Datums- und Zeitformate an.  
  
 **Unicode**  
 Gibt an, ob Unicode verwendet werden soll. Wenn Sie Unicode verwenden, können Sie keine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Gibt an, ob die Datei Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Die Trennung von Spalten erfolgt durch Trennzeichen. Welche Trennzeichen dies sind, wird auf der Seite **Spalten** angegeben.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.|  
  
 **Textqualifizierer**  
 Gibt die zu verwendenden Textqualifizierer an. So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind.  
  
> [!NOTE]  
>  Nachdem Sie einen Textqualifizierer ausgewählt haben, können Sie die Option **Keine** nicht erneut auswählen. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  
  
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
 Gibt an, wie viele Kopfzeilen bzw. erste Datenzeilen ggf. ausgelassen werden sollen.  
  
 **Spaltennamen in der ersten Datenzeile**  
 Gibt an, ob in der ersten Datenzeile Spaltennamen erwartet werden bzw. bereitzustellen sind.  
## <a name="flat-file-connection-manager-editor-columns-page"></a>Verbindungs-Manager-Editor für Flatfiles (Seite Spalten)
  Verwenden Sie die Seite **Spalten** im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** , um die Zeilen- und Spalteninformationen anzugeben und eine Vorschau der Datei anzuzeigen.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Flatfile-Verbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
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
  
 **Aktualisieren**  
 Zeigt durch Klicken auf **Aktualisieren**an, welche Auswirkung die Änderung der auszulassenden Trennzeichen hat. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
  
 **Vorschau der Zeilen**  
 Zeigt Beispieldaten in der Flatfile an, die entsprechend den von Ihnen ausgewählten Optionen in Spalten und Zeilen unterteilt sind.  
  
 **Spalten zurücksetzen**  
 Entfernt alle bis auf die ursprünglichen Spalten, wenn Sie auf **Spalten zurücksetzen**klicken.  
  
#### <a name="format--fixed-width"></a>Format = Feste Breite  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilenbreite**  
 Geben Sie erst die Länge der Zeile an, bevor Sie einzelnen Spalten Trennzeichen hinzufügen. Sie können auch die vertikale rote Linie im Vorschaufenster verschieben, um das Zeilenende zu kennzeichnen. Der Wert der Zeilenbreite wird automatisch aktualisiert.  
  
 **Spalten zurücksetzen**  
 Entfernt alle bis auf die ursprünglichen Spalten, wenn Sie auf **Spalten zurücksetzen**klicken.  
  
#### <a name="format--ragged-right"></a>Format = Rechter Flatterrand  
  
> [!NOTE]  
>  Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.  
  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
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
## <a name="flat-file-connection-manager-editor-advanced-page"></a>Verbindungs-Manager-Editor für Flatfiles (Seite Erweitert)
  Verwenden Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** die Seite **Erweitert** , um die Eigenschaften festzulegen, mit denen angegeben wird, wie mit Integration Services Daten in Flatfiles gelesen und geschrieben werden. Sie können die Namen der Spalten in der Flatfile ändern und Eigenschaften festlegen. Zu den Eigenschaften zählen der Datentyp und die Trennzeichen für jede Spalte in der Datei.  
  
 Standardmäßig beträgt die Länge von Zeichenfolgenspalten 50 Zeichen. Sie können die Länge dieser Spalten ändern, um das Abschneiden von Daten und das Entstehen übermäßig breiter Spalten zu verhindern. Sie können darüber hinaus andere Metadaten aktualisieren, um Kompatibitlität mit Zielspalten zu aktivieren. Sie können beispielsweise den Datentyp einer Spalte, die nur ganzzahlige Daten enthält, in einen numerischen Datentyp ändern, z. B. DT_I2. Nehmen Sie diese Änderungen manuell vor, oder klicken Sie auf die Schaltfläche **Typen vorschlagen** , um mithilfe des Dialogfelds **Spaltentypen vorschlagen** Beispieldaten auszuwerten und einige dieser Änderungen automatisch vornehmen zu lassen.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für den Verbindungs-Manager für Flatfiles im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie den Verbindungs-Manager. Die bewährte Methode ist hierbei, den Verbindungs-Manager zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Konfigurieren Sie die Eigenschaften für jede Spalte.**  
 Wählen Sie eine Spalte im linken Bereich, um im rechten Bereich ihre Eigenschaften anzuzeigen. In der folgenden Tabelle werden die Datentypeigenschaften beschrieben. Einige der aufgeführten Eigenschaften können nur für einige Flatfileformate konfiguriert werden.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**ColumnType**|Gibt an, ob eine Spalte getrennt ist, eine feste Breite hat bzw. einen unregelmäßigen rechten Rand aufweist. Diese Eigenschaft ist schreibgeschützt. Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.|  
|**OutputColumnWidth**|Geben Sie einen Wert an, der als Anzahl von Bytes gespeichert werden soll; bei Unicode-Dateien entspricht dieser Wert einer Zeichenanzahl. Im Datenflusstask dient dieser Wert dem Festlegen der Breite der Ausgabespalte für die Flatfilequelle. Im Objektmodell heißt diese Eigenschaft MaximumWidth.|  
|**DataType**|Wählen Sie eine Option aus der Liste der verfügbaren Datentypen aus. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Geben Sie an, ob Textdaten in Textqualifiziererzeichen eingeschlossen sind, z. B. in Anführungszeichen.<br /><br /> True: Die Textdaten in der Flatfile sind gekennzeichnet. False: Die Textdaten in der Flatfile sind nicht gekennzeichnet.|  
|**Name**|Geben Sie einen beschreibenden Spaltennamen an. Wenn Sie keinen Namen eingeben, wird in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch ein Name im Format Spalte 0, Spalte 1 usw. erstellt.|  
|**DataScale**|Gibt die Skala numerischer Daten an. Skala heißt in diesem Fall die Anzahl der Dezimalstellen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Wählen Sie eine Option aus der Liste der verfügbaren Spaltentrennzeichen aus. Dabei sollten Sie Spaltentrennzeichen auswählen, deren Auftreten als Zeichen im Text unwahrscheinlich ist. Bei Spalten fester Breite wird dieser Wert ignoriert.<br /><br /> **{CR}{LF}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.<br /><br /> **{CR}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf.<br /><br /> **{LF}**. Als Trennzeichen für Spalten dient ein Zeilenvorschub.<br /><br /> **Semikolon {;}**. Als Trennzeichen für Spalten dient ein Semikolon.<br /><br /> **Doppelpunkt {:}**. Als Trennzeichen für Spalten dient ein Doppelpunkt.<br /><br /> **Komma {,}**. Als Trennzeichen für Spalten dient ein Komma.<br /><br /> **Tabulator {t}**. Als Trennzeichen für Spalten dient ein Tabulator.<br /><br /> **Senkrechter Strich {&#124;}**. Als Trennzeichen für Spalten dient ein senkrechter Strich.|  
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
 Im Dialogfeld **Spaltentypen vorschlagen** können Sie die Beispieldaten in der Datei auswerten, um Vorschläge für den Datentyp und die -länge der einzelnen Spalten zu erhalten. Weitere Informationen finden Sie unter [Referenz zur Benutzeroberfläche des Dialogfelds „Spaltentypen vorschlagen“](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
## <a name="flat-file-connection-manager-editor-preview-page"></a>Verbindungs-Manager-Editor für Flatfiles (Vorschauseite)
  Über den Knoten **Vorschau** im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** können Sie den Inhalt der Quelldatei im Tabellenformat anzeigen.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Flatfile-Verbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Es ist eine bewährte Methode, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **Auszulassende Datenzeilen**  
 Geben Sie an, wie viele Zeilen am Anfang von Flatfiles ausgelassen werden sollen.  
  
 **Aktualisieren**  
 Zeigen Sie an, welche Auswirkung die Änderung der Anzahl der auszulassenden Zeilen hat, indem Sie auf **Aktualisieren**klicken. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
  
 **Vorschau der Zeilen**  
 Zeigen Sie Beispieldaten in der Flatfile an, die entsprechend der von Ihnen gewählten Option in Spalten und Zeilen unterteilt sind.  
 
