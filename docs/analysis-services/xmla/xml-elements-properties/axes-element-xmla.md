---
title: Axes-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Axes Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords: Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d8e1f992cd7cf9a6aceb1490d78aa0fba49b7758
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="axes-element-xmla"></a>Axes-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Enthält eine Auflistung von [Achse](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) Elemente Achsendaten enthalten sind, eine [Root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element, das verwendet die [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) -Datentyp.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Any|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Untergeordnete Elemente|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Unter den **Achsen** Element, das **Achse** Elemente in der Reihenfolge im Dataset, beginnend mit NULL Auftretens aufgeführt sind. Die **AxisFormat** XMLA-eigenschafteneinstellung bestimmt wie **Achse** -Elemente formatiert werden. Weitere Informationen zu den **AxisFormat** Eigenschaft finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Eine Achse stellt eine Menge von Tupeln dar, in der alle Tupel die gleiche Dimensionalität aufweisen. Eine Menge kann auf verschiedene Weisen dargestellt werden, die unterschiedliche Vorteile bieten. Beispielsweise kann die folgende Menge aus vier Tupeln als Auflistung zweidimensionaler Tupel oder als kartesisches Produkt zweidimensionaler Mengen dargestellt werden.  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|Tatsächlich|Budget|Tatsächlich|Budget|  
  
 Diese Menge aus Tupeln kann als Auflistung zweidimensionaler Tupel dargestellt werden:  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 Diese Menge kann auch als kartesisches Produkt zwei eindimensionaler Mengen dargestellt werden:  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 Die erste Darstellung, zweidimensionale Tupel, ist für die Verwendung durch Clienttools besser geeignet. Die zweite Darstellung, ein kartesisches Produkt eindimensionaler Mengen, verbraucht weniger Speicherplatz und erhält die mehrdimensionale Eigenschaft der Menge.  
  
 In der folgenden Tabelle sind Vorgänge aufgelistet, die zum Definieren und Charakterisieren der Struktur und der Elemente einer Achse verwendet werden können.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|Member|Die kleinste Einheit einer Achse, die das Element einer Dimensionshierarchie darstellt.|  
|Member|Eine Auflistung von **Member** Objekte aus der gleichen Dimensionshierarchie.|  
|Tupel|Eine Auflistung von Elementen anderer Dimensionshierarchien.|  
|Tupel|Eine Auflistung von **Tupel** Objekte mit der gleichen Dimensionalität.|  
|Union|Eine Vereinigung von Sätzen.|  
|CrossJoin|Ein kartesisches Produkt von Mengen.|  
  
 Diese Vorgänge übersetzen die zweidimensionalen Tupel und das kartesische Produkt eindimensionaler Mengen wie folgt:  
  
## <a name="two-dimensional-tuples"></a>Zweidimensionale Tupel  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>Kartesisches Produkt eindimensionaler Mengen  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 Kann ein Client verwenden die **AxisFormat** Eigenschaft, um eine bestimmte Darstellung anzufordern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDDataSet-Datentyp &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
