---
title: "Sicherheitsanforderungen für das Verwalten von Diensten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
caps.latest.revision: "28"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c55fe304fa1217149f90f83b2b111eb257690fa2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="security-requirements-for-managing-services"></a>Sicherheitsanforderungen für das Verwalten von Diensten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Um den [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst zu verwalten, verwenden Sie entweder den SQL Server-Konfigurations-Manager oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Auf gruppierten Servern verwalten Sie die Dienste mit der Clusterverwaltung.  
  
 Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst zu verwalten und die Konfigurationsoptionen für den Server festzulegen, müssen Sie Mitglied der festen Serverrolle **serveradmin** oder der festen Serverrolle **sysadmin** sein. Mitglieder der Windows-Gruppe **Administratoren** können Dienste starten und beenden und die unter Windows verfügbaren Serveroptionen konfigurieren.  
  
> [!NOTE]  
>  Um eine ordnungsgemäße Funktionsweise sicherzustellen, müssen die für die Dienste verwendeten Konten mit der richtigen Domäne, dem richtigen Dateisystem und den richtigen Registrierungsberechtigungen konfiguriert werden. Weitere Informationen zu erforderlichen Berechtigungen finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="windows-management-instrumentation"></a>Windows-Verwaltungsinstrumentation  
 Der SQL Server-Konfigurations-Manager und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden zum Anzeigen und Bearbeiten einiger Servereigenschaften die Windows-Verwaltungsinstrumentation (WMI, Windows Management Instrumentation). Um Dienste zu verwalten und den Status der Dienste abzufragen, muss der Benutzer über eine Zugriffsberechtigung für das WMI-Objekt verfügen. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]wird die WMI auf den folgenden Servereigenschaftenseiten verwendet:  
  
-   Dienste automatisch starten  
  
-   Startparameter  
  
-   Security  
  
-   Sonstige Servereinstellungen  
  
## <a name="related-tasks"></a>Related Tasks  
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Konzepte des WMI-Anbieters für die Konfigurationsverwaltung](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
