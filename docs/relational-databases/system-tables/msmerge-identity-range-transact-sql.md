---
title: MSmerge_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs: TSQL
helpviewer_keywords: MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec799b6fcf16f4cb7f0146c6e01915d7e40d464a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_identity_range** Tabelle wird verwendet, um numerische Bereiche, die Identitätsspalten zur Abonnierung von Veröffentlichungen zugewiesen nachverfolgen auf dem die Replikation automatisch diese bereichszuweisungen verwaltet wird. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|Die eindeutige ID für ein bestimmtes Abonnement.|  
|**artid**|**uniqueidentifier**|Die eindeutige ID des angegebenen Artikels.|  
|**"range_begin"**|**numeric(38)**|Der Identitätswert am Anfang des aktuellen Bereichs.|  
|**"range_end"**|**numeric(38)**|Der Identitätswert am Ende des aktuellen Bereichs.|  
|**"next_range_begin"**|**numeric(38)**|Der Identitätswert am Anfang des neuen Bereichs, der zugewiesen werden soll.|  
|**"next_range_end"**|**numeric(38)**|Der Identitätswert am Ende des neuen Bereichs, der zugewiesen werden soll.|  
|**is_pub_range**|**bit**|Der Wert **1** , wenn die Veröffentlichung der Identitätsbereich zugewiesen wird.|  
|**max_used**|**numeric(38)**|Der maximale Identitätswert, der zugewiesen werden kann.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
