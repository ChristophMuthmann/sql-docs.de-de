---
title: Erstellen von Sichten und gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1bc361e589dba1215781adcf951fd419b7dc806f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-3---creating-views-and-stored-procedures"></a>Lektion 2 – 3 – Erstellen von Sichten und gespeicherte Prozeduren
Nachdem Mary nun auf die **TestData** -Datenbank zugreifen kann, möchten Sie möglicherweise einige Datenbankobjekte erstellen, wie z. B. eine Sicht und eine gespeicherte Prozedur, und Mary dann Zugriff auf diese Objekte erteilen. Bei einer Sicht handelt es sich um eine gespeicherte SELECT-Anweisung, und eine gespeicherte Prozedur setzt sich aus einer oder mehreren [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen zusammen, die als Batch ausgeführt werden.  
  
Sichten werden wie Tabellen abgefragt und nehmen keine Parameter an. Gespeicherte Prozeduren sind komplexer als Sichten. Gespeicherte Prozeduren können sowohl Eingabe- als auch Ausgabeparameter aufweisen und Anweisungen enthalten, die den Ablauf des Codes steuern, wie z. B. IF- und WHILE-Anweisungen. Als eine der Grundregeln guter Programmierung gilt die Verwendung gespeicherter Prozeduren für alle Aktionen, die sich in der Datenbank wiederholen.  
  
In diesem Beispiel erstellen Sie mithilfe von CREATE VIEW eine Sicht, die nur zwei der Spalten in der **Products** -Tabelle auswählt. Sie erstellen dann mithilfe von CREATE PROCEDURE eine gespeicherte Prozedur, die einen Parameter für den Preis akzeptiert und nur die Produkte zurückgibt, deren Preis unter dem angegebenen Parameterwert liegt.  
  
### <a name="to-create-a-view"></a>So erstellen Sie eine Sicht  
  
1.  Führen Sie die folgende Anweisung aus, um eine sehr einfache Sicht zu erstellen, die eine SELECT-Anweisung ausführt und die Namen und Preise der Produkte an den Benutzer zurückgibt.  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>Testen der Sicht  
  
1.  Sichten werden genau wie Tabellen behandelt. Greifen Sie mithilfe einer `SELECT` -Anweisung auf eine Sicht zu.  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>So erstellen Sie eine gespeicherte Prozedur  
  
1.  Die folgende Anweisung erstellt eine gespeicherte Prozedur namens `pr_Names`, die einen Eingabeparameter mit der Bezeichnung `@VarPrice` vom Datentyp `money`akzeptiert. Die gespeicherte Prozedur druckt die mit dem Eingabeparameter verkettete `Products less than` -Anweisung. Dieser Parameter wird vom `money` -Datentyp in den `varchar(10)` -Zeichendatentyp geändert. Dann führt die Prozedur eine `SELECT` -Anweisung für die Sicht aus und übergibt dabei den Eingabeparameter als Teil der `WHERE` -Klausel. Dadurch werden alle Produkte zurückgegeben, deren Preis unter dem Wert des Eingabeparameters liegt.  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>Testen der gespeicherten Prozedur.  
  
1.  Wenn Sie die gespeicherte Prozedur testen möchten, geben Sie die folgende Anweisung ein, und führen Sie sie aus. Die Prozedur sollte die Namen der beiden Produkte zurückgeben, die Sie in Lektion 1 mit einem Preis unter `Products` in die `10.00`-Tabelle eingegeben haben.  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Erteilen des Zugriffs auf ein Datenbankobjekt](../t-sql/lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>Siehe auch  
[CREATE VIEW &#40;Transact-SQL&#41;](../t-sql/statements/create-view-transact-sql.md)  
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../t-sql/statements/create-procedure-transact-sql.md)  
  
  
  

