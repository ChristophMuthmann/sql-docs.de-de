---
title: Sys. dm_hadr_availability_group_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_group_states
- sys.dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states_TSQL
- dm_hadr_availability_group_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_group_states dynamic management view
ms.assetid: d18019dd-f8dc-4492-b035-b1a639369b65
caps.latest.revision: 43
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2c7ac7e50efeb3bb815aec54325067edd9f61bb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadravailabilitygroupstates-transact-sql"></a>sys.dm_hadr_availability_group_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede AlwaysOn-verfügbarkeitsgruppe, die ein verfügbarkeitsreplikat in der lokalen Instanz von besitzt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In jede Zeile werden die Statuswerte angezeigt, die den Zustand einer angegebenen Verfügbarkeitsgruppe definieren.  
  
> [!NOTE]  
>  Um die vollständige Liste der abzurufen, Fragen Sie die [availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) -Katalogsicht angezeigt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Eindeutiger Bezeichner der Verfügbarkeitsgruppe.|  
|**primary_replica**|**varchar(128)**|Name der Serverinstanz, die das aktuelle primäre Replikat hostet.<br /><br /> NULL = Nicht das primäre Replikat, oder mit dem WSFC-Failovercluster kann nicht kommuniziert werden.|  
|**primary_recovery_health**|**tinyint**|Gibt den Wiederherstellungszustand des primären Replikats an. Folgende Werte sind möglich:<br /><br /> 0 = wird ausgeführt<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Auf sekundären Replikaten der **Primary_recovery_health** Spalte ist NULL.|  
|**primary_recovery_health_desc**|**nvarchar(60)**|Beschreibung des **Primary_replica_health**, eine von:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**secondary_recovery_health**|**tinyint**|Gibt den Wiederherstellungszustand eines sekundären replikatreplikats, eines an:<br /><br /> 0 = wird ausgeführt<br /><br /> 1 = Online<br /><br /> NULL<br /><br /> Auf dem primären Replikat der **Secondary_recovery_health** Spalte ist NULL.|  
|**secondary_recovery_health_desc**|**nvarchar(60)**|Beschreibung des **Secondary_recovery_health**, eine von:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization_health**|**tinyint**|Stellt ein Rollup von der **"synchronization_health"** aller verfügbarkeitsreplikate in der verfügbarkeitsgruppe. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> 0: nicht fehlerfrei. Keines der verfügbarkeitsreplikate verfügt über einen fehlerfreien **"synchronization_health"** (2 = HEALTHY).<br /><br /> 1: teilweise fehlerfrei. Der Synchronisierungsstatus einiger, aber nicht aller Verfügbarkeitsreplikate ist fehlerfrei.<br /><br /> 2: fehlerfrei. Der Synchronisierungsstatus jedes Verfügbarkeitsreplikats ist fehlerfrei.<br /><br /> Informationen zum Synchronisierungsstatus des Replikats finden Sie unter der **"synchronization_health"** Spalte [Sys. dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md).|  
|**synchronization_health_desc**|**nvarchar(60)**|Beschreibung des **"synchronization_health"**, eine von:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen von Verfügbarkeitsgruppen & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn Availability Groups, dynamische Verwaltungssichten und-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
