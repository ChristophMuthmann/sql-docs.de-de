---
title: ID-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8d01b4de46aadcea6bc996062755b291a3a10a31
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="id-element-assl"></a>ID-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält den eindeutigen Bezeichner (ID) des übergeordneten Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (bis zu 100 Zeichen)|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md), [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md), [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [Dimension ](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [Ebene](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [ MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md), [Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md), [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md), [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Jedes Hauptobjekt in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verfügt über eine **ID** -Element als Eigenschaft. Der Wert, der eine **ID** -Elements hat die folgenden Einschränkungen:  
  
-   Der Wert darf keine führenden oder nachgestellten Leerzeichen enthalten. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] entfernt implizit führende oder nachfolgende Leerzeichen aus dem Wert einer **ID** Element.  
  
-   Der Wert kann keine Steuerzeichen enthalten. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] entfernt implizit Steuerzeichen aus dem Wert einer **ID** Element.  
  
-   Die folgenden reservierten Werte können nicht verwendet werden:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 bis COM9 (COM1, COM2, COM3 usw.)  
  
    -   CON  
  
    -   LPT1 bis LPT9 (LPT1, LPT2, LPT3 usw.)  
  
    -   NUL  
  
    -   PRN  
  
 Die folgende Tabelle enthält zusätzliche Zeichen, die im Wert verwendet werden können ein **ID** -Element, abhängig vom übergeordneten Element.  
  
|Übergeordnetes Element|Zeichen|  
|--------------------|----------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|Der Wert muss den Regeln für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Computernamen entsprechen. (IP-Adressen sind nicht gültig.)|  
|[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?" () []{}<>|  
|[Ebene](../../../analysis-services/scripting/objects/level-element-assl.md), [-Attribut-Element](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! += []{}<>|  
|Alle anderen übergeordneten Elemente|.,;' `:/\\*&#124;?" & % $!:: Operator += () []{}<>|  
  
## <a name="see-also"></a>Siehe auch  
 [Namen von Element &#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
