---
title: MStracer_tokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1822cdc0dd42a2e7797dec4aeb3a5b9627b4eac8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mstracertokens-transact-sql"></a>MStracer_tokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MStracer_tokens** -Tabelle unterhält eine Aufzeichnung der Überwachungstoken-Datensätze in einer Veröffentlichung eingefügt. Diese Tabelle wird in der Verteilungsdatenbank gespeichert. Sie wird von der Replikation für die Leistungsüberwachung verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifiziert einen Überwachungstoken-Datensatz.|  
|**publication_id**|**int**|Identifiziert die Veröffentlichung, in die der Überwachungstoken-Datensatz eingefügt wurde.|  
|**publisher_commit**|**datetime**|Das Datum und die Uhrzeit, zu dem ein Commit für den Überwachungstoken-Datensatz auf dem Verleger ausgeführt wurde.|  
|**distributor_commit**|**datetime**|Das Datum und die Uhrzeit, zu dem ein Commit für den Überwachungstoken-Datensatz auf dem Verteiler ausgeführt wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
