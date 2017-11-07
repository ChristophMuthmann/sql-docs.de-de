---
title: MeasureGroupBinding-Datentyp (Out-of-Line) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupBinding
helpviewer_keywords:
- MeasureGroupBinding data type
ms.assetid: e6c65597-89ac-457e-a0e5-01d85449a1b7
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2db6edd7c86ad9d233aa6002c77b4c2b2371d7dc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroupbinding-data-type-out-of-line-assl"></a>MeasureGroupBinding-Datentyp (Out-of-Line) (ASSL)
  Definiert einen Grunddatentyp, der eine Bindung mit einer Measuregruppe darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MeasureGroupBinding>  
   <ID>...</ID>  
   <Source>...</Source>  
   <EstimatedRows>...</EstimatedRows>  
   <Dimensions>...</Dimensions>  
   <Measures>...</Measures>  
      <Partitions>...</Partitions>  
</MeasureGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Dimensionen](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Measures](../../../analysis-services/scripting/collections/measures-element-assl.md), [Partitionen](../../../analysis-services/scripting/collections/partitions-element-assl.md), [Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|Abgeleitete Elemente|Finden Sie unter [binden](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen finden Sie im Abschnitt Out of Line-Bindungen [Datenquellen und Bindungen & #40; SSAS – mehrdimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

