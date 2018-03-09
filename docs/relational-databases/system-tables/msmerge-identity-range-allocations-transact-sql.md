---
title: MSmerge_identity_range_allocations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad5ad628c5f839c64d88c54e777aca7e0bc52b7e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeidentityrangeallocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_identity_range_allocations** Tabelle wird verwendet, um den Verlauf von identitätsbereichszuweisungen, um den Verlegern und Abonnenten für veröffentlichte Artikel nachverfolgt. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Die ID des Verlegers|  
|**publisher_db**|**vom Datentyp nvarchar(128)**|Der Name der Veröffentlichungsdatenbank.|  
|**Veröffentlichung**|**vom Datentyp nvarchar(128)**|Der Name der Veröffentlichung.|  
|**Artikel**|**vom Datentyp nvarchar(128)**|Der Name des Artikels.|  
|**subscriber**|**vom Datentyp nvarchar(128)**|Den Namen des Abonnenten.|  
|**subscriber_db**|**vom Datentyp nvarchar(128)**|Der Name der Abonnementdatenbank.|  
|**is_pub_range**|**bit**|Zeigt an, ob der Identitätsbereich einem Verleger zugewiesen ist.|  
|**"ranges_allocated"**|**tinyint**|Die Anzahl zugewiesener Identitätsbereiche.|  
|**"range_begin"**|**numeric(38)**|Der Anfangswert des Bereichs.|  
|**"range_end"**|**numeric(38)**|Der letzte Wert des Bereichs.|  
|**"next_range_begin"**|**numeric(38)**|Der Anfangswert des nächsten zuzuweisenden Bereichs.|  
|**"next_range_end"**|**numeric(38)**|Der letzte Wert des nächsten zuzuweisenden Bereichs.|  
|**max_used**|**numeric(38)**|Der höchste verwendete Identitätswert.|  
|**time_of_allocation**|**datetime**|Der Zeitpunkt, zu dem die Zuweisung erfolgte.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
