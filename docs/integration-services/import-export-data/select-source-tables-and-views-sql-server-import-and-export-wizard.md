---
title: "Quelltabellen und -sichten auswählen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
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
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 600e734c11a597cdcbae0279e1604bd96ccfb06f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Quelltabellen und -sichten auswählen (SQL Server-Import/Export-Assistent)
  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent zeigt die Seite **Quelltabellen und -sichten auswählen**an, nachdem Sie angegeben haben, dass Sie eine vollständige Tabelle kopieren möchten, oder nachdem Sie eine Abfrage bereitstellen. Auf dieser Seite wählen Sie die vorhandenen Tabellen und Sichten zum Kopieren aus. Anschließend ordnen Sie die Quelltabellen neuen oder vorhandenen Zieltabellen zu. Optional können Sie auch die Zuordnung einzelner Spalten überprüfen und eine Vorschau von Beispieldaten anzeigen.

> [!TIP]
> Wenn Sie mehr als eine SQL Server-Datenbank oder SQL Server-Datenbankobjekte kopieren müssen, die keine Tabellen und Sichten sind, verwenden Sie den Assistenten zum Kopieren von Datenbanken anstelle des Import/Export-Assistenten. Weitere Informationen finden Sie unter [Verwenden des Assistenten zum Kopieren von Datenbanken](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Screenshot: Wenn Sie Tabellen kopieren möchten  
 Der folgende Screenshot zeigt ein Beispiel der Seite **Quelltabellen und -sichten auswählen** des Assistenten, wenn Sie vorher die Option **Daten aus mindestens einer Tabelle oder Sicht kopieren** auf der Seite **Tabelle kopieren oder Datenbank abfragen** auswählen. In der Liste finden Sie alle in der Datenquelle verfügbaren Tabellen und Sichten.
 
In diesem Beispiel enthält die Liste **Quelle** alle Tabellen der AdventureWorks-Beispieldatenbank. Die ausgewählte Zeile zeigt an, dass der Benutzer die Tabelle **Sales.Customer** von der Quelle in die neue Tabelle **Sales.CustomerNew** des Ziels kopieren möchte. 
   
 ![Seite „Tabellen auswählen“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/select-tables1.png "Select tables page of the Import and Export Wizard")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Screenshot: Wenn Sie eine Abfrage bereitgestellt haben  
 Der folgende Screenshot zeigt ein Beispiel der Seite **Quelltabellen und -sichten auswählen** des Assistenten, wenn Sie zuvor die Option **Abfrage zum Angeben der zu übertragenden Daten schreiben** auf der Seite **Tabelle kopieren oder Datenbank abfragen** ausgewählt haben. Die Liste **Quelle** enthält nur eine einzige Zeile. In dieser stellt das Element `[Query]` die Abfrage dar, die Sie auf der Seite **Quellabfrage angeben** bereitgestellt haben.
 
In diesem Beispiel möchte der Benutzer die Abfrageergebnisse aus der Quelle in die **Sales.CustomerNew** am Ziel kopieren.  
    
 ![Seite „Tabellen auswählen“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/select-tables2.png "Select tables page of the Import and Export Wizard")  

## <a name="select-source-and-destination-tables"></a>Auswählen von Quell- und Zieltabellen 
**Quelle**  
Wählen Sie mithilfe der Kontrollkästchen aus der Liste der verfügbaren Tabellen und Sichten die in das Ziel zu kopierenden Elemente aus. Standardmäßig werden die Daten aus der Datenquelle unverändert kopiert. Wenn Sie eine neue Zieltabelle erstellen, wird das Schema für die neue Tabelle (d.h. die Liste der Zeilen und deren Eigenschaften) ebenfalls ohne Änderung aus der Datenquelle kopiert.

Wenn Sie eine Abfrage bereitgestellt haben, enthält die Liste nur das Element `[Query]`. 

**Ziel**  
 Wählen Sie eine Zieltabelle aus der Liste für jede Quelltabelle oder Abfrage aus, oder geben Sie den Namen einer neuen Tabelle ein, die vom Assistenten erstellt werden soll. Wenn Sie eine vorhandene Zieltabelle auswählen, muss die Tabelle über Spalten und Datentypen verfügen, die mit der Quelltabelle kompatibel sind.  

> [!NOTE]
> Wenn Sie zu diesem Zeitpunkt den Assistenten anhalten, um manuell mit einem Tool (wie z.B.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) eine neue Tabelle in der Zieldatenbank zu erstellen, ist die neue Tabelle in der Liste verfügbarer Zieltabellen nicht sofort sichtbar. Zum Aktualisieren der Liste der Zieltabellen wechseln Sie zurück zur Seite **Ziel auswählen** , wählen Sie die Zieldatenbank erneut aus, um die Liste der verfügbaren Tabellen und Sichten zu aktualisieren, und wechseln Sie dann wieder zur Seite **Quelltabellen und -sichten auswählen** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Optionales Überprüfen der Spaltenzuordnungen und Anzeigen der Datenvorschau
**Zuordnungen bearbeiten**   
Klicken Sie optional auf **Zuordnungen bearbeiten**, um das Dialogfeld **Spaltenzuordnungen** für die ausgewählte Tabelle anzuzeigen. Verwenden Sie das Dialogfeld **Spaltenzuordnungen** , um Folgendes auszuführen.
-   Überprüfen Sie die Zuordnung einzelner Spalten zwischen der Quelle und dem Ziel.
-   Wenn Sie nur eine Teilmenge von Spalten kopieren möchten, wählen Sie **ignore** für Spalten aus, die Sie nicht kopieren möchten.

Weitere Informationen finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vorschau**  
Klicken Sie optional auf **Vorschau**, um bis zu 200 Zeilen mit Beispieldaten im Dialogfeld **Datenvorschau** anzuzeigen. Dadurch können Sie sicherstellen, dass der Assistent die Daten kopieren wird, die Sie kopieren möchten. Weitere Informationen finden Sie unter [Datenvorschau](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
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

**Datentypen in Excel-Arbeitsmappen:** Excel ist keine Standarddatenbank. Die Spalten haben keine festen Datentypen. Der Assistent erkennt nur eine begrenzte Anzahl von Excel-Datentypen: numeric, currency, Boolean, date/time, string (255 Zeichen oder weniger) und memo (mehr als 255 Zeichen). Der Assistent fragt eine bestimmte Anzahl von Zeilen in einer vorhandenen Excel-Datenquelle ab (standardmäßig die ersten acht Zeilen), um den Datentyp jeder Spalte zu ermitteln.

Wenn der Assistent explizite Konvertierungen von Datentypen ausführen muss, um Daten aus oder in Excel zu laden, wird i.d.R. die Seite **Datentypzuordnung überprüfen** angezeigt, auf der Sie diese Konvertierungen überprüfen können. Diese Konvertierungen können Folgendes enthalten:
-   Konvertierung zwischen numerischen Excel-Spalten mit doppelter Genauigkeit und numerischen Spalten anderer Typen.
-   Konvertierung zwischen Excel-Zeichenfolgenspalten mit 255 Zeichen und Zeichenfolgenspalten anderer Längen.
-   Konvertierung zwischen Unicode-Excel-Zeichenfolgenspalten und Nicht-Unicode-Zeichenfolgenspalten, die bestimmte Codepages verwenden.

### <a name="special-considerations-for-excel-sources"></a>Besonderheiten bei Excel-Quellen
**NULL- oder fehlende Werte in den importierten Daten:** Wenn eine Excel-Spalte in den ersten acht Zeilen, die vom Assistenten als Stichprobe entnommen wurden, scheinbar gemischte Datentypen enthält (z.B. numerische Werte gemischt mit Textwerten), wählt der Assistent den am häufigsten verwendeten Datentyp der Spalte und gibt NULL-Werte für die Zellen zurück, die andere Datentypen enthalten. Es besteht keine Möglichkeit, dieses Verhalten des Assistenten zu ändern.

**Abgeschnittene Zeichenfolgen in importierten Daten:** Wenn der Assistent bestimmt, dass eine Excel-Spalte Textdaten enthält, wählt der Assistent anhand des längsten Werts in ersten acht Zeilen den Datentyp aus (string oder memo). Wenn der Assistent in den Stichprobezeilen keine Werte mit mehr als 255 Zeichen findet, wird die Spalte nicht als Memospalte, sondern als Zeichenfolgenspalte mit 255 Zeichen behandelt, und alle Werte mit mehr als 255 Zeichen werden abgeschnitten. Sie müssen zum Importieren von Daten aus einer Memospalte ohne Abschneiden sicherstellen, dass die Memospalte in den ersten acht Zeilen, die vom Assistenten als Stichprobe entnommen wurden, mindestens einen Wert enthält, der länger als 255 Zeichen ist.

### <a name="special-considerations-for-excel-destinations"></a>Besonderheiten bei Excel-Zielen
**Angeben eines vorhandenen Datenbereichs:** Wenn Sie einen vorhandenen Bereich als Ziel angeben, wird ein Fehler zurückgegeben, sofern dieser weniger *Spalten* als die Quelldaten enthält. Wenn der Bereich, den Sie angeben, jedoch weniger *Zeilen* als die Quelldaten aufweist, schreibt der Assistent weiterhin Zeilen und erweitert die Bereichsdefinition, sodass sie mit der neuen Zeilenanzahl übereinstimmt.

**Speichern von Memodaten (ntext):** Der Assistent muss den Datentyp der Zielspalte als **memo** , nicht als **string**erkennen, damit Sie Zeichenfolgen mit mehr als 255 Zeichen in einer Excel-Spalte erfolgreich speichern können.
-   Wenn die Zieltabelle bereits Datenzeilen enthält, müssen die ersten acht Zeilen, die vom Assistenten als Stichprobe entnommen werden, mindestens eine Zeile mit einem Wert mit mehr als 255 Zeichen in der Memospalte enthalten.
-   Wenn die Zieltabelle vom Assistenten erstellt wird, muss die **CREATE TABLE**-Anweisung **LONGTEXT** (oder Synonyme) als Datentyp für die Memospalte verwenden. Überprüfen Sie die Anweisung **CREATE TABLE**, und bearbeiten Sie diese bei Bedarf, indem Sie auf der Seite **Spaltenzuordnungen** neben der Option **Zieltabelle erstellen** auf **SQL bearbeiten** klicken.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nach der Auswahl der zu kopierenden vorhandenen Tabellen und Sichten und dem Zuordnen dieser zu ihren Zielen ist **Paket speichern und ausführen**die nächste Seite. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


