---
title: "Kontrollieren des Verhaltens von Triggern und Einschr&#228;nkungen w&#228;hrend der Synchronisierung (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Identitäten [SQL Server-Replikation]"
  - "Einschränkungen [SQL Server], Replikation"
  - "Trigger [SQL Server], Replikation"
  - "Trigger [SQL Server-Replikation]"
  - "Einschränkungen [SQL Server-Replikation]"
  - "NOT FOR REPLICATION-Option"
  - "NFR-Option"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Kontrollieren des Verhaltens von Triggern und Einschr&#228;nkungen w&#228;hrend der Synchronisierung (Replikationsprogrammierung mit Transact-SQL)
  Während der Synchronisierung führen Replikation-Agents [INSERT & #40; Transact-SQL & #41;](../../t-sql/statements/insert-transact-sql.md), [& #40; aktualisieren Transact-SQL & #41;](../../t-sql/queries/update-transact-sql.md), und [#40; & löschen Transact-SQL & #41;](../../t-sql/statements/delete-transact-sql.md) -Anweisungen für replizierte Tabellen, die Data Manipulation Language (DML)-Trigger auf diese Tabellen ausgeführt werden verursachen können. Es gibt Fälle, in denen Sie verhindern müssen, dass Trigger während der Synchronisierung ausgelöst werden oder Einschränkungen während der Synchronisierung erzwungen werden. Dieses Verhalten hängt davon ab, wie der Trigger oder die Einschränkung erstellt wird.  
  
### So verhindern Sie, dass Trigger während der Synchronisierung ausgeführt werden  
  
1.  Beim Erstellen eines neuen Triggers angeben, die Option NOT FOR REPLICATION [CREATE TRIGGER & #40; Transact-SQL & #41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
2.  Geben Sie für einen vorhandenen Trigger die NOT FOR REPLICATION-Option von [ALTER TRIGGER & #40; Transact-SQL & #41;](../../t-sql/statements/alter-trigger-transact-sql.md).  
  
### So verhindern Sie, dass Einschränkungen während der Synchronisierung erzwungen werden  
  
1.  Geben Sie beim Erstellen einer neuen CHECK- oder FOREIGN KEY-Einschränkung CHECK NOT FOR REPLICATION-Option in der Einschränkungsdefinition von [CREATE TABLE & #40; Transact-SQL & #41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## Siehe auch  
 [Erstellen Sie Tabellen & #40; Datenbankmodul & #41.](../../relational-databases/tables/create-tables-database-engine.md)  
  
  