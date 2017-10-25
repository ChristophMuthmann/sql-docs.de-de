---
title: CrossProduct-Element (XMLA) | Microsoft Docs
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
- CrossProduct Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a407c545fb4cc09b19a7b11c9e24a12c7f77c8b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="crossproduct-element-xmla"></a>CrossProduct-Element (XMLA)
  Enthält ein Kreuzprodukt geordneten Mengen an Elementen aus jeder Hierarchie für eine [Achse](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) Element, das verwendet die [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) von zurückgegebener Datentyp der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Axis>  
   ...  
   <CrossProduct Size="integer">  
      <Members>...</Members>  
   </CrossProduct>  
   ...  
</Axis>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|Untergeordnete Elemente|[Elemente](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Description|  
|---------------|-----------------|  
|Größe|Erforderliche **Ganzzahl** Attribut. Gibt die Anzahl von Tupeln in das Kreuzprodukt, dargestellt durch die **CrossProduct** Element.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Clientanwendung legt die **AxisFormat** Eigenschaft, um *' Clusterformat '*, die Elemente auf jeder Achse in Cluster in der jeder Cluster ein Kreuzprodukt geordneten Mengen an darstellt unterteilt Elemente aus jeder Hierarchie. Jeder Cluster wird dargestellt, durch eine **CrossProduct** Element. Jede **CrossProduct** Element enthält eine **Elemente** -Element für jede Hierarchie auf der Achse. Ein **CrossProduct** Element kann Elemente aus einer einzelnen Hierarchie enthalten.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die Struktur der **CrossProduct** -Element, wenn ein Client angibt, *' Clusterformat '* für die **AxisFormat** angegebene XMLA-Eigenschaft der folgende Elemente für die Achse:  
  
||||||  
|-|-|-|-|-|  
|**Time**-Hierarchie|1999|1999|2000|2001|  
|**Category**-Hierarchie|Tatsächlich|Budget|Budget|Budget|  
|Clusters|Cluster 1|Cluster 1|Cluster 1|Cluster 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size="4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size="1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

