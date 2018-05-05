---
title: MemberNamesUnique-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MemberNamesUnique Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MemberNamesUnique
helpviewer_keywords:
- MemberNamesUnique element
ms.assetid: bd4e75b2-4605-4ebc-a535-10f743eba08e
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1acf341602058cfca896b4bb9a23e8f8865461aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="membernamesunique-element-assl"></a>MemberNamesUnique-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Bestimmt, ob Elementnamen im übergeordneten Element eindeutig sein müssen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute> <!-- or Hierarchy -->  
   ...  
   <MemberNamesUnique>   </MemberNamesUnique>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|False|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md),.[ Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
