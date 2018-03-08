---
title: CASE-Anweisung (MDX) | Microsoft Docs
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
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], CASE
ms.assetid: 0aee3b4a-d5f7-4c9a-87b8-e5efc2da6b6d
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a4dbcc7ab42a0e044be0c7561adff4049fd8d1b9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="case-statement-mdx"></a>CASE-Anweisung (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ermöglicht die bedingte Rückgabe bestimmter Werte aus mehreren Vergleichen. Die folgenden zwei Arten von CASE-Anweisungen stehen zur Verfügung:  
  
-   Einfache CASE-Anweisungen, die einen Ausdruck mit mehreren einfachen Ausdrücken vergleichen, um bestimmte Werte zurückzugeben.  
  
-   Komplexe CASE-Anweisungen, die eine Menge boolescher Ausdrücke auswerten, um bestimmte Werte zurückzugeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>Argumente  
 *input_expression*  
 Ein MDX-Ausdruck (Multidimensional Expressions), dessen Auflösung einen Skalarwert ergibt.  
  
 *when_expression*  
 Ein angegebener Skalarwert, für die *Input_expression* ausgewertet wird, wenn die Auswertung den Wert true ist, gibt der Skalarwert von der *Else_result_expression*.  
  
 *when_true_result_expression*  
 Der Skalarwert, der zurückgegeben wird, wenn die Auswertung der WHEN-Klausel den Wert true ergibt.  
  
 *else_result_expression*  
 Der Skalarwert, der zurückgegeben wird, wenn keine Auswertung von WHEN-Klauseln den Wert true ergibt.  
  
 *Boolean_expression*  
 Ein MDX-Ausdruck, dessen Auswertung einen Skalarwert ergibt.  
  
## <a name="remarks"></a>Hinweise  
 Ist keine ELSE-Klausel angegeben, und werden alle WHEN-Klauseln zu FALSE ausgewertet, ist das Ergebnis eine leere Zelle.  
  
## <a name="simple-case-expression"></a>Einfache CASE-Ausdrücke  
 MDX wertet einen einfachen Case-Ausdruck, durch das Auflösen der *Input_expression* in einen skalaren Wert. Dieser Skalarwert wird dann mit der Skalarwert von verglichen, die *When_expression*. Wenn die beiden Skalarwerte übereinstimmen, wird die CASE-Anweisung gibt den Wert der die *When_true_expression*. Wenn die beiden Skalarwerte nicht übereinstimmen, wird die nächste WHEN-Klausel ausgewertet. Wenn alle von den WHEN-Klauseln ausgewertet werden auf "false", den Wert der *Else_result_expression* aus der ELSE-Klausel, sofern vorhanden, zurückgegeben wird.  
  
 Im folgenden Beispiel wird das Reseller Order Count-Measure für mehrere WHEN-Klauseln ausgewertet und als Ergebnis der Wert des Reseller Order Count-Measures für jedes Jahr zurückgegeben. Für Reseller Order Count-Werte, die einen skalaren Wert im angegebenen nicht entsprechen einem *When_expression* in einer WHEN-Klausel der Skalarwert von der *Else_result_expression* zurückgegeben wird.  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>Komplexe CASE-Ausdrücke  
 Verwenden Sie komplexe CASE-Ausdrücke, wenn Sie komplexere Auswertungen mithilfe von CASE-Ausdrücken durchführen möchten. Mit dieser Variante des Suchausdrucks können Sie auswerten, ob ein Eingabeausdruck innerhalb eines bestimmten Wertebereichs liegt. MDX wertet die WHEN-Klauseln in der Reihenfolge aus, in der die Klauseln in der CASE-Anweisung vorliegen.  
  
 Im folgenden Beispiel wird das Reseller Order Count-Measure ausgewertet gegen den angegebenen *Boolean_expression* aller mehrere WHEN-Klauseln. Als Ergebnis wird der Wert des Reseller Order Count-Measures für jedes Jahr zurückgegeben. Da WHEN-Klausel in der Reihenfolge ausgewertet werden, in der sie vorliegen, können alle Werte, die größer als 6 sind, problemlos dem Wert "VERY LARGE" zugewiesen werden, ohne jeden einzelnen Wert explizit angeben zu müssen. Für Reseller Order Count-Werte, die nicht in einer WHEN-Klausel der Skalarwert von angegeben sind die *Else_result_expression* zurückgegeben wird.  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Skriptanweisungen &#40; MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
