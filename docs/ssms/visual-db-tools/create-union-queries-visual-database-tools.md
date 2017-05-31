---
title: Erstellen von UNION-Abfragen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6c1ec545f2175067a3e4d6f9f625356607cb0eb4
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-union-queries-visual-database-tools"></a>Erstellen von UNION-Abfragen (Visual Database Tools)
Mit dem Schlüsselwort UNION können Sie die Ergebnisse von zwei SELECT-Anweisungen in eine Ergebnistabelle aufnehmen. Alle Zeilen, die von den beiden SELECT-Anweisungen zurückgegeben werden, werden zum Ergebnis des UNION-Ausdrucks kombiniert. Beispiele finden Sie unter [SELECT-Beispiele (Transact-SQL)](http://msdn.microsoft.com/en-us/9b9caa3d-e7d0-42e1-b60b-a5572142186c).  
  
> [!NOTE]  
> Im Diagrammbereich kann nur eine SELECT-Klausel angezeigt werden. Wenn Sie eine UNION-Abfrage verwenden, wird der Bereich Tabellenvorgänge Abfrage-Designer daher nicht angezeigt.  
  
### <a name="to-create-a-merged-select-query"></a>So erstellen Sie eine zusammengeführte SELECT-Abfrage  
  
1.  Öffnen Sie eine Abfrage, oder erstellen Sie eine neue.  
  
2.  Geben Sie im Bereich SQL einen gültigen UNION-Ausdruck ein.  
  
    Das folgende Beispiel stellt einen gültigen UNION-Ausdruck dar.  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  Klicken Sie im Menü **Abfrage-Designer** auf **SQL ausführen** , um die Abfrage auszuführen.  
  
    Die UNION-Abfrage wird jetzt vom Abfrage-Designer formatiert.  
  
## <a name="see-also"></a>Siehe auch  
[Unterstützte Abfragetypen (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](http://msdn.microsoft.com/en-us/607c296f-8a6a-49bc-975a-b8d0c0914df7)  
  

