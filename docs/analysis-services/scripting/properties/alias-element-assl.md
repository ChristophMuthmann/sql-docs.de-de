---
title: Alias-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Alias Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Alias
helpviewer_keywords: Alias element
ms.assetid: 674fdb06-e33c-4f35-bd6a-d9bbb13ececa
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ead0aae5b918d3803eeefcfd92005f0354a45bd8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="alias-element-assl"></a>Alias-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert einen Alias für eine [Konto](../../../analysis-services/scripting/objects/account-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aliase](../../../analysis-services/scripting/collections/aliases-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Der Wert des **Alias** -Elements wird als alternativer Name für das Konto verwendet, das vom übergeordneten **Account** -Element definiert wird, und hilft bei der Identifizierung des Kontotyps und der Aggregatfunktion bei einer Benutzeroberfläche.  
  
 Das Element, das das übergeordnete Element des entspricht, der **Aliase** Auflistung im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
