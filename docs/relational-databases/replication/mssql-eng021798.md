---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "MSSQL_ENG021798 (Fehler)"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21798|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der '%s'-Agent-Auftrag muss vor dem Fortsetzen des Vorgangs über '%s' hinzugefügt werden. Lesen Sie die Dokumentation zu '%3!s!'.|  
  
## Erklärung  
 Um eine Veröffentlichung erstellen zu können, muss ein Mitglied der **Sysadmin** auf dem Verleger oder Mitglied der festen Serverrolle die **Db_owner** festen Datenbankrolle in der Publikationsdatenbank. Wenn Sie ein Mitglied der **Db_owner** Rolle dieser Fehler wird ausgelöst, wenn:  
  
-   Sie führen Skripts von [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]aus. Das Sicherheitsmodell wurde in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]geändert, daher müssen die Skripts aktualisiert werden.  
  
-   Die gespeicherte Prozedur **Sp_addpublication** ausgeführt wird, vor dem Ausführen [Sp_addlogreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Dies gilt für alle Transaktionsveröffentlichungen.  
  
-   Die gespeicherte Prozedur **Sp_addpublication** ausgeführt wird, vor dem Ausführen [Sp_addqreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Dies gilt für transaktionsveröffentlichungen, die für Abonnements mit verzögerter Aktualisierung aktiviert sind (der Wert TRUE für die **@allow_queued_tran** Parameter **Sp_addpublication**).  
  
 Die gespeicherten Prozeduren **Sp_addlogreader_agent** und **Sp_addqreader_agent** jede erstellt einen Agentauftrag und ermöglichen es Ihnen, geben Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird. Für Benutzer in der **Sysadmin** Rolle-Agent-Aufträge werden implizit erstellt, wenn **Sp_addlogreader_agent** und **Sp_addqreader_agent** werden nicht ausgeführt; Agents werden im Kontext von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto auf dem Verteiler. Obwohl **Sp_addlogreader_agent** und **Sp_addqreader_agent** sind nicht erforderlich für Benutzer in der **Sysadmin** Rolle, es ist eine bewährte Sicherheitsmethode, ein separates Konto für die Agents anzugeben. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Benutzeraktion  
 Stellen Sie sicher, dass Sie die Prozeduren in der richtigen Reihenfolge ausführen. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md). Wenn Sie Replikationsskripts aus vorherigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übernehmen, aktualisieren Sie diese Skripts, sodass sie die für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und spätere Versionen erforderlichen gespeicherten Prozeduren und Parameter enthalten. Weitere Informationen finden Sie unter [Aktualisieren von Replikationsskripts & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  