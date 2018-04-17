---
title: Sys. availability_databases_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c781a3e8d09596096244e95855aa7ce0c71074e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede verfügbarkeitsdatenbank auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hostet, die ein verfügbarkeitsreplikat für eine beliebige Always On-verfügbarkeitsgruppe im Windows Server Failover Clustering (WSFC)-Cluster, unabhängig davon, ob die lokale Datenbank kopieren wurde bereits mit der verfügbarkeitsgruppe verknüpft wurde.  
  
> [!NOTE]  
>  Wenn eine Datenbank einer Verfügbarkeitsgruppe hinzugefügt wird, wird die primäre Datenbank automatisch mit der Gruppe verknüpft. Sekundäre Datenbanken müssen auf jedem sekundären Replikat vorbereitet werden, bevor sie mit der Verfügbarkeitsgruppe verknüpft werden können.   
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Eindeutiger Bezeichner der Verfügbarkeitsgruppe, in der die Datenbank enthalten ist, falls vorhanden.<br /><br /> NULL = Datenbank ist kein Teil eines Verfügbarkeitsreplikats einer Verfügbarkeitsgruppe|  
|**group_database_id**|**uniqueidentifier**|Eindeutiger Bezeichner der Datenbank innerhalb der Verfügbarkeitsgruppe, in der die Datenbank enthalten ist, falls vorhanden. **group_database_id** ist für diese Datenbank auf dem primären Replikat und jedem sekundären Replikat, auf dem die Datenbank der Verfügbarkeitsgruppe hinzugefügt wurde, identisch.<br /><br /> NULL = Datenbank ist kein Teil eines Verfügbarkeitsreplikats einer beliebigen Verfügbarkeitsgruppe|  
|**database_name**|**sysname**|Name der Datenbank, die der Verfügbarkeitsgruppe hinzugefügt wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn der Aufrufer von **sys.availability_databases_cluster** nicht der Besitzer der Datenbank ist, sind zum Anzeigen der entsprechenden Zeile mindestens die Berechtigungen ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene oder die CREATE DATABASE-Berechtigung für die **master** -Datenbank oder aktuelle Datenbank erforderlich.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys. dm_hadr_database_replica_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [Sys. dm_hadr_database_replica_cluster_states &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
