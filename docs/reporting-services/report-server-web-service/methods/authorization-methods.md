---
title: Autorisierungsmethoden | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
caps.latest.revision: 42
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ecd0306fe5a5d65c28045e263865bf749080b756
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="authorization-methods"></a>Autorisierungsmethoden
  Mit diesen Methoden können Sie Tasks, Rollen und Richtlinien auf dem Berichtsserver verwalten.  
  
|Methode|Aktion|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|Fügt der Berichtsserver-Datenbank eine neue Rolle hinzu. Diese Methode = gilt nur für den einheitlichen Modus.|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|Löscht eine Rolle aus der Berichtsserver-Datenbank. Diese Methode gilt nur für den einheitlichen Modus.|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|Gibt die Benutzerberechtigungen zurück, die einem bestimmten Element in der Berichtsserver-Datenbank oder SharePoint-Bibliothek zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|Gibt die Richtlinien zurück, die einem bestimmten Element in der Berichtsserver-Datenbank oder SharePoint-Bibliothek zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|Gibt die Eigenschaften von Rollenmetadaten und eine Auflistung zugehöriger Tasks zurück.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|Gibt die Systemberechtigungen des Benutzers zurück. Diese Methode gilt nur für den einheitlichen Modus.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|Gibt die Systemrichtlinien zurück, einschließlich der Gruppen und Rollen, denen sie zugeordnet sind. Diese Methode gilt nur für den einheitlichen Modus.|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|Löscht die Richtlinien, die einem bestimmten Element in der Berichtsserver-Datenbank zugeordnet sind, und setzt die Sicherheitsrichtlinien für das Element auf die Werte des übergeordneten.|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|Gibt einen booleschen Wert zurück, der angibt, ob das Secure Sockets Layer (SSL)-Protokoll zur Verwendung des <xref:ReportService2010>-Endpunkts erforderlich ist.|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|Gibt die Namen und Beschreibungen der Rollen zurück, die vom Berichtsserver verwaltet werden.|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|Gibt eine Liste von SOAP-Methoden (Simple Object Access Protocol) im <xref:ReportExecution2005>-Endpunkt zurück, bei deren Aufruf eine sichere Verbindung erforderlich ist. Die **SecureConnectionLevel** Einstellung des Berichtsservers wird verwendet, um zu bestimmen, welche Methoden zurückgegeben werden.|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|Gibt die Tasks zurück, die vom Berichtsserver verwaltet werden.|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|Legt die Richtlinien fest, die einem angegebenen Element zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|Legt die Eigenschaften der Rollenmetadaten fest und ordnet einer Rolle eine Reihe von Tasks zu. Diese Methode gilt nur für den einheitlichen Modus.|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|Legt die Systemrichtlinie fest, die die Gruppen und ihre zugehörigen Rollen definiert. Diese Methode gilt nur für den einheitlichen Modus.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Webdienstmethoden für Berichtsserver](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Technische Referenz &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
