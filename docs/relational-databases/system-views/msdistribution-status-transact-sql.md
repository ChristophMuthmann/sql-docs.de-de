---
title: MSdistribution_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdistribution_status_TSQL
- MSdistribution_status
dev_langs: TSQL
helpviewer_keywords: MSdistribution_status view
ms.assetid: 90d447de-3a4a-4f3e-aeab-e8fff6348361
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f6f18aa6d26fca65d26fd7d6dda39ee1ca54b2a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="msdistributionstatus-transact-sql"></a>MSdistribution_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdistribution_status** -Sicht macht zusätzliche Informationen zu den statusbefehlen in der Verteilungsdatenbank verfügbar. Diese Sicht wird in der distribution-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifiziert einen Artikel.|  
|**agent_id-Wert**|**int**|Identifiziert einen Replikations-Agent|  
|**UndelivCmdsInDistDB**|**int**|Die Anzahl der Befehle, die für die Übermittlung an Abonnenten ausstehen.|  
|**DelivCmdsInDistDB**|**int**|Die Anzahl der Befehle, die an Abonnenten übermittelt wurden|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
