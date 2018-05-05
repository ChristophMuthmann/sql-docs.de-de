---
title: Sysreplicationalerts (Transact-SQL) | Microsoft Docs
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
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a6579b75ab8d8af66ed62bd9af021f65235423f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu den Bedingungen, die die Auslösung einer Replikationswarnung verursachen. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Die ID der Warnung.|  
|**status**|**int**|Der benutzerdefinierte Wert:<br /><br /> **0** = nicht bedient.<br /><br /> **1** = bedient.|  
|**agent_type**|**int**|Typ der Momentaufnahme:<br /><br /> **1** = Momentaufnahme-Agent.<br /><br /> **2** = Protokolllese-Agent.<br /><br /> **3** = Verteilungs-Agent.<br /><br /> **4** = Merge-Agent.|  
|**agent_id**|**int**|Die Agent-ID aus den Tabellen **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**, oder **MSmerge_agents**.|  
|**Fehler-ID**|**int**|Die ID des Fehlers in gespeicherten **MSrepl_errors**.|  
|**alert_error_code**|**int**|Die Meldungs-ID der bei der Protokollierung dieses Datensatzes ausgelösten Warnung.|  
|**Uhrzeit**|**datetime**|Der Zeitpunkt, zu dem der Datensatz eingefügt wurde.|  
|**publisher**|**sysname**|Der Name des Verlegers, der dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**publisher_db**|**sysname**|Die Verlegerdatenbank, die dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**Veröffentlichung**|**sysname**|Die Veröffentlichung, die dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**publication_type**|**int**|Der Typ der Veröffentlichung:<br /><br /> **0** = Snapshot.<br /><br /> **1** = transaktionsveröffentlichung.<br /><br /> **2** = befindet.|  
|**subscriber**|**sysname**|Der Name des Abonnenten, der dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**subscriber_db**|**sysname**|Der Name der Abonnentendatenbank, die dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**article**|**sysname**|Der Name des Artikels, der dem Agent zugeordnet ist, der diese Warnung ausgelöst hat.|  
|**destination_object**|**sysname**|Der Name der der Warnung zugeordneten Abonnementtabelle.|  
|**source_object**|**sysname**|Der Name der der Warnung zugeordneten veröffentlichten Tabelle.|  
|**alert_error_text**|**ntext**|Der Text der Warnung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
