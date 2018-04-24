---
title: Verfügbarkeitsreplikat ist nicht verknüpft | Microsoft-Dokumentation
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
- sql13.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 655b71b1a921c5a43677d4341e950ca134a37adc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="availability-replica-is-not-joined"></a>Verfügbarkeitsreplikat ist nicht verknüpft
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Joinzustand des Verfügbarkeitsreplikats|  
|**Problem**|Verfügbarkeitsreplikat ist nicht verknüpft.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>Description  
 Diese Richtlinie überprüft den Verknüpfungsstatus des Verfügbarkeitsreplikats. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn der Verfügbarkeitsgruppe das Verfügbarkeitsreplikat hinzugefügt, aber nicht ordnungsgemäß damit verknüpft wird. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Das Verfügbarkeitsreplikat ist nicht verknüpft](http://go.microsoft.com/fwlink/p/?LinkId=220859) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Das sekundäre Replikat ist nicht mit der Verfügbarkeitsgruppe verknüpft. Damit ein Verfügbarkeitsreplikat erfolgreich mit der Verfügbarkeitsgruppe verknüpft wird, muss der Verknüpfungsstatus "Verknüpfte eigenständige Instanz" (1) oder "Verknüpfter Failovercluster" (2) lauten.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Verknüpfen Sie das sekundäre Replikat mit der Verfügbarkeitsgruppe mithilfe von Transact-SQL, PowerShell oder SQL Server Management Studio. Weitere Informationen zum Verknüpfen sekundärer Replikate mit Verfügbarkeitsgruppen finden Sie unter [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
