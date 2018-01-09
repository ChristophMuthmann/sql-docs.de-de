---
title: TopPercent (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: TOPPERCENT
dev_langs: kbMDX
helpviewer_keywords: TopPercent function
ms.assetid: a40cfbb8-5bf4-4ae2-8686-df9a07206d56
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 44e35ecb045336b826bbf1cecef01e9f2a42dea6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sortiert eine Menge in absteigender Reihenfolge und gibt eine Menge von Tupeln mit den höchsten Werten zurück, deren kumulativer Gesamtwert größer oder gleich einem angegebenen Prozentsatz ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Prozentsatz*  
 Ein gültiger numerischer Ausdruck, der den Prozentsatz der zurückzugebenden Tupel angibt.  
  
> [!IMPORTANT]  
>  *Prozentsatz* muss ein positiver Wert; werden negative Werte ein Fehler generiert.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Die **TopPercent** -Funktion berechnet die Summe der angegebenen numerischen Ausdrucks, ausgewertet über die angegebene Menge, die Menge in absteigender Reihenfolge sortiert. Anschließend gibt die Funktion die Elemente mit den höchsten Werten zurück, deren kumulativer Prozentsatz vom Gesamtwert mindestens dem angegebenen Prozentsatz entspricht. Diese Funktion gibt die kleinste Teilmenge einer Menge zurück, deren kumulativer Gesamtwert mindestens dem angegebenen Prozentsatz entspricht. Die zurückgegebenen Elemente werden der Größe nach absteigend sortiert.  
  
> [!WARNING]  
>  Wenn *numerischer_ausdruck* gibt einen negativen Wert **TopPercent** gibt nur ein (1) Zeile zurück.  
>   
>  Im zweiten Beispiel wird dieses Verhalten ausführlicher veranschaulicht.  
  
> [!IMPORTANT]  
>  Wie die [BottomPercent](../mdx/bottompercent-mdx.md) -Funktion, die **TopPercent** Funktion immer die Hierarchie unterbrochen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden die Orte zurückgegeben, in denen der Wiederverkäufer die ersten 10 % seines Umsatzes in der Kategorie Bike erzielt hat. Das Ergebnis wird in absteigender Reihenfolge sortiert und beginnt mit dem Ort mit dem höchsten Umsatzwert.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 Der vorangehende Ausdruck generiert die folgenden Ergebnisse:  
  
||Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3,508,904.84|  
|London|$1,521,530.09|  
|Seattle|$1,209,418.16|  
|Paris|$1,170,425.18|  
  
 Der ursprüngliche Datensatz kann mit der folgenden Abfrage abgerufen werden und gibt 588 Zeilen zurück:  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
## <a name="example"></a>Beispiel  
 Die folgende exemplarische Vorgehensweise wird verdeutlichen die Auswirkungen negative Werte in der *Numeric_Expression*. Zuerst muss ein Kontext erzeugt werden, in dem das Verhalten demonstriert werden kann.  
  
 Die folgende Abfrage gibt eine Tabelle mit Werten für Sales Amount, Total Product Cost und Gross Profit für den Wiederverkäufer zurück. Die Tabelle ist in absteigender Reihenfolge nach Gewinnen sortiert. Da nur negative Gewinnwerte vorhanden sind, wird der geringste Verlust zuoberst angezeigt.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 Die oben aufgeführte Abfrage gibt die folgenden Ergebnisse zurück. Zeilen im mittleren Abschnitt wurden entfernt, um die Lesbarkeit zu verbessern.  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157,444.56|$163,112.57|($5,668.01)|  
|Touring-2000 Blau, 46|$321,027.03|$333,021.50|($11,994.47)|  
|Touring-3000 Blau, 62|$87,773.61|$100,133.52|($12,359.91)|  
|…|…|…|…|  
|Touring-1000 Gelb, 46|$1,016,312.83|$1,234,454.27|($218,141.44)|  
|Touring-1000 Yellow, 60|$1,184,363.30|$1,443,407.51|($259,044.21)|  
  
 Wenn Sie nun die ersten 100 % in der Kategorie Bikes nach Gewinn ermitteln müssten, würden Sie eine mit der folgenden vergleichbare Abfrage schreiben:  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 Beachten Sie, dass in der Abfrage einhundert Prozent (100 %) angefordert werden. Dies bedeutet, dass alle Zeilen zurückgegeben werden sollten. Jedoch, da es negative Werte in der *Numeric_Expression* , wird nur eine Zeile zurückgegeben.  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157,444.56|$163,112.57|($5,668.01)|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
