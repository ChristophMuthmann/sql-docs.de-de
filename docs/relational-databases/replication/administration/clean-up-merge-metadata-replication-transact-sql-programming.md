---
title: "Cleanup von Mergemetadaten (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
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
  - "Metadaten [SQL Server-Replikation]"
  - "sp_mergemetadataretentioncleanup"
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Cleanup von Mergemetadaten (Replikationsprogrammierung mit Transact-SQL)
  Der Cleanup von Mergereplikationsmetadaten wird basierend auf der Beibehaltungseinstellung für die Veröffentlichung in regelmäßigen Abständen vom Merge-Agent ausgeführt. In diesem Fall auf dem Verleger und Abonnenten in der [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), und [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) -Systemtabellen. Der Cleanup der Daten in diesen Tabellen kann mithilfe gespeicherter Replikationsprozeduren auch programmgesteuert ausgeführt werden.  
  
### So führen Sie einen Cleanup von Mergemetadaten manuell aus  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md).  
  
2.  (Optional) Beachten Sie die Anzahl der Zeilen entfernt, die Schritt 1 aus der [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), und [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) Systemtabellen jeweils in den **@num_genhistory_rows**, **@num_contents_rows**, und **@num_tombstone_rows** Ausgabeparameter.  
  
3.  Wiederholen Sie die Schritte 1 und 2 auf dem Abonnenten, um einen Cleanup der Metadaten für die Abonnementdatenbank auszuführen.  
  
## Siehe auch  
 [Abonnementablauf und -deaktivierung](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  