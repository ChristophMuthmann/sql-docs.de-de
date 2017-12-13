---
title: Herstellen einer Verbindung mit Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 683474e873b45eca2fc39d0b8f254da06d205cf2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="connect-to-analysis-services"></a>Verbindung mit Analysis Services herstellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Verwenden Sie die Informationen in diesem Abschnitt, um Informationen zu Eigenschaften von Verbindungszeichenfolgen, Clientbibliotheken für Verbindungen, die die unterstützten Authentifizierungsmethoden werden vom Analysis Services sowie zum Einrichten oder Löschen von Verbindungen, bevor ein Server offline geschaltet.  
  
## <a name="analysis-services-connections"></a>Analysis Services-Verbindungen  
 Analysis Services verwendet TCP als Netzwerkprotokoll und XML for Analysis (XMLA) als Kommunikationsprotokoll. Auf der untersten Ebene wird von allen Clientbibliotheken, die mit Analysis Services bereitgestellt wurden, XMLA-over-TCP implementiert. Obwohl es möglich ist, Anwendungen auf Grundlage der XMLA-Struktur zu erstellen, verwenden die meisten Anwendungen und Anwendungsentwickler Clientbibliotheken, um die Vorteile von Objektmodellen und die damit verbundene effiziente Codierung zu nutzen. Für Clientverbindungen zu Analysis Services können Sie IIS als zwischengeschaltete Verbindung verwenden, wenn Sie TCP nicht über den Stapel hinweg verwenden können. Ein Vorteil der Verwendung von HTTP-Zugriff über IIS ist die Möglichkeit, eine Verbindung von Anwendungen aus herzustellen, die Anmeldeinformationen in der Verbindungszeichenfolge übergeben.  
  
 In Zusammenhang mit Konnektivität geht es immer auch um Authentifizierung. Im Unterschied zu anderen SQL Server-Funktionen verwendet Analysis Services ausschließlich die Windows-Anmeldeinformationen. Es ist nicht möglich, auf der Back-End-Verbindung mit Analysis Services die SQL Server-Datenbankauthentifizierung, die Forderungsauthentifizierung, die formularbasierte Authentifizierung oder Digest zu verwenden. Weitere Informationen zur Authentifizierung finden Sie in diesem Abschnitt.  
  
##  <a name="bkmk_clientApps"></a> Verbindungsaufgaben  
  
|Link|Taskbeschreibung|  
|----------|----------------------|  
|[Herstellen einer Verbindung von Clientanwendungen &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|Wenn Sie mit Analysis Services nicht vertraut sind, lesen Sie dieses Thema, um sich einen Überblick über die Tools und Anwendungen zu verschaffen, die am häufigsten mit Analysis Services verwendet werden.|  
|[Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services umfasst zahlreiche Server- und Datenbankeigenschaften, mit denen eine Verbindung unabhängig davon, wie die Instanz oder Datenbank konfiguriert ist, an spezifische Anwendungen angepasst werden kann.|  
|[Von Analysis Services unterstützte Authentifizierungsmethoden](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|Dieses Thema gibt eine kurze Einführung in die Authentifizierungsmethoden, die von Analysis Services verwendet werden.|  
|[Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|Viele Business Intelligence-Lösungen setzen den Identitätswechsel voraus, um sicherzustellen, dass nur berechtigte Daten an die einzelnen Benutzer zurückgegeben werden. In diesem Thema werden die Voraussetzungen für die Verwendung des Identitätswechsels beschrieben. In diesem Thema werden außerdem die Schritte zum Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung beschrieben.|  
|[SPN-Registrierung für eine Analysis Services-Instanz](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|Die Kerberos-Authentifizierung setzt einen gültigen Dienstprinzipalnamen (Service Principal Name, SPN) für Dienste voraus, durch die die Identität eines Benutzers in einer Multiserverlösung angenommen oder delegiert wird. Verwenden Sie die Informationen in diesem Thema, um mehr darüber zu erfahren, wie Sie die SPN-Registrierung für Analysis Services erstellen und ausführen.|  
|[Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|Standardauthentifizierung oder domänenübergreifende Nutzung sind zwei wichtige Gründe, um Analysis Services für den HTTP-Zugriff zu konfigurieren.|  
|[Für Analysis Services-Verbindungen verwendete Datenanbieter](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services stellt drei Clientbibliotheken für den Zugriff auf Servervorgänge oder Analysis Services-Daten bereit. Dieses Thema enthält eine kurze Einführung zu ADOMD.NET, AMOs (Analysis Services Management Objects) und dem OLE DB-Anbieter für Analysis Services (MSOLAP).|  
|[Trennen von Benutzern und Sitzungen auf Analysis Services-Server](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|Löschen Sie vorhandene Verbindungen und Sitzungen, bevor Sie einen Server offline schalten oder Baseline-Leistungstests durchführen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration nach der Installation &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
