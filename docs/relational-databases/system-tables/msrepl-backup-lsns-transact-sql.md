---
title: MSrepl_backup_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4223b1bac4bd9990d328fd00092be2630b8cf736
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSrepl_backup_lsns** -Tabelle enthält Transaktions-protokollfolgenummern (LSN) für die Unterstützung der Option "sync with Backup" der Verteilungsdatenbank. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|Die ID der Verlegerdatenbank.|  
|**valid_xact_id**|**varbinary(16)**|Die ID der Transaktion, die an den Verleger gesendet werden soll, um den Protokollkürzungspunkt zu markieren. Wird nur verwendet, wenn sich die Verteilungsdatenbank im Modus 'sync with backup' befindet. Enthält die ID der zuletzt in der Verteilungsdatenbank replizierten Transaktion, die gesichert wurde. Sie wird an den Verleger gesendet, damit der Protokollkürzungspunkt vom Protokollleser markiert werden kann.|  
|**valid_xact_seqno**|**varbinary(16)**|Die Sequenznummer der Transaktion, die an den Verleger gesendet werden soll, um den Protokollkürzungspunkt zu markieren. Sie wird nur verwendet, wenn sich die Verteilungsdatenbank im Modus 'sync with backup' befindet. Dies ist die Protokollfolgenummer (LSN, Log Sequence Number) der zuletzt in der Verteilungsdatenbank replizierten Transaktion, die gesichert wurde. Sie wird an den Verleger gesendet, damit der Protokollkürzungspunkt vom Protokollleser markiert werden kann.|  
|**next_xact_id**|**varbinary(16)**|Die temporäre Protokollfolgenummer (LSN, Log Sequence Number), die von Sicherungsvorgängen verwendet wird.|  
|**nextx_xact_seqno**|**varbinary(16)**|Die temporäre Protokollfolgenummer (LSN, Log Sequence Number), die von Sicherungsvorgängen verwendet wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
