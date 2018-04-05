---
title: Bewährte Methoden für die Ausnahmebehandlung in Reporting Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e6ae230c7d3e21ad4b5ac19ab791f63db8d51c50
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Bewährte Methoden für die Ausnahmebehandlung in Reporting Services
  Wenn Sie [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Anwendungen entwickeln, können Sie verschiedene Methoden verwenden, um das Auftreten von Ausnahmezuständen zu verhindern oder zu reduzieren. Wenn Ausnahmen auftreten, sorgen Sie für klare und prägnante Fehlermeldungen, und fügen Sie eine adäquate Behandlung der Ausnahme hinzu, um unerwartete Abbrüche Ihrer Anwendungen zu verhindern.  
  
 Eine Anwendung, die Anforderungen an den Berichtsserver-Webdienst sendet, sollte wie folgt vorgehen:  
  
-   Keine Ausnahmen verursachen, indem möglichst viele ungültige Anforderungen verhindert werden.  
  
-   Abfangen von Ausnahmen und Angabe eines spezifischen Fehlerbehandlungscodes, wenn möglich.  
  
-   Behandlung von Fehlerfällen, die keine Ausnahmen auslösen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Preventing Invalid Requests (Verhindern von ungültigen Anforderungen)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|Beschreibt Techniken, mit denen verhindert wird, dass ungültige Anforderungen zum Berichtsserver gesendet werden.|  
|[Using Try and Catch Blocks (Verwenden von Try- und Catch-Blöcken)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|Beschreibt, wie die Zuverlässigkeit Ihrer Anwendung mithilfe von try/catch-Blöcken weiter verbessert wird.|  
|[Handling Warnings and Cases That Do Not Cause Exceptions (Behandeln von Warnungen und Fällen, die keine Ausnahmen verursachen)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|Erklärt, wie Fehler behandelt werden, die nicht zu einer Ausnahme führen, die von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ausgelöst wird.|  
|[Using the Detail Property to Handle Specific Errors (Verwenden der Detail-Eigenschaft zur Handhabung bestimmter Fehler)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|Erklärt, wie bestimmte Fehler programmgesteuert mit der **Detail**-Eigenschaft des **SoapException**-Objekts behandelt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Detail-Eigenschaft](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException Class (Reporting Services-SoapException-Klasse)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
