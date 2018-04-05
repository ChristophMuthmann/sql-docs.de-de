---
title: IsGeneration (MDX) | Microsoft Docs
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
- ISGENERATION
dev_langs:
- kbMDX
helpviewer_keywords:
- IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d1b73679fed735599104dd3588d298602e48d3e7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt zurück, ob sich ein angegebenes Element in einer angegebenen Generation befindet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Generation_Number*  
 Ein gültiger numerischer Ausdruck, der die Generierung angibt, für die das angegebene Element ausgewertet wird.  
  
## <a name="remarks"></a>Remarks  
 Die **IsGeneration** -Funktion gibt **"true"** , wenn das angegebene Element in der angegebenen Generierungsnummer befindet. Die Funktion hingegen gibt **"false"**. Auch, wenn das angegebene Element zu einem leeren Element ausgewertet wird die **IsGeneration** -Funktion gibt **"false"**.  
  
 Für die Zwecke der Generierungsindizierung haben Blattelemente den Generierungsindex 0. Der Generationsindex von Nichtblattelementen wird bestimmt, indem zuerst der höchste Generationsindex aus der Vereinigung aller untergeordneten Elemente des angegebenen Elements abgerufen wird und dann 1 zu diesem Index addiert wird. Aufgrund der Bestimmungsweise des Generationsindexes von Nichtblattelementen kann es vorkommen, dass ein bestimmtes Nichtblattelement mehreren Generationen angehört.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird TRUE zurückgegeben, wenn [Date].[Fiscal].CurrentMember Teil der zweiten Generierung ist:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
