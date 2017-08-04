---
title: ': (Bereich) (MDX) | Microsoft Docs'
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
- ':'
dev_langs:
- kbMDX
helpviewer_keywords:
- ': (range operator)'
- range operator (:)
ms.assetid: f9b36aca-4efd-49b4-9e4f-12914c1b24a6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b80f453f0553404d1d337e15e9194f7d4b97ccd7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="-range-mdx"></a>: (Bereich) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt eine Mengenoperation aus, die eine natürlich geordnete Menge zurückgibt, wobei die beiden angegebenen Elemente als Endpunkte dienen und alle Elemente zwischen den beiden angegebenen Elementen als Elemente der Menge eingeschlossen werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>Parameter  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Menge, die die angegebenen Elemente und alle Elemente zwischen diesen enthält.  
  
## <a name="remarks"></a>Hinweise  
 Beide Parameter müssen Elemente in derselben Ebene und Hierarchie einer bestimmten Dimension angeben. Wenn beide Parameter dasselbe Element an, geben Sie die **: (Bereich)** -Operator eine Menge zurück, die nur das angegebene Element enthält. Wenn der erste Parameter NULL ist, enthält die Menge alle Elemente vom Anfang der Ebene des Elements, das im zweiten Parameter angegeben ist, bis einschließlich jenes Elements. Wenn der zweite Parameter NULL ist, enthält die Menge alle Elemente vom Element, das im ersten Parameter angegeben ist bis einschließlich dem letzten Element derselben Ebene.  
  
 Dieser Mengenoperator weist kein funktionelles Äquivalent in MDX auf.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung dieses Operators.  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

