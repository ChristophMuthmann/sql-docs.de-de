---
title: --(Kommentar) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: --
dev_langs: kbMDX
helpviewer_keywords:
- commenting characters
- -- (comment character)
ms.assetid: 02aec133-6809-4829-b9a2-102c376e21da
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8ec94e2553e55d7d4f3806a3ca548e7379f3bdd3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="comment---mdx-operator-reference"></a>Comment - MDX-Operatorreferenz
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt vom Benutzer bereitgestellten Kommentartext an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parameter  
 *Comment_Text*  
 Die Zeichenfolge, die den Text des Kommentars enthält.  
  
## <a name="remarks"></a>Hinweise  
 Kommentare können in einer eigenen Zeile, geschachtelt am Ende einer MDX-Skriptzeile (Multidimensional Expressions) oder geschachtelt in einer MDX-Anweisung eingefügt werden. Der Kommentar wird vom Server nicht ausgewertet.  
  
 Verwenden Sie diesen Operator für einzeilige oder geschachtelte Kommentare. Kommentare, die mit -- eingefügt werden, sind vom Zeilenschaltzeichen begrenzt.  
  
 Es gibt keine Maximallänge für Kommentare.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung dieses Operators.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Kommentar &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40; Kommentar &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
