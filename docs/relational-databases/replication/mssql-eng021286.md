---
title: "MSSQL_ENG021286 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021286 (Fehler)"
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021286
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21286|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die %1!s!-Konflikttabelle ist nicht vorhanden.|  
  
## Erklärung  
 Dieser Fehler wird ausgelöst, wenn die Konflikttabelle für einen Artikel im aufgeführt [Sysmergearticles & #40; Transact-SQL & #41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) tatsächlich existiert nicht. Der Fehler kann bei dem Versuch auftreten, einer Tabelle, die für die Mergereplikation veröffentlicht wurde, eine Spalte hinzuzufügen oder aber eine Spalte aus der Tabelle zu entfernen.  
  
## Benutzeraktion  
 Führen Sie [DBCC CHECKDB & #40; Transact-SQL & #41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) in der Datenbank mit der fehlenden Konflikttabelle aus, um zu überprüfen, stehen Datenkonsistenzprobleme.  
  
 Wenn die Konflikttabelle auf einem Abonnenten fehlt, sollten Sie das Abonnement löschen und es dann gänzlich neu erstellen. Fehlt die Konflikttabelle auf einem Verleger, empfiehlt es sich, alle Abonnements und die Veröffentlichung zu löschen und dann die Veröffentlichung und alle Abonnements neu zu erstellen. Weitere Informationen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md) und [abonnieren Publikationen](../../relational-databases/replication/subscribe-to-publications.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  