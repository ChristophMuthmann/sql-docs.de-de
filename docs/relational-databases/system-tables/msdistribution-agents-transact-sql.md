---
title: MSdistribution_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
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
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2bb6aa8917a34946eeaab0d79ccb7a9ed04dcf0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msdistributionagents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdistribution_agents** Tabelle enthält eine Zeile für jeden auf dem lokalen Verteiler ausgeführten Verteilungs-Agent. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Die ID des Verteilungs-Agents.|  
|**name**|**Nvarchar(100)**|Der Name des Verteilungs-Agents.|  
|**publisher_database_id**|**int**|Die ID der Verlegerdatenbank.|  
|**publisher_id**|**smallint**|Die ID des Verlegers|  
|**publisher_db**|**sysname**|Der Name der Verlegerdatenbank.|  
|**Veröffentlichung**|**sysname**|Der Name der Veröffentlichung.|  
|**subscriber_id**|**smallint**|Die ID des Abonnenten; wird nur von bekannten Agents verwendet. Für anonyme Agents ist dies eine reservierte Spalte.|  
|**subscriber_db**|**sysname**|Der Name der Abonnementdatenbank|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> **0** = Push.<br /><br /> **1** = Pullabonnement.<br /><br /> **2** = anonym.|  
|**local_job**|**bit**|Gibt an, ob ein SQL Server-Agent-Auftrag auf dem lokalen Verteiler vorhanden ist.|  
|**job_id**|**Binary(16)**|Die Auftrags-ID|  
|**subscription_guid**|**Binary(16)**|Die ID der Abonnements dieses Agents|  
|**profile_id**|**int**|Der Konfigurations-ID aus der [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) Tabelle.|  
|**anonymous_subid**|**uniqueidentifier**|Die ID eines anonymen Agents.|  
|**subscriber_name**|**sysname**|Der Name des Abonnenten; wird nur von anonymen Agents verwendet|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|Datum und Uhrzeit der Erstellung des Verteilungs- oder Merge-Agents|  
|**queue_id**|**sysname**|Der Bezeichner für die Suche nach der Warteschlange für Abonnements mit verzögertem Update über eine Warteschlange. Für Abonnements ohne verzögertes Aktualisieren über eine Warteschlange ist der Wert gleich NULL. Für eine Veröffentlichung, die auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing basiert, ist der Wert ein GUID, der eindeutig die für das Abonnement zu verwendende Warteschlange bezeichnet. Für eine SQL Server-basierten Warteschlange enthält die Spalte den Wert **SQL**.<br /><br /> Hinweis: Mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing wurde als veraltet markiert und wird nicht mehr unterstützt.|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|Zeigt an, ob der Agent remote aktiviert werden kann.<br /><br /> **0** gibt an, dass der Agent Remote aktiviert werden kann.<br /><br /> **1** gibt an, dass der Agent Remote und auf dem Remotecomputer, die im angegebenen aktiviert werden die *Offload_server* Eigenschaft.|  
|**offload_server**|**sysname**|Der Netzwerkname des Servers, auf dem der Agent remote aktiviert werden soll|  
|**dts_package_name**|**sysname**|Der Name des DTS-Pakets. Z. B. für ein Paket mit dem Namen **DTSPub_Package**, geben Sie `@dts_package_name = N'DTSPub_Package'`.|  
|**dts_package_password**|**nvarchar(524)**|Das Kennwort für das Paket|  
|**dts_package_location**|**int**|Der Speicherort des Pakets. Der Speicherort des Pakets kann **Verteiler** oder **Abonnenten**.|  
|**SID**|**varbinary(85)**|Die Sicherheits-ID (SID) für den Verteilungs-Agent oder Merge-Agent, während er das erste Mal ausgeführt wird.|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|Der Sicherheitsmodus, der vom Agent beim Herstellen einer Verbindung mit dem Abonnenten verwendet wird, wobei die folgenden Werte möglich sind:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server-Authentifizierung<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung.|  
|**subscriber_login**|**sysname**|Der Anmeldename, der verwendet wird, um eine Verbindung mit dem Abonnenten herzustellen.|  
|**subscriber_password**|**nvarchar(524)**|Der verschlüsselte Wert des Kennworts, das beim Herstellen einer Verbindung mit dem Abonnenten verwendet wird|  
|**reset_partial_snapshot_progress**|**bit**|Gibt an, ob eine teilweise heruntergeladene Momentaufnahme verworfen wird, damit der gesamte Momentaufnahmeprozess erneut gestartet werden kann|  
|**job_step_uid**|**uniqueidentifier**|Die eindeutige ID des SQL Server-Agent-Auftrags Schritt, in dem der Agent gestartet wird.|  
|**subscriptionstreams**|**tinyint**|Legt die Anzahl der Verbindungen fest, die pro Verteilungs-Agent für die parallele Anwendung von Batches von Änderungen auf einen Abonnenten zulässig sind. Mögliche Werte zwischen 1 und 64 werden unterstützt.|  
|**memory_optimized**|**bit**|1 gibt an, dass der Abonnent für Speicheroptimierte Tabellen verwendet werden kann.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
