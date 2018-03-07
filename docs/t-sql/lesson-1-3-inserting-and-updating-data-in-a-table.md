---
title: "Einfügen und Aktualisieren von Daten in einer Tabelle (Lernprogramm) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c64d3f2835e7c63b8c8e86946545641015188e29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-1-3---inserting-and-updating-data-in-a-table"></a>Lektion 1 bis 3-einfügen und Aktualisieren von Daten in einer Tabelle
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]Nun, dass Sie erstellt haben die **Produkte** auswählen, sollten Sie zum Einfügen von Daten in die Tabelle mit der INSERT-Anweisung bereit. Nach dem Einfügen der Daten ändern Sie den Inhalt einer Zeile mithilfe einer UPDATE-Anweisung. Mithilfe der WHERE-Klausel der UPDATE-Anweisung schränken Sie das Update auf eine einzelne Zeile ein. Durch die vier Anweisungen werden die folgenden Daten eingegeben.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
Die grundlegende Syntax lautet: INSERT, Tabellenname, Spaltenliste, VALUES und dann eine Liste der einzufügenden Werte. Die beiden Bindestriche vor einer Zeile geben an, dass es sich bei der Zeile um einen Kommentar handelt, der vom Compiler ignoriert wird. In diesem Fall wird im Kommentar eine zulässige Variante der Syntax beschrieben.  
  
### <a name="to-insert-data-into-a-table"></a>So fügen Sie Daten in eine Tabelle ein  
  
1.  Führen Sie die folgende Anweisung aus, um eine Zeile in die in der vorhergehenden Aufgabe erstellte `Products` -Tabelle einzufügen. Dies ist die grundlegende Syntax.  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  In der folgenden Anweisung sehen Sie, wie die Reihenfolge, in der die Parameter bereitgestellt werden, durch Wechseln der Position von `ProductID` und `ProductName` sowohl in der Liste der Felder (in Klammern) als auch in der Liste der Werte geändert werden kann.  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  Die folgende Anweisung veranschaulicht, dass die Namen der Spalten optional sind, solange die Werte in der richtigen Reihenfolge aufgelistet werden. Obwohl diese Syntax gängig ist, wird ihre Verwendung nicht empfohlen, da sie das Verständnis des Codes durch Dritte erschweren könnte. `NULL` wird für die `Price` -Spalte angegeben, da der Preis für dieses Produkt noch nicht bekannt ist.  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  Der Schemaname ist optional, solange Sie auf eine Tabelle im Standardschema zugreifen und diese ändern. Da die `ProductDescription` -Spalte NULL-Werte zulässt und kein Wert bereitgestellt wird, können Name und Wert der `ProductDescription` -Spalte vollständig aus der Anweisung gelöscht werden.  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>So aktualisieren Sie die Products-Tabelle  
  
1.  Geben Sie die folgende `UPDATE` -Anweisung zum Ändern von `ProductName` des zweiten Produkts von `Screwdriver`in `Flat Head Screwdriver`ein, und führen Sie sie aus.  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Lesen der Daten in einer Tabelle &#40;Tutorial&#41;](../t-sql/lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>Siehe auch  
[INSERT &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../t-sql/queries/update-transact-sql.md)  
  
  
  
