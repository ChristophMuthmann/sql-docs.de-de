---
title: SetToStr (MDX) | Microsoft Docs
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
- SETTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToStr function
ms.assetid: b761e002-26cd-460e-b424-fb8e306746fa
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e0a2db653917d53ac25c290bd6dc14f3afe2cd09
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="settostr-mdx"></a>SetToStr (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeichenfolge im MDX-Format (Multidimensional Expressions) zurück, die einer angegebenen Menge entspricht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion wird zum Übertragen der Zeichenfolgendarstellung einer Menge an eine externe Funktion zur Analyse verwendet. Die Zeichenfolge, die zurückgegeben wird, wird in geschweifte Klammern {} eingeschlossen, wobei die einzelnen Elemente durch ein Komma getrennt werden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Zeichenfolge zurückgegeben, die alle Elemente der Geography.Country-Attributhierarchie enthält.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

