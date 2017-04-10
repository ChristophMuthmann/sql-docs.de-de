---
title: "Datensynchronisierungsstatus der Verf&#252;gbarkeitsdatenbank ist nicht fehlerfrei | Microsoft Docs"
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
  - "sql13.swb.agdashboard.arp3datasynchealthy.issues.f1"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server-HADR], Richtlinien"
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
caps.latest.revision: 15
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "erikre"
caps.handback.revision: 15
---
# Datensynchronisierungsstatus der Verf&#252;gbarkeitsdatenbank ist nicht fehlerfrei
    
## Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Datensynchronisierungsstatus der Verfügbarkeitsdatenbank|  
|**Problem**|Der Datensynchronisierungsstatus der Verfügbarkeitsdatenbank ist nicht fehlerfrei.|  
|**Kategorie**|**Warnung**|  
|**Facet**|Verfügbarkeitsdatenbank|  
  
## Beschreibung  
 Diese Richtlinie führt ein Rollup des Datensynchronisierungsstatus aller Verfügbarkeitsdatenbanken (auch bekannt als "Datenbankreplikate") im Verfügbarkeitsreplikat aus. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn ein beliebiges Datenbankreplikat nicht den erwarteten Datensynchronisierungsstatus aufweist. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für dieses Release von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Datensynchronisierungsstatus einer Verfügbarkeitsdatenbank ist nicht fehlerfrei](http://go.microsoft.com/fwlink/p/?LinkId=220858).  
  
## Mögliche Ursachen  
 Der Datensynchronisierungsstatus dieser Verfügbarkeitsdatenbank ist fehlerhaft. Auf einem Verfügbarkeitsreplikat für asynchrone Commits sollte sich jede Verfügbarkeitsdatenbank im Status SYNCHRONIZING befinden. Auf einem Replikat für synchrone Commits muss sich jede Verfügbarkeitsdatenbank im Status SYNCHRONIZED befinden.  
  
## Mögliche Lösung  
 Verwenden Sie die Datenbankreplikatrichtlinie zum Suchen nach dem Datenbankreplikat mit einem fehlerhaften Datensynchronisierungsstatus, und beheben Sie das Problem für das Datenbankreplikat.  
  
## Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../Topic/Overview%20of%20Always On%20Availability%20Groups%20\(SQL%20Server\).md)   
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20Always On%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md)  
  
  