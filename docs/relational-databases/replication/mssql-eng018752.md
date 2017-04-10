---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018752 (Fehler)"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|18752|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Nur jeweils ein Protokolllese-Agent oder eine protokollbezogene Prozedur (sp_repldone, sp_replcmds oder sp_replshowcmds) kann eine Verbindung mit einer Datenbank herstellen. Falls Sie eine protokollbezogene Prozedur ausgeführt haben, löschen Sie vor dem Starten des Protokolllese-Agents oder dem Ausführen einer weiteren protokollbezogenen Prozedur die Verbindung, über die sie ausgeführt wurde, oder führen Sie 'sp_replflush' über diese Verbindung aus.|  
  
## Erklärung  
 Mehrere aktuelle Verbindungen versuchen, führen Sie eine der folgenden: **Sp_repldone**, **Sp_replcmds**, oder **Sp_replshowcmds**. Die gespeicherten Prozeduren [Sp_repldone & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) und [Sp_replcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) gespeicherte Prozeduren dienen der Protokolllese-Agent zum Suchen und Aktualisieren von Informationen zu replizierten Transaktionen in einer veröffentlichten Datenbank. Die gespeicherte Prozedur [Sp_replshowcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) wird zum Behandlung bestimmter Arten von Problemen mit Transaktionsreplikation verwendet.  
  
 Dieser Fehler wird in folgenden Situationen ausgelöst:  
  
-   Wenn der Protokolllese-Agent für eine veröffentlichte Datenbank ausgeführt und versucht wird, einen zweiten Protokolllese-Agent für dieselbe Datenbank auszuführen, wird der Fehler für den zweiten Agent ausgelöst und im Agentverlauf angezeigt.  
  
     In einer Situation, in der offenbar mehrere Agents vorhanden sind, kann es sein, dass einer dieser Agents das Ergebnis eines verwaisten Prozesses ist.  
  
-   Wenn der Protokolllese-Agent für eine veröffentlichte Datenbank gestartet wird und ein Benutzer führt **Sp_repldone**, **Sp_replcmds**, oder **Sp_replshowcmds** für dieselbe Datenbank, der Fehler ausgelöst wird, in der Anwendung, in dem die gespeicherte Prozedur ausgeführt wurde (z. B. **Sqlcmd**).  
  
-   Wenn für eine veröffentlichte Datenbank kein Protokolllese-Agent ausgeführt wird und ein Benutzer führt **Sp_repldone**, **Sp_replcmds**, oder **Sp_replshowcmds** und dann schließen die Verbindung über den die Prozedur ausgeführt wurde, wird der Fehler ausgelöst wird, wenn der Protokolllese-Agent versucht, die Verbindung mit der Datenbank.  
  
## Benutzeraktion  
 Folgende Schritte können Ihnen bei der Problembehandlung behilflich sein. Wenn der Protokolllese-Agent in einem beliebigen Schritt ohne Fehler gestartet werden kann, müssen die verbleibenden Schritte nicht mehr ausgeführt werden.  
  
-   Überprüfen Sie den Verlauf des Protokolllese-Agents für alle anderen Fehler, die möglicherweise zu diesem Fehler beitragen. Weitere Informationen zum Anzeigen des Status und zu Fehlerdetails im Replikationsmonitor, finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Überprüfen Sie die Ausgabe von [Sp_who & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) bestimmten Prozess-IDs (SPIDs), die mit der veröffentlichten Datenbank verbunden sind. Schließen Sie alle Verbindungen, die möglicherweise ausgeführt wurden **Sp_repldone**, **Sp_replcmds**, oder **Sp_replshowcmds**.  
  
-   Starten Sie den Protokolllese-Agent neu. Weitere Informationen finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent-Dienst auf dem Verteiler neu (schalten Sie ihn in einem Cluster offline oder online). Wenn die Möglichkeit besteht, die ein geplanter Auftrag ausgeführt wurde **Sp_repldone**, **Sp_replcmds**, oder **Sp_replshowcmds** aus einem anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, starten Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent für diese Instanzen ebenfalls. Weitere Informationen finden Sie unter [starten, beenden oder Anhalten der SQL Server-Agent-Dienst](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
-   Führen Sie [Sp_replflush & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank, und starten Sie den Protokolllese-Agent.  
  
-   Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und/oder weitere Fehlermeldungen.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  