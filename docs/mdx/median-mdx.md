---
title: Median (MDX) | Microsoft Docs
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
- MEDIAN
dev_langs:
- kbMDX
helpviewer_keywords:
- Median function
ms.assetid: 7a326a3f-0123-45c4-9b18-31f83b90d986
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dbe31042708d3c4cb4f78c4f5cc291ecf5684a33
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="median-mdx"></a>Median (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Median eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben ist, wird der angegebene numerische Ausdruck über die Menge ausgewertet und anschließend der Median der Auswertung zurückgegeben. Wenn kein numerischer Ausdruck angegeben ist, wird die angegebene Menge im aktuellen Kontext der Elemente der Menge ausgewertet und anschließend der Median der Auswertung zurückgegeben.  
  
 Der Median stellt den mittleren Wert in einer Menge geordneter Zahlen dar. (Der Median unterscheidet sich vom Mittelwert, der die Summe einer Menge von Zahlen, dividiert durch die Anzahl der Zahlen in der Menge darstellt.) Der Median wird folgendermaßen bestimmt: Es wird der kleinste Wert gewählt, für den gilt, dass mindestens die Hälfte der Werte in der Menge nicht größer als der gewählte Wert sind. Ist die Anzahl der Werte in der Menge eine ungerade Zahl, entspricht der Median einem einzelnen Wert. Ist die Anzahl der Werte in der Menge eine gerade Zahl, entspricht der Median der Summe der beiden mittleren Werte, dividiert durch zwei.  
  
> [!NOTE]  
>  In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] werden Nullen ignoriert, wenn der Median in einer Menge geordneter Zahlen berechnet wird.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Median der Monatsumsätze für jedes Quartal, jede Unterkategorie und jedes Land/jede Region im Adventure Works-Cube zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS Median   
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
  
  
