---
title: Integration von Reporting Services in Anwendungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 39e601d5e3adab3bf94da6f5d3fc7ba8a81d6b0c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="integrating-reporting-services-into-applications"></a>Integration von Reporting Services in Anwendungen

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt eine offene und erweiterbare Berichtsplattform dar, die Entwicklern eine umfangreiche Reihe von APIs zur Entwicklung von Lösungen zur Verfügung stellt.

> [!NOTE]
> Ab SQL Server 2017 Reporting Services ist der Zugriff auf die REST-API für die Entwicklung von Lösungen verfügbar. Der Zugriff auf die SOAP-API ist veraltet. Weitere Informationen finden Sie unter [Develop with the REST APIs for Reporting Services (Entwickeln mit den REST-APIs für Reporting Services)](../developer/rest-api.md).
  
 Es gibt drei Möglichkeiten für die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in benutzerdefinierte Anwendungen: den Berichtsserver-Webdienst, auch als [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-SOAP-API bezeichnet, die ReportViewer-Steuerelemente für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] und den URL-Zugriff. Jede Option hat einen anderen Ansatz zur Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in die Anwendungen.
  
## <a name="report-server-web-service"></a>Berichtsserver-Webdienst

 Der Berichtsserver-Webdienst stellt die primäre Schnittstelle zum Entwickeln für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dar. Unabhängig davon, ob Sie Code zur Verwaltung Ihres Berichtskatalogs oder Code zum Rendern von Berichten in einem unterstützten Format entwickeln, verfügt der Webdienst über alle notwendigen Methoden, um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihre Anwendungen zu integrieren. Ein Beispiel für eine solche Anwendung ist der Berichts-Manager, der in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthalten ist. Er verwaltet die Berichtsserver-Datenbank mithilfe des Webdiensts.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>ReportViewer-Steuerelemente für Visual Studio

 Mit den für [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] verfügbaren ReportViewer-Steuerelementen können Berichtsanzeigen in Ihre Anwendungen integriert werden. Es gibt zwei Steuerelemente: eines für Windows Forms-Anwendungen und eines für WebForms-Anwendungen. Jedes Steuerelement verfügt über die Möglichkeit zur Anzeige von Berichten, die auf einem Berichtsserver bereitgestellt wurden, sowie zum Rendern von Berichten, die in einer Umgebung vorliegen, in der kein Berichtsserver installiert ist.  
  
## <a name="url-access"></a>URL-Zugriff  
 Der URL-Zugriff ist eine weitere Option für die Integration der Berichtsanzeige in Ihren Anwendungen, wenn die ReportViewer-Steuerelemente nicht zur Verfügung stehen. Darüber hinaus ist der URL-Zugriff hilfreich, wenn Links zu Berichten per E-Mail an Benutzer gesendet werden sollen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt

 [Integrating Reporting Services Using SOAP (Integrieren von Reporting Services mit SOAP)](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation und -verwaltung mithilfe des Berichtsserver-Webdiensts in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
 [Integrieren von Reporting Services mithilfe der ReportViewer-Steuerelemente](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Beschreibt, wie Sie die Berichtsanzeige mithilfe der ReportViewer-Steuerelemente in Ihre vorhandenen Anwendungen integrieren.  
  
 [Integrating Reporting Services Using URL Access (Integrieren von Reporting Services mit URL-Zugriff)](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation mithilfe des URL-Zugriffs in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
## <a name="next-steps"></a>Nächste Schritte

Für weitere Informationen zur Entscheidung, ob der URL-Zugriff oder die SOAP-API verwendet wird, finden Sie unter [Entscheidung zwischen URL-Zugriff und SOAP in Reporting Services](choosing-between-url-access-and-soap.md).

Weitere Informationen zur REST API für SQL Server 2017 Reporting Services finden Sie unter [Develop with the REST APIs for Reporting Services (Entwickeln mit den REST-APIs für Reporting Services)](../developer/rest-api.md).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
