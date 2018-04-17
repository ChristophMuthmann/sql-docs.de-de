---
title: MSpeer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
applies_to:
- SQL Server
f1_keywords:
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8029d9e4f9e8dda7f5003865bb6a8066654165d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Mspeer_lsns** Tabelle wird verwendet, um jede Transaktion zu einem Abonnement in einer Peer-zu-Peer-Replikationstopologie zugeordnet. Diese Tabelle wird in jeder Veröffentlichungsdatenbank in einer Peer-zu-Peer-Replikationstopologie sowie in der Abonnementdatenbank aller Abonnenten einer Peer-zu-Peer-Veröffentlichung gespeichert. Weitere Informationen zu dieser Art der transaktionsreplikationstopologie finden Sie unter [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifiziert eine Peer-zu-Peer-LSN.|  
|**last_updated**|**datetime**|Die **"DateTime"** an dem die letzte zeilenaktualisierung vorgenommen wurde.|  
|**originator**|**sysname**|Der Name des Verlegers, von dem die Transaktion stammt|  
|**originator_db**|**sysname**|Der Name der Datenbank, aus der die Transaktion stammt|  
|**originator_publication**|**sysname**|Der Name der Veröffentlichung, aus der die Transaktion stammt|  
|**originator_publication_id**|**int**|Die ID der Veröffentlichung, aus der die Transaktion stammt|  
|**originator_db_version**|**int**|Kennzeichnet die Versionsnummer der ursprünglichen Datenbank.|  
|**originator_lsn**|**int**|Identifiziert die LSN in der Ausgangsveröffentlichung|  
|**originator_version**|**int**|Kennzeichnet die Versionsnummer des Verlegers|  
|**originator_id**|**smallint**|Identifiziert jeden Knoten in der Topologie zum Zweck der Konflikterkennung. Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
