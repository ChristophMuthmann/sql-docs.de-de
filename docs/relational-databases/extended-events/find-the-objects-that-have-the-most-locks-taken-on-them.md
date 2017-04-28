---
title: "Suchen der Objekte, die über die meisten Sperren verfügen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- objects [SQL Server], extended events
- xe
- extended events [SQL Server], locks
- objects [SQL Server], locks
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd171596bf52ebc25887b378103ffe751955fd03
ms.lasthandoff: 04/11/2017

---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>Suchen der Objekte, die über die meisten Sperren verfügen
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Datenbankadministratoren müssen oft die Quelle von Sperren identifizieren, die die Datenbankleistung beeinträchtigen.  
  
 Sie überwachen z. B. den Produktionsserver auf alle möglichen Engpässe. Sie erwarten einen starken Wettbewerb um die Ressourcen und würden daher gern ermitteln, wie viele Sperren für diese Objekte gelten. Nachdem die am häufigsten gesperrten Objekte ermittelt sind, können Sie Schritte zur Optimierung des Zugangs auf die im Wettbewerb befindlichen Objekte ergreifen.  
  
 Verwenden Sie hierzu den Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>So suchen Sie die Objekte, die über die meisten Sperren verfügen  
  
1.  Führen Sie im Abfrage-Editor die folgenden Anweisungen aus.  
  
    ```  
    -- Find objects in a particular database that have the most  
    -- lock acquired. This sample uses AdventureWorksDW2012.  
    -- Create the session and add an event and target.  
    --   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')  
    DROP EVENT session LockCounts ON SERVER  
    GO  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorksDW2012')  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE event session LockCounts ON SERVER  
    ADD EVENT sqlserver.lock_acquired (WHERE database_id =' + CAST(@dbid AS nvarchar) +')  
    ADD TARGET package0.histogram(   
    SET filtering_event_name=''sqlserver.lock_acquired'', source_type=0, source=''resource_0'')'  
  
    EXEC (@sql)  
    GO  
    ALTER EVENT session LockCounts ON SERVER   
    STATE=start  
    GO  
    --   
    -- Create a simple workload that takes locks.  
    --   
    USE AdventureWorksDW2012  
    GO  
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems  
    GO  
    -- The histogram target output is available from the   
    -- sys.dm_xe_session_targets dynamic management view in  
    -- XML format.  
    -- The following query joins the bucketizing target output with  
    -- sys.objects to obtain the object names.  
    --  
    SELECT name, object_id, lock_count FROM   
    (SELECT objstats.value('.','bigint') AS lobject_id,   
    objstats.value('@count', 'bigint') AS lock_count  
    FROM (  
    SELECT CAST(xest.target_data AS XML)  
    LockData  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'  
    ) Locks  
    CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)  
     ) LockedObjects   
    INNER JOIN sys.objects o  
    ON LockedObjects.lobject_id = o.object_id  
    WHERE o.type != 'S' AND o.type = 'U'  
    ORDER BY lock_count desc  
    GO  
    --   
    -- Stop the event session.  
    --   
    ALTER EVENT SESSION LockCounts ON SERVER  
    state=stop  
    GO  
  
    ```  
  
 Nach Abschluss der Anweisungen in dieser Prozedur werden auf der Registerkarte **Ergebnisse** des Abfrage-Editors die folgenden Spalten angezeigt:  
  
-   name  
  
-   object_id  
  
-   lock_count  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  
