---
title: Root-Element (XMLA) | Microsoft Docs
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
apiname: Root Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#root
- urn:schemas-microsoft-com:xml-analysis#root
- microsoft.xml.analysis.root
helpviewer_keywords: root element
ms.assetid: ecd9d6e8-b16c-4d62-9a87-107c413a0056
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 402d03a39b1eb4711b338c8e3bc0ff29de11437a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="root-element-xmla"></a>root-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Ein zurückgegebenes Ergebnis enthält die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode oder ein XML for Analysis (XMLA)-Befehl ausgeführt wird, mithilfe der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Finden Sie in der folgenden Tabelle aus.|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|1-n: Erforderliches Element, das mehr als einmal auftreten kann.|  
  
|Ancestor|Datentyp|  
|--------------|---------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [Olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md), [Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [Olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Ergebnisse](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md), [zurückgeben](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Die **Root** -Element enthält die Informationen, die entweder die [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) -Element über einen einzelnen **Discover** -Methodenaufruf, oder in der [ ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) -Element über einen einzelnen XMLA-Befehl ausgeführt wird, über einen einzelnen **Execute** -Methodenaufruf.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
