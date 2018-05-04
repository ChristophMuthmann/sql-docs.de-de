---
title: Min (MDX) | Microsoft Docs
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
- MIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Min function [MDX]
ms.assetid: 9f3799c0-2502-4056-a259-053898f69b7c
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e80628b0545b03649a9b5a3edfe5e80a1f76e461
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="min-mdx"></a>Min (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Minimalwert eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben ist, wird der angegebene numerische Ausdruck über die Menge ausgewertet und anschließend der Minimalwert der Auswertung zurückgegeben. Wenn kein numerischer Ausdruck angegeben ist, wird die angegebene Menge im aktuellen Kontext der Elemente der Menge ausgewertet und anschließend der Minimalwert der Auswertung zurückgegeben.  
  
> [!NOTE]  
>  In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] werden Nullen ignoriert, wenn der kleinste Wert in einer Menge von Zahlen berechnet wird.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Minimalwert der Quartalsumsätze für jede Unterkategorie und jedes Land/jede Region im Adventure Works-Cube zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS Min   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
