---
title: Aktuelle (MDX) | Microsoft Docs
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
- CURRENT
dev_langs:
- kbMDX
helpviewer_keywords:
- Current function
ms.assetid: 6f689742-f9b6-4339-a691-31ff28582c36
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0e12e6549e02161589c769610625c82243decd17
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="current-mdx"></a>Current (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das aktuelle Tupel in einer Menge während einer Iteration zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Bei jedem Schritt einer Iteration ist das gerade bearbeitete Tupel das aktuelle Tupel. Die **aktuelle** Funktion gibt dieses Tupel zurück. Diese Funktion ist nur während einer Iteration über eine Menge gültig.  
  
 MDX-Funktionen, die einen Satz durchlaufen enthalten die [generieren](../mdx/generate-mdx.md) Funktion.  
  
> [!NOTE]  
>  Diese Funktion ist nur mit benannten Mengen ausführbar, d. h. beim Verwenden eines Mengen-Alias oder Definieren einer benannten Menge.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie Sie die **aktuelle** -Funktion **generieren**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

