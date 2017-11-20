---
title: "Sekundäre Datenbank ist nicht verknüpft | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6041c31fa2c2e015980c8fc8a7875ddd1e53ac13
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="secondary-database-is-not-joined"></a>Sekundäre Datenbank ist nicht verknüpft
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Joinzustand der Verfügbarkeitsdatenbank|  
|**Problem**|Die sekundäre Datenbank ist nicht verknüpft.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsdatenbank|  
  
## <a name="description"></a>Beschreibung  
 Diese Richtlinie überprüft den Joinstatus der sekundären Datenbank (auch bekannt als "sekundäres Datenbankreplikat"). Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn das Datenbankreplikat nicht verknüpft wird. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Sekundäre Datenbank ist nicht verknüpft](http://go.microsoft.com/fwlink/p/?LinkId=220862) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Diese sekundäre Datenbank ist nicht mit der Verfügbarkeitsgruppe verknüpft. Die Konfiguration dieser sekundären Datenbank ist unvollständig.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Verknüpfen Sie das sekundäre Replikat mit der Verfügbarkeitsgruppe mithilfe von Transact-SQL, PowerShell oder SQL Server Management Studio. Weitere Informationen zum Verknüpfen sekundärer Replikate mit Verfügbarkeitsgruppen finden Sie unter [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

