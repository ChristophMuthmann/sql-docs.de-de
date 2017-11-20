---
title: Herstellen einer Verbindung mit einer Flatfile-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 568d02ef58102b47501415d35f64369e997e875b
ms.contentlocale: de-de
ms.lasthandoff: 10/18/2017

---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Flatfile-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Flatfile** (Textdatei) Datenquellen aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite SQL Server-Import und Export Assistenten. Für Flatfiles enthalten diese beiden Seiten des Assistenten verschiedene Gruppen von Optionen, damit der Flatfile-Quelle und das Flatfileziel separat beschrieben.

## <a name="an-alternative-for-simple-text-import"></a>Eine Alternative für einfachen Text importieren
Wenn Sie in SQL Server eine Textdatei importieren, und Sie nicht alle Konfigurationsoptionen im Import / Export-Assistenten verfügbar brauchen, können Sie verwenden die **Flatfile-Assistenten importieren** in SQL Server Management Studio (SSMS). Weitere Informationen finden Sie in den folgenden Artikeln:
- [Neuigkeiten in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/)
- [Einführung in den neuen Assistenten zum Importieren von Flatfiles in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173)

## <a name="connect-to-a-flat-file-source"></a>Herstellen einer Verbindung mit einer Flatfilequelle
 
 Es gibt vier Seiten der Optionen für die Flatfile-Datenquellen. Das sind viele Seiten! Allerdings müssen Sie nicht viel Zeit für jede Seite ausgeben. Hier sind die Aufgaben zu berücksichtigen.
 
Seite|Empfehlung  |Typ  
----|---------|---------
**Allgemein**|Stellen Sie sicher, dass die Aktualisierungsoptionen in der **Format** Abschnitt.|Empfohlen    
**Spalten**|Stellen Sie sicher, überprüfen Sie die Spalten- und Zeilentrennzeichen (bei einer Datei mit Trennzeichen) oder markieren die Spalten (für eine feste Breite-Datei).|Empfohlen
**Erweitert**|Aktivieren Sie optional die Datentypen und anderen Eigenschaften standardmäßig auf die Spalten zugewiesen.|Optional
**Vorschau**|Optional, Vorschau eine Stichprobe der Daten, die mit den Einstellungen, die Sie angegeben haben.|Optional

