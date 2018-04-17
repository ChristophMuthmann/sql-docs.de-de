---
title: MSpeer_response (Transact-SQL) | Microsoft Docs
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
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e095e2602c791693954f7400e32c1075d4ed206
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mspeerresponse-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSpeer_response** Tabelle wird in der Peer-zu-Peer-Replikation zum Speichern des Knotens als Antwort auf eine veröffentlichungsstatusanforderung verwendet. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|Identifiziert einen statusanforderungseintrag in der [MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) Tabelle.|  
|**Peer**|**sysname**|Der Peer, der die Antwort generiert hat.|  
|**peer_db**|**sysname**|Die Abonnementdatenbank auf dem Peer, der die Antwort generiert hat.|  
|**received_date**|**datetime**|Datum und Uhrzeit des Empfangs der Peeranforderung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
