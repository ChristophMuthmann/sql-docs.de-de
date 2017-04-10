---
title: "Sekund&#228;re Datenbank ist nicht verkn&#252;pft | Microsoft Docs"
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
  - "sql13.swb.agdashboard.drp2joined.issues.f1"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server-HADR], Richtlinien"
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 14
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 14
---
# Sekund&#228;re Datenbank ist nicht verkn&#252;pft
    
## Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Joinzustand der Verfügbarkeitsdatenbank|  
|**Problem**|Die sekundäre Datenbank ist nicht verknüpft.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsdatenbank|  
  
## Beschreibung  
 Diese Richtlinie überprüft den Joinstatus der sekundären Datenbank (auch bekannt als "sekundäres Datenbankreplikat"). Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn das Datenbankreplikat nicht verknüpft wird. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Sekundäre Datenbank ist nicht verknüpft](http://go.microsoft.com/fwlink/p/?LinkId=220862).  
  
## Mögliche Ursachen  
 Diese sekundäre Datenbank ist nicht mit der Verfügbarkeitsgruppe verknüpft. Die Konfiguration dieser sekundären Datenbank ist unvollständig.  
  
## Mögliche Lösung  
 Verknüpfen Sie das sekundäre Replikat mit der Verfügbarkeitsgruppe mithilfe von Transact-SQL, PowerShell oder SQL Server Management Studio. Weitere Informationen zum Verknüpfen sekundärer Replikate mit Verfügbarkeitsgruppen finden Sie unter [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  