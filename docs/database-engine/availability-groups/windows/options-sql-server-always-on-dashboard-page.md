---
title: "Optionen (SQL Server Always On, Dashboardseite) | Microsoft Docs"
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
  - "VS.ToolsOptionsPages.Alwayson.Dashboard"
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
caps.latest.revision: 8
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 8
---
# Optionen (SQL Server Always On, Dashboardseite)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Seite **SQL Server Always On-Dashboard** des [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Dialogfelds **Optionen**, um das Always On-Dashboard zu konfigurieren.  
  
 **So greifen Sie auf diese Seite zu:**  
  
 Klicken Sie im Menü **Extras** auf **Optionen**, erweitern Sie den Ordner **SQL Server Always On**, und klicken Sie dann auf **Dashboard**.  
  
## Auf dieser Seite  
 **Automatische Aktualisierung aktivieren**  
 Klicken Sie, um die automatische Aktualisierung zu aktivieren. Folgende Optionen sind verfügbar:  
  
-   Das Feld **Aktualisierungsintervall (in Sekunden)** zeigt die Anzahl der Sekunden an, bei der das Dashboard aktualisiert wird. Der Standardwert ist 30. Wenn die automatische Aktualisierung aktiviert ist, können Sie dieses Feld bearbeiten, um das Aktualisierungsintervall zu ändern.  
  
-   Die **Anzahl der Verbindungswiederholungen** zeigt an, wie oft das Dashboard versucht, eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herzustellen, die ein Verfügbarkeitsreplikat für eine Verfügbarkeitsgruppe hostet, die das Dashboard überwacht. Der Standardwert ist "65535". Wenn die automatische Aktualisierung aktiviert ist, können Sie dieses Feld bearbeiten, um die Anzahl der Verbindungswiederholungen zu ändern.  
  
 **Aktivieren Sie die benutzerdefinierte Always On-Richtlinie.**  
 Wenn Sie eine eigene Always On-Richtlinie definiert haben, klicken Sie auf diese Option, um die Richtlinie zu aktivieren.  
  
## Siehe auch  
 [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  