---
title: Integrieren von Reporting Services-in Anwendungen | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
caps.latest.revision: 57
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8a1cabc088c7c0ec6c69c8290549e035a4cec7bb
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="integrating-reporting-services-into-applications"></a>Integration von Reporting Services in Anwendungen
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt eine offene und erweiterbare Berichtsplattform dar, die Entwicklern eine umfangreiche Reihe von APIs zur Entwicklung von Lösungen zur Verfügung stellt.  
  
 Es gibt drei Möglichkeiten für die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in benutzerdefinierte Anwendungen: den Berichtsserver-Webdienst, auch bekannt als die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP-API, die ReportViewer-Steuerelemente für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)], und URL-Zugriff. Jede Option hat einen anderen Ansatz zur Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in die Anwendungen.  
  
## <a name="report-server-web-service"></a>Report Server-Webdienst  
 Der Berichtsserver-Webdienst stellt die primäre Schnittstelle zum Entwickeln für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dar. Unabhängig davon, ob Sie Code zur Verwaltung Ihres Berichtskatalogs oder Code zum Rendern von Berichten in einem unterstützten Format entwickeln, verfügt der Webdienst über alle notwendigen Methoden, um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihre Anwendungen zu integrieren. Ein Beispiel für eine solche Anwendung ist Berichts-Manager enthaltene [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; er den Webdienst verwendet, um die Berichtsserver-Datenbank zu verwalten.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>ReportViewer-Steuerelemente für Visual Studio  
 Mit den in [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] enthaltenen ReportViewer-Steuerelementen können Berichtsanzeigen in Ihre Anwendungen integriert werden. Es gibt zwei Steuerelemente: eines für Windows Forms-Anwendungen und eines für WebForms-Anwendungen. Jedes Steuerelement verfügt über die Möglichkeit zur Anzeige von Berichten, die auf einem Berichtsserver bereitgestellt wurden, sowie zum Rendern von Berichten, die in einer Umgebung vorliegen, in der kein Berichtsserver installiert ist.  
  
## <a name="url-access"></a>URL-Zugriff  
 Der URL-Zugriff ist eine weitere Option für die Integration der Berichtsanzeige in Ihren Anwendungen, wenn die ReportViewer-Steuerelemente nicht zur Verfügung stehen. Darüber hinaus ist der URL-Zugriff hilfreich, wenn Links zu Berichten per E-Mail an Benutzer gesendet werden sollen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Integrating Reporting Services Using SOAP (Integrieren von Reporting Services mit SOAP)](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation und -verwaltung mithilfe des Berichtsserver-Webdiensts in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
 [Integrieren von Reporting Services, die mit den ReportViewer-Steuerelementen](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Beschreibt, wie Sie die Berichtsanzeige mithilfe der ReportViewer-Steuerelemente in Ihre vorhandenen Anwendungen integrieren.  
  
 [Integrating Reporting Services Using URL Access (Integrieren von Reporting Services mit URL-Zugriff)](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Beschreibt, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigation mithilfe des URL-Zugriffs in Ihre vorhandenen Geschäftsanwendungen integrieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichts-Manager &#40; SSRS im einheitlichen Modus &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Entscheidung zwischen URL-Zugriff und SOAP](../../reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [Technische Referenz &#40; SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)   
 [Berichtsserver-Webdienst](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
