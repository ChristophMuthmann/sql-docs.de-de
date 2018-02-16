---
title: EntitySet-Element (CSDLBI) | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ae8366ecec5bf25e1fd27a63d22ac796c080660
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="entityset-element-csdlbi"></a>EntitySet-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 **Tabellarische**  
  
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
 **Mehrdimensionale**  
  
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
  
  
