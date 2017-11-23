---
title: MSsync_states (Transact-SQL) | Microsoft Docs
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
- MSsync_states
- MSsync_states_TSQL
dev_langs: TSQL
helpviewer_keywords: MSsync_states system table
ms.assetid: b25e17e1-7718-432e-a442-c4946741d474
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ba8b39693791917df675e80fcaff8ffb51a0c2a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssyncstates-transact-sql"></a>MSsync_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsync_states** -Tabelle verfolgt nach, welche Veröffentlichung noch im Modus der gleichzeitigen momentaufnahmeverarbeitung ist. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Die ID des Verlegers.|  
|**publisher_db**|**sysname**|Der Name der Veröffentlichungsdatenbank.|  
|**publication_id**|**int**|Die ID der Veröffentlichung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Integration Services-Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)   
 [Sichern und Wiederherstellen von Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [Protokollversandtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
