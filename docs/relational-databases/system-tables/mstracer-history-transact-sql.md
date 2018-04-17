---
title: MStracer_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 789289c449c70f4bffafb26798f3364a404cc174
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MStracer_history** -Tabelle unterhält eine Aufzeichnung aller Überwachungstoken, die auf dem Abonnenten empfangen wurden. Diese Tabelle wird in der Verteilungsdatenbank gespeichert. Sie wird von der Replikation für die Leistungsüberwachung verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|Die eindeutige Identifikation eines Überwachungstokens.|  
|**agent_id**|**int**|Identifiziert den Agent, der den Überwachungstokendatensatz behandelt hat.|  
|**subscriber_commit**|**datetime**|Das Datum und die Uhrzeit, zu denen der Commit des Überwachungstokendatensatzes auf dem Abonnenten durchgeführt wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
