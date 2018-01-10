---
title: "Webdienst für Berichtsserver | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: "47"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9d3da908870f8aac0d56217514625e055ae24d27
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-server-web-service"></a>Report Server-Webdienst
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt über den Berichtsserver-Webdienst den Zugriff auf die kompletten Funktionen des Berichtsservers bereit. Der Berichtsserver-Webdienst stellt einen XML-Webdienst mit einer SOAP-API dar. Er verwendet SOAP über HTTP und agiert als Kommunikationsschnittstelle zwischen den Clientprogrammen und dem Berichtsserver. Der Webdienst versieht zwei Endpunkte (einen für die Berichtsausführung und einen für die Berichtsverwaltung) mit Methoden, anhand derer die Funktionen des Berichtsservers zugänglich gemacht werden und die Ihnen die Erstellung benutzerdefinierter Tools für jeden Teil des gesamten Berichtslebenszyklus ermöglichen.  
  
 Es gibt drei Hauptmöglichkeiten, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Anwendungen auf Grundlage des Webdiensts zu entwickeln. Folgende Aktionen sind möglich:  
  
-   Entwickeln Sie Anwendungen mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] und dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Weitere Informationen zur Verwendung von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] zur Erstellung von Webdienstanwendungen finden Sie unter [Building Applications Using the Web Service and the .NET Framework (Erstellen von Anwendungen mit dem Webdienst und .NET Framework)](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Entwickeln Sie Anwendungen mit dem **RS**-Hilfsprogramm (RS.exe) und der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Skriptumgebung. Mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]- und [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Skripts können alle Vorgänge des Berichtsserver-Webdiensts ausgeführt werden. Weitere Informationen zur Skripterstellung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Skripterstellung mit dem Hilfsprogramm rs.exe und dem Webdienst](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Entwickeln Sie Anwendungen mithilfe von SOAP-aktivierten Entwicklungstools. Weitere Informationen finden Sie unter [The Role of SOAP in Reporting Services (Die Rolle von SOAP in Reporting Services)](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Programmierdiagramm  
 ![Entwicklungsoptionen für den Berichtsserver-Webdienst](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "Report Server Web service development options")  
Reporting Services, verfügbare Webdienstentwicklungsoptionen  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Report Server Web Service Methods (Webdienstmethoden für Berichtsserver)](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 Beschreibt die Funktionen und Methoden jedes Berichtsserver-Webdiensts.  
  
 [The Role of SOAP in Reporting Services (Die Rolle von SOAP in Reporting Services)](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Bietet eine Übersicht über SOAP und erläutert die Verwendung in den Berichtsserver-Webdiensten.  
  
 [Accessing the SOAP API (Accessing the SOAP API)](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 Beschreibt die Webdienstbeschreibungssprache (WSDL) und stellt URLs bereit, mit denen auf eine Reporting Services-WSDL-Datei zugegriffen werden kann.  
  
 [Building Applications Using the Web Service and the .NET Framework (Erstellen von Anwendungen mit dem Webdienst und .NET Framework)](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Enthält Informationen über die Entwicklung von Anwendungen und Webdiensten, die die Reporting Services-SOAP-API aufrufen.  
  
 [Script with the rs.exe Utility and the Web Service (Skripterstellung mit dem Hilfsprogramm rs.exe und dem Webdienst)](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Enthält eine Übersicht über die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Skriptumgebung.  
  
 [Technische Referenz (SSRS)](../../reporting-services/technical-reference-ssrs.md)  
 Enthält Referenzmaterial, das speziell für die Methoden des Berichtsserver-Webdiensts und die entsprechenden komplexen Typen bestimmt ist.  
  
## <a name="user-requirements-for-web-service-development"></a>Benutzeranforderungen für Webdienstentwicklung  
 Um Anwendungen mithilfe des Berichtserver-Webdiensts zu entwickeln, benötigen Sie:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 oder eine spätere Version auf Ihrem Computer, einen Internetanschluss und Zugriff auf den Berichtsserver.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK auf Ihrem Computer, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Anwendungen mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] entwickeln und bereitstellen möchten.  
  
-   Sehr gute Kenntnisse der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Funktionen und -Möglichkeiten.  
  
-   Sehr gute Kenntnisse von SOAP und [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Entwicklungserfahrung in einer [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-kompatiblen Sprache wie z.B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], wenn Sie [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] als Entwicklungsplattform verwenden möchten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Report Server Web Service (Report Server-Webdienst)](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
