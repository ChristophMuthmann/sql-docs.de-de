---
title: Integrieren von Reporting Services mit SOAP | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 945209e19c1bb9744c8683c090a3f2a059339542
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-soap"></a>Integrieren von Reporting Services mit SOAP
  Die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-SOAP-API verfügt über mehrere Webdienst-Endpunkte zur Entwicklung von benutzerdefinierten Berichtslösungen. Die Endpunkte lassen sich derzeit in zwei Kategorien unterteilen: Verwaltung und Ausführung. Die Verwaltungsfunktionen werden durch die Endpunkte <xref:ReportService2005>, <xref:ReportService2006> und <xref:ReportService2010> verfügbar gemacht. Mit dem <xref:ReportService2005>-Endpunkt wird ein Berichtsserver verwaltet, der im einheitlichen Modus konfiguriert ist, und mit dem <xref:ReportService2006>-Endpunkt wird ein Berichtsserver verwaltet, der für den integrierten SharePoint-Modus konfiguriert ist. Der <xref:ReportService2010>-Endpunkt führt die Funktionen von <xref:ReportService2005> und <xref:ReportService2006> zusammen und kann einen Berichtsserver verwalten, der entweder für den einheitlichen Modus oder integrierten SharePoint-Modus konfiguriert ist.  
  
> [!NOTE]  
>  Der <xref:ReportService2005>-Endpunkt und der <xref:ReportService2006>-Endpunkt sind in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] als veraltet markiert. Der <xref:ReportService2010>-Endpunkt schließt die Funktionen beider Endpunkte ein und beinhaltet zusätzliche Verwaltungsfunktionen.  
  
 Die Ausführungsfunktion wird durch den <xref:ReportExecution2005>-Endpunkt verfügbar gemacht und wird verwendet, wenn der Berichtsserver im einheitlichen Modus oder im integrierten SharePoint-Modus konfiguriert ist. Folgende Themen zeigen, wie diese Endpunkte für die Entwicklung von Berichtslösungen in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-, SharePoint- und Webanwendungen verwendet werden können.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Verwenden der SOAP-API in einer Windows-Anwendung](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
 Beschreibt, wie Sie die SOAP-API verwenden, um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in eine Windows-Umgebung zu integrieren  
  
 [Verwenden der SOAP-API in einer Webanwendung](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
 Beschreibt, wie Sie die SOAP-API verwenden, um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in eine Webumgebung zu integrieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration von Reporting Services in Anwendungen](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Report Server-Webdienst](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Building Applications Using the Web Service and the .NET Framework (Erstellen von Anwendungen mit dem Webdienst und .NET Framework)](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
