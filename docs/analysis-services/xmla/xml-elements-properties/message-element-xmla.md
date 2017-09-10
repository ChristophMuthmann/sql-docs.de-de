---
title: Message-Element (XMLA) | Microsoft Docs
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
- Message Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords:
- Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 513b0b4be9666d667bd33221552fd792e92e3790
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="message-element-xmla"></a>Message-Element (XMLA)
  Enthält eine Meldung, die von einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] durch einen Aufruf der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) - oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methode zurückgegeben wurde.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Messages>  
   ...  
   <Message>  
      <Error>...</Error>  
      <!-- or -->  
      <Warning>...</Warning>  
   </Message>  
   ...  
</Messages>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Meldungen](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|Untergeordnete Elemente|[Error](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md), [Warning](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element wird verwendet, wenn ein **Discover** -Methodenaufruf oder ein einzelner XMLA-Befehl innerhalb eines **Execute** -Methodenaufrufs erfolgreich, jedoch mit Fehlern oder Warnungen, abgeschlossen wird. In einem solchen Fall wird dem Stammelement nach allen anderen Elementen ein **Messages** -Element hinzugefügt, das wiederum mindestens ein **Message** -Element enthält. Jedes **Message** -Element stellt eine einzelne Nachricht dar, entweder eine Fehler- oder eine Warnungsmeldung, die von der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz zurückgegeben wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
