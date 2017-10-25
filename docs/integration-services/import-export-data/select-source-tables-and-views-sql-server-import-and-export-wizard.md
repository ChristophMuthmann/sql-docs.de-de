---
title: "Wählen Sie Quelltabellen und-Sichten (SQL Server-Import / Export-Assistent) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a0c3c4fc8d41206ea077498dafb755e7b433a78
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Quelltabellen und -sichten auswählen (SQL Server-Import/Export-Assistent)
  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent zeigt die Seite **Quelltabellen und -sichten auswählen**an, nachdem Sie angegeben haben, dass Sie eine vollständige Tabelle kopieren möchten, oder nachdem Sie eine Abfrage bereitstellen. Auf dieser Seite wählen Sie die vorhandenen Tabellen und Sichten zum Kopieren aus. Anschließend ordnen Sie die Quelltabellen neuen oder vorhandenen Zieltabellen zu. Optional können Sie auch die Zuordnung einzelner Spalten überprüfen und eine Vorschau von Beispieldaten anzeigen.

> [!TIP]
> Wenn Sie mehr als eine SQL Server-Datenbank oder SQL Server-Datenbankobjekte Ausnahme Tabellen und Sichten kopieren müssen, verwenden Sie the Copy Database Wizard anstelle des Import / Export-Assistenten. Weitere Informationen finden Sie unter [Verwenden des Assistenten zum Kopieren von Datenbanken](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Screenshot – Wenn Sie, zum Kopieren von Tabellen Vorhaben  
 Der folgende Screenshot zeigt ein Beispiel der **wählen Quelltabellen und-Sichten** Seite des Assistenten, wenn Sie zuvor ausgewählt haben die **Kopieren von Daten aus Tabellen oder Sichten** option der  **Tabelle kopieren oder Datenbank Abfragen** Seite. In der Liste finden Sie alle in der Datenquelle verfügbaren Tabellen und Sichten.
 
In diesem Beispiel wird die **Quelle** Liste enthält alle Tabellen in der AdventureWorks-Beispieldatenbank. Die ausgewählte Zeile zeigt, dass der Benutzer möchte kopieren Sie die **Sales.Customer** Tabelle aus der Quelldatenbank in die neue **Sales.CustomerNew** Tabelle am Ziel. 
   
 ![Wählen Sie Tabellen auf der Seite des Import / Export-Assistenten](../../integration-services/import-export-data/media/select-tables1.png "Tabellen auswählen auf der Seite des Import / Export-Assistenten")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Screenshot – Wenn Sie eine Abfrage angegeben haben.  
 Der folgende Screenshot zeigt ein Beispiel der **wählen Quelltabellen und-Sichten** Seite des Assistenten, wenn Sie zuvor ausgewählt haben die **Abfrage zum Angeben der zu übertragenden Daten schreiben** Option für die **Geben Tabelle kopieren oder Datenbank Abfragen** Seite. Die **Quelle** Liste enthält nur eine einzelne Zeile, wobei das Element mit dem Namen `[Query]` stellt die Abfrage, die Sie bereitgestellt, auf die **Quellabfrage angeben** Seite.
 
In diesem Beispiel möchte der Benutzer die Abfrageergebnisse aus der Quelle in die **Sales.CustomerNew** am Ziel kopieren.  
    
 ![Wählen Sie Tabellen auf der Seite des Import / Export-Assistenten](../../integration-services/import-export-data/media/select-tables2.png "Tabellen auswählen auf der Seite des Import / Export-Assistenten")  

## <a name="select-source-and-destination-tables"></a>Auswählen von Quell- und Zieltabellen 
**Quelle**  
Wählen Sie mithilfe der Kontrollkästchen aus der Liste der verfügbaren Tabellen und Sichten die in das Ziel zu kopierenden Elemente aus. Standardmäßig werden die Daten aus der Datenquelle unverändert kopiert. Wenn Sie eine neue Zieltabelle erstellen, wird das Schema für die neue Tabelle – d. h. die Liste der Spalten und deren Eigenschaften - auch ohne Änderung aus der Datenquelle kopiert.

Wenn Sie eine Abfrage angegeben, wird die Liste enthält nur ein Element mit dem Namen `[Query]`. 

**Ziel**  
 Wählen Sie eine Zieltabelle aus der Liste für jede Quelltabelle oder Abfrage aus, oder geben Sie den Namen einer neuen Tabelle ein, die vom Assistenten erstellt werden soll. Wenn Sie eine vorhandene Zieltabelle auswählen, muss die Tabelle über Spalten und Datentypen verfügen, die mit der Quelltabelle kompatibel sind.  

> [!NOTE]
> Wenn Sie zu diesem Zeitpunkt den Assistenten anhalten, um manuell mit einem Tool (wie z.B.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) eine neue Tabelle in der Zieldatenbank zu erstellen, ist die neue Tabelle in der Liste verfügbarer Zieltabellen nicht sofort sichtbar. Zum Aktualisieren der Liste der Zieltabellen wechseln Sie zurück zur Seite **Ziel auswählen** , wählen Sie die Zieldatenbank erneut aus, um die Liste der verfügbaren Tabellen und Sichten zu aktualisieren, und wechseln Sie dann wieder zur Seite **Quelltabellen und -sichten auswählen** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Optional, überprüfen Sie die spaltenzuordnungen und anzeigen Daten in der Vorschau
**Zuordnungen bearbeiten**   
Klicken Sie optional auf **Zuordnungen bearbeiten** zum Anzeigen der **Spaltenzuordnungen** im Dialogfeld für die ausgewählte Tabelle. Verwenden Sie das Dialogfeld **Spaltenzuordnungen** , um Folgendes auszuführen.
-   Überprüfen Sie die Zuordnung einzelner Spalten zwischen der Quelle und dem Ziel.
-   Wenn Sie nur eine Teilmenge von Spalten kopieren möchten, wählen Sie **ignore** für Spalten aus, die Sie nicht kopieren möchten.

Weitere Informationen finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vorschau**  
Klicken Sie optional auf **Vorschau** um bis zu 200 Zeilen der Beispieldaten in der Vorschau anzuzeigen die **Vorschaudaten** (Dialogfeld). Dadurch können Sie sicherstellen, dass der Assistent die Daten kopieren wird, die Sie kopieren möchten. Weitere Informationen finden Sie unter [Datenvorschau](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Nachdem Sie die Daten in der Vorschau anzeigen, sollten Sie die Optionen ändern, die Sie auf den vorherigen Seiten des Assistenten ausgewählt haben. Um diese Änderungen vorzunehmen, wechseln Sie zurück auf die Seite **Quelltabellen und -sichten auswählen** , und klicken Sie auf **Zurück** , um zu vorherigen Seiten zurückzukehren, auf denen Sie Ihre jeweilige Auswahl ändern können.  

## <a name="select-source-and-destination-tables-for-excel"></a>Auswählen von Quell- und Zieltabellen für Excel

### <a name="excel-source-tables"></a>Excel-Quellentabellen
Die Liste der Quelltabellen und-sichten für eine Excel-Datenquelle enthält zwei Typen von Excel-Objekten.
-   **Arbeitsblätter:** Die Namen von Arbeitsblättern enden auf das Dollarzeichen ($): z.B. **Sheet1$**.
-   **Benannte Bereiche:** Benannte Bereiche sind ggf. nach dem Namen aufgeführt.

Sie müssen eine Abfrage schreiben, wenn Sie Daten von oder in einen bestimmten, unbenannten Zellbereich laden möchten: z.B. von oder in **[Sheet1$ A1:B4]**. Wechseln Sie zurück auf die Seite **Tabelle kopieren oder Datenbank abfragen** , uns wählen Sie **Abfrage zum Angeben der zu übertragenden Daten schreiben**aus.

#### <a name="prepare-the-excel-source-data"></a>Vorbereiten der Daten der Excel-Quelle
Unabhängig davon, ob Sie ein Arbeitsblatt oder einen Bereich als Quelltabelle angeben, liest der Treiber den *zusammenhängenden* Zellenblock ab der ersten nicht leeren Zelle in der linken oberen Ecke des Arbeitsblatts oder Bereichs. Folglich sind keine leeren Zeilen in den Quelldaten erlaubt. Es sind z.B. keine leeren Zellen zwischen den Spaltenkopfzeilen und den Datenzeilen erlaubt. Wenn sich zwischen dem Titel oben auf dem Arbeitsblatt und Ihren Daten eine leere Zeile befindet, können Sie das Arbeitsblatt nicht abfragen. In Excel müssen Sie Ihrem Datenbereich einen Namen zuweisen und den benannten Bereich statt des Arbeitsblatts abfragen.

### <a name="excel-destination-tables"></a>Excel-Zieltabellen
Wenn Sie Daten nach Excel exportieren, können Sie das Ziel wie folgt angeben.
-   **Arbeitsblatt:** Fügen Sie das $-Zeichen an das Ende des Blattnamens an, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B. **[Sheet1$]**, um ein Arbeitsblatt anzugeben.
-   **Benannter Bereich:** Verwenden Sie einfach den Namen des Bereichs, z.B. **MyDataRange**, um einen benannten Bereich anzugeben.
-   **Unbenannter Bereich:** Um einen Bereich von Zellen anzugeben, den Sie nicht benannt haben, fügen Sie das $-Zeichen an das Ende des Blattnamens an, fügen Sie die Bereichsspezifikation hinzu, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B: **[Sheet1$A1:B4]**.

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Besonderheiten bei Excel-Quellen und -Zielen
Wenn Sie Excel als Quelle oder Ziel verwenden, sollten Sie auf **Zuordnungen bearbeiten** klicken und die Datentypzuordnungen auf der Seite **Spaltenzuordnungen** überprüfen. 

**Datentypen in Excel-Arbeitsmappen:** Excel ist keine Standarddatenbank. Die Spalten haben keine festen Datentypen. Der Assistent erkennt nur eine begrenzte Anzahl von Excel-Datentypen: numeric, currency, Boolean, date/time, string (255 Zeichen oder weniger) und memo (mehr als 255 Zeichen). Der Assistent prüft eine bestimmte Anzahl von Zeilen (standardmäßig den ersten acht Zeilen) in einer vorhandenen Excel-Datenquelle, den Datentyp jeder Spalte zu erraten.

Wenn der Assistent explizite Konvertierungen von Datentypen ausführen muss, um Daten aus oder in Excel zu laden, wird i.d.R. die Seite **Datentypzuordnung überprüfen** angezeigt, auf der Sie diese Konvertierungen überprüfen können. Diese Konvertierungen können Folgendes enthalten:
-   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderer Typen.
-   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten anderer Längen.
-   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und nicht-Unicode-Zeichenfolgenspalten, die bestimmten Codepages verwenden.

### <a name="special-considerations-for-excel-sources"></a>Besonderheiten bei Excel-Quellen
**NULL- oder fehlende Werte in den importierten Daten:** Wenn eine Excel-Spalte offensichtlich gemischte Datentypen in den ersten acht Zeilen als Stichprobe verwendet, durch den Assistenten - enthält z. B. numerische Werte gemischt mit Textwerten - der Assistent wählt den meisten-Datentyp mit dem Datentyp der Spalte und gibt null-Werte für die Zellen dieser contai n Daten anderer Typen. Es besteht keine Möglichkeit, dieses Verhalten des Assistenten zu ändern.

**Abgeschnittene Zeichenfolgen in importierten Daten:** Wenn der Assistent bestimmt, dass eine Excel-Spalte Textdaten enthält, wählt der Assistent anhand des längsten Werts in ersten acht Zeilen den Datentyp aus (string oder memo). Wenn der Assistent in den Stichprobezeilen keine Werte mit mehr als 255 Zeichen findet, wird die Spalte nicht als Memospalte, sondern als Zeichenfolgenspalte mit 255 Zeichen behandelt, und alle Werte mit mehr als 255 Zeichen werden abgeschnitten. Zum Importieren von Daten aus einer Memospalte ohne das Abschneiden müssen Sie sicherstellen, dass die Memospalte mindestens ein Wert mit mehr als 255 Zeichen in den ersten acht Zeilen enthält, die vom Assistenten geprüft werden.

### <a name="special-considerations-for-excel-destinations"></a>Besonderheiten bei Excel-Zielen
**Angeben eines vorhandenen Datenbereichs:** Wenn Sie einen vorhandenen Bereich als Ziel angeben, erhalten Sie eine Fehlermeldung, wenn der Bereich weniger hat *Spalten* als die Quelldaten. Allerdings weniger verfügt der angegebene Bereich *Zeilen* als die Quelldaten der Assistent weiterhin des Schreibens von Zeilen und die Bereichsdefinition entsprechend die neue Anzahl der Zeilen erweitert.

**Speichern von Memodaten (ntext):** Der Assistent muss den Datentyp der Zielspalte als **memo** , nicht als **string**erkennen, damit Sie Zeichenfolgen mit mehr als 255 Zeichen in einer Excel-Spalte erfolgreich speichern können.
-   Wenn die Zieltabelle bereits Datenzeilen enthält, müssen die ersten acht Zeilen, die vom Assistenten als Stichprobe genommen werden mindestens eine Zeile mit einem Wert, der länger als 255 Zeichen in der Memospalte enthalten.
-   Wenn die Zieltabelle vom Assistenten erstellt wird die **CREATE TABLE** -Anweisung verwenden muss **LONGTEXT** (oder eines der Synonyme) mit dem Datentyp, der die der Memospalte. Überprüfen Sie die **CREATE TABLE** Anweisung und überarbeiten, falls erforderlich, indem Sie auf **SQL bearbeiten** neben der **Zieltabelle erstellen** option die **Spalte Zuordnungen** Seite.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nach der Auswahl der zu kopierenden vorhandenen Tabellen und Sichten und dem Zuordnen dieser zu ihren Zielen ist **Paket speichern und ausführen**die nächste Seite. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



