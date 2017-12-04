---
title: "Webdienstmethoden für Berichtsserver | Microsoft-Dokumentation"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
caps.latest.revision: "49"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 89804c5a980a3fed4869dca8de1603d42e7b481a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="report-server-web-service-methods"></a>Webdienstmethoden für Berichtsserver
  Der Berichtsserver-Webdienst umfasst mehrere Kategorien von Methoden, die auf Komponentenfunktionen basieren. Diese Methoden werden über mehrere Webdienst-Endpunkte (drei für die Berichtsverwaltung und einer für die Berichtsausführung) bereitgestellt, die als Mitglieder der Klassen <xref:ReportService2010.ReportingService2010> und <xref:ReportExecution2005.ReportExecutionService> verfügbar gemacht werden. Diese Klassen können über ein Proxyklassentool wie „wsdl.exe“ generiert werden, das im [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK enthalten ist. Weitere Informationen zu Berichtsserver-Webdiensten und [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] finden Sie unter [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
## <a name="endpoints-and-methods"></a>Endpunkte und Methoden  
 In der folgenden Tabelle sind die Endpunkte des Berichtsserver-Webdiensts und die vom <xref:ReportService2010.ReportingService2010>-Endpunkt bereitgestellten Methodenkategorien aufgeführt. Informationen zu den in den anderen Endpunkten verfügbaren Methoden finden Sie unter [Technische Referenz (SSRS)](../../../reporting-services/technical-reference-ssrs.md).  
  
|Thema|Description|  
|-----------|-----------------|  
|[Report Server Web Service Endpoints (Report Server-Webdienst-Endpunkte)](../../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)|Beschreibt die Verwaltungs- und Ausführungsendpunkte des Berichtsserver-Webdiensts.|  
|[Report Server Namespace Management Methods (Methoden zur Berichtsserver-Namespaceverwaltung)](../../../reporting-services/report-server-web-service/methods/report-server-namespace-management-methods.md)|Beschreibt Methoden, mit denen Sie die Berichtsserver-Datenbank verwalten können. Insbesondere können Sie Ordner und Ressourcen verwalten und Elementeigenschaften festlegen.|  
|[Authorization Methods (Autorisierungsmethoden)](../../../reporting-services/report-server-web-service/methods/authorization-methods.md)|Beschreibt Methoden, mit denen Sie Aufgaben, Rollen und Richtlinien verwalten können.|  
|[Data Sources and Connection Methods (Datenquellen- und Verbindungsmethoden)](../../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)|Beschreibt Methoden, mit denen Sie Datenquellenverbindungen und Anmeldeinformationen für Berichte festlegen und verwalten können.|  
|[Report Parameters Methods (Melden von Parametermethoden)](../../../reporting-services/report-server-web-service/methods/report-parameters-methods.md)|Beschreibt Methoden, mit denen Sie Parameter für Berichte festlegen und abrufen können.|  
|[Model Methods - Report Server Web Service (Modellmethoden: Berichtsserver-Webdienst)](../../../reporting-services/report-server-web-service/methods/model-methods-report-server-web-service.md)|Beschreibt Methoden, mit denen Sie Modelle verwalten können.|  
|[Rendering and Execution Methods (Rendering- und Execution-Methode)](../../../reporting-services/report-server-web-service/methods/rendering-and-execution-methods.md)|Beschreibt Methoden, mit denen Sie die Berichtsausführung sowie das Rendern und Zwischenspeichern verwalten können.|  
|[Report History Methods (Berichtsverlaufsmethoden)](../../../reporting-services/report-server-web-service/methods/report-history-methods.md)|Beschreibt Methoden, mit denen Sie Berichtsverlaufs-Momentaufnahmen erstellen und verwalten können.|  
|[Scheduling Methods (Zeitplanmethoden)](../../../reporting-services/report-server-web-service/methods/scheduling-methods.md)|Beschreibt Methoden, mit denen Sie freigegebene Zeitpläne und Cacheaktualisierungspläne, die auf dem Berichtsserver verwendet werden, erstellen und verwalten können.|  
|[Subscription and Delivery Methods (Abonnement und Übermittlungsmethoden)](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|Beschreibt Methoden, mit denen Sie Abonnements und die Übermittlung von Berichten erstellen und verwalten können.|  
|[Linked Reports Methods (Methoden für verknüpfte Berichte)](../../../reporting-services/report-server-web-service/methods/linked-reports-methods.md)|Beschreibt Methoden, mit denen Sie verknüpfte Berichte erstellen und verwalten können.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zugriff auf die SOAP-API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Technische Referenz (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
