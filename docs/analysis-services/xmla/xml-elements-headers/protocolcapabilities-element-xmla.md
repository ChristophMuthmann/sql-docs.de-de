---
title: ProtocolCapabilities-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ProtocolCapabilities Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5d2ff72b1fdc3a3e3a4b09a046933d3ead88fc78
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# ProtocolCapabilities-Element (XMLA)
  Verwendet den SOAP-Header in einer SOAP-Anforderungsnachricht zur Identifizierung von Protokollfunktionen zwischen einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und einer Clientanwendung.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/engine`  
  
## Syntax  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
```  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Funktion](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## Hinweise  
 Die **ProtocolCapabilities** Element ermöglicht Clientanwendungen das aushandeln, Protokollfunktionen, z. B. für binäres XML und Komprimierung unterstützt, wobei ein [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz zu einem beliebigen Zeitpunkt. Die Protokollaushandlung schließt die folgenden Schritte ein:  
  
1.  Die Clientanwendung identifiziert die Protokollfunktion, indem sie eine SOAP-Anforderung sendet, die sowohl das **ProtocolCapabilities** -Element als auch den SOAP-Header enthält.  
  
2.  Die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz empfängt und verarbeitet die SOAP-Anforderung.  
  
3.  Wenn die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz hat die gleiche Protokollfunktion wie angefordert, sendet die Instanz eine SOAP-Antwort, die die gleiche enthält **ProtocolCapabilities** Element in der SOAP-Anforderung gesendet und das Protokoll wurde erfolgreich ausgehandelt. Andernfalls werden die Protokollfunktionen nicht erfolgreich ausgehandelt, und die Instanz gibt einen SOAP-Fehler zurück.  
  
 Nach erfolgreich Protokollfunktionen, wie lange die Clientanwendung und die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz Verwendung eines bestimmten Protokolls hängt davon ab, ob die Sitzung implizit oder explizit ist:  
  
-   Eine explizite Sitzung ist eine, die erstellt wird, mithilfe der [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) Header-Element. Bei einer expliziten Sitzung wird das verhandelte Protokoll so lange verwendet, bis die Clientanwendung ein neues **ProtocolCapabilities** -Element sendet oder bis die Sitzung endet.  
  
-   Eine implizite Sitzung ist eine Sitzung, die über eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz erstellt wird und nicht beim Übermitteln einer SOAP-Anforderung explizit von der Clientanwendung angegeben wird. Bei einer impliziten Sitzung wird das ausgehandelte Protokoll nur so lange verwendet, bis die SOAP-Anforderung abgeschlossen ist.  
  
 Protokollfunktionen müssen nicht explizit ausgehandelt werden. Das heißt, dass eine Clientanwendung kein **ProtocolCapabilities** -Element als Teil der SOAP-Anforderung enthalten muss. Wenn eine SOAP-Anforderung nicht enthalten ist ein **ProtocolCapabilities** Element, das [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz antwortet mit dem gleichen Format wie die SOAP-Anforderung.  
  
## Siehe auch  
 [Verwalten von Verbindungen und Sitzungen &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Header &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  

