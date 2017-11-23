---
title: Binding-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Binding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: BINDING
helpviewer_keywords: Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64b5234cdeb661c3f25b0d6ed2e00db330ea0ca7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="binding-data-type-assl"></a>Binding-Datentyp (ASSL)
  Definiert einen abstrakten Grunddatentyp, der eine abhängige Beziehung zwischen zwei Objekten darstellt, in der die Daten oder Metadaten des einen Objekts von den Daten oder Metadaten eines gebundenen Objekts abhängen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [ MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md), [ TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md), [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md), [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|Keine|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Binding>.  
  
 Weitere Informationen zur Datenbindung finden Sie unter [&#40; Datenquellen und Bindungen SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elemente des Typs "Bindung"  
 Die folgende Tabelle enthält Elemente des Typs **Binding**.  
  
|Übergeordnetes Element|Element des Typs **Binding**|Kommentare|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md) von [CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) (des Typs [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Geben Sie für die **binden** muss [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) oder [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (Out-of-Line)](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Geben Sie für die **binden** muss [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Binding** kann ein beliebiger Typ sein.|  
|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), oder [ TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) oder [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[Column](../../../analysis-services/scripting/objects/column-element-assl.md)|Geben Sie für die **binden** muss [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) oder [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[Measure](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md) (des Typs [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Geben Sie für die **binden** muss [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), oder [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md) von [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) (des Typs [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Geben Sie für die **binden** muss [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) oder [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), oder [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (Out-of-Line)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Geben Sie für die **binden** muss [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (Out-of-Line)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Measure](../../../analysis-services/scripting/objects/measure-element-assl.md)|Geben Sie für die **binden** muss [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (Out-of-Line)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|Geben Sie für die **binden** muss [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (Out-of-Line)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), oder [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Geben Sie für die **binden** muss [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), oder [MeasureBinding-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Geben Sie für die **binden** muss [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
