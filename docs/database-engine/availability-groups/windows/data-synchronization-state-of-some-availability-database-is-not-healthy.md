---
title: "Datensynchronisierungsstatus einer Verfügbarkeitsdatenbank ist nicht fehlerfrei | Microsoft-Dokumentation"
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
- sql13.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 38a5c364965a31d1442ea68a982270b109aa3451
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>Datensynchronisierungsstatus einer Verfügbarkeitsdatenbank ist nicht fehlerfrei
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Datensynchronisierungsstatus des Verfügbarkeitsreplikats|  
|**Problem**|Der Datensynchronisierungsstatus einer Verfügbarkeitsdatenbank ist nicht fehlerfrei.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>Beschreibung  
 Diese Richtlinie überprüft den Datensynchronisierungsstatus der Verfügbarkeitsdatenbank (auch bekannt als "Datenbankreplikat"). Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn der Datensynchronisierungsstatus NOT SYNCHRONIZING lautet oder wenn der Status für das Datenbankreplikat mit synchronem Commit SYNCHRONIZED lautet.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Datensynchronisierungsstatus der Verfügbarkeitsdatenbank ist nicht fehlerfrei](http://go.microsoft.com/fwlink/p/?LinkId=220863) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Mindestens eine Verfügbarkeitsdatenbank des Replikats verfügt über einen fehlerhaften Datensynchronisierungsstatus. Wenn das Replikat ein Verfügbarkeitsreplikat für asynchrone Commits ist, sollten alle Verfügbarkeitsdatenbanken den Status SYNCHRONIZING aufweisen. Falls es sich dabei um ein Verfügbarkeitsreplikat für synchrone Commits handelt, sollten sich alle Verfügbarkeitsdatenbanken im Status SYNCHRONIZED befinden. Dieses Problem kann folgende Ursachen haben:  
  
-   Die Verbindung des Verfügbarkeitsreplikats wurde getrennt.  
  
-   Die Datenverschiebung wurde angehalten.  
  
-   Auf die Datenbank kann nicht zugegriffen werden.  
  
-   Es liegt ein vorübergehendes Verzögerungsproblem aufgrund der Netzwerklatenzzeit oder der Last auf dem primären oder sekundären Replikat vor.  
  
## <a name="possible-solution"></a>Mögliche Lösung  
 Beheben Sie alle Probleme in Bezug auf die Verbindung oder auf die angehaltene Datenverschiebung. Überprüfen Sie die Ereignisse für dieses Problem mit SQL Server Management Studio, und ermitteln Sie den Datenbankfehler. Führen Sie die entsprechenden Schritte der Problembehandlung für den Fehler aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

