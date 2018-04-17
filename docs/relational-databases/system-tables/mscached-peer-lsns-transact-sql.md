---
title: MScached_peer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b888b2e7b713b81d4e7a3e150702c31e14c9d025
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mscachedpeerlsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MScached_peer_lsns** Tabelle wird verwendet, um die LSN-Werte in das Transaktionsprotokoll zu verfolgen, die verwendet werden, um zu bestimmen, welche Befehle an den betreffenden Abonnenten bei der Peer-zu-Peer-Replikation zurück. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Die ID des Verteilungs-Agents.|  
|**originator**|**sysname**|Der Name des ursprünglichen Verlegers.|  
|**originator_db**|**sysname**|Der Name der ursprünglichen Veröffentlichungsdatenbank.|  
|**originator_publication_id**|**int**|Kennzeichnet die ursprüngliche Veröffentlichung.|  
|**originator_db_version**|**int**|Kennzeichnet die Versionsnummer der ursprünglichen Datenbank.|  
|**originator_lsn**|**varbinary(16)**|Die LSN der ursprünglichen Transaktion.|  
  
## <a name="remarks"></a>Hinweise  
 LSN-Werte werden nur unmittelbar nach der Einfügung verwendet. Sie haben keine andauernde Bedeutung im System.  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
