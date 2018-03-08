---
title: HideMemberIf-Element (ASSL) | Microsoft Docs
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
apiname: HideMemberIf Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HideMemberIf
helpviewer_keywords: HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5a53e8896e389b2b0cb4b478ef8a9e8ff9bd45a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="hidememberif-element-assl"></a>HideMemberIf-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Gibt an, ob und wann ein Element auf einer Ebene aus Clientanwendungen ausgeblendet werden soll.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Nie*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*Nie*|Elemente werden nie ausgeblendet.|  
|*OnlyChildWithNoName*|Ein Element wird ausgeblendet, wenn es das einzige untergeordnete Element seines übergeordneten Elements ist und sein Name leer ist.|  
|*OnlyChildWithParentName*|Ein Element wird ausgeblendet, wenn es das einzige untergeordnete Element seines übergeordneten Elements ist und identisch mit seinem übergeordneten Element ist.|  
|*NoName*|Ein Element wird ausgeblendet, wenn sein Name leer ist.|  
|*ParentName*|Ein Element wird ausgeblendet, wenn sein Name dem seines übergeordneten Elements entspricht.|  
  
## <a name="remarks"></a>Hinweise  
 Die Enumeration, die den zulässigen Werten für entspricht **HideMemberIf** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.HideIfValue>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
