---
title: Verwenden von logischen Funktionen | Microsoft Docs
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
dev_langs: kbMDX
helpviewer_keywords: logical functions [MDX]
ms.assetid: 0cb34d53-9146-4924-9c9b-607afcb7a2be
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a752a7af9a1c24fa600adfbf969f99f5176acbde
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="using-logical-functions"></a>Verwenden von logischen Funktionen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Eine logische Funktion führt eine logische Operation oder einen logischen Vergleich für Objekte sowie Ausdrücke aus und gibt einen booleschen Wert zurück. Logische Funktionen sind in MDX (Multidimensional Expressions) unverzichtbar, um die Position eines Elements zu ermitteln.  
  
 Die am häufigsten verwendete logische Funktion ist die **IsEmpty** Funktion. Weitere Informationen zum Verwenden der **IsEmpty** funktionieren, finden Sie unter [arbeiten mit leeren Werten](../mdx/working-with-empty-values.md).  
  
 Die folgende Abfrage zeigt, wie die **IsLeaf** und **IsAncestor** Funktionen:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; MDX-Syntax &#41;](../mdx/functions-mdx-syntax.md)  
  
  
