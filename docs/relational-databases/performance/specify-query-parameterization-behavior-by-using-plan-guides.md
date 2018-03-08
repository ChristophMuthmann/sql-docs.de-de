---
title: Angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
caps.latest.revision: "35"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 300fd06c7de6889cf8198aeb803d67398a0776e9
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>Angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn die PARAMETERIZATION-Datenbankoption auf SIMPLE festgelegt ist, kann der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer die Abfragen ggf. parametrisieren. Dies bedeutet, dass alle eventuell in einer Abfrage enthaltenen Literalwerte durch Parameter ersetzt werden. Dieses Verfahren wird als einfache Parametrisierung bezeichnet. Wenn die einfache Parametrisierung aktiviert ist, können Sie nicht steuern, welche Abfragen parametrisiert werden sollen und welche nicht. Sie können jedoch angeben, dass alle Abfragen einer Datenbank parametrisiert werden sollen, indem Sie die PARAMETERIZATION-Datenbankoption auf FORCED festlegen. Dieses Verfahren wird als erzwungene Parametrisierung bezeichnet.  
  
 Sie können das Parametrisierungsverhalten einer Datenbank überschreiben, in dem Sie Planhinweislisten verwenden. Es gibt dabei folgende Möglichkeiten:  
  
-   Wenn die PARAMETERIZATION-Datenbankoption auf SIMPLE festgelegt ist, können Sie angeben, dass für eine bestimmte Abfrageklasse die erzwungene Parametrisierung versucht werden soll. Erstellen Sie dazu eine TEMPLATE-Planhinweisliste für die parametrisierte Form der Abfrage, und geben Sie den PARAMETERIZATION FORCED-Abfragehinweis in der gespeicherten Prozedur [sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) an. Betrachten Sie diese Art, Planhinweislisten zu verwenden, als Verfahren, die erzwungene Parametrisierung nur für eine bestimmte, jedoch nicht alle Abfrageklassen zu aktivieren.  
  
-   Wenn die PARAMETERIZATION-Datenbankoption auf FORCED festgelegt ist, können Sie angeben, dass für eine bestimmte Abfrageklasse nur die einfache Parametrisierung versucht werden soll, jedoch nicht die erzwungene Parametrisierung. Erstellen Sie dazu eine TEMPLATE-Planhinweisliste für die erzwungene parametrisierte Form der Abfrage, und geben Sie in **sp_create_plan_guide**den PARAMETERIZATION SIMPLE-Abfragehinweis an.  
  
 Betrachten Sie die folgende Abfrage in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank:  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 Als Datenbankadministrator haben Sie bestimmt, dass Sie die erzwungene Parametrisierung nicht für alle Abfragen der Datenbank aktivieren möchten. Sie sind jedoch darauf bedacht, den Aufwand zu vermeiden, alle Abfragen neu zu kompilieren, obwohl sie syntaktisch mit vorherigen Abfragen gleichwertig sind und sich lediglich durch ihre konstanten Literalwerte unterscheiden. Mit anderen Worten möchten Sie solche Abfragen parametrisieren, sodass für diese Art von Abfragen ein Abfrageplan wiederverwendet wird. Führen Sie in diesem Fall die folgenden Schritte aus:  
  
1.  Rufen Sie die parametrisierte Form der Abfrage ab. Die einzig sichere Möglichkeit, diesen Wert zum Verwenden in **sp_create_plan_guide** abzurufen, besteht in der Verwendung der gespeicherten Systemprozedur [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) .  
  
2.  Erstellen Sie die Planhinweisliste für die parametrisierte Form der Abfrage, indem Sie den PARAMETERIZATION FORCED-Abfragehinweis angeben.  
  
    > [!IMPORTANT]  
    >  Im Rahmen der Parametrisierung einer Abfrage weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Parametern, die die Literalwerte ersetzen, abhängig von Wert und Größe der Literalwerte, einen Datentyp zu. Dasselbe Verfahren wird auf den Wert der an den **@stmt** -Ausgabeparameter von **sp_get_query_template**den PARAMETERIZATION SIMPLE-Abfragehinweis an. Da der im **@params** -Argument von **sp_create_plan_guide** angegebene Datentyp mit dem der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]parametrisierten Abfrage übereinstimmen muss, müssen Sie möglicherweise mehrere Planhinweislisten erstellen, um die gesamte Palette der möglichen Parameterwerte abzudecken.  
  
 Verwenden Sie das folgende Skript, um die parametrisierte Abfrage und anschließend eine Planhinweisliste dafür zu erstellen:  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Auf ähnliche Weise können Sie in einer Datenbank mit bereits aktivierter erzwungener Parametrisierung sicherstellen, dass die Beispielabfrage und andere, mit Ausnahme ihrer konstanten Literalwerte, syntaktisch gleichwertige Abfragen gemäß den Regeln für die einfache Parametrisierung parametrisiert werden. Geben Sie dazu in der OPTION-Klausel PARAMETERIZATION SIMPLE anstelle von PARAMETERIZATION FORCED an.  
  
> [!NOTE]  
>  Durch TEMPLATE-Planhinweislisten wird eine Übereinstimmung zwischen Anweisungen und batchweise übermittelten Abfragen hergestellt, die nur aus einer einzigen Anweisung bestehen. Für Anweisungen innerhalb von Batches mit mehreren Anweisungen können TEMPLATE-Planhinweislisten keine Übereinstimmungen herstellen.  
  
  
