---
title: "Konfigurieren von Integritätsrichtlinien (SQL Server-Hilfsprogramm) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b8d0fff3e8a9194cbc2bf4945c134cb18715d83a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-health-policies-sql-server-utility"></a>Konfigurieren von Integritätsrichtlinien (SQL Server-Hilfsprogramm)
  Verwenden Sie das Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um Ressourcenparameter des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Datenebenenanwendungen anzuzeigen. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Um Ergebnisse der Integritätsrichtlinien des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms anzuzeigen, stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Steuerungspunkt für das Hilfsprogramm her. Weitere Informationen finden Sie unter [Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integritätsrichtlinien des Hilfsprogramms können für Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert werden. Integritätsrichtlinien können global für alle Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm definiert werden, oder Sie definieren sie für jede Datenebenenanwendung und jede verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einzeln im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm.  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>Überwachen von Richtlinien für Datenebenenanwendungen  
 Folgende Richtlinien gelten für die Über- und Unterauslastung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenebenenanwendungen:  
  
-   Prozessorauslastung der Datenebenenanwendung  
  
-   Dateispeicherplatz der Datenebenenanwendung für Datenbankdateien  
  
-   Dateispeicherplatz der Datenebenenanwendung für Speichervolumes  
  
-   Prozessorauslastung des Computers  
  
> [!NOTE]  
>  Speichervolume und Prozessorauslastung sind für Datenebenenanwendungen schreibgeschützte Richtlinien.  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien für Datenebenenanwendungen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien für Datenebenenanwendungen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>Überwachen von Richtlinien für verwaltete SQL Server-Instanzen  
 Richtlinien zur Über- und Unterauslastung für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lauten wie folgt:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für Datenbankdateien  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für Speichervolumes  
  
-   Prozessorauslastung des Computers  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Weitere Informationen zum Anzeigen oder Ändern von Überwachungsrichtlinien für einzelne verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
