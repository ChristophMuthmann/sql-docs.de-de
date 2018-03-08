---
title: Angeben einer Quellabfrage (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4399fdeb68ee0768ac083e0193ae0513b221021d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Quellabfrage angeben (SQL Server-Import/Export-Assistent)
Wenn Sie angegeben haben, dass Sie eine Abfrage zum Auswählen der zu kopierenden Daten bereitstellen möchten, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent **Quellabfrage angeben**an. Auf dieser Seite schreiben und testen Sie die SQL-Abfrage, die die Daten sammelt, die aus der Datenquelle in das Ziel kopiert werden sollen. Sie können außerdem den Text einer gespeicherten Abfrage einfügen oder den Abfragetext aus einer Datei laden.

## <a name="screen-shot-of-the-source-query-page"></a>Screenshot der Seite „Quellabfrage“  
Die folgende Abbildung zeigt die Seite **Quellabfrage angeben** des Assistenten.
 
In diesem einfachen Beispiel hat der Benutzer die Abfrage `SELECT * FROM Sales.Customer` eingegeben, um alle Zeilen und Spalten aus der Tabelle **Sales.Customer** in der Quelldatenbank zu kopieren.
-   `SELECT *` bedeutet, dass alle Spalten kopiert werden.
-   Das Fehlen einer `WHERE`-Klausel bedeutet, dass alle Zeilen kopiert werden.
  
 ![Seite „Quellabfrage“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/source-query.png "Source query page of the Import and Export Wizard")  

## <a name="provide-the-query-and-check-its-syntax"></a>Bereitstellen der Abfrage und Überprüfen von deren Syntax
**SQL-Anweisung**  
 Geben Sie eine SELECT-Abfrage ein, um bestimmte Datenzeilen und -spalten aus der Quelldatenbank abzurufen. Sie können auch den Text einer gespeicherten Abfrage einfügen oder die Abfrage aus einer Datei laden, indem Sie auf **Durchsuchen** klicken. 
  
 Die folgende Abfrage ruft z.B. die Daten zu **SalesPersonID**, **SalesQuota** und **SalesYTD** aus der AdventureWorks-Beispieldatenbank für Vertriebsmitarbeiter ab, deren Provisionsanteil größer als 1,5 % ist.  
  
```sql
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

Weitere Beispiele für SELECT-Abfragen finden Sie unter [SELECT-Beispiele &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) oder suchen Sie online.  

Wenn Ihre Datenquelle Excel ist, gehen Sie zu [Bereitstellen einer Datenabfrage für Excel](#excelQueries) weiter unten in diesem Thema, um zu erfahren, wie Excel-Arbeitsblätter und Excel-Bereiche in einer Abfrage angegeben werden.
  
 **Analysieren**  
 Überprüft die Syntax der SQL-Anweisung, die Sie in das Textfeld **SQL-Anweisung** eingegeben haben.  
  
> [!NOTE]
> Wenn die für die Prüfung der Anweisungssyntax erforderliche Zeit den Timeoutwert von 30 Sekunden überschreitet, wird die Analyse beendet und ein Fehler ausgelöst. Sie können erst nach erfolgreicher Analyse über diese Seite des Assistenten hinaus gelangen. Eine Lösung zum Vermeiden eines Timeouts besteht darin, eine Datenbanksicht basierend auf der gewünschten Abfrage zu erstellen und die Sicht im Assistenten abzufragen, statt den Abfragetext direkt einzugeben.  
  
 **Durchsuchen**  
 Suchen Sie mithilfe des Dialogfelds **Öffnen** eine Datei, die den Text einer SQL-Abfrage enthält. Durch das Auswählen einer Datei wird der Test aus der Datei in das Textfeld **SQL-Anweisung** kopiert.  
 
## <a name="excelQueries"></a> Bereitstellen einer Datenabfrage für Excel
### <a name="specify-excel-objects-in-queries"></a>Angeben von Excel-Objekten in Abfragen
Es gibt drei Arten von Excel-Objekten, die Sie abfragen können.
-   **Arbeitsblatt:** Fügen Sie das $-Zeichen an das Ende des Blattnamens an, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B. **[Sheet1$]**, um ein Arbeitsblatt abzufragen.

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **Benannter Bereich:** Verwenden Sie einfach den Namen des Bereichs, z.B. **MyDataRange**, um einen benannten Bereich anzugeben.
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **Unbenannter Bereich:** Um einen Bereich von Zellen anzugeben, den Sie nicht benannt haben, fügen Sie das $-Zeichen an das Ende des Blattnamens an, fügen Sie die Bereichsspezifikation hinzu, und schließen Sie die Zeichenfolge in Trennzeichen ein, z.B: **[Sheet1$A1:B4]**.

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

### <a name="prepare-the-excel-source-data"></a>Vorbereiten der Daten der Excel-Quelle
Unabhängig davon, ob Sie ein Arbeitsblatt oder einen Bereich als Quelltabelle angeben, liest der Treiber den *zusammenhängenden* Zellenblock ab der ersten nicht leeren Zelle in der linken oberen Ecke des Arbeitsblatts oder Bereichs. Folglich sind keine leeren Zeilen in den Quelldaten erlaubt. Es sind z.B. keine leeren Zellen zwischen den Spaltenkopfzeilen und den Datenzeilen erlaubt. Wenn sich zwischen dem Titel oben auf dem Arbeitsblatt und Ihren Daten eine leere Zeile befindet, können Sie das Arbeitsblatt nicht abfragen. In Excel müssen Sie Ihren Datenbereich einen Namen zuweisen und den benannten Bereich statt des Arbeitsblatts abfragen.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie die SQL-Abfrage geschrieben und getestet haben, die die zu kopierenden Daten auswählt, hängt die nächste Seite vom Ziel Ihrer Daten ab.  
  
-   Für die meisten Ziele lautet die nächste Seite **Quelltabellen und -sichten auswählen**. Auf dieser Seite überprüfen Sie die Abfrage, die Sie angegeben haben, und wählen optional die zu kopierenden Spalten und Vorschaubeispieldaten. Weitere Informationen finden Sie unter [Quelltabellen und -sichten auswählen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).  
  
-   Wenn Ihr Ziel eine Flatfile ist, lautet die nächste Seite **Flatfileziel konfigurieren**. Auf dieser Seite geben Sie Formatierungsoptionen für das Flatfileziel an. (Nach der Konfiguration der Flatfile heißt die nächste Seite **Quelltabellen und -sichten auswählen**.) Weitere Informationen finden Sie unter [Flatfileziel konfigurieren](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  


