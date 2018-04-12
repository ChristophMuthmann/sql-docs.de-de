---
title: Quelltabellen und -sichten auswählen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2424f3f7ad290a3ae81c7b97a39abf55f52e771
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
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

> [!IMPORTANT]
> Ausführliche Informationen über das Herstellen einer Verbindung mit Excel-Dateien sowie Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).

### <a name="excel-source-tables"></a>Excel-Quellentabellen
Die Liste der Quelltabellen und-sichten für eine Excel-Datenquelle enthält zwei Typen von Excel-Objekten.
-   **Arbeitsblätter:** Die Namen von Arbeitsblättern enden auf das Dollarzeichen ($): z.B. **Sheet1$**.
-   **Benannte Bereiche:** Benannte Bereiche sind ggf. nach dem Namen aufgeführt.

Sie müssen eine Abfrage schreiben, wenn Sie Daten von oder in einen bestimmten, unbenannten Zellbereich laden möchten: z.B. von oder in **[Sheet1$ A1:B4]**. Wechseln Sie zurück auf die Seite **Tabelle kopieren oder Datenbank abfragen** , uns wählen Sie **Abfrage zum Angeben der zu übertragenden Daten schreiben**aus.

### <a name="excel-destination-tables"></a>Excel-Zieltabellen
Wenn Sie Daten nach Excel exportieren, können Sie das Ziel wie folgt angeben.
-   **Arbeitsblatt:** Fügen Sie das $-Zeichen an das Ende des Blattnamens an, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B. **[Sheet1$]**, um ein Arbeitsblatt anzugeben.
-   **Benannter Bereich:** Verwenden Sie einfach den Namen des Bereichs, z.B. **MyDataRange**, um einen benannten Bereich anzugeben.
-   **Unbenannter Bereich:** Um einen Bereich von Zellen anzugeben, den Sie nicht benannt haben, fügen Sie das $-Zeichen an das Ende des Blattnamens an, fügen Sie die Bereichsspezifikation hinzu, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B: **[Sheet1$A1:B4]**.

> [!TIP]
> Wenn Sie Excel als Quelle oder Ziel verwenden, sollten Sie auf **Zuordnungen bearbeiten** klicken und die Datentypzuordnungen auf der Seite **Spaltenzuordnungen** überprüfen. 

## <a name="whats-next"></a>Wie geht es weiter?  
 Nach der Auswahl der zu kopierenden vorhandenen Tabellen und Sichten und dem Zuordnen dieser zu ihren Zielen ist **Paket speichern und ausführen**die nächste Seite. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md)



