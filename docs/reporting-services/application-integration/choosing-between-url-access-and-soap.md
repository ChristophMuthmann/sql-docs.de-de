---
title: Entscheidung zwischen URL-Zugriff und SOAP | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- SOAP [Reporting Services], vs. URL access
- Report Server Web service, application integration
- URL access [Reporting Services], vs. SOAP
- Web service [Reporting Services], application integration
ms.assetid: bccdc243-4366-4ce5-8e63-3dd6c463fa52
caps.latest.revision: 40
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6837170f3ebe0e92e7914c3f0f863aa9534e0cb8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="choosing-between-url-access-and-soap"></a>Entscheidung zwischen URL-Zugriff und SOAP
  Die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in benutzerdefinierte Anwendungen ist manchmal nicht ganz einfach. Die Herausforderung liegt jedoch nicht in der Komplexität des Programmiermodells oder in den APIs, sondern in den vielen Möglichkeiten der Integration. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wurde von Grund auf als Entwicklerplattform konzipiert, daher stand die Flexibilität bei der Programmierung immer im Vordergrund. Die hohe Flexibilität fordert jedoch häufige Entscheidungen, wenn die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigations- und Verwaltungsfunktionen in die vorhandenen Geschäftsanwendungen integriert werden.  
  
 ![Reporting Services-Programmierungsszenarien](../../reporting-services/application-integration/media/bk-ext-04.gif "Reporting Services programming scenarios")  
Die Programmierung der Reporting Services unterstützt eine Vielzahl von Szenarien.  
  
 Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf zwei verschiedene Arten in benutzerdefinierte Anwendungen integrieren: über den URL-Zugriff und die Reporting Services-SOAP-API. Welche der beiden Arten verwendet werden soll, hängt von mehreren Faktoren ab. In einigen Fällen müssen für die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in die benutzerdefinierten Anwendungen sowohl URL-Zugriff als auch SOAP verwendet werden. Sie sollten sich folgende Fragen stellen:  
  
-   Welche Art Berichtsfunktionen benötigen Sie oder die Endbenutzer? Brauchen Sie einfache Start- und Navigationsfunktionen für die Berichte, oder benötigen Sie ausgereifte Berichtsserver-Verwaltungsfunktionen aus Ihrer benutzerdefinierten Geschäftsanwendung?  
  
-   In welcher Art Umgebung arbeiten die Benutzer normalerweise? Ist die Geschäftsanwendung eine Webanwendung oder eine Windows-Anwendung? Wie leicht können die Endbenutzer von einer Win32-Umgebung in eine Webumgebung wechseln? Welche Art der Kontrolle benötigen Sie für die Umgebung, in der die Berichte ausgeführt und verwaltet werden?  
  
 Wenn Sie diese Fragen beantwortet haben, können Sie entscheiden, wie Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihre IT-Infrastruktur integrieren. Normalerweise wird der URL-Zugriff für die Anzeige und Navigation der Berichte bevorzugt. Der URL-Zugriff ermöglicht eine rasche Navigation durch die Berichte ohne den Aufwand eines Webdiensts. Außerdem ist der URL-Zugriff derzeit die einzige Programmiertechnik, die die komplette Funktionalität von HTML Viewer, einschließlich der Berichtssymbolleiste, für die Berichtsnavigation verwendet. Darüber hinaus sorgt der URL-Zugriff für eine bessere Leistung als SOAP, da das Marshalling der SOAP-Anforderungen zum Server hin und wieder zurück umgangen wird. In den Integrationsszenarien, in denen rasch und problemlos mit integrierten Anzeige- und Navigationstools auf die Berichte zugegriffen werden muss, ist der URL-Zugriff die bessere Variante.  
  
> [!NOTE]  
>  Der Berichtsserver-URL-Zugriff unterstützt HTML Viewer und die erweiterten Funktionen der Berichtssymbolleiste. Die SOAP-API unterstützt diese Art des gerenderten Berichts nicht. Sie müssen eine eigene Berichtssymbolleiste entwerfen und entwickeln, wenn Sie Berichte mit der SOAP rendern möchten.  
  
 Weitere Informationen zur Berichtssymbolleiste finden Sie unter [HTML-Viewer und die Berichtssymbolleiste](../../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
 Weitere Informationen zum URL-Zugriff finden Sie unter [URL-Zugriff &#40; SSRS &#41; ](../../reporting-services/url-access-ssrs.md).  
  
 Der URL-Zugriff ist sinnvoll für die Anzeige von Berichten, er liefert jedoch nicht die Berichts- und Namespace-Verwaltungsfunktionen, die in bestimmten Unternehmensberichtsszenarien von erheblicher Bedeutung sein können. In diesem Fall empfiehlt sich die Verwendung der umfangreichen Funktionalität der Reporting Services-SOAP-API. Mit der SOAP-API können Sie Berichte verwalten und bereitstellen, Zeitpläne erstellen, Servereigenschaften konfigurieren, Berichtsserver-Namespaces verwalten, Abonnements erstellen und vieles mehr. Die SOAP-API stellt Ihnen die vollständige Verwaltungsfunktionalität in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zur Verfügung. Die SOAP-API kann die Berichtsanzeige und -navigation auch über die <xref:ReportExecution2005.ReportExecutionService.Render%2A>-Methode der API ermöglichen. Die Berichtsanzeige über die SOAP-API ermöglicht jedoch weder die integrierte Anzeigefunktion der Berichtssymbolleiste noch die automatische Berichtsinteraktivität wie beim URL-Zugriff.  
  
 Weitere Informationen über die Reporting Services-SOAP-API finden Sie unter [Berichtsserver-Webdienst](../../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 In der Mehrheit der Fälle werden sowohl der URL-Zugriff als auch die SOAP-Aufrufe benötigt, um Ihre Berichtsanforderungen zu erfüllen. SOAP wird verwendet, wenn Sie zum ersten Mal eine Verbindung zur Berichtsserver-Datenbank herstellen und die verfügbare Liste der Berichte in einer Benutzeroberfläche darstellen. URL-Zugriff wird verwendet, um die einzelnen Berichte tatsächlich aufzurufen und darin zu navigieren.  
  
 Ein Beispiel für das Kombinieren von URL-Zugriff und den Webdienst für eine integrierte berichterstellung bereitzustellen, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Integrieren von Reporting Services in Anwendungen](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrieren von Reporting Services mit SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)   
 [Integrieren von Reporting Services mit URL-Zugriff](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Technische Referenz &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
