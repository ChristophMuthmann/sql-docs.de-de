---
title: WTD (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- WTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Wtd function
ms.assetid: 41066e1b-e802-4582-be4b-3ed7807b033e
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 83fc733e36f6e68674d3f32b47087090499cf7cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="wtd-mdx"></a>Wtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Menge von gleichgeordneten Elementen zurück, die derselben Ebene angehören wie ein angegebenes Element. Die Menge beginnt mit dem ersten gleichgeordneten Element und endet mit dem angegebenen Element, entsprechend der Einschränkung durch die Week-Ebene in der Time-Dimension.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Elementausdruck nicht angegeben ist, wird die Standardeinstellung ist das aktuelle Element der ersten Hierarchie mit einer Ebene des Typs Wochen, in der ersten Dimension des Typs Zeit (**Time.CurrentMember**) in der Measuregruppe.  
  
 Die **Wtd** Funktion ist eine Verknüpfungsfunktion für die [PeriodsToDate](../mdx/periodstodate-mdx.md) Funktion, auf die Ebene festgelegt ist *Wochen*. Somit ist `Wtd(Member_Expression)` äquivalent zu `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Siehe auch  
 [QTD &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [MTd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [YTD &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
