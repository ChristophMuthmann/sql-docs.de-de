---
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
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
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs: TSQL
helpviewer_keywords: Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60f13f390ec499a3cc6f8add79538ea6d2cb133d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSagentparameterlist** Tabelle enthält Parameterinformationen für Replikations-Agent und wird verwendet, um die Parameter angeben, die für einen bestimmten Agenttyp festgelegt werden können. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_type-Wert**|**tinyint**|Der Agenttyp:<br /><br /> **1** = Momentaufnahme-Agent.<br /><br /> **2** = Protokolllese-Agent.<br /><br /> **3** = Verteilungs-Agent.<br /><br /> **4** = Merge-Agent.<br /><br /> **9** = Warteschlangenlese-Agent.|  
|**Parametername**|**sysname**|Der Name eines gültigen Agentparameters.|  
|**Standardwert**|**nvarchar(4000)**|Der Standardwert des Agentparameters, wobei NULL darauf hinweist, dass kein Standardwert vorhanden ist.|  
|**MIN_VALUE**|**int**|Legt einen unteren Grenzwert für den Agentparameter fest, wobei NULL darauf hinweist, dass kein unterer Grenzwert vorhanden ist.|  
|**MAX_VALUE**|**int**|Legt einen oberen Grenzwert für den Agentparameter fest, wobei NULL darauf hinweist, dass kein oberer Grenzwert vorhanden ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
