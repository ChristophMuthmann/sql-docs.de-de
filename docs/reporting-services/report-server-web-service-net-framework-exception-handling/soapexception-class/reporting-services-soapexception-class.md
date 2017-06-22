---
title: Reporting Services-SoapException-Klasse | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3b19743906654dfcbfe6289181ae62b43a2df143
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="reporting-services-soapexception-class"></a>Reporting Services-SoapException-Klasse
  Sie sollten bestimmte [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Fehler angeben, die erfahrungsgemäß auftreten können. In einer Anwendung, in der Sie den Benutzer auffordern, einen Ordner zu erstellen, kann es beispielsweise passieren, dass der Benutzer einen Ordner erstellen möchte, der bereits vorhanden ist. Als Entwickler können Sie nicht steuern, welchen Ordnernamen und welches Verzeichnis der Benutzer in der Anwendung angibt. Allerdings können Sie steuern, was passieren soll, wenn jemand ein Element erstellen möchte, das bereits vorhanden ist.  
  
 Für die Sie zum Abfangen von bestimmten fehlerbedingungen, erleichtern [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] klassifiziert einen Fehlercode für die Ausnahme und gibt die Klassifizierung des Fehlers mithilfe der Eigenschaften aus den **SoapException** Klasse. Weitere Informationen finden Sie unter "SoapException-Klasse" in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
 Die folgende Tabelle enthält die öffentlichen Eigenschaften der **SoapException** Klasse.  
  
|Öffentliche Eigenschaft|Description|  
|---------------------|-----------------|  
|**Akteur**|Der Code, der die Ausnahme verursacht hat. Der Wert ist die URL der Webdienstmethode.|  
|**Detail**|Anwendungsspezifische Fehlerinformationen. Der Wert wird vom Berichtsserver festgelegt und ist im XML-Format. Weitere Informationen finden Sie unter [Detaileigenschaft](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) und [mithilfe der Detail-Eigenschaft auf bestimmte Fehler behandeln](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Eine URL oder eine URN zu einer zum Fehler gehörigen Hilfedatei. Der Wert wird normalerweise durch einen Webdienst festgelegt, und er richtet eine URL zu [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Hilfe und Support ein. Da [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] unterstützt mehrere helplinks für auftretende Fehler der Berichtsserver, HelpLink-Informationen als Teil der **Detail** Eigenschaft. Weitere Informationen finden Sie unter [HelpLink-Element](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).|  
|**MessageBox**|Eine informative, lokalisierte Meldung, die den Fehler beschreibt. Dieser Text kann in der Benutzeroberfläche der Anwendung angezeigt werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Einführung in die Ausnahmebehandlung in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Tabelle für SoapException-Fehler](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
