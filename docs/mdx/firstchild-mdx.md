---
title: FirstChild (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: FIRSTCHILD
dev_langs: kbMDX
helpviewer_keywords: FirstChild function
ms.assetid: 3c19a169-7658-4b31-93a9-85f74225ba05
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f39317291f1b7423eb6b151112ea5a2bfac75347
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="firstchild-mdx"></a>FirstChild (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das erste untergeordnete Element eines angegebenen Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.FirstChild   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
### <a name="example"></a>Beispiel  
 Die folgende Abfrage gibt das erste untergeordnete Element von Fiscal Year 2003 in der Fiscal-Hierarchie zurück, d. h. das erste Semester von Fiscal Year 2003.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [LastChild &#40; MDX &#41;](../mdx/lastchild-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
