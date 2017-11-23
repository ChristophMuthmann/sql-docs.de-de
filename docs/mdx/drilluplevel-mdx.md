---
title: DrillupLevel (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLUPLEVEL
dev_langs: kbMDX
helpviewer_keywords: DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5b17f352e31fe3cb08a2ca2af629cf9cde1bc08f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
