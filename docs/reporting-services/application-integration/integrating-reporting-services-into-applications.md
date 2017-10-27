---
title: Integrieren von Reporting Services-in Anwendungen | Microsoft Docs
ms.custom: 
ms.date: 10/19/2017
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
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 26e1da5a720aab965d014cada16f85086e0f70a0
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="integrating-reporting-services-into-applications"></a>Integration von Reporting Services in Anwendungen

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt eine offene und erweiterbare Berichtsplattform dar, die Entwicklern eine umfangreiche Reihe von APIs zur Entwicklung von Lösungen zur Verfügung stellt.

> [!NOTE]
> Beginnend mit SQL Server 2017 Reporting Services, ist die REST-API-Zugriff für die Entwicklung von Lösungen zur Verfügung. SOAP-API-Zugriff wurde als veraltet markiert. Weitere Informationen finden Sie unter [entwickeln Sie mit der REST-APIs für Reporting Services](../developer/rest-api.md).
  
 Es gibt drei Möglichkeiten für die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in benutzerdefinierte Anwendungen: den Berichtsserver-Webdienst, auch bekannt als die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP-API, die ReportViewer-Steuerelemente für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], und URL-Zugriff. Jede Option hat einen anderen Ansatz zur Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in die Anwendungen.
  
## <a name="report-server-web-service"></a>Berichtsserver-Webdienst

 Der Berichtsserver-Webdienst stellt die primäre Schnittstelle zum Entwickeln für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dar. Unabhängig davon, ob Sie Code zur Verwaltung Ihres Berichtskatalogs oder Code zum Rendern von Berichten in einem unterstützten Format entwickeln, verfügt der Webdienst über alle notwendigen Methoden, um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihre Anwendungen zu integrieren. Ein Beispiel für eine solche Anwendung ist Berichts-Manager enthaltene [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; er den Webdienst verwendet, um die Berichtsserver-Datenbank zu verwalten.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>ReportViewer-Steuerelemente für Visual Studio

 Die ReportViewer-Steuerelemente zur [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] für die Integration der Berichtsanzeige in Ihren Anwendungen verwendet werden. Es gibt zwei Steuerelemente: eines für Windows Forms-Anwendungen und eines für WebForms-Anwendungen. Jedes Steuerelement verfügt über die Möglichkeit zur Anzeige von Berichten, die auf einem Berichtsserver bereitgestellt wurden, sowie zum Rendern von Berichten, die in einer Umgebung vorliegen, in der kein Berichtsserver installiert ist.  
  
## <a name="url-access"></a>URL-Zugriff  
 Der URL-Zugriff ist eine weitere Option für die Integration der Berichtsanzeige in Ihren Anwendungen, wenn die ReportViewer-Steuerelemente nicht zur Verfügung stehen. Darüber hinaus ist der URL-Zugriff hilfreich, wenn Links zu Berichten per E-Mail an Benutzer gesendet werden sollen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt

 [Integrating Reporting Services Using SOAP (Integrieren von Reporting Services mit SOAP)](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation und -verwaltung mithilfe des Berichtsserver-Webdiensts in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
 [Integrieren von Reporting Services, die mit den ReportViewer-Steuerelementen](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Beschreibt, wie Sie die Berichtsanzeige mithilfe der ReportViewer-Steuerelemente in Ihre vorhandenen Anwendungen integrieren.  
  
 [Integrating Reporting Services Using URL Access (Integrieren von Reporting Services mit URL-Zugriff)](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation mithilfe des URL-Zugriffs in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
## <a name="next-steps"></a>Nächste Schritte

Bei der Entscheidung zur Verwendung von URL-Zugriff oder die SOAP-APIs, finden Sie unter [auswählen zwischen URL-Zugriff und SOAP in Reporting Services](choosing-between-url-access-and-soap.md).

Informationen zur SQL Server 2017 Reporting Services REST-API finden Sie unter [entwickeln Sie mit der REST-APIs für Reporting Services](../developer/rest-api.md).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

