---
title: "Erstellen einer Planhinweisliste für parametrisierte Abfragen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d3d5c980047d9c84a1eea6e48d6070ca704377a9
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>Erstellen einer Planhinweisliste für parametrisierte Abfragen
  Eine TEMPLATE-Planhinweisliste zur Übereinstimmung mit eigenständigen Abfragen, die in einer angegebenen Form parametrisiert werden.  
  
 Im folgenden Beispiel wird eine Planhinweisliste erstellt, die mit einer beliebigen Abfrage übereinstimmt, die in einer bestimmten Form parametrisiert wird. Außerdem wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angewiesen, die Parametrisierung der Abfrage zu erzwingen. Die folgenden beiden Abfragen sind syntaktisch gleichwertig, unterscheiden sich jedoch in ihren konstanten Literalwerten.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 Dies ist die Planhinweisliste für die parametrisierte Form der Abfrage:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Im vorhergehenden Beispiel entspricht der Wert des `@stmt` -Parameters der parametrisierten Form der Abfrage. Die einzig zuverlässige Möglichkeit, diesen Wert für die Verwendung in sp_create_plan_guide abzurufen, ist die gespeicherte Systemprozedur [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) . Mithilfe des folgenden Skripts können Sie die parametrisierte Abfrage abrufen und anschließend eine Planhinweisliste für die Abfrage erstellen.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  Der Wert der konstanten Literale in dem an `@stmt` übergebenen `sp_get_query_template` -Parameter kann sich auf den Datentyp auswirken, der für den Parameter, der das Literal ersetzt, gewählt wird. Dies wiederum beeinflusst den Planhinweislistenabgleich. Möglicherweise müssen mehrere Planhinweislisten für verschiedene Parameterwertbereiche erstellt werden.  
  
 Sie haben auch die Möglichkeit, TEMPLATE-Planhinweislisten zusammen mit SQL-Planhinweislisten zu verwenden. Beispielsweise können Sie eine TEMPLATE-Planhinweisliste erstellen, um sicherzustellen, dass eine bestimmte Abfrageklasse parametrisiert wird. Anschließend können Sie eine SQL-Planhinweisliste für die parametrisierte Form dieser Abfragen erstellen.  
  
  
