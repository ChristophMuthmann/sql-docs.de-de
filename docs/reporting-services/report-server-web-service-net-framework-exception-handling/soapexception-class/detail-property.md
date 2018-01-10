---
title: Detail-Eigenschaft | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
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
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: "33"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9178a7767e95d39ff380fd79fc72964571a5ddbb
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="detail-property"></a>Detail-Eigenschaft
  Die **Detail**-Eigenschaft der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException**-Klasse verfügt über folgende XML-Struktur:  
  
## <a name="elements"></a>Elemente  
 **Detail**  
 Das Element der obersten Ebene, das alle anderen Fehlerdetailelemente enthält.  
  
 **ErrorCode**  
 Der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-spezifische Fehlercode.  
  
 **HttpStatus**  
 Der HTTP-Statuscode.  
  
 **MessageBox**  
 Die Fehlermeldung und der Fehlercode, die vom Berichtsserver zugewiesen werden.  
  
 **HelpLink**  
 Die HelpLink-URL zu einer Website, unter der weitere Informationen zum Fehler zur Verfügung stehen. Weitere Informationen finden Sie unter [HelpLink-Element](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).  
  
 **LinkID**  
 Die dem Link zugewiesene ID.  
  
 **ProductName**  
 Der Name des Produkts. Der Standardwert ist **Microsoft SQL Server Reporting Services**.  
  
 **ProductVersion**  
 Die Version von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Die maximale Länge beträgt 15 Zeichen. Das Format der Versionsnummer sollte folgendermaßen sein: 8.00.0xxx.00.  
  
 **ProductLocaleId**  
 Die Gebietsschema- oder Sprach-ID der INTL DLL (z.B. 0x41A) der Anwendung.  
  
 **OperatingSystem**  
 Das Betriebssystem, auf dem [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] installiert ist. Gültige Werte sind: **0** für betriebssystemunabhängig, **1** für [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] und **16** für Windows XP.  
  
 **CountryLocaleId**  
 Die Gebietsschema- oder Sprach-ID des Betriebssystems. Der Wert für die französische Version von Windows kann z. B. "0x040c" sein.  
  
 **MoreInformation**  
 Eine XML-Zeichenfolge, die geschachtelte Ausnahmen enthält, die während der Ausführung der Methode aufgetreten sind.  
  
 **Quelle**  
 Ein untergeordnetes Element von **MoreInformation**. Die Ursache des Fehlers.  
  
 **MessageBox**  
 Ein untergeordnetes Element von **MoreInformation**. Die Fehlermeldung einer verschachtelten Ausnahme. Dieses Element enthält XML-Attribute für **ErrorCode** und **HelpLink**.  
  
 **Warnungen**  
 Eine XML-Zeichenfolge, die die von der Berichtsverarbeitung zurückgegebenen Warnungen enthält.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Introducing Exception Handling in Reporting Services (Einführung in die Ausnahmebehandlung in Reporting Services)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException-Klasse von Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Using the Detail Property to Handle Specific Errors (Verwenden der Detail-Eigenschaft zur Handhabung bestimmter Fehler)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
