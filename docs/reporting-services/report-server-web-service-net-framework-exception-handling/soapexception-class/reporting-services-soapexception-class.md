---
title: SoapException-Klasse von Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: "33"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7546e48cca2920665f7d31bdafcc81e863d544c3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="reporting-services-soapexception-class"></a>Reporting Services-SoapException-Klasse
  Sie sollten bestimmte [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Fehler angeben, die erfahrungsgemäß auftreten können. In einer Anwendung, in der Sie den Benutzer auffordern, einen Ordner zu erstellen, kann es beispielsweise passieren, dass der Benutzer einen Ordner erstellen möchte, der bereits vorhanden ist. Als Entwickler können Sie nicht steuern, welchen Ordnernamen und welches Verzeichnis der Benutzer in der Anwendung angibt. Allerdings können Sie steuern, was passieren soll, wenn jemand ein Element erstellen möchte, das bereits vorhanden ist.  
  
 Um bestimmte Fehlerbedingungen leichter zu erfassen, klassifiziert [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] einen Fehlercode für die Ausnahme und gibt die Fehlerklassifizierung mithilfe der Eigenschaften aus der **SoapException**-Klasse zurück. Weitere Informationen finden Sie unter „SoapException-Klasse“ in der Dokumentation zum [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK.  
  
 In der folgenden Tabelle sind die öffentlichen Eigenschaften der **SoapException**-Klasse aufgeführt.  
  
|Öffentliche Eigenschaft|Description|  
|---------------------|-----------------|  
|**Actor**|Der Code, der die Ausnahme verursacht hat. Der Wert ist die URL der Webdienstmethode.|  
|**Detail**|Anwendungsspezifische Fehlerinformationen. Der Wert wird vom Berichtsserver festgelegt und ist im XML-Format. Weitere Informationen finden Sie unter [Detail-Eigenschaft](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) und [Verwenden der Detail-Eigenschaft zur Handhabung bestimmter Fehler](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Eine URL oder eine URN zu einer zum Fehler gehörigen Hilfedatei. Der Wert wird normalerweise durch einen Webdienst festgelegt, und er richtet eine URL zu [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Hilfe und Support ein. Da [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] mehrere HelpLinks für auftretende Fehler unterstützt, richtet der Berichtsserver die HelpLink-Informationen als Teil der **Detail**-Eigenschaft ein. Weitere Informationen finden Sie unter [HelpLink-Element](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).|  
|**MessageBox**|Eine informative, lokalisierte Meldung, die den Fehler beschreibt. Dieser Text kann in der Benutzeroberfläche der Anwendung angezeigt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException Errors Table (Tabelle für SoapException-Fehler)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
