---
title: Description-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Description Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Description
helpviewer_keywords: Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 49be4d5ed0f50a6ec97c3ac8c7391d5c0dac0bb2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="description-element-assl"></a>Description-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Enthält die Beschreibung des übergeordneten Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-1: Optionales Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md), [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md), [AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md), [ CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md), [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md), [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) , [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [Ebene](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [ Partition](../../../analysis-services/scripting/objects/partition-element-assl.md), [Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md), [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md), [Ablaufverfolgung](../../../analysis-services/scripting/objects/trace-element-assl.md), [Übersetzung](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert eines **Description** -Elements hat die folgenden Einschränkungen:  
  
-   Der Wert darf keine führenden oder nachgestellten Leerzeichen enthalten. Wenn im Wert des führende oder nachgestellte Leerzeichen enthalten sind eine **Beschreibung** Element, diese Leerzeichen implizit durch entfernt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Der Wert kann keine Steuerzeichen enthalten. Wenn im Wert des Steuerzeichen enthalten sind eine **Beschreibung** Element, diese Zeichen werden implizit durch entfernt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Name-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
