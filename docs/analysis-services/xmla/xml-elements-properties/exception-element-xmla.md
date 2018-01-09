---
title: Exception-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Exception Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords: Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e9baae4041109f17653ffdb4e7747643a60c8336
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="exception-element-xmla"></a>Exception-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Gibt an, dass eine Ausnahme zurückgegeben wurde, aus einer [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methodenaufruf.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|InclusionThresholdSetting|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Fehler auftritt, während der **Discover** -Methodenaufruf oder ein einzelner XMLA-Befehl in einem **Execute** -Methodenaufruf auftritt, der verhindert, dass die Methode oder der Befehl abgeschlossen werden kann, enthält das **root** -Element für diese Methode/diesen Befehl ein **Exception** - und ein **Messages** -Element. Das **Exception** -Element gibt an, dass ein Fehler aufgetreten ist, der verhindert, dass die Methode oder der Befehl erfolgreich ausgeführt wird, und das **Messages** -Element enthält die Liste der entsprechenden Fehler- oder Warnmeldungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Messages-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
