---
title: Count (Hierarchieebenen) (MDX) | Microsoft Docs
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
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d3e031210ea5b19628bc11a044b5c3977c465b9a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="count-hierarchy-levels-mdx"></a>Count (Hierarchieebenen) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der Ebenen in der Hierarchie zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Gibt die Anzahl der Ebenen in einer Hierarchie zurück, ggf. einschließlich der `[All]`-Ebene.  
  
> [!IMPORTANT]  
>  Wenn eine Dimension nur eine einzige sichtbare Hierarchie enthält, kann auf die Hierarchie entweder mit dem Dimensionsnamen oder mit dem Hierarchienamen verwiesen werden, weil der Dimensionsname in seine einzige sichtbare Hierarchie aufgelöst wird. `Measures.Levels.Count` ist z. B. ein gültiger MDX-Ausdruck, weil er in die einzige vorhandene Hierarchie in der Measures-Dimension aufgelöst wird.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Anzahl der Ebenen in der benutzerdefinierten Product Categories-Hierarchie des Adventure Works-Cubes zurückgegeben.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzahl &#40; Dimension &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Anzahl &#40; Tupel &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [Anzahl &#40; Set &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

