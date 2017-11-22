---
title: Median (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEDIAN
dev_langs: kbMDX
helpviewer_keywords: Median function
ms.assetid: 7a326a3f-0123-45c4-9b18-31f83b90d986
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 44e92801c99d7ca2990d656fda13b395a9b0229b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="median-mdx"></a>Median (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