## <a name="general-page-source"></a>Seite "Allgemein" (Quelle)
 Suchen Sie auf der Seite **Allgemein** nach der Datei, und wählen Sie sie aus. Überprüfen Sie dann die Einstellungen im Abschnitt **Format**.
 
 ![Flatfile-Verbindung, Allgemein](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Optionen zum festlegen (**allgemeine** Seite)

 **Dateiname**  
 Geben Sie der Pfad und Dateiname der Flatfile.  
  
 **Durchsuchen**  
 Suchen Sie die Flatfile an.  
  
 **Gebietsschema**  
 Geben Sie das Gebietsschema Sprachspezifische Informationen zum Sortieren und für Datums- und Zeitformate an.  
  
 **Unicode**  
 Geben Sie an, ob die Datei Unicode verwendet. Wenn Sie Unicode verwenden, können nicht Sie eine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Wählen Sie, ob die Datei mit Trennzeichen, fester Breite oder rechtem rechten Formatierung verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Spalten werden durch Trennzeichen getrennt. Geben Sie das Trennzeichen an, auf die **Spalten** Seite.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Geben Sie den Textqualifizierer ggf. von der Datei verwendet. So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind. (Diese Eigenschaft gilt nur für Dateien mit Trennzeichen.) 
  
> [!NOTE]
> Nachdem Sie einen Textqualifizierer ausgewählt haben, kann nicht erneut Auswahl der **keine** Option. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  
  
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
 Geben Sie die Anzahl der Zeilen am Anfang der Datei überspringen, falls vorhanden.  
  
 **Spaltennamen in der ersten Datenzeile**  
 Geben Sie an, ob die erste Zeile (nach der übersprungenen Zeilen) Spaltennamen enthält.

## <a name="columns-page---format--delimited-source"></a>Seite "Spalten" - Format = mit Trennzeichen (Quelle)
 Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite aus, wenn Sie ausgewählt haben **Delimited** mit dem Flatfile-Format.
 
![Flatfile, begrenzt, Seite "Spalten"](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Optionen zum festlegen (**Spalten** Seite - Format = mit Trennzeichen)

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
  
 **Vorschau der Zeilen**  
 Zeigt Beispieldaten in der Flatfile an, die entsprechend den von Ihnen ausgewählten Optionen in Spalten und Zeilen unterteilt sind.  
 
 **Aktualisieren**  
 Zeigt durch Klicken auf **Aktualisieren**an, welche Auswirkung die Änderung der auszulassenden Trennzeichen hat. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
  
 **Spalten zurücksetzen**  
 Stellen Sie die ursprünglichen Spalten wieder her.  

## <a name="columns-page---format--fixed-width-source"></a>Seite "Spalten" - Format = feste Breite (Quelle)
Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite aus, wenn Sie ausgewählt haben **feste Breite** mit dem Flatfile-Format.
  
![Flatfile, feste Breite, Seite "Spalten"](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Optionen zum festlegen (**Spalten** Seite - Format = feste Breite)

 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilenbreite**  
 Geben Sie erst die Länge der Zeile an, bevor Sie einzelnen Spalten Trennzeichen hinzufügen. Sie können auch die vertikale rote Linie im Vorschaufenster verschieben, um das Zeilenende zu kennzeichnen. Der Wert der Zeilenbreite wird automatisch aktualisiert.  
  
 **Spalten zurücksetzen**  
 Stellen Sie die ursprünglichen Spalten wieder her.  
  
## <a name="columns-page---format--ragged-right-source"></a>Seite "Spalten" - Format = rechter Flatterrand (Quelle)
Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite aus, wenn Sie ausgewählt haben **rechtem Flatterrand** mit dem Flatfile-Format.

> [!NOTE]
> Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.  
 
![Flatfile, rechter Flatterrand, Seite "Spalten"](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Optionen zum festlegen (**Spalten** Seite - Format = rechter Flatterrand)
   
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
 Stellen Sie die ursprünglichen Spalten wieder her.  

## <a name="advanced-page-source"></a>Seite "Erweitert" (Quelle)
Auf der Seite **Erweitert** werden detaillierte Informationen zu jeder Spalte in der Datenquelle angezeigt, einschließlich Datentyp und Größe. Die folgende Abbildung zeigt die **erweitert** Seite für die erste Spalte in einer durch Trennzeichen getrennten Flatfile.

![Flatfile-Datei mit Trennzeichen, Seite "Erweitert"](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

Screenshot, beachten Sie, dass die **Id** Spalte, die Zahlen enthält, weist zunächst einen Datentyp Zeichenfolge.

### <a name="options-to-specify-advanced-page"></a>Optionen zum festlegen (**erweitert** Seite)

 **Konfigurieren Sie die Eigenschaften für jede Spalte.**  
 Wählen Sie eine Spalte im linken Bereich, um im rechten Bereich ihre Eigenschaften anzuzeigen. Finden Sie eine Beschreibung der Spalteneigenschaften in der folgenden Tabelle aus. Einige der aufgeführten Eigenschaften sind konfigurierbar, nur für bestimmte Flatfile-Formate und Spalten bestimmter Datentypen.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Name**|Geben Sie einen beschreibenden Spaltennamen an. Wenn Sie einen Namen nicht eingeben [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch ein Name im Format Spalte 0, Spalte1 usw. erstellt.|
|**ColumnDelimiter**|Wählen Sie eine Option aus der Liste der verfügbaren Spaltentrennzeichen aus. Dabei sollten Sie Spaltentrennzeichen auswählen, deren Auftreten als Zeichen im Text unwahrscheinlich ist. Bei Spalten fester Breite wird dieser Wert ignoriert.<br /><br /> **{CR}{LF}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.<br /><br /> **{CR}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf.<br /><br /> **{LF}**. Als Trennzeichen für Spalten dient ein Zeilenvorschub.<br /><br /> **Semikolon {;}**. Als Trennzeichen für Spalten dient ein Semikolon.<br /><br /> **Doppelpunkt {:}**. Als Trennzeichen für Spalten dient ein Doppelpunkt.<br /><br /> **Komma {,}**. Als Trennzeichen für Spalten dient ein Komma.<br /><br /> **Tabulator {t}**. Als Trennzeichen für Spalten dient ein Tabulator.<br /><br /> **Senkrechter Strich {&#124;}**. Als Trennzeichen für Spalten dient ein senkrechter Strich.|
|**ColumnType**|Gibt an, ob eine Spalte getrennt ist, eine feste Breite hat bzw. einen unregelmäßigen rechten Rand aufweist. Diese Eigenschaft ist schreibgeschützt. Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.|  
|**InputColumnWidth**|Geben Sie einen Wert als Anzahl von Bytes gespeichert werden soll; Bei Unicode-Dateien ist dieser Wert einer Zeichenanzahl. Bei mit Trennzeichen versehenen Spalten wird dieser Wert ignoriert.<br /><br /> **Hinweis:** Im Objektmodell heißt diese Eigenschaft ColumnWidth.|
|**DataPrecision**|Gibt die Präzision numerischer Daten an. Präzision heißt in diesem Fall die Anzahl der Stellen.|
|**DataScale**|Gibt die Skala numerischer Daten an. Skala heißt in diesem Fall die Anzahl der Dezimalstellen.|
|**DataType**|Wählen Sie eine Option aus der Liste der verfügbaren Datentypen aus.<br/>Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Geben Sie einen Wert an, der als Anzahl von Bytes gespeichert werden soll; bei Unicode-Dateien entspricht dieser Wert einer Zeichenanzahl. Im Datenflusstask dient dieser Wert dem Festlegen der Breite der Ausgabespalte für die Flatfilequelle. Im Objektmodell heißt diese Eigenschaft MaximumWidth.|  
|**TextQualified**|Geben Sie an, ob Textdaten in Textqualifiziererzeichen eingeschlossen sind, z. B. in Anführungszeichen.<br /><br /> True: Die Textdaten in der Flatfile sind gekennzeichnet. False: Die Textdaten in der Flatfile sind nicht gekennzeichnet.|  
  
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
 Im Dialogfeld **Spaltentypen vorschlagen** können Sie die Beispieldaten in der Datei auswerten, um Vorschläge für den Datentyp und die -länge der einzelnen Spalten zu erhalten.  
 
Klicken Sie auf **Typen vorschlagen**, um das Dialogfeld **Spaltentypen vorschlagen** anzuzeigen. 

![Flatfile-Verbindung vorschlagen Typen (Dialogfeld)](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Nach dem Auswählen von Optionen in der **Spaltentypen vorschlagen** (Dialogfeld), und klicken Sie auf **OK**, der Assistent kann die Datentypen der einige der Spalten ändern.

Der folgende Screenshot zeigt, dass nach Anklicken **Typen vorschlagen**, der Assistent hat erkannt, die die **Id** Spalte in der Datenquelle ist tatsächlich eine Zahl und keiner Textzeichenfolge, und den Datentyp des geändert wurde die Spalte aus einer Zeichenfolge in eine ganze Zahl.

![Flatfile-Verbindung, „Erweitert“ – nachher](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Weitere Informationen finden Sie unter [vorschlagen Spalte Typen Dialogfeld Referenz zur Benutzeroberfläche des](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Seite "Datenvorschau" (Quelle)

Überprüfen Sie auf der Seite **Vorschau**, ob die Liste der Spalten und die Beispieldaten Ihren Erwartungen entsprechen.

![Flatfile, Seite "Datenvorschau"](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Optionen zum festlegen (**Vorschau** Seite)

 **Auszulassende Datenzeilen**  
 Geben Sie an, wie viele Zeilen am Anfang von Flatfiles ausgelassen werden sollen.  
  
 **Vorschau der Zeilen**  
 Zeigen Sie Beispieldaten in der Flatfile an, die entsprechend der von Ihnen gewählten Option in Spalten und Zeilen unterteilt sind.
 
 **Aktualisieren**  
 Zeigen Sie an, welche Auswirkung die Änderung der Anzahl der auszulassenden Zeilen hat, indem Sie auf **Aktualisieren**klicken. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
 
Weitere Informationen zur Seite **Vorschau** finden Sie auf der folgenden Referenzseite zu Integration Services: [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Herstellen einer Verbindung mit einem Flatfileziel
Für ein Flatfileziel ist nur eine einzelne Seite mit Optionen, wie im folgenden Screenshot gezeigt. Suchen Sie die Datei auszuwählen, und überprüfen Sie die Einstellungen in der **Format** Abschnitt.

![Herstellen einer Verbindung mit dem Flatfileziel](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Optionen zum festlegen (**wählen Sie ein Ziel** Seite)

 **Dateiname**  
 Geben Sie der Pfad und Dateiname der Flatfile.  
  
 **Durchsuchen**  
 Suchen Sie die Flatfile an.  
  
 **Gebietsschema**  
 Geben Sie das Gebietsschema Sprachspezifische Informationen zum Sortieren und für Datums- und Zeitformate an.  
  
 **Unicode**  
 Geben Sie an, ob die Datei Unicode verwendet. Wenn Sie Unicode verwenden, können nicht Sie eine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Wählen Sie, ob die Datei mit Trennzeichen, fester Breite oder rechtem rechten Formatierung verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Spalten werden durch Trennzeichen getrennt. Geben Sie das Trennzeichen an, auf die **Spalten** Seite.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Geben Sie den Textqualifizierer ggf. von der Datei verwendet. So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind. (Diese Eigenschaft gilt nur für Dateien mit Trennzeichen.) 
  
> [!NOTE] 
> Nachdem Sie einen Textqualifizierer ausgewählt haben, kann nicht erneut die **keine** Option. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


