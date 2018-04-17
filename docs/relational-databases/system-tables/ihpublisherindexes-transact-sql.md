---
title: IHpublisherindexes (Transact-SQL) | Microsoft Docs
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
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afb9bb4d3dacab141e63bd330fd8bf6d2d67eb5a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHpublisherindexes** -Systemtabelle enthält eine Zeile für jeden Index, der von nicht - SQL Server-Verlegern mithilfe des aktuellen Verteilers repliziert. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|Identifiziert einen veröffentlichten Index.|  
|**table_id**|**int**|Identifiziert die Tabelle aus [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) zu der der Index gehört.|  
|**publisher_id**|**smallint**|Identifiziert den nicht - SQL Server-Verleger aus dem der Index veröffentlicht wird.|  
|**name**|**sysname**|Der Name des veröffentlichten Indexes.|  
|**type**|**nvarchar(255)**|Ein unterstützter Indextyp aus der [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) -Systemtabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
