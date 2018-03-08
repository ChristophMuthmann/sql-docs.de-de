---
title: ValueColumn-Element (ASSL) | Microsoft Docs
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
apiname: ValueColumn Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a3dab1859f50e4f2806ac46ce24a07f77a21305f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="valuecolumn-element-assl"></a>ValueColumn-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifiziert die Spalte, die den Wert des übergeordneten Elements bereitstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Standardwert|Variiert (siehe Hinweise)|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Wenn die [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md) Element des **DimensionAttribute** angegeben wird, die gleiche **DataItem** Werte dienen als Standardwerte für die **ValueColumn** Element. Wenn die **NameColumn** Element des **DimensionAttribute** nicht angegeben wird und die [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) Auflistung von **DimensionAttribute** enthält ein einziges [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) Element, das eine Schlüsselspalte mit einem Zeichenfolgen-Datentyp, der darstellt **DataItem** Werte dienen als Standardwerte für die **ValueColumn** Element.  
  
 Weitere Informationen zu den **DataItem** Typ, einschließlich einer Tabelle von Analysis Services Scripting Language (ASSL)-Objekten und Eigenschaften der **DataItem** finden Sie unter [DataItem-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **NameColumn** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.DimensionAttribute> und <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
