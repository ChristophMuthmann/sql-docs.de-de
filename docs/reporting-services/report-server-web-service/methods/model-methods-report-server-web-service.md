---
title: "Modellmethoden – Berichtsserver-Webdienst | Microsoft-Dokumentation"
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
applies_to: SQL Server 2016 Preview
ms.assetid: d3e658c9-bb22-480b-a3d5-bcde8f537ab2
caps.latest.revision: "4"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c9730c12ed92d1035238b6836016b0f62e03bba0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="model-methods---report-server-web-service"></a>Modellmethoden – Berichtsserver-Webdienst
  Sie können Modelle mithilfe dieser Methoden verwalten.  
  
|Methode|Aktion|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GenerateModel%2A>|Generiert auf Grundlage einer freigegebenen Datenquelle ein Standardmodell.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPermissions%2A>|Ruft die Benutzerberechtigungen ab, die dem Modellelement zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPolicies%2A>|Ruft die Richtlinien ab, die einem Modellelement zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.GetUserModel%2A>|Gibt den semantischen Teil eines Modells für den aktuellen Benutzer zurück.|  
|<xref:ReportService2010.ReportingService2010.InheritModelItemParentSecurity%2A>|Löscht die Richtlinien, die einem Modellelement zugeordnet sind, und bewirkt, dass das Modellelement die Richtlinien von dessen übergeordnetem Element erbt.|  
|<xref:ReportService2010.ReportingService2010.ListModelDrillthroughReports%2A>|Listet Drillthroughberichte auf, die einer Entität in einem Modell zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemChildren%2A>|Gibt ein Array untergeordneter Elemente von Modellelementen zurück.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemTypes%2A>|Gibt eine Liste unterstützter Modellelementtypen zurück.|  
|<xref:ReportService2010.ReportingService2010.ListModelPerspectives%2A>|Listet Modelle und Perspektiven auf, die dem Benutzer zur Verfügung stehen.|  
|<xref:ReportService2010.ReportingService2010.RegenerateModel%2A>|Aktualisiert ein vorhandenes Modell auf Grundlage von Änderungen am Datenquellenschema.|  
|<xref:ReportService2010.ReportingService2010.RemoveAllModelItemPolicies%2A>|Löscht alle Richtlinien, die Modellelementen im angegebenen Modell zugeordnet sind.|  
|<xref:ReportService2010.ReportingService2010.SetModelDrillthroughReports%2A>|Ordnet mehrere Drillthroughberichte einem Modell zu.|  
|<xref:ReportService2010.ReportingService2010.SetModelItemPolicies%2A>|Legt Sicherheitsrichtlinien für ein Modellelement fest.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Webdienstmethoden für Berichtsserver](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Technische Referenz (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
