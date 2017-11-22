---
title: MSSQLSERVER_4186 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20e18dc0d5ed5411c259fada355a25a9fba4b9bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver4186"></a>MSSQLSERVER_4186
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|4186|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Auf die Spalte "%ls.%.*ls" kann in der OUTPUT-Klausel nicht verwiesen werden, weil die Spaltendefinition eine Unterabfrage enthält oder auf eine Funktion verweist, die einen Zugriff auf Benutzer- oder Systemdaten ausführt. Für eine Funktion, die nicht schemagebunden ist, wird standardmäßig angenommen, dass sie auf Daten zugreift. Erwägen Sie, die Unterabfrage bzw. die Funktion aus der Spaltendefinition zu entfernen oder die Spalte aus der OUTPUT-Klausel zu entfernen.|  
  
## <a name="explanation"></a>Erklärung  
Um nicht deterministisches Verhalten zu vermeiden, darf die OUTPUT-Klausel nicht auf eine Spalte einer Sicht oder Inline-Tabellenwertfunktion verweisen, wenn diese Spalte mithilfe einer der folgenden Methoden definiert wurde:  
  
-   Eine Unterabfrage.  
  
-   Eine benutzerdefinierte Funktion, die auf Benutzer- oder Systemdaten zugreift bzw. bei der davon ausgegangen wird, dass sie einen solchen Zugriff ausführt.  
  
-   Eine berechnete Spalte, die eine benutzerdefinierte Funktion enthält, die in ihrer Definition auf Benutzer- oder Systemdaten zugreift.  
  
### <a name="examples"></a>Beispiele  
**Von einer Unterabfrage definierte Sichtspalte**  
  
Im folgenden Beispiel wird eine Sicht erstellt, die eine Unterabfrage in der Auswahlliste verwendet, um die Spalte `State` zu definieren. Anschließend verweist eine UPDATE-Anweisung auf die `State`-Spalte in der OUTPUT-Klausel und verursacht aufgrund der Unterabfrage in der Auswahlliste einen Fehler.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
**Von einer Funktion definierte Sichtspalte**  
  
Im folgenden Beispiel wird eine Sicht erstellt, die eine Datenzugriff-Skalarfunktion `dbo.ufnGetStock` in der Auswahlliste verwendet, um die `CurrentInventory`-Spalte zu definieren. Anschließend verweist eine UPDATE-Anweisung auf die `CurrentInventory`-Spalte in der OUTPUT-Klausel.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>Benutzeraktion  
Sie können Fehler 4186 auf eine der folgenden Arten beheben:  
  
-   Verwenden Sie anstelle von Unterabfragen Joins, um die Spalte in der Sicht oder der Funktion zu definieren. Sie können die Sicht `dbo.V1` z. B. wie folgt umschreiben.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   Untersuchen Sie die Definition der benutzerdefinierten Funktion. Wenn die Funktion keinen Zugriff auf Benutzer- oder Systemdaten ausführt, können Sie die Funktion ändern, um die WITH SCHEMABINDING-Klausel einzubinden.  
  
-   Entfernen Sie die Spalte aus der OUTPUT-Klausel.  
  
## <a name="see-also"></a>Siehe auch  
[OUTPUT Clause &#40;Transact-SQL&#41;](~/t-sql/queries/output-clause-transact-sql.md)  
  
