---
title: Bereinigen von Mergemetadaten (Replikationsprogrammierung mit Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5572b29922b76781429b71612e061d9014c32a7d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Cleanup von Mergemetadaten (Replikationsprogrammierung mit Transact-SQL)
  Der Cleanup von Mergereplikationsmetadaten wird basierend auf der Beibehaltungseinstellung für die Veröffentlichung in regelmäßigen Abständen vom Merge-Agent ausgeführt. Dies erfolgt auf dem Verleger und auf dem Abonnenten in den Systemtabellen [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)und [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . Der Cleanup der Daten in diesen Tabellen kann mithilfe gespeicherter Replikationsprozeduren auch programmgesteuert ausgeführt werden.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>So führen Sie einen Cleanup von Mergemetadaten manuell aus  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md)aus.  
  
2.  (Optional) Beachten Sie die Anzahl von Zeilen, die in Schritt 1aus den Systemtabellen [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)und [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) entfernt und jeweils in den Ausgabeparametern **@num_genhistory_rows**, **@num_contents_rows**und **@num_tombstone_rows** zurückgegeben werden.  
  
3.  Wiederholen Sie die Schritte 1 und 2 auf dem Abonnenten, um einen Cleanup der Metadaten für die Abonnementdatenbank auszuführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Abonnementablauf und -deaktivierung](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
