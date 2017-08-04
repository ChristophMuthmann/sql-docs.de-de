---
title: Kommentar (MDX) | Microsoft Docs
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
- '*/'
- /*
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- /*...*/ (comment)
ms.assetid: 64434ae4-80ce-4634-86b8-4125dfaa7f61
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fca15a526cbd5329c8116e751bda4959a46e1713
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="comment-mdx"></a>Kommentar (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt vom Benutzer bereitgestellten Kommentartext an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parameter  
 *Comment_Text*  
 Die Zeichenfolge, die den Text des Kommentars enthält.  
  
## <a name="remarks"></a>Hinweise  
 Der Server wertet nicht den Text zwischen den Kommentarzeichen / * und \*/. Kommentare können sowohl in einer eigenen Zeile als auch innerhalb einer MDX-Anweisung (Multidimensional Expressions) eingefügt werden. Mehrzeilige Kommentare müssen angegeben werden, indem Sie /\* und \*/.  
  
 Es gibt keine Maximallänge für Kommentare. Kommentare können geschachtelt sein; so ist `/* Test /*Comment*/ Text*/` ein Beispiel für einen geschachtelten Kommentar.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung dieses Operators.  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [&#40; Kommentar &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40; Kommentar &#41; &#40; MDX &#41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

