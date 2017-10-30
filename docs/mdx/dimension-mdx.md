---
title: Dimension (MDX) | Microsoft Docs
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
- Dimension
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimension function
ms.assetid: 0e3ce539-1d34-45ca-8342-67796e11b730
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4d8bbf0f22d1a2370c167f2569ae388742836933
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="dimension-mdx"></a>Dimension (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Hierarchie zurück, die ein angegebenes Element, eine angegebene Ebene oder Hierarchie enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
### <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die **Dimension** -Funktion in Verbindung mit der **Namen** -Funktion verwendet, um den Hierarchienamen des angegebenen Elements zurück.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird die Dimension-Funktion in Verbindung mit der Levels- und der Count-Funktion verwendet, um die Anzahl der Ebenen in der Hierarchie zurückzugeben, die das angegebene Element enthalten.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird die **Dimension** -Funktion in Verbindung mit der **Elemente** und **Anzahl** -Funktion verwendet, um die Anzahl der Elemente in der Hierarchie, die das angegebene Element enthält zurückzugeben.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzahl &#40; Hierarchieebenen &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Anzahl &#40; Set &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Ebenen &#40; MDX &#41;](../mdx/levels-mdx.md)   
 [Mitglieder &#40; Set &#41; &#40; MDX &#41;](../mdx/members-set-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

