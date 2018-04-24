---
title: WSFC-Clusterdienst ist offline | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5fe8f821f046e8838893c33ab61ebabd7454688
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="wsfc-cluster-service-is-offline"></a>WSFC-Clusterdienst ist offline
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|WSFC-Clusterstatus|  
|**Problem**|Der WSFC-Clusterdienst ist offline.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|SQL Server-Instanz|  
  
## <a name="description"></a>Description  
 Diese Richtlinie überprüft den Status des Windows Server-Failoverclusters (WSFC). Die Richtlinie befindet sich in einem fehlerhaften Zustand und löst eine Warnung aus, wenn der WSFC-Cluster offline ist oder sich im erzwungenen Quorumstatus befindet. Alle innerhalb dieses Clusters gehosteten Verfügbarkeitsgruppen sind offline, oder eine Notfallwiederherstellungsaktion ist erforderlich.  
  
 Der Richtlinienstatus ist fehlerfrei, wenn der Clusterstatus das normale Quorum aufweist.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [WSFC-Clusterdienst ist offline](http://go.microsoft.com/fwlink/p/?LinkId=220849) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Dieses Problem kann von einem Clusterdienstfehler oder aufgrund des Verlusts des Quorums im Cluster verursacht werden.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Verwenden Sie das Clusterverwaltungstool, um den Workflow für das erzwungene Quorum oder für die Notfallwiederherstellung auszuführen. Falls Sie das Problem nicht beheben können, indem Sie den Workflow für das erzwungene Quorum oder die Notfallwiederherstellung ausführen, sollten Sie Ihren Clusteradministrator um Unterstützung bei der Lösung dieses Problems bitten. Weitere Informationen finden Sie unter: [Erzwingen des Starts eines Clusters ohne Quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
