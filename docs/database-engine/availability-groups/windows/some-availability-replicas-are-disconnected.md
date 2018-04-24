---
title: Einige Verfügbarkeitsreplikate sind getrennt | Microsoft-Dokumentation
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
- sql13.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c81031bdfd58458f917109e14c2c6794f57fc920
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="some-availability-replicas-are-disconnected"></a>Einige Verfügbarkeitsreplikate sind getrennt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verbindungsstatus von Verfügbarkeitsreplikaten|  
|**Problem**|Einige Verfügbarkeitsreplikate sind getrennt.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsgruppe|  
  
## <a name="description"></a>Description  
 Diese Richtlinie führt ein Rollup des Verbindungsstatus aller Verfügbarkeitsreplikate durch und überprüft, ob Verfügbarkeitsreplikate den Status DISCONNECTED aufweisen. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn der Verbindungsstatus von einem der Verfügbarkeitsreplikate DISCONNECTED lautet. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Einige Verfügbarkeitsreplikate sind getrennt](http://go.microsoft.com/fwlink/p/?LinkId=220855) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 In dieser Verfügbarkeitsgruppe ist mindestens ein sekundäres Replikat nicht mit dem primären Replikat verbunden. Der Verbindungsstatus lautet DISCONNECTED.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Verwenden Sie den Verfügbarkeitsreplikat-Richtlinienstatus, um nach dem Verfügbarkeitsreplikat mit dem Status DISCONNECTED zu suchen, und beheben Sie dann das Problem des Verfügbarkeitsreplikats.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
