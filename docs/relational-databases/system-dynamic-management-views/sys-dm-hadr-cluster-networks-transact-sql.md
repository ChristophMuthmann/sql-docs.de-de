---
title: Sys. dm_hadr_cluster_networks (Transact-SQL) | Microsoft Docs
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
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 242d31e316102dd58319aa5630aa6ffe8bb915e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes WSFC-Clusterelement zurück, das an der Subnetzkonfiguration einer Verfügbarkeitsgruppe beteiligt ist. Sie können diese dynamische Verwaltungssicht verwenden, um die virtuelle IP-Adresse des Netzwerks zu überprüfen, die für jedes Verfügbarkeitsreplikat konfiguriert ist.  
  
 Primärschlüssel: **Member_name** + **Network_subnet_IP** + **Network_subnet_prefix_length**  
  
 > [!TIP]
 > Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], diese dynamische verwaltungssicht unterstützt immer auf Failoverclusterinstanzen zusätzlich zu AlwaysOn-Verfügbarkeitsgruppen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Der Computername eines Knotens im WSFC-Cluster.|  
|**network_subnet_ip**|**nvarchar(48)**|Die Netzwerk-IP-Adresse des Subnetzes, zu der der Computer gehört. Dies kann eine IPv4- oder eine IPv6-Adresse sein.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Die Netzwerksubnetz-Maske, die das Subnetz angibt, zu dem die IP-Adresse gehört. **network_subnet_ipv4_mask** DHCP < Network_subnet_option >-Optionen in einer mit DHCP-Klausel an die [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) oder [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.<br /><br /> NULL = IPv6-Subnetz.|  
||||  
|**network_subnet_prefix_length**|**int**|Die Präfixlänge der Netzwerk-IP-Adresse, die das Subnetz angibt, zu dem der Computer gehört.|  
|**is_public**|**bit**|Gibt an, ob das Netzwerk im WSFC-Cluster privat oder öffentlich ist. Folgende Werte sind möglich:<br /><br /> 0 = Privat<br /><br /> 1 = Öffentlich|  
|**is_ipv4**|**bit**|Der Typ des Subnetzes. Folgende Werte sind möglich:<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Failoverclustering und Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
