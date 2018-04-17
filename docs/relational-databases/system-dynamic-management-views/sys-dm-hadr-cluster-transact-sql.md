---
title: Sys. dm_hadr_cluster (Transact-SQL) | Microsoft Docs
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
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 911630f4d93505611d3773f61b8afc5f1a4d9dda
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Wenn der Windows Server Failover Clustering (WSFC)-Knoten, der eine Instanz von hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -fähige [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] verfügt über ein WSFC-Quorum **Sys. dm_hadr_cluster** eine Zeile zurück, die den Clusternamen und Informationen verfügbar macht über das Quorum. Wenn der WSFC-Knoten nicht über ein Quorum verfügt, wird keine Zeile zurückgegeben.  
 > [!TIP]
 > Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], diese dynamische verwaltungssicht unterstützt immer auf Failoverclusterinstanzen zusätzlich zu AlwaysOn-Verfügbarkeitsgruppen.

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Der Name des WSFC-Clusters, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-fähigen Instanzen von [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] hostet.|  
|**quorum_type**|**tinyint**|Der Typ des Quorums, der von diesem WSFC-Cluster verwendet wird. Folgende Werte sind möglich:<br /><br /> 0 = Knotenmehrheit Diese Quorumkonfiguration kann Fehler bei der Hälfte der Knoten (aufgerundet) minus einem tolerieren. In einem Cluster mit sieben Knoten kann diese Quorumkonfiguration z. B. drei Knotenfehler tolerieren.<br /><br /> 1 = Knoten- und Datenträgermehrheit Wenn der Datenträgerzeuge online bleibt, kann diese Quorumkonfiguration Fehler bei der Hälfte der Knoten (aufgerundet) tolerieren. So kann ein Cluster mit sechs Knoten, in dem der Datenträgerzeuge online ist, beispielsweise drei Knotenfehler tolerieren. Wenn der Datenträgerzeuge offline geht oder ein Datenträgerzeugenfehler auftritt, kann diese Quorumkonfiguration Fehler bei der Hälfte der Knoten (aufgerundet) minus einem Knoten tolerieren. Ein Cluster mit sechs Knoten, in dem ein Datenträgerzeugenfehler aufgetreten ist, kann beispielsweise zwei (3 minus 1 = 2) Knotenfehler tolerieren.<br /><br /> 2 = Knoten- und Dateifreigabemehrheit Diese Quorumkonfiguration funktioniert auf eine ähnliche Weise wie die Knoten- und Datenträgermehrheit, verwendet aber einen Dateifreigabenzeugen statt eines Datenträgerzeugen.<br /><br /> 3 = Keine Mehrheit: Nur Datenträger Wenn der Quorumdatenträger online ist, kann diese Quorumkonfiguration Fehler bei allen Knoten außer einem tolerieren.|  
|**quorum_type_desc**|**varchar(50)**|Beschreibung von **quorum_type**. Folgende Werte sind möglich:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY|  
|**quorum_state**|**tinyint**|Status des WSFC-Quorums. Folgende Werte sind möglich:<br /><br /> 0 = Unbekannter Quorumstatus<br /><br /> 1 = Normales Quorum<br /><br /> 2 = Erzwungenes Quorum|  
|**quorum_state_desc**|**varchar(50)**|Beschreibung von **quorum_state**. Folgende Werte sind möglich:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen für Always On-Verfügbarkeitsgruppen (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Katalogsichten Always On-Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Überwachen von Verfügbarkeitsgruppen & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
