---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a5f1530091601cb241da7f1e4b1d48e02f699497
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriptionarticles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsubscription_articles** Tabelle enthält Informationen zu den Artikeln in einem Abonnement mit Warteschlange. Diese Tabelle wird nur für die folgenden Replikationstypen aufgefüllt: Verzögertes Update über eine Warteschlange und sofortiges Update mit verzögertem Update über eine Warteschlange als Failover.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Die ID der Momentaufnahme, die diesen Artikel bedient.|  
|**artid**|**int**|Die Artikel-ID aus der **Sysarticles** Tabelle.|  
|**article**|**sysname**|Der Name des Artikels aus der **Sysarticles** Tabelle.|  
|**dest_table**|**sysname**|Der Name der Zieltabelle aus der **Sysarticles** Tabelle.|  
|**Besitzer**|**sysname**|Der Besitzer des Abonnements.|  
|**cft_table**|**sysname**|Der Name der Konflikttabelle dieses Artikels für den Replikationstyp Verzögertes Update über eine Warteschlange.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
