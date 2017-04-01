---
title: "Sicherheitsanforderungen f&#252;r das Verwalten von Diensten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server-Agent-Dienst, Sicherheit"
  - "Dienste [SQL Server], Sicherheit"
  - "SQL Server-Dienste, Sicherheit"
  - "WMI-Anbieter [SQL Server]"
  - "Serverkonfiguration [SQL Server]"
  - "Sicherheit [SQL Server], Dienste"
  - "Dienste [SQL Server], WMI"
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Sicherheitsanforderungen f&#252;r das Verwalten von Diensten
  Um den [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst zu verwalten, verwenden Sie entweder den SQL Server-Konfigurations-Manager oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Auf gruppierten Servern verwalten Sie die Dienste mit der Clusterverwaltung.  
  
 Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst zu verwalten und die Konfigurationsoptionen für den Server festzulegen, müssen Sie Mitglied der festen Serverrolle **serveradmin** oder der festen Serverrolle **sysadmin** sein. Mitglieder der Windows-Gruppe **Administratoren** können Dienste starten und beenden und die unter Windows verfügbaren Serveroptionen konfigurieren.  
  
> [!NOTE]  
>  Um eine ordnungsgemäße Funktionsweise sicherzustellen, müssen die für die Dienste verwendeten Konten mit der richtigen Domäne, dem richtigen Dateisystem und den richtigen Registrierungsberechtigungen konfiguriert werden. Weitere Informationen zu erforderlichen Berechtigungen finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## Windows-Verwaltungsinstrumentation  
 Der SQL Server-Konfigurations-Manager und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden zum Anzeigen und Bearbeiten einiger Servereigenschaften die Windows-Verwaltungsinstrumentation (WMI, Windows Management Instrumentation). Um Dienste zu verwalten und den Status der Dienste abzufragen, muss der Benutzer über eine Zugriffsberechtigung für das WMI-Objekt verfügen. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]wird die WMI auf den folgenden Servereigenschaftenseiten verwendet:  
  
-   Dienste automatisch starten  
  
-   Startparameter  
  
-   Sicherheit  
  
-   Sonstige Servereinstellungen  
  
## Verwandte Aufgaben  
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
## Verwandte Inhalte  
 [Konzepte des WMI-Anbieters für die Konfigurationsverwaltung](../Topic/WMI%20Provider%20for%20Configuration%20Management%20Concepts.md)  
  
  