---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL020011 (Fehler)"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20011|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Prozess konnte '%1' nicht auf '%2' ausführen.|  
  
## Erklärung  
 Dieser Fehler kann in vielen Situationen ausgelöst werden, während der Verarbeitung, z. B. wenn der Protokolllese-Agent ausgeführt wird und Transaktionsreplikation **Sp_replcmds** (der Prozess konnte 'Sp_replcmds' nicht ausführen, auf \< ServerName>) oder **Sp_repldone** (der Prozess konnte nicht ' sp_repldone ' für \< ServerName>).  
  
## Benutzeraktion  
 Wenn dieser Fehler in einer Datenbank ausgelöst wird, die Sie gerade erst aus einer Sicherung wiederhergestellt haben, stellen Sie sicher haben Sie die Schritte in der Sicherung und Wiederherstellung finden Sie auch die Ausführung von befolgt **Sp_replrestart** bei Bedarf. Weitere Informationen finden Sie unter [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 Bei diesem Fehler handelt es sich um einen internen Verarbeitungsfehler. Wenn er nicht im Zusammenhang mit einer Wiederherstellung ausgelöst wird, weist er in der Regel darauf hin, dass die Replikation entfernt und neu konfiguriert werden muss. Wenn das Entfernen der Replikation nicht möglich ist, wenden Sie sich an den Kundendienst.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Sp_replcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Sp_repldone & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  