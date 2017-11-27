---
title: Extrahieren (MDX) | Microsoft Docs
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
- EXTRACT
dev_langs:
- kbMDX
helpviewer_keywords:
- Extract function
ms.assetid: c0d27d31-e36e-4b7f-bb86-1e4707351392
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0e18c7ac7dcf37ce41bc7917c9d7170a815c1f58
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="extract-mdx"></a>Extract (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Menge von Tupeln aus extrahierten Hierarchieelementen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Hierarchy_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
 *Hierarchy_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **extrahieren** -Funktion eine Menge, die aus Tupeln aus den extrahierten Hierarchieelementen besteht zurück. Zu jedem Tupel in der angegebenen Menge werden die Elemente der angegebenen Hierarchien in neue Tupel im Resultset extrahiert. Doppelte Tupel werden von der Funktion immer entfernt.  
  
 Die **extrahieren** Funktion führt die umkehraktion der [Crossjoin](../mdx/crossjoin-mdx.md) Funktion.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage zeigt, wie die **extrahieren** Funktion für eine Menge von Tupeln, die zurückgegeben werden, indem Sie die **NonEmpty** Funktion:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

