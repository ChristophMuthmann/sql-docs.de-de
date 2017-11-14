---
title: EntitySet-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e48f4d90853e954618d770feda70c4a72d0f607a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="entityset-element-csdlbi"></a>EntitySet-Element (CSDLBI)
  Das EntitySet-Element definiert eine Auflistung von Entitäten eines bestimmten Typs in einem CSDLBI-Datenmodell.  
  
 Das EntitySet muss jeden der Entitätstypen angeben, die im Datenmodell enthalten sind. Informationen zu diesen Modellentitäten werden anhand der Auflistung von untergeordneten Entitäten des Typs (Entitätselement) angegeben. Weitere Informationen finden Sie unter [EntityType-Element &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Eigenschaften wie Sortierung und Sprache werden auf der EntityContainer-Ebene und nicht auf Ebene einzelner Objekte definiert. Spalten und Textattribute innerhalb des Modells können jedoch über Beschriftungen oder Übersetzungen in anderen Sprachen verfügen.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgelistet, die ein EntitySet definieren.  
  
|Attributname|Ist erforderlich|Description|  
|--------------------|-----------------|-----------------|  
|Beschriftung|Nein|Eine benutzerfreundliche Beschreibung der Entitätenmenge.|  
|CollectionCaption|Nein|Eine Zeichenfolge, die den Namen der Entität im Plural enthält.|  
|ReferenceName|Nein|Enthält den nicht zusammengeführten und vollqualifizierten Namen der Entität. In einem mehrdimensionalen Modell entspricht dies dem CubeDimensions-Namen.|  
|Hidden|Nein|Gibt an, ob das die Entität ausgeblendet ist. Standardmäßig werden Entitäten nicht ausgeblendet.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Im folgenden Beispiel werden die Definitionen der Date- und der Geography-Tabelle aus dem tabellarischen AdventureWorks-Modell in CSDLBI, Version 1.1, veranschaulicht.  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Im folgenden Beispiel werden einige EntitySet-Elemente aus dem Contoso Retail Operations-Cube in CSDLBI, Version 1.1, veranschaulicht.  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Technische Referenz für BI-Anmerkungen zu CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

