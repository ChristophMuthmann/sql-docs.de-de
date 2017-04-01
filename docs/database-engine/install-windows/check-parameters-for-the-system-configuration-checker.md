---
title: "&#220;berpr&#252;fen der Parameter f&#252;r die Systemkonfigurationspr&#252;fung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Installieren von SQL Server, Systemkonfigurationsprüfungen"
  - "Fehler bei Systemkonfigurationsüberprüfungen [SQL Server]"
  - "Prüfen der Konfiguration vor der Installation"
  - "SCC [SQL Server]"
  - "Systemkonfigurationsprüfung"
  - "Scannen des Computers vor der Installation [SQL Server]"
  - "Überprüfen der Konfiguration vor der Installation"
  - "Statusinformationen [SQL Server], Systemkonfigurationsprüfung"
  - "Parameter [SQL Server], Systemkonfigurationsprüfung"
  - "Konfigurationsprüfungen [SQL Server]"
  - "Setup [SQL Server], Systemkonfigurationsprüfung"
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 46
---
# &#220;berpr&#252;fen der Parameter f&#252;r die Systemkonfigurationspr&#252;fung
  Während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durchsucht die Systemkonfigurationsprüfung (System Configuration Checker, SCC) den Computer, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert werden soll. Die SCC sucht nach Bedingungen, die eine erfolgreiche Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verhindern. Bevor Setup den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installations-Assistenten startet, ruft SCC den Status jedes Elements ab. SCC vergleicht dann das Ergebnis mit den erforderlichen Bedingungen und gibt Anweisungen zum Entfernen der Blockierungsprobleme.  
  
 Die Systemkonfigurationsprüfung generiert einen Bericht, der eine kurze Beschreibung für jede ausgeführte Regel sowie den Ausführungsstatus enthält. Der Bericht der Systemkonfigurationsprüfung befindet sich in „%programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<JJJJMMTT_hhmm>\\.  
  
## Siehe auch  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  