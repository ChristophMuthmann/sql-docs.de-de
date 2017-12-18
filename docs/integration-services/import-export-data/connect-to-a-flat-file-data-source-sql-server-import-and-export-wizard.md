---
title: Herstellen einer Verbindung mit einer Flatfile-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9fa0b3192455d022288100f2997309598dae774b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Flatfile-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Flatfile**-Datenquelle (Textdatei) von der Seite **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen. Für Flatfiles enthalten diese beiden Seiten des Assistenten verschiedene Optionen, deshalb werden in diesem Artikel die Flatfilequelle und das Flatfileziel separat beschrieben.

## <a name="an-alternative-for-simple-text-import"></a>Alternative zum einfachen Importieren von Text
Wenn Sie eine Textdatei in SQL Server importieren müssen und nicht alle Konfigurationen benötigen, die im Import/Export-Assistenten verfügbar sind, verwenden Sie den **Assistenten zum Importieren von Flatfiles** in SQL Server Management Studio (SSMS). Weitere Informationen finden Sie in den folgenden Artikeln:
- [Neuigkeiten in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/)
- [Einführung in den neuen Assistenten zum Importieren von Flatfiles in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173)

## <a name="connect-to-a-flat-file-source"></a>Herstellen einer Verbindung mit einer Flatfilequelle
 
 Es gibt vier Seiten mit Optionen für Flatfile-Datenquellen. Das sind viele Optionen. Sie müssen jedoch nicht viel Zeit in diese investieren. Im Folgenden finden Sie die Aufgaben, die Sie berücksichtigen sollten.
 
Seite|Empfehlung  |Typ  
----|---------|---------
**Allgemein**|Stellen Sie sicher, dass Sie die Optionen im Abschnitt **Format** aktualisieren.|Empfohlen    
**Spalten**|Stellen Sie sicher, dass Sie die Spalten- und Zeilentrennzeichen (für eine durch Trennzeichen getrennte Datei) überprüfen oder die Spalten markieren (für eine Datei mit fester Breite).|Empfohlen
**Erweitert**|Überprüfen Sie optional die Datentypen und andere Eigenschaften, die den Spalten standardmäßig zugewiesen sind.|Optional
**Vorschau**|Zeigen Sie optional mithilfe der von Ihnen angegebenen Einstellungen die Vorschau eines Datenbeispiels an.|Optional

