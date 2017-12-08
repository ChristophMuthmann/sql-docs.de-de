---
title: Session-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Session Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords: Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 53698817a6ae3cf6e59752eae2caf7182d843d99
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="session-element-xmla"></a>Session-Element (XMLA)
  Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht identifiziert eine vorhandene, explizierte Sitzung auf einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
-   Eine SOAP-Antwort mit einer [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) SOAP-Header-Element.  
  
-   Eine SOAP-Anforderung zur Identifikation der Sitzung für die Ausführung der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
 Eine Sitzungs-ID garantiert nicht, dass eine Sitzung gültig bleibt. Die im **Session** -Element angegebene Sitzung kann ablaufen. Eine Sitzung kann beispielsweise ablaufen, wenn das Timeout der Sitzung erreicht ist oder wenn die der Sitzung zugeordnete Verbindung beendet wird. Wenn die Sitzung abläuft und nicht mehr gültig ist, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] wird die Sitzung beendet und ein Rollback eine Transaktion derzeit im Prozess. Jede SOAP-Nachricht, die zusammen mit einer nicht mehr gültigen ID gesendet wird, schlägt mit einem SOAP-Fehler fehl, der angibt, dass die angegebene Sitzung nicht gefunden werden kann.  
  
 Wenn eine **Sitzung** Element nicht als Teil einer SOAP-Anforderung gesendet wird die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz beginnt implizit eine Sitzung für die Dauer der der **Discover** oder **Execute** Methodenaufruf, und klicken Sie dann endet die Sitzung, wenn der Methodenaufruf abgeschlossen ist.  
  
## <a name="see-also"></a>Siehe auch  
 [EndSession-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Verwalten von Verbindungen und Sitzungen &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Header &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
