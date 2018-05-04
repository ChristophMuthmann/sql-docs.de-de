---
title: Tuples-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Tuples Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords:
- Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4eed093e987af9cb58497caa317f796aa4fcf8a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tuples-element-xmla"></a>Tuples-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält eine Reihe von [Tupel](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md) von Objekten für die ein [Achse](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) Element, das verwendet die [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) von zurückgegebener Datentyp der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Axis>  
   ...  
   <Tuples>  
      <Tuple>...</Tuple>  
   </Tuples>  
   ...  
</Axis>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Achse](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|Untergeordnete Elemente|[Tupel](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Clientanwendung die **AxisFormat**-Eigenschaft auf *TupleFormat* festlegt, wird eine Achse als Menge von Tupeln dargestellt. Jedes **Axis**-Element enthält ein **Tuples**-Element, das die Menge von Tupeln auf dieser Achse darstellt. Jedes Tupel wird mithilfe eines **Tuple**-Elements dargestellt, das [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)-Elemente aus jeder Hierarchie auf der Achse enthält.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die Struktur der **Tupel** -Element, wenn ein Client angibt, *' TupleFormat '* oder *CustomFormat* für die **AxisFormat**  XML for Analysis (XMLA)-Eigenschaft, wobei die folgenden Elemente für die Achse:  
  
|||||  
|-|-|-|-|  
|**Time**-Hierarchie|1999|1999|2000|  
|**Category**-Hierarchie|Tatsächlich|Budget|Budget|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