## <a name="general-page-source"></a>Seite „Allgemein“ (Quelle)
 Suchen Sie auf der Seite **Allgemein** nach der Datei, und wählen Sie sie aus. Überprüfen Sie dann die Einstellungen im Abschnitt **Format**.
 
 ![Flatfile-Verbindung, Allgemein](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Anzugebende Optionen (Seite **Allgemein**)

 **Dateiname**  
 Geben Sie den Pfad und Dateinamen der Flatfile ein.  
  
 **Durchsuchen**  
 Suchen Sie die Flatfile.  
  
 **Gebietsschema**  
 Gibt das Gebietsschema für die Bereitstellung sprachspezifischer Informationen für das Sortieren sowie für Datums- und Zeitformate an.  
  
 **Unicode**  
 Geben Sie an, ob die Datei Unicode verwendet. Wenn Sie Unicode verwenden, können Sie keine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Wählen Sie aus, ob die Datei eine Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Spalten werden mit Trennzeichen getrennt. Geben Sie das Trennzeichen auf der Seite **Spalten** an.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Geben Sie den von der Datei verwendeten Textqualifizierer an (falls vorhanden). So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind. (Diese Eigenschaft gilt nur für durch Trennzeichen getrennte Dateien.) 
  
> [!NOTE]
> Nachdem Sie einen Textqualifizierer ausgewählt haben, können Sie die Option **Keine** nicht erneut auswählen. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  
  
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
 Geben Sie die Anzahl der zu überspringenden Zeilen am Anfang der Datei an (falls vorhanden).  
  
 **Spaltennamen in der ersten Datenzeile**  
 Geben Sie an, ob die erste Zeile (nach jeder übersprungenen Zeile) Spaltennamen enthält.

## <a name="columns-page---format--delimited-source"></a>Seite „Spalten“ – Format = Mit Trennzeichen (Quelle)
 Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite, wenn Sie **Mit Trennzeichen** als Flatfileformat ausgewählt haben.
 
![Flatfile, mit Trennzeichen, Seite „Spalten“](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Anzugebende Optionen (Seite **Spalten** – Format = Mit Trennzeichen)

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

## <a name="columns-page---format--fixed-width-source"></a>Seite „Spalten“ – Format = Feste Breite (Quelle)
Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite, wenn Sie **Feste Breite** als Flatfileformat ausgewählt haben.
  
![Flatfile, feste Breite, Seite „Spalten“](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Anzugebende Optionen (Seite **Spalten** – Format = Feste Breite)

 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilenbreite**  
 Geben Sie erst die Länge der Zeile an, bevor Sie einzelnen Spalten Trennzeichen hinzufügen. Sie können auch die vertikale rote Linie im Vorschaufenster verschieben, um das Zeilenende zu kennzeichnen. Der Wert der Zeilenbreite wird automatisch aktualisiert.  
  
 **Spalten zurücksetzen**  
 Stellen Sie die ursprünglichen Spalten wieder her.  
  
## <a name="columns-page---format--ragged-right-source"></a>Seite „Spalten“ – Format = Rechter Flatterrand (Quelle)
Überprüfen Sie auf der Seite **Spalten** die Liste der Spalten und die Trennzeichen, die der Assistent identifiziert hat. Der folgende Screenshot zeigt die Seite, wenn Sie **Rechter Flatterrand** als Flatfileformat ausgewählt haben.

> [!NOTE]
> Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.  
 
![Flatfile, rechter Flatterrand, Seite „Spalten“](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Anzugebende Optionen (Seite **Spalten** – Format = Rechter Flatterrand)
   
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

## <a name="advanced-page-source"></a>Seite „Erweitert“ (Quelle)
Auf der Seite **Erweitert** werden detaillierte Informationen zu jeder Spalte in der Datenquelle angezeigt, einschließlich Datentyp und Größe. Der folgende Screenshot zeigt die Seite **Erweitert** für die erste Spalte in einer durch Trennzeichen getrennten Flatfile.

![Flatfile, mit Trennzeichen, Seite „Erweitert“](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

Beachten Sie im Screenshot, dass die Spalte **id**, die Zahlen enthält, anfänglich den Datentyp „String“ aufweist.

### <a name="options-to-specify-advanced-page"></a>Anzugebende Optionen (Seite **Erweitert**)

 **Konfigurieren Sie die Eigenschaften für jede Spalte.**  
 Wählen Sie eine Spalte im linken Bereich, um im rechten Bereich ihre Eigenschaften anzuzeigen. In der folgenden Tabelle werden die Spalteneigenschaften beschrieben. Einige der aufgelisteten Eigenschaften sind nur für bestimmte Flatfileformate und für Spalten mit bestimmten Datentypen konfigurierbar.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Name**|Geben Sie einen beschreibenden Spaltennamen an. Wenn Sie keinen Namen eingeben, wird in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch ein Name im Format „Spalte 0“, „Spalte 1“ usw. erstellt.|
|**ColumnDelimiter**|Wählen Sie eine Option aus der Liste der verfügbaren Spaltentrennzeichen aus. Dabei sollten Sie Spaltentrennzeichen auswählen, deren Auftreten als Zeichen im Text unwahrscheinlich ist. Bei Spalten fester Breite wird dieser Wert ignoriert.<br /><br /> **{CR}{LF}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.<br /><br /> **{CR}**. Als Trennzeichen für Spalten dient ein Wagenrücklauf.<br /><br /> **{LF}**. Als Trennzeichen für Spalten dient ein Zeilenvorschub.<br /><br /> **Semikolon {;}**. Als Trennzeichen für Spalten dient ein Semikolon.<br /><br /> **Doppelpunkt {:}**. Als Trennzeichen für Spalten dient ein Doppelpunkt.<br /><br /> **Komma {,}**. Als Trennzeichen für Spalten dient ein Komma.<br /><br /> **Tabulator {t}**. Als Trennzeichen für Spalten dient ein Tabulator.<br /><br /> **Senkrechter Strich {&#124;}**. Als Trennzeichen für Spalten dient ein senkrechter Strich.|
|**ColumnType**|Gibt an, ob eine Spalte getrennt ist, eine feste Breite hat bzw. einen unregelmäßigen rechten Rand aufweist. Diese Eigenschaft ist schreibgeschützt. Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.|  
|**InputColumnWidth**|Geben Sie einen Wert an, der als Anzahl von Bytes gespeichert werden soll. Bei Unicode-Dateien entspricht dieser Wert einer Zeichenanzahl. Bei mit Trennzeichen versehenen Spalten wird dieser Wert ignoriert.<br /><br /> **Hinweis:** Im Objektmodell heißt diese Eigenschaft ColumnWidth.|
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

![Flatfileverbindung: Dialogfeld „Typen vorschlagen“](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Klicken Sie nach Auswahl der Optionen im Dialogfeld **Spaltentypen vorschlagen** auf **OK**. Der Assistent kann die Datentypen einiger Spalten ändern.

Der folgende Screenshot zeigt, dass der Assistent nach dem Klicken auf **Typen vorschlagen** erkannt hat, dass die Spalte **id** in der Datenquelle eine Zahl und keine Textzeichenfolge darstellt, und den Datentyp der Spalte von „String“ zu „Integer“ geändert hat.

![Flatfile-Verbindung, „Erweitert“ – nachher](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Weitere Informationen finden Sie unter [Suggest Column Types Dialog Box UI Reference (Referenz zur Benutzeroberfläche des Dialogfelds „Spaltentypen vorschlagen“)](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Seite „Vorschau“ (Quelle)

Überprüfen Sie auf der Seite **Vorschau**, ob die Liste der Spalten und die Beispieldaten Ihren Erwartungen entsprechen.

![Flatfile, Seite „Vorschau“](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Anzugebende Optionen (Seite **Vorschau**)

 **Auszulassende Datenzeilen**  
 Geben Sie an, wie viele Zeilen am Anfang von Flatfiles ausgelassen werden sollen.  
  
 **Vorschau der Zeilen**  
 Zeigen Sie Beispieldaten in der Flatfile an, die entsprechend der von Ihnen gewählten Option in Spalten und Zeilen unterteilt sind.
 
 **Aktualisieren**  
 Zeigen Sie an, welche Auswirkung die Änderung der Anzahl der auszulassenden Zeilen hat, indem Sie auf **Aktualisieren**klicken. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
 
Weitere Informationen zur Seite **Vorschau** finden Sie auf der folgenden Referenzseite zu Integration Services: [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Herstellen einer Verbindung mit einem Flatfileziel
Für ein Flatfileziel gibt es wie im folgenden Screenshot dargestellt nur eine Seite mit Optionen. Suchen Sie nach der Datei, und wählen Sie sie aus. Überprüfen Sie dann die Einstellungen im Abschnitt **Format**.

![Herstellen einer Verbindung mit einem Flatfileziel](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Anzugebende Optionen (Seite **Ziel auswählen**)

 **Dateiname**  
 Geben Sie den Pfad und Dateinamen der Flatfile ein.  
  
 **Durchsuchen**  
 Suchen Sie die Flatfile.  
  
 **Gebietsschema**  
 Gibt das Gebietsschema für die Bereitstellung sprachspezifischer Informationen für das Sortieren sowie für Datums- und Zeitformate an.  
  
 **Unicode**  
 Geben Sie an, ob die Datei Unicode verwendet. Wenn Sie Unicode verwenden, können Sie keine Codepage angeben.  
  
 **Codepage**  
 Gibt die Codepage für Nicht-Unicode-Text an.  
  
 **Format**  
 Wählen Sie aus, ob die Datei eine Formatierung mit Trennzeichen, fester Breite oder rechtem Flatterrand verwendet.  
  
|Wert|Description|  
|-----------|-----------------|  
|Mit Trennzeichen|Spalten werden mit Trennzeichen getrennt. Geben Sie das Trennzeichen auf der Seite **Spalten** an.|  
|Feste Breite|Spalten haben eine feste Breite.|  
|Rechter Flatterrand|Bei Dateien mit rechtem Flatterrand weisen alle Spalten mit Ausnahme der letzten eine feste Breite auf. Die letzte Spalte wird durch das Zeilentrennzeichen begrenzt.|  
  
 **Textqualifizierer**  
 Geben Sie den von der Datei verwendeten Textqualifizierer an (falls vorhanden). So können Sie beispielsweise angeben, dass Textfelder in Anführungszeichen eingeschlossen sind. (Diese Eigenschaft gilt nur für durch Trennzeichen getrennte Dateien.) 
  
> [!NOTE] 
> Nachdem Sie einen Textqualifizierer ausgewählt haben, können Sie die Option **Keine** nicht erneut auswählen. Geben Sie **Keine** ein, um die Auswahl des Textqualifizierers aufzuheben.  

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

