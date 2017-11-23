---
title: Count (Dimension) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 4b9c52f6-5bb0-401a-947c-e14134558b4a
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fce9b0bde39c81536754966734678e639a456f20
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="count-dimension-mdx"></a>Count (Dimension) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der Hierarchien in einem Cube zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Hinweise  
 Gibt die Anzahl der Hierarchien in einem Cube zurück, einschließlich der `[Measures].[Measures]`-Hierarchie.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Anzahl der Hierarchien im Adventure Works-Cube zurückgegeben.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzahl &#40; Tupel &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [Anzahl &#40; Hierarchieebenen &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Anzahl &#40; Set &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
