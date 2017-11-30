---
title: Generieren von (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: GENERATE
dev_langs: kbMDX
helpviewer_keywords: Generate function
ms.assetid: 696a229d-c2f1-47b7-9dca-7b0a6b547d9b
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4ef13a4355c73458023c7d11663587a771d71c23
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="generate-mdx"></a>Generate (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Wendet eine Menge auf jedes Element einer anderen Menge an und verknüpft dann die entstehenden Mengen durch den Vereinigungsoperator. Alternativ gibt die Funktion eine verkettete Zeichenfolge zurück, die durch Auswerten eines Zeichenfolgenausdrucks über einer Menge erstellt wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich in der Regel um den Namen des aktuellen Elements (CurrentMember.Name) jedes Tupels in der angegebenen Menge handelt.  
  
 *Trennzeichen*  
 Ein gültiges Trennzeichen, ausgedrückt als Zeichenfolgenausdruck.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine zweite Menge angegeben wird, die **generieren** Funktion gibt einen Satz generiert, indem die Tupel in der zweiten Menge auf jedes Tupel in der ersten Menge angewendet*,* und dann wird das resultierende verknüpft Mengen durch vereinigungsmengenbildung. Wenn **alle** angegeben ist, wird die Funktion behält Duplikate in der sich ergebenden Menge.  
  
 Wenn ein Zeichenfolgenausdruck angegeben wird, die **generieren** Funktion gibt eine Zeichenfolge, die durch das Auswerten des angegebenen Zeichenfolgenausdruck für jedes Tupel in der ersten Menge generiert*,* und dann die Ergebnisse verkettet. Optional kann die Zeichenfolge begrenzt werden, sodass die einzelnen Ergebnisse in der verketteten Ergebniszeichenfolge voneinander getrennt sind.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="set"></a>Legen Sie  
 Im folgenden Beispiel gibt die Abfrage eine Menge zurück, die Measure Internet Sales Amount vier Mal enthält, da in der Menge [Date].[Calendar Year].[Calendar Year].ELEMENTE vier Elemente zu finden sind:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 Lässt man ALL weg, gibt die Abfrage Internet Sales Amount nur ein Mal zurück:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 Die am häufigsten verwendeten praktische Nutzen von **generieren** ist um einen komplexen Mengenausdruck wie TopCount, über eine Menge von Elementen. Die folgende Beispielabfrage zeigt die obersten 10 Produkte für jedes Kalenderjahr in Zeilen an:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 Beachten Sie, dass eine andere Top 10 für jedes Jahr, und dass angezeigt wird die Verwendung von **generieren** ist die einzige Möglichkeit, dieses Ergebnis zu erhalten. Ein einfacher Crossjoin der Kalenderjahre und der Menge der obersten 10 Produkte würde mit jährlicher Wiederholung die 10 obersten Produkte der ewigen Bestenliste anzeigen, wie das folgende Beispiel zeigt:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 Das folgende Beispiel zeigt die Verwendung von **generieren** gibt eine Zeichenfolge zurück:  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Diese Form der **generieren** Funktion ist nützlich beim Debuggen von Berechnungen, wie Sie zum Zurückgeben einer Zeichenfolge, die die Namen aller Elemente in einem Satz anzeigen können. Dies ist möglicherweise einfacher, als die strikte MDX-Darstellung einer Gruppe zu lesen, die die [SetToStr &#40; MDX &#41; ](../mdx/settostr-mdx.md) -Funktion zurückgegeben wird.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
