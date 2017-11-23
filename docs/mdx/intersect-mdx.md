---
title: Intersect (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: INTERSECT
dev_langs: kbMDX
helpviewer_keywords: Intersect function
ms.assetid: 0de8fbb4-e2db-480c-86f1-2abbbcfdb1d8
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5b0c893ae58a1040912366492b8cec0ddcbc4a86
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="intersect-mdx"></a>Intersect (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Schnittmenge zweier Eingabesets zurück. Optional werden doppelte Werte beibehalten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Intersect** Funktion gibt die Schnittmenge zweier Mengen zurück. Doppelte Werte werden von der Funktion standardmäßig aus den beiden Mengen entfernt, bevor die Schnittmenge gebildet wird. Die beiden angegebenen Mengen müssen dieselbe Dimensionalität haben.  
  
 Das optionale **alle** Flag werden doppelte Werte beibehalten. Wenn **alle** angegeben wird, die **Intersect** Funktion Schnittmenge Elemente wie gewohnt überschneidet, und jeder doppelte Wert in der ersten Menge, die über einen übereinstimmenden doppelten in der zweiten Menge verfügt auch überschneidet. Die beiden angegebenen Mengen müssen dieselbe Dimensionalität haben.  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage gibt die Jahre 2003 und 2004 zurück, die beiden Elemente, die in beiden angegebenen Mengen vorhanden sind:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Die folgende Abfrage schlägt fehl, da die beiden angegebenen Mengen Elemente aus verschiedenen Hierarchien enthalten:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
