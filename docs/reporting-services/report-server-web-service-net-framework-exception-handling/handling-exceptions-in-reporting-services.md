---
title: Behandeln von Ausnahmen in Reporting Services | Microsoft-Dokumentation
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
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 40b238f118a957a86f7fb0791d9a6012cc150ff6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="handling-exceptions-in-reporting-services"></a>Behandeln von Ausnahmen in Reporting Services
  Wenn eine Anforderung auf den Reporting Services-SOAP-API-Client nicht durchgeführt werden kann, gibt der Berichtsserver eine Fehlermeldung statt der erwarteten Ergebnisse des Aufrufs aus. Wenn ein Aufruf nicht durchgeführt werden kann, wird eine Fehlermeldung für den Berichtsserver-Webdienst als ein SOAP-**Fault**-XML-Element zurückgegeben. Das wichtigste Beschreibungselement des Fehlers ist das **detail**-Element, das alle vom Berichtsserver gelieferten Fehlerdaten sowie weitere Fehlerdaten des Webdiensts enthält. Die wichtigste Information im **detail**-Element ist der Fehlercode des Berichtsservers. Auf der Grundlage der Meldung und des Fehlercodes können Sie bestimmen, welche Aktion als Nächstes in Ihren Anwendungen vorgenommen werden muss. Weitere Informationen zu SOAP-Fehlern finden Sie im World Wide Web Consortium (W3C) auf der Website unter (http://www.w3.org/TR/SOAP).  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP-Fehler und das .NET Framework  
 Falls in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ein Fehler in einer Clientanforderung an einen Webdienst auftritt, kommuniziert der Berichtsserver den Fehler an den Clientcode, der den Webdienst aufruft, indem er ein **SoapException**-Objekt auslöst. Die **SoapException** umbricht die in einem SOAP-Fehler enthaltenen Informationen in die nächste Zeile. Die **Detail**-Eigenschaft in der **SoapException** entspricht dem **detail**-Element im SOAP-Fehler. Anwendungen sollten das **SoapException**-Objekt mit einem try/catch-Block erfassen und die **Detail**-Eigenschaft der **SoapException** verwenden, um die entsprechende Aktion vorzunehmen. Weitere Informationen zur **SoapException**-Klasse und der **Detail**-Eigenschaft in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [SoapException-Klasse von Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Weitere Informationen zur **SoapException**-Klasse finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Detail-Eigenschaft](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException Class (Reporting Services-SoapException-Klasse)](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
