---
title: "Einige Verf&#252;gbarkeitsreplikate haben keine fehlerfreie Rolle | Microsoft Docs"
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
  - "sql13.swb.agdashboard.agp6allroleshealthy.issues.f1"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server-HADR], Richtlinien"
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
caps.latest.revision: 12
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 12
---
# Einige Verf&#252;gbarkeitsreplikate haben keine fehlerfreie Rolle
    
## Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsreplikat-Rollenstatus|  
|**Problem**|Einige Verfügbarkeitsreplikate haben keine fehlerfreie Rolle.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsgruppe|  
  
## Beschreibung  
 Diese Richtlinie führt ein Rollup des Verbindungsstatus aller Verfügbarkeitsreplikate aus und überprüft, ob Verfügbarkeitsreplikate vorhanden sind, die keine fehlerfreie Rolle aufweisen. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn jedes Verfügbarkeitsreplikat weder primär noch sekundär ist. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Einige Verfügbarkeitsreplikate haben keine fehlerfreie Rolle](http://go.microsoft.com/fwlink/p/?LinkId=220854).  
  
## Mögliche Ursachen  
 In dieser Verfügbarkeitsgruppe verfügt mindestens ein Verfügbarkeitsreplikat derzeit nicht über die primäre oder sekundäre Rolle.  
  
## Mögliche Lösung  
 Verwenden Sie den Verfügbarkeitsreplikat-Richtlinienstatus, um nach dem Verfügbarkeitsreplikat zu suchen, dessen Rolle nicht primär oder sekundär ist, und beheben Sie das Problem des Verfügbarkeitsreplikats.  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  