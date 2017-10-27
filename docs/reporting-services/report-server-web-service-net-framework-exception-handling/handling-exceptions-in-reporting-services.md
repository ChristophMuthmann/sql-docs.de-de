---
title: Behandeln von Ausnahmen in Reporting Services | Microsoft Docs
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
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 7e1472c11575ba8bed99992ec9630e408c347291
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>Behandeln von Ausnahmen in Reporting Services
  Wenn eine Anforderung auf den Reporting Services-SOAP-API-Client nicht durchgeführt werden kann, gibt der Berichtsserver eine Fehlermeldung statt der erwarteten Ergebnisse des Aufrufs aus. Wenn ein Aufruf abgeschlossen werden kann, wird ein Fehler für die Berichtsserver-Webdienst zurückgegeben, als ein SOAP- **Fehler** XML-Element. Das wichtigste Beschreibungselement des Fehlers ist der **Detail** -Element, das alle von der Fehlerinformationen von der Berichtsserver als auch für jede weitere Fehlerdaten des Webdiensts enthält. Die wichtigsten Informationen in den **Detail** Element ist der Fehlercode für den Berichtsserver. Auf der Grundlage der Meldung und des Fehlercodes können Sie bestimmen, welche Aktion als Nächstes in Ihren Anwendungen vorgenommen werden muss. Weitere Informationen zu SOAP-Fehlern finden Sie im World Wide Web Consortium (W3C) auf der Website unter (http://www.w3.org/TR/SOAP).  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP-Fehler und das .NET Framework  
 In der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], wenn ein Fehler in einer Clientanforderung an den Webdienst auftritt, kommuniziert der Berichtsserver den Fehler an den Clientcode, der den Webdienst, durch Auslösen aufruft einer **SoapException** Objekt. Die **SoapException** dient als Wrapper für die Informationen in einen SOAP-Fehler. Die **Detail** Eigenschaft von der **SoapException** ordnet die **Detail** Element in der SOAP-Fehler. Fangen Anwendungen sollten die **SoapException** Objekt mit einem Try/Catch-Block, und verwenden Sie die **Detail** Eigenschaft von der **SoapException** geeignete Aktion ausführen. Weitere Informationen zu den **SoapException** Klasse und die **Detail** Eigenschaft im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], finden Sie unter [Reporting Services-SoapException-Klasse](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Weitere Informationen zu den **SoapException** Klasse, finden Sie unter der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Detail-Eigenschaft](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Einführung in die Ausnahmebehandlung in Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services-SoapException-Klasse](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  

