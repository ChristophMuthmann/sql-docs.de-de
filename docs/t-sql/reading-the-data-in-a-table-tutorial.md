---
title: "Lesen der Daten in einer Tabelle (Lernprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "Lesen von Daten in einer Tabelle"
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Lesen der Daten in einer Tabelle (Lernprogramm)
Daten in einer Tabelle können mithilfe der SELECT-Anweisung gelesen werden. Die SELECT-Anweisung gehört zu den wichtigsten [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen. Ihre Syntax zeichnet sich durch unzählige Variationen aus. In diesem Lernprogramm arbeiten Sie mit fünf einfachen Versionen.  
  
### So lesen Sie die Daten in einer Tabelle  
  
1.  Geben Sie die folgenden Anweisungen zum Lesen der Daten in der `Products` -Tabelle ein, und führen Sie sie aus.  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  Sie können alle Spalten in der Tabelle mithilfe eines Sternchens (*) auswählen. Dies wird häufig bei Ad-hoc-Abfragen verwendet. Sie sollten die Spaltenliste im dauerhaften Code bereitstellen, sodass die Anweisung die vorhergesagten Spalten zurückgibt, selbst wenn der Tabelle später eine neue Spalte hinzugefügt wird.  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  Sie können Spalten auslassen, die nicht zurückgegeben werden sollen. Die Spalten werden in der Reihenfolge zurückgegeben, in der sie aufgelistet sind.  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  Mithilfe einer `WHERE` -Klausel können Sie die an den Benutzer zurückgegebenen Zeilen beschränken.  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  Sie können die Werte in den Spalten direkt nach ihrer Rückgabe bearbeiten. Im folgenden Beispiel wird eine mathematische Operation für die `Price` -Spalte ausgeführt. Spalten, die auf diese Weise geändert wurden, weisen keinen Namen auf, es sei denn, Sie geben einen Namen mithilfe des `AS` -Schlüsselworts an.  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## Funktionen, die in einer SELECT-Anweisung nützlich sind  
Weitere Informationen zu bestimmten Funktionen, die zum Bearbeiten von Daten in SELECT-Anweisungen verwendet werden können, finden Sie in den folgenden Themen:  
  
|||  
|-|-|  
|[Zeichenfolgenfunktionen &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Mathematische Funktionen &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Text- und Bildfunktionen &#40;Transact-SQL&#41;](../Topic/Text%20and%20Image%20Functions%20(Transact-SQL).md)|  
  
## Nächste Aufgabe in der Lektion  
[Zusammenfassung: Erstellen von Datenbankobjekten](../t-sql/summary-creating-database-objects.md)  
  
## Siehe auch  
[SELECT &#40;Transact-SQL&#41;](../t-sql/queries/select-transact-sql.md)  
  
  
  
