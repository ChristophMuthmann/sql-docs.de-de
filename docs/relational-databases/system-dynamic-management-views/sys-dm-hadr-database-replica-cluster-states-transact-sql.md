---
title: Sys. dm_hadr_database_replica_cluster_states (Transact-SQL) | Microsoft Docs
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
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61b390df7f8d7b55472e11380b8eea429be20124
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrdatabasereplicaclusterstates-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile mit Informationen einen Einblick in den Zustand der verfügbarkeitsdatenbanken in der Always On-Verfügbarkeitsgruppen in jeder AlwaysOn-verfügbarkeitsgruppe auf dem Windows Server Failover Clustering (WSFC)-Cluster geben sollen. Abfrage **dm_hadr_database_replica_states** die folgenden Fragen beantworten:  
  
-   Sind alle Datenbanken in einer Verfügbarkeitsgruppe für ein Failover bereit?  
  
-   Wurde eine sekundäre Datenbank nach einem erzwungenen Failover lokal angehalten, und wurde das neue primäre Replikat über diesen Status informiert?  
  
-   Bei welchem sekundären Replikat wäre der Datenverlust am geringsten, wenn es zum primären Replikat würde, weil das primäre Replikat derzeit nicht verfügbar wäre?  
  
-   Wenn der Wert der [sys.databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)**Log_reuse_wait_desc** Spalte ist "AVAILABILITY_REPLICA", welches sekundäres Replikat in einer verfügbarkeitsgruppe kürzungen von Transaktionsprotokollen in einer bestimmten primären Datenbank aufhält ?  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Der Bezeichner des Verfügbarkeitsreplikats in der Verfügbarkeitsgruppe.|  
|**group_database_id**|**uniqueidentifier**|Der Bezeichner der Datenbank in der Verfügbarkeitsgruppe. Dieser Bezeichner ist auf jedem Replikat, mit dem diese Datenbank verknüpft ist, identisch.|  
|**database_name**|**sysname**|Der Name der Datenbank, die zur Verfügbarkeitsgruppe gehört.|  
|**is_failover_ready**|**bit**|Gibt an, ob die sekundäre Datenbank mit der entsprechenden primären Datenbank synchronisiert ist. Angaben sind möglich:<br /><br /> 0 = Die Datenbank ist im Cluster nicht als synchronisiert gekennzeichnet. Die Datenbank ist nicht zu einem Failover bereit.<br /><br /> 1 = Die Datenbank ist im Cluster als synchronisiert gekennzeichnet. Die Datenbank ist zu einem Failover bereit.|  
|**is_pending_secondary_suspend**|**bit**|Gibt an, ob das Anhalten der Datenbank nach einem erzwungenen Failover ansteht. Die möglichen Werte sind:<br /><br /> 0 = Beliebiger Status außer HADR_SYNCHRONIZED_ SUSPENDED.<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED. Wenn ein erzwungenes Failover abgeschlossen wird, wird jede der sekundären Datenbanken auf HADR_SYNCHONIZED_SUSPENDED festgelegt und bleibt in diesem Status, bis das neue primäre Replikat von dieser sekundären Datenbank eine Bestätigung für die SUSPEND-Meldung empfängt.<br /><br /> NULL = Unbekannt (kein Quorum)|  
|**is_database_joined**|**bit**|Gibt an, ob die Datenbank auf diesem Verfügbarkeitsreplikat mit der Verfügbarkeitsgruppe verknüpft wurde. Die möglichen Werte sind:<br /><br /> 0 = Die Datenbank ist nicht mit der Verfügbarkeitsgruppe auf diesem Verfügbarkeitsreplikat verknüpft.<br /><br /> 1 = Die Datenbank ist mit der Verfügbarkeitsgruppe auf diesem Verfügbarkeitsreplikat verknüpft.<br /><br /> NULL = unbekannt (Das Verfügbarkeitsreplikat hat kein Quorum.)|  
|**recovery_lsn**|**numeric(25,0)**|Bei einem primären Replikat das Ende des Transaktionsprotokolls, bevor das Replikat nach einer Wiederherstellung oder einem Failover neue Protokolldatensätze schreibt. Auf dem primären Replikat verfügt die Zeile für eine bestimmte sekundäre Datenbank über den Wert, in den das primäre Replikat das sekundäre Replikat synchronisieren soll (also der Wert für die Wiederherstellung und erneute Initialisierung).<br /><br /> Auf sekundären Replikaten ist dieser Wert NULL. Beachten Sie, dass jedes sekundäre Replikat entweder den MAX-Wert oder einen niedrigeren Wert aufweist, auf den das sekundäre Replikat auf Aufweisung des primären Replikats zurückgesetzt werden soll.|  
|**truncation_lsn**|**numeric(25,0)**|Der [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Protokollkürzungswert, der höher als die lokale Kürzungs-LSN sein kann, wenn die lokale Protokollkürzung blockiert wird (z. B. durch einen Sicherungsvorgang).|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen für Always On-Verfügbarkeitsgruppen (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Katalogsichten Always On-Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Überwachen von Verfügbarkeitsgruppen & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Sys. dm_hadr_database_replica_states & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
