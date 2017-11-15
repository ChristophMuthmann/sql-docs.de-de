---
title: "Einige Verfügbarkeitsreplikate sind getrennt | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords: Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1dae927419403deb993127620c3ff7a012241b7b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="some-availability-replicas-are-disconnected"></a>Einige Verfügbarkeitsreplikate sind getrennt
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verbindungsstatus von Verfügbarkeitsreplikaten|  
|**Problem**|Einige Verfügbarkeitsreplikate sind getrennt.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsgruppe|  
  
## <a name="description"></a>Beschreibung  
 Diese Richtlinie führt ein Rollup des Verbindungsstatus aller Verfügbarkeitsreplikate durch und überprüft, ob Verfügbarkeitsreplikate den Status DISCONNECTED aufweisen. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn der Verbindungsstatus von einem der Verfügbarkeitsreplikate DISCONNECTED lautet. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Einige Verfügbarkeitsreplikate sind getrennt](http://go.microsoft.com/fwlink/p/?LinkId=220855) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 In dieser Verfügbarkeitsgruppe ist mindestens ein sekundäres Replikat nicht mit dem primären Replikat verbunden. Der Verbindungsstatus lautet DISCONNECTED.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Verwenden Sie den Verfügbarkeitsreplikat-Richtlinienstatus, um nach dem Verfügbarkeitsreplikat mit dem Status DISCONNECTED zu suchen, und beheben Sie dann das Problem des Verfügbarkeitsreplikats.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
