---
title: Header (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0fd680e1fe5df195752e1618fe23551f4c10f2a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xml-elements---headers"></a>XML-Elemente - Header
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Das XMLA-Protokoll (XML for Analysis) verwendet XML-Elemente innerhalb des SOAP-Headers, um Funktionen auf Protokollebene zu verwalten, wie Sitzungsunterstützung und die Aushandlung von unterstützten Funktionen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Die folgenden Themen beschreiben die XMLA-Header-Elemente von implementiert [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Methode|Description|  
|------------|-----------------|  
|[BeginSession-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|Verwendet einen SOAP-Header in einer SOAP-Anforderungsnachricht, um eine neue Sitzung auf einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu starten.|  
|[EndSession-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht, um eine vorhandene Sitzung auf einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu beenden.|  
|[Session-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht, um eine vorhandene, explizierte Sitzung auf einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu identifizieren.|  
|[ProtocolCapabilities-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht, um Protokollfunktionen zwischen einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und einer Clientanwendung zu identifizieren.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Elemente & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML-Datentypen & #40; XMLA & #41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML-Elemente & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
