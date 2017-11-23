---
title: Mithilfe von Dimensions-, Hierarchie- und Ebenenfunktionen | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0138b030823990b0bb5ec052ab8791f7ac3e5879
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Verwenden von Dimensions-, Hierarchie- und Ebenenfunktionen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit Dimensions-, Hierarchie- und Ebenenfunktionen lassen sich die mehrdimensionalen Strukturen traversieren, die in Analysis Services zu finden sind. Üblicherweise verwenden Sie solche Funktionen zusammen mit anderen Funktionen dazu, Informationen zu den Elementen einer Dimension, Hierarchie oder Ebene abzurufen.  
  
 Das folgende Beispiel zeigt, wie Sie die **. Dimension**, **. Hierarchie**, und **. Ebene** Funktionen:  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [Dimension &#40; MDX &#41;](../mdx/dimension-mdx.md)   
 [Funktionen &#40; MDX-Syntax &#41;](../mdx/functions-mdx-syntax.md)   
 [Hierarchie &#40; MDX &#41;](../mdx/hierarchy-mdx.md)   
 [Level &#40; MDX &#41;](../mdx/level-mdx.md)  
  
  
