---
title: Analysis Services-Objekttypcodes in ablaufverfolgungen verwendete | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e4119db1-4a41-4335-9b33-f1ea95564300
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cd17ad086169a53673d7c9ba48f79058dd87769d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>In Ablaufverfolgungen verwendete Analysis Services-Objekttypcodes
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Diese Seite enthält den Objekttyp (eine Zahl mit sechs Ziffern) der einzelnen Objekte in einem Analysis Services-Datenmodell. Diese Codes werden in Ablaufverfolgungsprotokollen angezeigt und dienen der Identifizierung des Objekttyps, dem eine bestimmte Sperre zugeordnet ist. Angenommen, ein Sperrtimeout in einer Datenbank zeigt den Objekttyp 100002 an, der der Datenbank-Objekttyp ist.  
  
> [!NOTE]  
>  Unten werden weitere Codes aufgeführt. Im Ablaufverfolgungsprotokoll werden tatsächlich weniger Codes angezeigt. Die folgende umfassende Liste beinhaltet Codetypen für jedes Objekt. Allerdings stellen nur solche Objekte, die eine Sperre annehmen, einen Objekttypcode in einem Ablaufverfolgungsprotokoll dar.  
  
## <a name="object-type-reference"></a>Referenz des Objekttyps  
  
|Objekttyp|Objektname|  
|-----------------|-----------------|  
|100000|Server|  
|100001|Befehl|  
|100002|Datenbank|  
|100003|DataSource|  
|100004|DatabasePermission|  
|100005|-Rolle|  
|100006|Dimension|  
|100007|DimensionAttribute|  
|100008|Hierarchy|  
|100009|Ebene|  
|100010|Cube|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|Measuregruppe|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|Measure|  
|100021|Partition|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|Aggregation|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|MiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|Assembly|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|Ablaufverfolgung|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Befehl|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|Perspektive|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DatabasePermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  
