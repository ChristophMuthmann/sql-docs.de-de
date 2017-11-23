---
title: MSreplication_subscriptions (Transact-SQL) | Microsoft Docs
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
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3840528a0a566f250eae99c2764f64766c4e0891
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationsubscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSreplication_subscriptions** -Tabelle enthält eine Zeile mit Replikationsinformationen für jeden Verteilungs-Agent, der die lokale Abonnentendatenbank Wartung. Diese Tabelle wird in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Der Name des Verlegers.|  
|**publisher_db**|**sysname**|Der Name der Verlegerdatenbank.|  
|**Veröffentlichung**|**sysname**|Der Name der Veröffentlichung.|  
|**independent_agent**|**bit**|Zeigt an, ob ein Verteilungs-Agent im Einzelplatzmodus für diese Veröffentlichung vorhanden ist.|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> 0 = Push.<br /><br /> 1 = Pull.<br /><br /> 2 = Anonym.|  
|**distribution_agent**|**sysname**|Der Name des Verteilungs-Agents.|  
|**Zeit**|**smalldatetime**|Der Zeitpunkt des letzten Updates durch den Verteilungs-Agent.|  
|**Beschreibung**|**nvarchar(255)**|Die Beschreibung des Abonnements.|  
|**transaction_timestamp**|**varbinary(16)**|Intern-nur zur Verwendung.|  
|**update_mode**|**tinyint**|Der Typ des Updates.|  
|**agent_id-Wert**|**Binary(16)**|Die ID der Momentaufnahme.|  
|**subscription_guid**|**Binary(16)**|Der globale Bezeichner für die Version des Abonnements für die Veröffentlichung.|  
|**subid**|**Binary(16)**|Der globale Bezeichner für ein anonymes Abonnement.|  
|**immediate_sync**|**bit**|Zeigt an, ob bei jeder Ausführung des Momentaufnahme-Agents Synchronisierungsdateien erstellt oder neu erstellt werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
