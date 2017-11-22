---
title: "Verfügbarkeitsreplikat hat keine fehlerfreie Rolle | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords: Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 52d4b09e46adcaeb65bedd0cb9dc7c5b28e27016
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="availability-replica-does-not-have-a-healthy-role"></a>Verfügbarkeitsreplikat hat keine fehlerfreie Rolle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsreplikat-Rollenstatus|  
|**Problem**|Das Verfügbarkeitsreplikat hat keine fehlerfreie Rolle.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>Beschreibung  
 Diese Richtlinie überprüft den Status der Verfügbarkeitsreplikatrolle. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn die Rolle des Verfügbarkeitsreplikats weder primär noch sekundär ist. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Verfügbarkeitsreplikat hat keine fehlerfreie Rolle](http://go.microsoft.com/fwlink/p/?LinkId=220856) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Die Rolle dieses Verfügbarkeitsreplikats ist fehlerhaft. Das Replikat hat nicht entweder die primäre oder sekundäre Rolle inne.  
  
## <a name="possible-solution-informationstilltocome"></a>Mögliche Lösung: Informationen_werden_noch_bereitgestellt  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
