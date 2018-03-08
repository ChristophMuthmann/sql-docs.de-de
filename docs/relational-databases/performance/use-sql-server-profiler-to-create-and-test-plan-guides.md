---
title: Verwenden von SQL Server Profiler zum Erstellen und Testen von Planhinweislisten | Microsoft-Dokumentation
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
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bbb800f0f0bd06e32357cda69d9a01a5c25e866
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>Verwenden von SQL Server Profiler zum Erstellen und Testen von Planhinweislisten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn Sie eine Planhinweisliste erstellen, können Sie durch Verwenden von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] den genauen Abfragetext aufzeichnen, um diesen im *statement_text*-Argument der gespeicherten Prozedur **sp_create_plan_guide** zu verwenden. Damit kann sichergestellt werden, dass die Planhinweisliste zum Zeitpunkt der Kompilierung mit der Abfrage in Übereinstimmung gebracht wird. Nach dem Erstellen der Planhinweisliste kann [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] auch verwendet werden, um zu testen, ob die Planhinweisliste tatsächlich in Übereinstimmung mit der Abfrage gebracht wird. Im Allgemeinen sollten Sie Planhinweislisten mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] testen, um zu überprüfen, dass Ihre Abfrage mit Ihrer Planhinweisliste übereinstimmt.  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>Aufzeichnen von Abfragetext mithilfe von SQL Server Profiler  
 Wenn Sie eine Abfrage ausführen und den Text mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genau so aufzeichnen, wie er an [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]übermittelt wurde, können Sie eine Planhinweisliste des Typs SQL oder TEMPLATE erstellen, die genau mit dem Abfragetext übereinstimmt. Damit wird sichergestellt, dass die Planhinweisliste vom Abfrageoptimierer verwendet wird.  
  
 Angenommen, die folgende Abfrage wird durch eine Anwendung als eigenständiger Batch übermittelt:  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 Nehmen wir jetzt an, Sie möchten diese Abfrage mithilfe eines Vorgangs zur Zusammenführungsjoins ausführen, von SHOWPLAN wird jedoch angezeigt, dass die Abfrage keine Zusammenführungsjoin verwendet. Es ist nicht möglich, die Abfrage direkt in der Anwendung zu ändern. Also erstellen Sie stattdessen eine Planhinweisliste, um anzugeben, dass der MERGE JOIN-Abfragehinweis zum Kompilierzeitpunkt an die Abfrage angehängt wird.  
  
 Um den Text genau so aufzuzeichnen, wie er von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] empfangen wird, gehen Sie folgendermaßen vor:  
  
1.  Starten Sie eine [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgung, und stellen Sie dabei sicher, dass der **SQL:BatchStarting** -Ereignistyp ausgewählt ist.  
  
2.  Führen Sie Abfrage mithilfe der Anwendung aus.  
  
3.  Halten Sie die [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgung an.  
  
4.  Klicken Sie auf das **SQL:BatchStarting** -Ereignis, das der Abfrage entspricht.  
  
5.  Klicken Sie mit der rechten Maustaste auf dieses Ereignis, und wählen Sie **Ereignisdaten extrahieren**aus.  
  
    > [!IMPORTANT]  
    >  Versuchen Sie nicht, den Batchtext zu kopieren, indem Sie ihn im unteren Bereich des Profiler-Ablaufverfolgungsfensters markieren. Das kann dazu führen, dass die von Ihnen erstellte Planhinweisliste nicht mit dem ursprünglichen Batch übereinstimmt.  
  
6.  Speichern Sie die Ereignisdaten in einer Datei. Das ist der Batchtext.  
  
7.  Öffnen Sie die Batchtextdatei in Editor, und kopieren Sie den Text in die Zwischenablage.  
  
8.  Erstellen Sie die Planhinweisliste, und fügen Sie den kopierten Text zwischen die Anführungszeichen (**''**) ein, die für das **@stmt** -Argument angegeben sind. Sie müssen alle einfachen Anführungszeichen im **@stmt** -Argument abgrenzen, indem Sie ihnen ein weiteres einfaches Anführungszeichen voranstellen. Achten Sie darauf, beim Einfügen dieser einfachen Anführungszeichen keine weiteren Zeichen hinzuzufügen oder zu entfernen. So muss z. B. das Datumsliteral **'**20000101**'** als **''**20000101**''**abgegrenzt werden.  
  
 Die Planhinweisliste sieht dann folgendermaßen aus:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>Testen von Planhinweislisten mithilfe von SQL Server Profiler  
 Um zu überprüfen, ob eine Planhinweisliste mit einer Abfrage in Übereinstimmung gebracht wird, gehen Sie folgendermaßen vor:  
  
1.  Starten Sie eine [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgung, und stellen Sie dabei sicher, dass der **Showplan XML** -Ereignistyp ausgewählt ist (dieser befindet sich unter dem Knoten **Leistung** ).  
  
2.  Führen Sie Abfrage mithilfe der Anwendung aus.  
  
3.  Halten Sie die [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgung an.  
  
4.  Suchen Sie das **Showplan XML** -Ereignis für die betroffene Abfrage.  
  
    > [!NOTE]  
    >  Das Ereignis **Showplan XML for Query Compile** kann nicht verwendet werden. **PlanGuideDB** ist in diesem Ereignis nicht vorhanden.  
  
5.  Wenn die Planhinweisliste vom Typ OBJECT oder SQL ist, überprüfen Sie, ob das **Showplan XML** -Ereignis die Attribute **PlanGuideDB** und **PlanGuideName** für die Planhinweisliste enthält, die mit der Abfrage übereinstimmen soll. Handelt es sich um eine Planhinweisliste vom Typ TEMPLATE, überprüfen Sie, ob das **Showplan XML** -Ereignis die Attribute **TemplatePlanGuideDB** und **TemplatePlanGuideName** für die erwartete Planhinweisliste enthält. Damit wird die Funktionsfähigkeit der Planhinweisliste überprüft. Diese Attribute sind im **\<<StmtSimple**-Element der Planhinweisliste enthalten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
  
  
