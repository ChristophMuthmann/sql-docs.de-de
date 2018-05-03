---
title: Abhängige Elemente (MDX) | Microsoft Docs
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
- DESCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Descendants function
ms.assetid: d103b0f5-e794-4828-aa57-43f6918a0749
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 200fd06f596c02056ae5b55a5f20ad55ed4eb9a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="descendants-mdx"></a>Descendants (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Menge von nachfolgenden Werten eines Elements auf einer angegebenen Ebene oder in einem angegebenen Abstand zurück. Optional können nachfolgende Werte anderer Ebenen ein- oder ausgeschlossen werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Abstand*  
 Ein gültiger numerischer Ausdruck, der den Abstand vom angegebenen Element angibt.  
  
 *Desc_Flag*  
 Ein gültiger Zeichenfolgenausdruck, der ein Beschreibungs-Flag zur Unterscheidung möglicher Mengen von nachfolgenden Werten angibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Ebene angegeben ist, die **Nachfolger** Funktion gibt eine Gruppe mit den nachfolgenden Werten des angegebenen Elements oder die Mitglieder der angegebenen Menge auf einer angegebenen Ebene, optional geändert durch ein Flag, das im angegebenen *Desc_Flag*.  
  
 Wenn *Abstand* angegeben wird, die **Nachfolger** Funktion gibt eine Gruppe, die untergeordneten Elemente des angegebenen Elements oder die Mitglieder der angegebenen Menge, die die angegebene Anzahl von Ebenen in der Hierarchie des angegebenen Elements enthält, optional geändert durch ein Flag, das im angegebenen *Desc_Flag*. Das Distance-Argument dieser Funktion wird in der Regel bei unregelmäßigen Hierarchien verwendet. Wenn der angegebene Abstand null (0) ist, gibt die Funktion eine Menge zurück, die nur das angegebene Element oder die angegebene Menge enthält.  
  
 Wenn ein Mengenausdruck angegeben ist, die **Nachfolger** Funktion wird für jedes Element der Menge einzeln aufgelöst und die Menge erneut erstellt. Das heißt, die Syntax für die **Nachfolger** Funktion ist funktionell gleichwertig mit der MDX-Abfrage [generieren](../mdx/generate-mdx.md) Funktion.  
  
 Wenn keine Ebene oder Entfernung angegeben wird, wird der Standardwert für die von der Funktion verwendete Ebene bestimmt, durch Aufrufen der [Ebene](../mdx/level-mdx.md) Funktion (<\<Member >>. Level) für das angegebene Element aus (wenn ein Element angegeben wird) oder durch Aufrufen der **Ebene** Funktion für jedes Element des angegebenen Satzes (sofern eine Menge angegeben wird). Wenn kein Ebenenausdruck, Abstand oder Flag angegeben ist, wird die Funktion ausgeführt, als wenn die folgende Syntax verwendet würde:  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 Wenn eine Ebene und kein Beschreibungs-Flag angegeben ist, wird die Funktion ausgeführt, als wenn die folgende Syntax verwendet würde:  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 Durch Ändern des Wertes des Beschreibungs-Flags können Sie nachfolgende Elemente in der angegebenen Ebene bzw. dem angegebenen Abstand, untergeordnete Elemente vor und nach der angegebenen Ebene bzw. dem angegebenen Abstand (bis zum Blattknoten) sowie die untergeordneten Blattelemente unabhängig von der angegebenen Ebene bzw. dem angegebenen Abstand ein- oder ausschließen. Die folgende Tabelle beschreibt die Flags zulässig, der *Desc_Flag* Argument.  
  
|Flag|Description|  
|----------|-----------------|  
|SELF|Gibt nur nachfolgende Elemente auf der angegebenen Ebene oder in dem angegebenen Abstand zurück. Die Funktion schließt das angegebene Element ein, wenn es sich bei der angegebenen Ebene um die Ebene des angegebenen Elements handelt.|  
|AFTER|Gibt nachfolgende Elemente aus allen Ebenen zurück, die der angegebenen Ebene oder dem angegebenen Abstand untergeordnet sind.|  
|BEFORE|Gibt nachfolgende Elemente aus allen Ebenen zwischen dem angegebenen Element und der angegebenen Ebene oder im angegebenen Abstand zurück. Das angegebene Element enthält, aber enthält keine Elemente aus der angegebenen Ebene oder Entfernung.|  
|BEFORE_AND_AFTER|Gibt nachfolgende Elemente aus allen Ebenen zurück, die der Ebene des angegebenen Elements untergeordnet sind. Das angegebene Element wird eingeschlossen, jedoch nicht Elemente der angegebenen Ebene oder im angegebenen Abstand.|  
|SELF_AND_AFTER|Gibt nachfolgende Elemente aus der angegebenen Ebene oder im angegebenen Abstand sowie alle Ebenen, die der angegebenen Ebene oder dem angegebenen Abstand untergeordnet sind, zurück.|  
|SELF_AND_BEFORE|Gibt nachfolgende Elemente aus der angegebenen Ebene oder im angegebenen Abstand sowie aus allen Ebenen zwischen dem angegebenen Element und der angegebenen Ebene oder im angegebenen Abstand, einschließlich des angegebenen Elements, zurück.|  
|SELF_BEFORE_AFTER|Gibt nachfolgende Elemente aus allen Ebenen zurück, die der Ebene des angegebenen Elements untergeordnet sind, sowie das angegebene Element selbst.|  
|LEAVES|Gibt nachfolgende Blattelemente zwischen dem angegebenen Element und der angegebenen Ebene oder im angegebenen Abstand zurück.|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden das angegebene Element (United States), die Elemente zwischen dem angegebenen Element (United States) und den Elementen der Ebene vor der angegebenen Ebene (City) zurückgegeben. Im Beispiel werden das angegebene Element selbst (United States) und die Elemente der State-Province-Ebene (die Ebene vor der City-Ebene) zurückgegeben. Die Argumente in diesem Beispiel sind kommentiert, um Ihnen das Testen dieser Funktion mit anderen Argumenten zu erleichtern.  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 Das folgende Beispiel gibt den täglichen Durchschnitt der `Measures.[Gross Profit Margin]` Measures, berechnet über die Tage jedes Monats im Geschäftsjahr 2003 aus der **Adventure Works** Cube. Die **Nachfolger** Funktion gibt eine Menge von Tagen, die über das aktuelle Element der bestimmt, die `[Date].[Fiscal]` Hierarchie.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 Im folgende Beispiel wird ein Ebenenausdruck verwendet und Internet Sales Amount für alle Bundesstaaten in Australien zurückgegeben, und gibt den Prozentsatz der gesamten Internet Sales Amount für Australien für alle Bundesstaaten. In diesem Beispiel verwendet die Item-Funktion, um die erste (und einzigen) Tupels aus dem Satz zu extrahieren, die von zurückgegeben wird das **Vorgänger** Funktion.  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
