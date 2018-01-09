---
title: NavigationProperty-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b004e611448db0100186a9f6d7fa9812d3de9c15
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das NavigationProperty-Element ist ein komplexer Typ, der sich die CSDL-Elementtyp, um die Navigation in Business Intelligence-Datenmodelle unterstützen erstreckt.  
  
> [!WARNING]  
>  Dieses Element dient der Berichterstellung und kann nicht geändert oder bearbeitet werden.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, die das NavigationProperty-Element definieren.  
  
|Name|Ist erforderlich|Description|  
|----------|-----------------|-----------------|  
|CollectionCaption|nein|Der Pluralname für den Verweis auf einen Satz von Instanzen der Navigationseigenschaft.<br /><br /> Wenn dieses Attribut weggelassen wird, wird das Caption-Attribut des base-Elements verwendet.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
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
 **Multidimensional**  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Informationen zum tabellarischen Objektmodell auf Kompatibilität Ebenen 1050 bis 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
