---
title: DisplayKey-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ea38abe670eb7585a8f0b6286f8ffa059d6a4457
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="displaykey-element-csdlbi"></a>DisplayKey-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das DisplayKey-Element enthält eine Liste der folgenden Elemente, die einen starken Bezeichner bilden. DisplayKey ist nur als untergeordnetes Element des EntityType-Elements vorhanden. Das Element kann auf Spalten- oder Rollenenden verweisen.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle werden die im DisplayKey-Element enthaltenen Attribute aufgelistet.  
  
|Name|Ist erforderlich|Beschreibung|  
|----------|-----------------|-----------------|  
|IsDisplayKey|Nein|True oder False|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element ist für Berichte bestimmt. Das Element, auf das Sie dieses Attribut anwenden, muss nicht der tatsächliche Tabellenschlüssel sein, sondern kann einem Element entsprechen, das Sie als Schlüssel darstellen. Allerdings muss die Spalte, die Sie für DisplayKey verwenden, eindeutige Werte enthalten.  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Im folgenden Beispiel wird in CSDLBI, Version 1.1, eine Spalte im AdventureWorks-Beispieldatenmodell veranschaulicht, die als DisplayKey für die Tabelle festgelegt wurde.  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Im folgenden Beispiel wird in CSDLBI, Version 1.1, ein Auszug aus der Darstellung des Contoso-Vorgangscube veranschaulicht. In diesem Modell ist die Spalte „Color“ als Anzeigeschlüssel für die Tabelle „Bikes“ gekennzeichnet.  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI-Konzepte](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  
