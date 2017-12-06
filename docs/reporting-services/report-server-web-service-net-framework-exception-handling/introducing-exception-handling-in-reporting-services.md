---
title: "Einführung der Ausnahmebehandlung in Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
caps.latest.revision: "29"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3e2d23525b74dbfeeea7d65262237b52e305772f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Einführung in die Ausnahmebehandlung in Reporting Services
  Wenn die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Anwendung die Anforderung an den Berichtsserver-Webdienst sendet, dass der Dienst die Verarbeitung nicht durchführen kann, gibt der Dienst eine SOAP-Ausnahme an den Client zurück. Die Behandlung von Ausnahmen, die vom Berichtsserver-Webdienst ausgelöst werden, stellt einen wichtigen Teil der Anwendungen dar, die Sie entwickeln, da Sie damit sinnvolle Informationen an die Benutzer zurückgeben können, wenn ein Fehler auftritt.  
  
 Dieser Abschnitt enthält spezielle Informationen zur Ausnahmebehandlung, damit ungültige Benutzereingaben verhindert und sinnvolle Fehlermeldungen an die Benutzer ausgegeben werden. Allgemeine Informationen über die Ausnahmebehandlung finden Sie in „Behandeln und Auslösen von Ausnahmen“ in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Handling Exceptions in Reporting Services (Behandeln von Ausnahmen in Reporting Services)](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|Bietet eine Übersicht der Ausnahmen in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und die Rolle von SOAP, wenn Fehler von einem Webdienst zurückgegeben werden.|  
|[Best Practices for Reporting Services Exception Handling (Bewährte Methoden für die Ausnahmebehandlung in Reporting Services)](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|Gibt Empfehlungen darüber, wie Ausnahmen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] behandelt werden sollten.|  
|[Reporting Services SoapException Class (Reporting Services-SoapException-Klasse)](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|Beschreibt die **SoapException**-Klasse in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Siehe auch  
 [Building Applications Using the Web Service and the .NET Framework (Erstellen von Anwendungen mit dem Webdienst und .NET Framework)](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
