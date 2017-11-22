---
title: MeasureGroupID-Element (ASSL) | Microsoft Docs
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
apiname: MeasureGroupID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MeasureGroupID
helpviewer_keywords: MeasureGroupID element
ms.assetid: 3b075f86-dbbc-4285-8d2d-61fa722181c7
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fad98c2acc4873721a30a22fd1ee14a871b0d0b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="measuregroupid-element-assl"></a>MeasureGroupID-Element (ASSL)
  Ordnet eine [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) mit dem übergeordneten Element, Bindung oder Out-of-Line-Bindung.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ManyToManyMeasureGroupDimension> <!-- or MeasureGroupAttributeBinding, MeasureGroupBinding, PerspectiveMeasureGroup -->  
   ...  
   <MeasureGroupID>...</MeasureGroupID>  
   ...  
</ManyToManyMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Cardinality|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Cardinality|  
|------------------------|-----------------|  
|[ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)|0-1: Optionales Element, das nur einmal auftreten kann.|  
|[MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md) und [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die Elemente, die den übergeordneten Elementen von entsprechen **MeasureGroupID** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.ManyToManyMeasureGroupDimension>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding>, und <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
