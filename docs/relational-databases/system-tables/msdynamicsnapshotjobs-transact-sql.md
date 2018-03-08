---
title: MSdynamicsnapshotjobs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs: TSQL
helpviewer_keywords: MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79f353d2c95f9e7c9c8071de60bb8c2705f675b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdynamicsnapshotjobs** -Tabelle verfolgt nach, die parametrisierten zeilenfilterinformationen angewendet, um eine Momentaufnahme gefilterter Daten zu generieren. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Die ID des gefilterten Datenmomentaufnahmeauftrags.|  
|**name**|**sysname**|Der Name des gefilterten Datenmomentaufnahmeauftrags.|  
|**pubid**|**uniqueidentifier**|Die eindeutige ID für diese Veröffentlichung.|  
|**job_id**|**uniqueidentifier**|Die ID des SQL Server-Agent-Auftrags auf dem Verteiler.|  
|**agent_id-Wert**|**int**|Die ID der SQL Server-Agent.|  
|**dynamic_filter_login**|**sysname**|Der Wert für die Bewertung der [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion in parametrisierten Zeilenfiltern für die Veröffentlichung.|  
|**den Wert**|**sysname**|Der Wert für die Bewertung der [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) -Funktion in parametrisierten Zeilenfiltern für die Veröffentlichung.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Der Pfad zu dem Ordner, aus dem die Momentaufnahmedateien gelesen werden, wenn eine gefilterte Datenmomentaufnahme verwendet wird.|  
|**partition_id**|**int**|Die ID der Datenpartition, der der Auftrag angehört.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
