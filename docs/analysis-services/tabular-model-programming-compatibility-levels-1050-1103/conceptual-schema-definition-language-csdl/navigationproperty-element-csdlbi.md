---
title: NavigationProperty-Element (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 385a0859a8b0f668ed5d2c93c775a3072f9e37fa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Das NavigationProperty-Element ist ein komplexer Typ, der den CSDL-Elementtyp erweitert, um die Navigation in Business Intelligence-Datenmodellen zu unterstützen.  
  
> [!WARNING]  
>  Dieses Element dient der Berichterstellung und kann nicht geändert oder bearbeitet werden.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, die das NavigationProperty-Element definieren.  
  
|Name|Ist erforderlich|Beschreibung|  
|----------|-----------------|-----------------|  
|CollectionCaption|Nein|Der Pluralname für den Verweis auf einen Satz von Instanzen der Navigationseigenschaft.<br /><br /> Wenn dieses Attribut weggelassen wird, wird das Caption-Attribut des base-Elements verwendet.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarische**  
  
 Das folgende Beispiel zeigt eine Navigationseigenschaft in CSDLBI, Version 1.1, die die Verknüpfung zwischen der „Product SubCategory“-Tabelle und der „Product“-Tabelle beschreibt.  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>Beispiel  
 **Mehrdimensionale**  
  
 Das folgende Beispiel zeigt eine Navigationseigenschaft in CSDLBI, Version 1.1, an, die die Beziehung zwischen zwei Tabellen im Contoso-Vorgangscube beschreibt. Die Beziehung verbindet die „Bike Category“-Tabelle und die „Product Subcategory“-Tabelle.  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
