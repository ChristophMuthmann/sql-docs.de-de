---
title: "Aktuelle &#196;nderungen in SQL Server Reporting Services in SQL Server 2016 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verweise auf Me.Value"
  - "Reporting Services, Abwärtskompatibilität"
  - "Wichtige Änderungen [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# Aktuelle &#196;nderungen in SQL Server Reporting Services in SQL Server 2016
  In diesem Thema werden wichtige Änderungen in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]beschrieben. Diese Änderungen können u. U. zur Funktionsunfähigkeit von Anwendungen, Skripts oder Funktionen führen, die auf früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] basieren. Diese Probleme können nach einem Upgrade oder in benutzerdefinierten Skripts oder Berichten auftreten.  
  
  ## Sicherheitserweiterungen
  
  Benutzerdefinierte Sicherheitserweiterungen erfordern einige Änderungen, damit sie mit dem neuen [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] funktionieren. Sicherheitserweiterungen müssen die IAuthenticationExtension2-Schnittstelle verwenden.
  
  ## WMI-Anbieter
  
  Der Name der [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]-Anwendung ändert sich von „ReportManager“ in „ReportServerWebApp“.
  
## Siehe auch  
 [Verhaltensänderungen in SQL Server Reporting Services in SQL Server 2016](http://msdn.microsoft.com/de-de/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Neues bei Reporting Services &#40;SSRS&#41;](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [Als veraltet markierte Features in SQL Server Reporting Services in SQL Server 2016](http://msdn.microsoft.com/de-de/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [Nicht mehr unterstützte Features in SQL Server Reporting Services in SQL Server 2016](http://msdn.microsoft.com/de-de/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  