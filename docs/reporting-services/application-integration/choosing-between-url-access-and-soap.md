---
title: "Auswählen zwischen URL-Zugriff und SOAP in Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 1d9b4df388cd1d6bb96d88b64bf319f5fd9866e9
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>Auswählen zwischen URL-Zugriff und SOAP in Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in benutzerdefinierte Anwendungen ist manchmal nicht ganz einfach. Die Herausforderung liegt jedoch nicht in der Komplexität des Programmiermodells oder in den APIs, sondern in den vielen Möglichkeiten der Integration. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wurde von Grund auf als Entwicklerplattform konzipiert, daher stand die Flexibilität bei der Programmierung immer im Vordergrund. Die hohe Flexibilität fordert jedoch häufige Entscheidungen, wenn die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichtsnavigations- und Verwaltungsfunktionen in die vorhandenen Geschäftsanwendungen integriert werden.

> [!NOTE]
> Beginnend mit SQL Server 2017 Reporting Services, ist die REST-API-Zugriff für die Entwicklung von Lösungen zur Verfügung. SOAP-API-Zugriff wurde als veraltet markiert. Weitere Informationen finden Sie unter [entwickeln Sie mit der REST-APIs für Reporting Services](../developer/rest-api.md).
  
 Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf zwei verschiedene Arten in benutzerdefinierte Anwendungen integrieren: über den URL-Zugriff und die Reporting Services-SOAP-API. Welche der beiden Arten verwendet werden soll, hängt von mehreren Faktoren ab. In einigen Fällen, die Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihr Geschäft, benutzerdefinierte Anwendungen erfordert die Verwendung von URL-Zugriff und SOAP. Sie sollten sich folgende Fragen stellen:  
  
-   Welche Art Berichtsfunktionen benötigen Sie oder die Endbenutzer? Brauchen Sie einfache Start- und Navigationsfunktionen für die Berichte, oder benötigen Sie ausgereifte Berichtsserver-Verwaltungsfunktionen aus Ihrer benutzerdefinierten Geschäftsanwendung?  
  
-   In welcher Art Umgebung arbeiten die Benutzer normalerweise? Ist die Geschäftsanwendung eine Webanwendung oder eine Windows-Anwendung? Wie leicht können Ihre Endbenutzer von einer Win32-Umgebung in eine webumgebung wechseln? Welche Art der Kontrolle benötigen Sie für die Umgebung, in der die Berichte ausgeführt und verwaltet werden?  
  
 Wenn Sie diese Fragen beantwortet haben, können Sie entscheiden, wie Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in Ihre IT-Infrastruktur integrieren. Normalerweise wird der URL-Zugriff für die Anzeige und Navigation der Berichte bevorzugt. Der URL-Zugriff ermöglicht eine rasche Navigation durch die Berichte ohne den Aufwand eines Webdiensts. Außerdem ist der URL-Zugriff derzeit die einzige Programmiertechnik, die die komplette Funktionalität von HTML Viewer, einschließlich der Berichtssymbolleiste, für die Berichtsnavigation verwendet. Darüber hinaus sorgt der URL-Zugriff für eine bessere Leistung als SOAP, da das Marshalling der SOAP-Anforderungen zum Server hin und wieder zurück umgangen wird. In den Integrationsszenarien, in denen rasch und problemlos mit integrierten Anzeige- und Navigationstools auf die Berichte zugegriffen werden muss, ist der URL-Zugriff die bessere Variante.  
  
> [!NOTE]  
> Der Berichtsserver-URL-Zugriff unterstützt HTML Viewer und die erweiterten Funktionen der Berichtssymbolleiste. Die SOAP-API unterstützt diese Art des gerenderten Berichts nicht. Wenn Sie Berichte mithilfe der SOAP-API gerendert, Entwerfen Sie und entwickeln Sie eine eigene Berichtssymbolleiste.
  
 Weitere Informationen zur Berichtssymbolleiste finden Sie unter [HTML-Viewer und die Berichtssymbolleiste](../../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
 Weitere Informationen zum URL-Zugriff finden Sie unter [URL-Zugriff](../../reporting-services/url-access-ssrs.md).  
  
 Der URL-Zugriff ist sinnvoll für die Anzeige von Berichten, er liefert jedoch nicht die Berichts- und Namespace-Verwaltungsfunktionen, die in bestimmten Unternehmensberichtsszenarien von erheblicher Bedeutung sein können. In diesem Fall empfiehlt sich die Verwendung der umfangreichen Funktionalität der Reporting Services-SOAP-API. Mit der SOAP-API können Sie Berichte verwalten und bereitstellen, Zeitpläne erstellen, Servereigenschaften konfigurieren, Berichtsserver-Namespaces verwalten, Abonnements erstellen und vieles mehr. Die SOAP-API stellt Ihnen die vollständige Verwaltungsfunktionalität in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zur Verfügung. Die SOAP-API kann die Berichtsanzeige und -navigation auch über die <xref:ReportExecution2005.ReportExecutionService.Render%2A>-Methode der API ermöglichen. Allerdings wird die Berichtsanzeige über die SOAP-API nicht aktiviert die integrierte anzeigen Funktionalität der Berichtssymbolleiste noch wird, die Sie automatisch die berichtsinteraktivität behandelt, die URL-Zugriff.  
  
 Weitere Informationen über die Reporting Services-SOAP-API finden Sie unter [Berichtsserver-Webdienst](../../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 In der Mehrheit der Fälle werden sowohl der URL-Zugriff als auch die SOAP-Aufrufe benötigt, um Ihre Berichtsanforderungen zu erfüllen. SOAP wird verwendet, wenn Sie zum ersten Mal eine Verbindung zur Berichtsserver-Datenbank herstellen und die verfügbare Liste der Berichte in einer Benutzeroberfläche darstellen. URL-Zugriff wird verwendet, um die einzelnen Berichte tatsächlich aufzurufen und darin zu navigieren.  
  
 Ein Beispiel für das Kombinieren von URL-Zugriff und den Webdienst für eine integrierte berichterstellung bereitzustellen, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

