---
title: "Verf&#252;gbarkeitsdatenbank angehalten | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.drp1notsuspended.issues.f1"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server-HADR], Richtlinien"
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
caps.latest.revision: 15
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 15
---
# Verf&#252;gbarkeitsdatenbank angehalten
    
## Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsdatenbank im angehaltenen Zustand|  
|**Problem**|Die Verfügbarkeitsdatenbank wurde angehalten.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsdatenbank|  
  
## Beschreibung  
 Diese Richtlinie überprüft den Status der Datenverschiebung für die sekundäre Datenbank (auch bekannt als "sekundäres Datenbankreplikat"). Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn die Datenverschiebung angehalten wird. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Availability database is suspended](http://go.microsoft.com/fwlink/p/?LinkId=220860).  
  
## Mögliche Ursachen  
 Die Datensynchronisierung dieser Verfügbarkeitsdatenbank kann aus den folgenden Gründen angehalten worden sein:  
  
-   Aufgrund eines Fehlers kann es sein, dass das System die Datensynchronisierung angehalten hat.  
  
-   Der Datenbankadministrator hat die Datensynchronisierung ggf. zu Wartungszwecken angehalten.  
  
## Mögliche Lösung  
 Setzen Sie die Datensynchronisierung fort. Falls das Problem weiterhin auftritt, sollten Sie die Verfügbarkeitsgruppe im Ereignisprotokoll überprüfen und dann diagnostizieren, warum das System die Datenverschiebung angehalten hat.  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  