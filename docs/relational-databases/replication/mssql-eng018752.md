---
title: MSSQL_ENG018752 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da945958bccc9fd0380ab371b43221ca9643fd1b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|18752|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Nur jeweils ein Protokolllese-Agent oder eine protokollbezogene Prozedur (sp_repldone, sp_replcmds oder sp_replshowcmds) kann eine Verbindung mit einer Datenbank herstellen. Falls Sie eine protokollbezogene Prozedur ausgeführt haben, löschen Sie vor dem Starten des Protokolllese-Agents oder dem Ausführen einer weiteren protokollbezogenen Prozedur die Verbindung, über die sie ausgeführt wurde, oder führen Sie 'sp_replflush' über diese Verbindung aus.|  
  
## <a name="explanation"></a>Erklärung  
 Mehrere aktuelle Verbindungen versuchen, **sp_repldone**, **sp_replcmds**oder **sp_replshowcmds**auszuführen. Die gespeicherten Prozeduren [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) und [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) werden vom Protokolllese-Agent verwendet, um Informationen zu replizierten Transaktionen in einer veröffentlichten Datenbank zu finden und zu aktualisieren. Die gespeicherte Prozedur [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) wird für die Behandlung bestimmter Problemtypen einer Transaktionsreplikation verwendet.  
  
 Dieser Fehler wird in folgenden Situationen ausgelöst:  
  
-   Wenn der Protokolllese-Agent für eine veröffentlichte Datenbank ausgeführt und versucht wird, einen zweiten Protokolllese-Agent für dieselbe Datenbank auszuführen, wird der Fehler für den zweiten Agent ausgelöst und im Agentverlauf angezeigt.  
  
     In einer Situation, in der offenbar mehrere Agents vorhanden sind, kann es sein, dass einer dieser Agents das Ergebnis eines verwaisten Prozesses ist.  
  
-   Wenn der Protokolllese-Agent für eine veröffentlichte Datenbank gestartet wird und ein Benutzer **sp_repldone**, **sp_replcmds**oder **sp_replshowcmds** für dieselbe Datenbank ausführt, wird der Fehler in der Anwendung ausgelöst, in der die gespeicherte Prozedur ausgeführt wurde (z. B. **sqlcmd**).  
  
-   Wenn für eine veröffentlichte Datenbank kein Protokolllese-Agent ausgeführt wird und ein Benutzer **sp_repldone**, **sp_replcmds**oder **sp_replshowcmds** ausführt, ohne anschließend die Verbindung zu schließen, über die die Prozedur ausgeführt wurde, wird der Fehler ausgelöst, wenn der Protokolllese-Agent versucht, eine Verbindung mit der Datenbank herzustellen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Folgende Schritte können Ihnen bei der Problembehandlung behilflich sein. Wenn der Protokolllese-Agent in einem beliebigen Schritt ohne Fehler gestartet werden kann, müssen die verbleibenden Schritte nicht mehr ausgeführt werden.  
  
-   Überprüfen Sie den Verlauf des Protokolllese-Agents für alle anderen Fehler, die möglicherweise zu diesem Fehler beitragen. Informationen zum Anzeigen des Agentstatus und der Fehlerinformationen im Replikationsmonitor finden Sie unter [View Information and Perform Tasks for the Agents Associated With a Publication &#40;Replication Monitor&#41; (Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;)](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Überprüfen Sie die Ausgabe von [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) für spezielle SPIDs, die mit der veröffentlichten Datenbank verbunden sind. Schließen Sie alle Verbindungen, mit denen **sp_repldone**, **sp_replcmds**oder **sp_replshowcmds**möglicherweise ausgeführt wurden.  
  
-   Starten Sie den Protokolllese-Agent neu. Weitere Informationen finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent-Dienst auf dem Verteiler neu (schalten Sie ihn in einem Cluster offline oder online). Wenn die Möglichkeit besteht, dass **sp_repldone**, **sp_replcmds**oder **sp_replshowcmds** durch einen geplanten Auftrag von einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wurde, starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent für die betreffenden Instanzen ebenfalls neu. Weitere Informationen finden Sie unter [Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c).  
  
-   Führen Sie auf dem Verleger in der Veröffentlichungsdatenbank [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) aus, und starten Sie den Protokolllese-Agent anschließend neu.  
  
-   Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und/oder weitere Fehlermeldungen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  
