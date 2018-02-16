---
title: OLAP-Modulserverkomponenten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services, architecture
- ports [Analysis Services]
- XML/A listener
- server architecture [Analysis Services]
ms.assetid: 5193c976-9dcd-459c-abba-8c3c44e7a7f2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 462dc47d0bb6545517fd8d11cab487196c00bfcb
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="olap-engine-server-components"></a>OLAP-Modulserverkomponenten
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Die Serverkomponente von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ist die **msmdsrv.exe** Anwendung, die als Windows-Dienst ausgeführt wird. Diese Anwendung besteht aus Sicherheitskomponenten, einer XMLA-Überwachungskomponente (XML for Analysis), einer Abfrageverarbeitungskomponente und zahlreichen internen Komponenten, die die folgenden Funktionen ausführen:  
  
-   Analysieren von Anweisungen, die von Client empfangen werden  
  
-   Verwalten von Metadaten  
  
-   Behandeln von Transaktionen  
  
-   Verarbeiten von Berechnungen  
  
-   Speichern von Dimensions- und Zellendaten  
  
-   Erstellen von Aggregationen  
  
-   Planen von Abfragen  
  
-   Zwischenspeichern von Objekten  
  
-   Verwalten von Serverressourcen  
  
## <a name="architectural-diagram"></a>Architekturdiagramm  
 Eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz wird als eigenständiger Dienst ausgeführt, und die Kommunikation mit dem Dienst erfolgt in XMLA (XML for Analysis) über HTTP oder TCP. AMO ist eine Ebene zwischen der Benutzeranwendung und der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz. Diese Ebene bietet Zugriff auf [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Verwaltungsobjekte. AMO ist eine Klassenbibliothek, die Befehle von Clientanwendungen entgegennimmt und diese Befehle in XMLA-Nachrichten für die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz übersetzt. AMO stellt Objekte der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz für die Endbenutzerumgebung als Klassen dar, wobei Methodenmember Befehle ausführen und Eigenschaftenmember die Daten für die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Objekte speichern.  
  
 Die folgende Abbildung stellt die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Komponentenarchitektur dar, einschließlich aller wichtigen Elemente, die in der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz ausgeführt werden, und aller Benutzerkomponenten, die mit der Instanz zusammenarbeiten. Diese Abbildung zeigt auch, dass nur mit dem XMLA (XML for Analysis)-Listener entweder über HTTP oder TCP auf die Instanz zugegriffen werden kann.  
  
 ![Analysis Services-System-Architekturdiagramm](../../../analysis-services/data-mining/media/analysisservicessystemarchitecture.gif "Analysis Services-System-Architekturdiagramm")  
  
## <a name="xmla-listener"></a>XMLA-Überwachung  
 Die XMLA-Überwachungskomponente verarbeitet die gesamte XMLA-Kommunikation zwischen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und den zugehörigen Clients. Mithilfe der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] **Port** in der Datei msmdsrv.ini können Sie einen Port angeben, der von einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] überwacht wird. Wird in dieser Datei der Wert 0 angegeben, wird der Standardport von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] überwacht. Falls nicht anders angegeben, verwendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] die folgenden TCP-Standardports:  
  
|Port|Description|  
|----------|-----------------|  
|2383|Standardinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|2382|Redirector für andere Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|Dynamische Zuweisung beim Serverstart.|Benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
 Finden Sie unter [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) Weitere Details.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekt Naming Funktionsregeln &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/olap-physical/object-naming-rules-analysis-services.md)   
 [Physische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)  
  
  
