---
title: Warning-Element (XMLA) | Microsoft Docs
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
- Warning Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords:
- Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5bd57e1ca9819f750f2538eba53b437aa8191a8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="warning-element-xmla"></a>Warning-Element (XMLA)
  Enthält Informationen über eine Warnung zurückgegeben, die von einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
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
|Übergeordnete Elemente|[MessageBox](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|ErrorCode|Erforderliches **UnsignedInt** -Attribut. Enthält den numerischen Rückgabecode der Warnung.|  
|Severity|Optionales **String** -Attribut. Enthält das Ausmaß von der Warnung.|  
|Beschreibung|Optionales **String** -Attribut. Enthält den beschreibenden Text von der Warnung.|  
|Quelle|Optionales **String** -Attribut. Enthält den Namen der Komponente, die die Warnung generiert hat.|  
|Helpfile|Optionales **String** -Attribut. Enthält den Pfad oder die URL zur Hilfedatei oder dem Thema, das die Warnung beschreibt.|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Error-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

