---
title: Analysis Services Scripting Language-XML-Daten Typhierarchie (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname:
- Analysis Services Scripting Language XML Data Type Hierarchy
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
ms.assetid: f143c9f8-225d-495d-ac8e-ac2d2a7b4c07
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d95434e118735dca90480933a1d7e04c18307fe6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-scripting-language-xml-data-type-hierarchy-assl"></a>Analysis Services Scripting Language-XML-Datentypenhierarchie (ASSL)
  In der folgenden Tabelle wird die Vererbungshierarchie von Datentypen in Analysis Services Scripting Language (ASSL) angezeigt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
Action  
      DrillThroughAction  
      ReportAction  
      StandardAction  
AggregationAttribute  
AggregationDesignAttribute  
AggregationDesignDimension  
AggregationDimension  
Assembly  
      ClrAssembly  
      ComAssembly  
AttributeTranslation  
Binding  
      AttributeBinding  
      ColumnBinding  
      CubeAttributeBinding  
      CubeDimensionBinding  
      DataSourceViewBinding  
      DimensionBinding  
      InheritedBinding  
      MeasureBinding  
      MeasureGroupBinding  
      MeasureGroupDimensionBinding  
      PartitionBinding  
      ProactiveCachingBinding  
            ProactiveCachingIncrementalProcessingBinding  
            ProactiveCachingObjectNotificationBinding  
                  ProactiveCachingInheritedBinding  
                  ProactiveCachingTablesBinding  
            ProactiveCachingQueryBinding  
      RowBinding  
      TabularBinding  
            DSVTableBinding  
            QueryBinding  
            TableBinding  
      TimeAttributeBinding  
      TimeBinding  
      UserDefinedGroupBinding  
ClrAssemblyFile  
CubeAttribute  
CubeBinding (out-of-line)  
CubeDimension  
CubeDimensionPermission  
CubeHierarchy  
DataBlock  
DataItem  
DataMiningMeasureGroupDimension  
DegenerateMeasureGroupDimension  
DimensionAttribute  
EventColumn  
ManyToManyMeasureGroupDimension  
MeasureGroupAttribute  
MeasureGroupBinding (out-of-line)  
MeasureGroupDimension  
MeasureGroupHierarchy  
MiningModelColumn  
MiningModelingFlag  
MiningStructureColumn  
OlapDataSource  
Permission  
PerspectiveAction  
PerspectiveAttribute  
PerspectiveCalculation  
PerspectiveDimension  
PerspectiveHierarchy  
PerspectiveKpi  
PerspectiveMeasure  
PerspectiveMeasureGroup  
PushedDataSource  
ReferenceMeasureGroupDimension  
RegularMeasureGroupDimension  
RelationalDataSource  
ScalarMiningStructureColumn  
TableMiningStructureColumn  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)   
 [Analysis Services Scripting Language-XML-Element-Hierarchie &#40; ASSL &#41;](../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)   
 [Analysis Services Scripting Language &#40; ASSL XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
  

