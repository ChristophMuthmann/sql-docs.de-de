---
title: "Konfigurieren von Integrit&#228;tsrichtlinien (SQL Server-Hilfsprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Konfigurieren von Integrit&#228;tsrichtlinien (SQL Server-Hilfsprogramm)
  Verwenden Sie das Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramms in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um Ressourcenparameter des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramms für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Datenebenenanwendungen anzuzeigen. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Um Ergebnisse der Integritätsrichtlinien des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramms anzuzeigen, stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] eine Verbindung mit dem Steuerungspunkt für das Hilfsprogramm her. Weitere Informationen finden Sie unter [Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integritätsrichtlinien des Hilfsprogramms können für Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konfiguriert werden. Integritätsrichtlinien können global für alle Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm definiert werden, oder Sie definieren sie für jede Datenebenenanwendung und jede verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einzeln im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm.  
  
## Überwachen von Richtlinien für Datenebenenanwendungen  
 Folgende Richtlinien gelten für die Über- und Unterauslastung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenebenenanwendungen:  
  
-   Prozessorauslastung der Datenebenenanwendung  
  
-   Dateispeicherplatz der Datenebenenanwendung für Datenbankdateien  
  
-   Dateispeicherplatz der Datenebenenanwendung für Speichervolumes  
  
-   Prozessorauslastung des Computers  
  
> [!NOTE]  
>  Speichervolume und Prozessorauslastung sind für Datenebenenanwendungen schreibgeschützte Richtlinien.  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien für Datenebenenanwendungen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md).  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien für Datenebenenanwendungen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Deployed%20Data-tier%20Application%20Details%20\(SQL%20Server%20Utility\).md).  
  
## Überwachen von Richtlinien für verwaltete SQL Server-Instanzen  
 Richtlinien zur Über- und Unterauslastung für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lauten wie folgt:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für Datenbankdateien  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für Speichervolumes  
  
-   Prozessorauslastung des Computers  
  
 Weitere Informationen zum Anzeigen oder Ändern globaler Überwachungsrichtlinien von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md).  
  
 Weitere Informationen zum Anzeigen oder Ändern von Überwachungsrichtlinien für einzelne verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](../Topic/Managed%20Instance%20Details%20\(SQL%20Server%20Utility\).md).  
  
## Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  