---
title: "MSSQL_ENG021797 | Microsoft Docs"
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
  - "MSSQL_ENG021797 (Fehler)"
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021797
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21797|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|'%1!s!' muss eine gültige Windows-Anmeldung der folgenden Form sein: 'MACHINE\Login' oder 'DOMAIN\Login'. Lesen Sie die Dokumentation zu '%3!s!'.|  
  
## Erklärung  
 Dieser Fehler wird durch die folgenden gespeicherten Replikationsprozeduren ausgelöst, wenn der Wert für angegeben der **@job_login** Parameter ist null oder ungültig. Dieser Fehler kann auftreten, wenn ein Mitglied der **Db_owner** festen Datenbankrolle führt Skripts aus früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Das Sicherheitsmodell wurde in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]geändert, daher müssen die Skripts aktualisiert werden.  
  
-   [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [Sp_addqreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [Sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [Sp_addmergepushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [Sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 Diese gespeicherten Prozeduren ausgeführt werden können, von einem Mitglied der **Sysadmin** auf dem entsprechenden Server oder Mitglied der festen Serverrolle die **Db_owner** festen Datenbankrolle in der entsprechenden Datenbank. Jede gespeicherte Prozedur erstellt einen Agentauftrag, für den Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto angeben können, unter dem der Agent ausgeführt werden soll. Für Benutzer in der **Sysadmin** Rolle-Agent-Aufträge werden implizit erstellt, auch wenn ein Windows-Konto nicht angegeben wird (Wenn kein Konto angegeben wird, muss gültig sein); Agents werden im Kontext von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto auf dem entsprechenden Server. Das Festlegen eines Kontos ist zwar nicht erforderlich, aus Sicherheitsgründen empfiehlt es sich jedoch, ein separates Konto für jeden Agent anzugeben. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Benutzeraktion  
 Stellen Sie sicher, Sie geben Sie ein gültiges Windowskonto für die **@job_login** Parameter von jeder Prozedur. Wenn Sie Replikationsskripts aus vorherigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übernehmen, aktualisieren Sie diese Skripts, sodass sie die für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]erforderlichen gespeicherten Prozeduren und Parameter enthalten. Weitere Informationen finden Sie unter [Aktualisieren von Replikationsskripts & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  