---
title: Verwenden von Zeichenfolgenfunktionen | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- string functions
ms.assetid: 962e820a-a1f9-49b5-90f0-a05261e6682b
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bf114f9b706497512f10e3629e871ba64ecaaee9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-string-functions"></a>Verwenden von Zeichenfolgenfunktionen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Zeichenfolgenfunktionen können Sie für fast jedes Objekt in MDX (Multidimensional Expressions) verwenden. In gespeicherten Prozeduren werden Zeichenfolgenfunktionen hauptsächlich dazu verwendet, das jeweilige Objekt in eine Zeichenfolgendarstellung zu konvertieren. Zeichenfolgenfunktionen können auch dazu verwendet werden, einen Zeichenfolgenausdruck anhand eines Objekts auszuwerten, um einen Wert zurückzugeben.  
  
 Die am häufigsten verwendeten Zeichenfolgenfunktionen sind **Namen** und **Uniquename**. Diese Funktionen geben den Namen und den eindeutigen Namen eines Objekts zurück. Sie werden meistens zum Debuggen von Berechnungen verwendet, um zu ermitteln, welches Element eine Funktion zurückgibt.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Beispielabfrage veranschaulicht die Verwendung dieser Funktionen:  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Die **generieren** Funktion kann verwendet werden, um eine Zeichenfolgenfunktion auf jedes Element einer Menge und verketten die Ergebnisse. Dies ist nützlich beim Debuggen von Berechnungen, da es Ihnen ermöglicht, den Inhalt einer Menge sichtbar zu machen. Im folgenden Beispiel wird diese Art der Verwendung veranschaulicht:  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Eine weitere Gruppe häufig verwendeter Zeichenfolgenfunktionen ermöglichen Ihnen eine Zeichenfolge umzuwandeln, die den eindeutigen Namen eines Objekts oder einen Ausdruck enthält, der sich in das Objekt auflöst. Die folgende Beispielabfrage veranschaulicht, wie die **StrToMember** und **StrToSet** Funktionen dazu:  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  Die **StrToMember** und **StrToSet** Funktionen sollte mit Vorsicht verwendet werden. Sie können zu schlechter Abfrageleistung führen, wenn sie innerhalb von Berechnungsdefinitionen verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Generieren von &#40;MDX&#41;](../mdx/generate-mdx.md)   
 [Namen &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Funktionen &#40;MDX-Syntax&#41;](../mdx/functions-mdx-syntax.md)   
 [Verwenden von gespeicherten Prozeduren &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
