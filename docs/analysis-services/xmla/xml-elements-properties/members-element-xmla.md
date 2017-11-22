---
title: Members-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Members Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords: Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d2b4f8a9c466fa85bdd1131a58c2c11fc232967
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="members-element-xmla"></a>Members-Element (XMLA)
  Enthält eine Auflistung von [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) vom übergeordneten Element enthaltenen Elemente [CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
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
|Übergeordnete Elemente|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|Untergeordnete Elemente|[Datenmember](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|Hierarchy|Erforderliches **String** -Attribut. Der Name der Hierarchie, der die Elemente, durch enthält, die **Elemente** Element gehören.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Clientanwendung legt die **AxisFormat** Eigenschaft, um *' Clusterformat '*, die Elemente auf jeder Achse in Cluster in der jeder Cluster ein Kreuzprodukt geordneten Mengen an darstellt unterteilt Elemente aus jeder Hierarchie. Jede **Achse** Element besteht aus einem oder mehreren **CrossProduct** Elemente. Jede **CrossProduct** Element enthält eine **Elemente** -Element für jede Hierarchie auf der Achse. Die **Elemente** -Element wiederum enthält ein **Member** -Element für jedes Mitglied in das Kreuzprodukt enthaltenen Hierarchie.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die Struktur der **Mitglieder** -Element, wenn ein Client angibt, *' Clusterformat '* für die **AxisFormat** angegebene XMLA-Eigenschaft der folgende Elemente für die Achse:  
  
||||||  
|-|-|-|-|-|  
|**Time**-Hierarchie|1999|1999|2000|2001|  
|**Category**-Hierarchie|Tatsächlich|Budget|Budget|Budget|  
|Clusters|Cluster 1|Cluster 1|Cluster 1|Cluster 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
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
      <CrossProduct Size = "1">  
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
  
  
