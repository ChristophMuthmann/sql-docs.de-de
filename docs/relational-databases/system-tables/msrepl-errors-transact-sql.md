---
title: MSrepl_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 48346fe7e8beb4c1885507de48d14889bd6ffee6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSrepl_errors** -Tabelle enthält Zeilen mit erweiterten Fehlerinformationen Verteilungs-Agent und Merge-Agent. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Die ID des Fehlers.|  
|**Uhrzeit**|**datetime**|Zeitpunkt des Auftretens des Fehlers.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|Die Typ-ID der Fehlerquelle.|  
|**source_name**|**Nvarchar(100)**|Der Name der Fehlerquelle.|  
|**error_code**|**sysname**|Der Fehlercode.|  
|**Fehlertext**|**ntext**|Die Fehlermeldung.|  
|**xact_seqno**|**varbinary(16)**|Die Protokollsequenznummer der ersten Transaktion des Batches, der bei der Ausführung einen Fehler erzeugt hat. Wird nur von Verteilungs-Agents verwendet und ist die Transaktions-Protokollfolgenummer der ersten Transaktion des bei der Ausführung fehlerhaften Batches.|  
|**command_id**|**int**|Die Befehls-ID des Batches, der bei der Ausführung einen Fehler erzeugt hat. Wird nur von Verteilungs-Agents verwendet und ist die Befehls-ID des ersten Befehls des Batches, der bei der Ausführung einen Fehler erzeugt hat.|  
|**session_id**|**int**|Die ID der Agentsitzung, in der der Fehler auftrat.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
