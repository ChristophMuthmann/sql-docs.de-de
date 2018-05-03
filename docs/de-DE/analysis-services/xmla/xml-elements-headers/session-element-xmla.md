---
title: Session-Element (XMLA) | Microsoft Docs
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
apiname:
- Session Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b0352de12de4e7dcfa9a91115d700d4040dd5daa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="session-element-xmla"></a>Session-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht, um eine vorhandene, explizierte Sitzung auf einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]zu identifizieren.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|Keine|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|SessionID|Erforderliches **String** -Attribut, das die Sitzung identifiziert, die verwendet werden soll. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] identifiziert eine Sitzung anhand einer GUID (Globally Unique Identifier).|  
  
## <a name="remarks"></a>Hinweise  
 Die **Sitzung** Header-Element identifiziert eine vorhandene, explizit gestartete Sitzung auf die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Das **Session** -Element ist in den folgenden Nachrichtentypen Teil des SOAP-Headers:  
  
-   Eine SOAP-Antwort, die ein [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) SOAP-Header-Element enthält.  
  
-   Eine SOAP-Anforderung zur Identifikation der Sitzung, auf der die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) - oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methode ausgeführt wird.  
  
 Eine Sitzungs-ID garantiert nicht, dass eine Sitzung gültig bleibt. Die im **Session** -Element angegebene Sitzung kann ablaufen. Eine Sitzung kann beispielsweise ablaufen, wenn das Timeout der Sitzung erreicht ist oder wenn die der Sitzung zugeordnete Verbindung beendet wird. Wenn die Sitzung abläuft und nicht mehr länger gültig ist, beendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] die Sitzung und führt für alle derzeit stattfindenden Transaktionen ein Rollback durch. Jede SOAP-Nachricht, die zusammen mit einer nicht mehr gültigen ID gesendet wird, schlägt mit einem SOAP-Fehler fehl, der angibt, dass die angegebene Sitzung nicht gefunden werden kann.  
  
 Wenn eine **Sitzung** Element nicht als Teil einer SOAP-Anforderung gesendet wird die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz beginnt implizit eine Sitzung für die Dauer der der **Discover** oder **Execute** Methodenaufruf, und klicken Sie dann endet die Sitzung, wenn der Methodenaufruf abgeschlossen ist.  
  
## <a name="see-also"></a>Siehe auch  
 [EndSession-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Verwalten von Verbindungen und Sitzungen & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Header & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
