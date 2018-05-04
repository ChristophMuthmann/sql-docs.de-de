---
title: DefaultMember-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DefaultMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6214a899d1bb1cc48e4fd3399d5840a9e7a01beb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="defaultmember-element-assl"></a>DefaultMember-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält einen MDX-Ausdruck (Multidimensional Expression), der das Standardelement des übergeordneten Elements definiert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **DefaultMember** -Element definiert das Standardelement für das übergeordnete Element. Wenn **DefaultMember** nicht angegeben oder auf eine leere Zeichenfolge festgelegt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] wählt ein Element als Standardelement verwendet.  
  
 Bei **ManyToManyMeasureGroupDimension** -Elementen enthält das **DefaultMember** -Element einen MDX-Ausdruck, der ein Element in der Dimension angibt, die vom **CubeDimensionID** -Element von **ManyToManyMeasureGroupDimension**-identifiziert wird. Der MDX-Ausdruck ähnelt der [StrToMember](../../../mdx/strtomember-mdx.md) MDX-Funktion mit dem Schlüsselwort CONSTRAINED, da sie MDX-Funktionen oder benutzerdefinierte Funktionen enthalten kann.  
  
 Weitere Informationen zu Standardelementen finden Sie unter [Definieren eines Standardelements](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **DefaultMember** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, und <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
