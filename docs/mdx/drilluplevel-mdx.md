---
title: DrillupLevel (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLUPLEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a59de1459ecc5953b4612c64603eff958049e3e6
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen Drillup bei Elementen einer Menge aus, die sich unterhalb einer angegebenen Ebene befinden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **DrillupLevel** Funktion gibt eine Menge von Elementen hierarchisch organisiert basierend auf den Elementen in der angegebenen Menge. Die Reihenfolge der Elemente in der angegebenen Menge wird beibehalten.  
  
 Wenn ein Ebenenausdruck angegeben wird, die **DrillupLevel** Funktion erstellt die Menge, indem nur die Elemente, die über der angegebenen Ebene abgerufen. Wenn ein Mengenausdruck angegeben ist und kein Element der angegebenen Ebene in der angegebenen Menge vorhanden ist, wird die angegebene Menge zurückgegeben.  
  
 Wenn kein Ebenenausdruck angegeben wird, erstellt die Funktion die Menge, indem nur die Elemente eine Ebene über der untersten Ebene der ersten Dimension abgerufen werden, auf die in der angegebenen Menge verwiesen wird.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Menge der Elemente oberhalb der Subcategory-Ebene aus der ersten Menge zurückgegeben.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

