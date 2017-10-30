---
title: Item (Element) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 71cca249-910b-4ecd-9097-1a17b224e219
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c2649598e6224c3458dfa0b0278df8d6458b7ce
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="item-member-mdx"></a>Item (Element) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Element aus einem angegebenen Tupel zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>Argumente  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
 *Index*  
 Ein gültiger numerischer Ausdruck, der ein bestimmtes Element über die Position im zurückzugebenden Tupel angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Element** Funktion gibt ein Element aus dem angegebenen Tupel zurück. Die Funktion gibt das Element finden Sie unter der vom angegebenen nullbasierten Position *Index*.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Element `[2003]` auf Spalten zurückgegeben - das erste Element im Tupel `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).`:  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

