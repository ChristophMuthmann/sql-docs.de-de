---
title: Bezeichner (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- formats [Analysis Services]
- Multidimensional Expressions [Analysis Services], identifiers
- identifiers [MDX]
- MDX [Analysis Services], identifiers
- delimited identifiers [MDX]
- regular identifiers [MDX]
- formats [Analysis Services], identifiers
ms.assetid: 739a8a67-bef3-4b56-961d-ee96cfc36b5b
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a04d387c0ee40d825fddf3c50f02793e722cdbc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-mdx"></a>Bezeichner (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ein Bezeichner ist der Name des ein [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Objekt. Jedes [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Objekt muss einen Bezeichner haben. Dies gilt für Cubes, Dimensionen, Hierarchien, Ebenen, Elemente usw. Sie verwenden den Bezeichner eines Objekts, um in MDX-Anweisungen (Multidimensional Expressions) auf das Objekt zu verweisen.  
  
 Abhängig davon, wie Sie ein Objekt benennen, ist der Objektbezeichner ein regulärer oder ein Begrenzungsbezeichner.  
  
> [!NOTE]  
>  Sowohl reguläre als auch begrenzungsezeichner müssen zwischen 1 und 100 Zeichen enthalten.  
  
## <a name="using-regular-identifiers"></a>Verwenden von regulären Bezeichnern  
 Ein regulärer Bezeichner ist ein Objektname, der folgenden Formatierungsregeln für reguläre Bezeichner entspricht. Ein regulärer Bezeichner kann mit oder ohne Trennzeichen verwendet werden.  
  
### <a name="formatting-rules-for-regular-identifiers"></a>Formatierungsregeln für reguläre Bezeichner  
  
1.  Das erste Zeichen muss eines der folgenden Zeichen sein:  
  
    -   Ein Buchstabe gemäß Unicode Standard 2.0. Neben Buchstaben aus anderen Sprachen enthält die Unicode-Definition von Buchstaben die lateinischen Buchstaben von a bis z und von A bis Z.  
  
    -   Der Unterstrich (_).  
  
2.  Im Anschluss daran können die folgenden Zeichen verwendet werden:  
  
    -   Buchstaben in Unicode Standard 2.0 definiert.  
  
    -   Dezimalzahlen aus dem lateinischen Grundalphabet oder anderen nationalen Schriften.  
  
    -   Der Unterstrich (_).  
  
3.  Der Bezeichner darf kein reserviertes MDX-Schlüsselwort sein. Für reservierte Schlüsselwörter erfolgt in MDX keine Unterscheidung nach Groß-/Kleinschreibung. Weitere Informationen finden Sie unter [reservierte Schlüsselwörter &#40;MDX-Syntax&#41;](../mdx/reserved-keywords-mdx-syntax.md).  
  
4.  Eingebettete Leerzeichen oder Sonderzeichen sind nicht zulässig.  
  
### <a name="examples-of-regular-identifiers"></a>Beispiele zu regulären Bezeichnern  
 In der folgenden MDX-Anweisung entsprechen die Bezeichner `Measures`, `Product` und `Style` den Formatierungsregeln für reguläre Bezeichner. Für diese regulären Bezeichner sind keine Trennzeichen erforderlich.  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 Für reguläre Bezeichner können auch, obwohl nicht erforderlich, Trennzeichen verwendet werden. In der folgenden MDX-Anweisung wurden die regulären Bezeichner `Measures`, `Product` und `Style` mithilfe von eckigen Klammern ordnungsgemäß begrenzt.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>Verwenden von Begrenzungsbezeichnern  
 Ein Bezeichner, der nicht den Formatierungsregeln für reguläre Bezeichner entspricht, muss immer mit eckigen Klammern ([]) begrenzt sein.  
  
> [!NOTE]  
>  Trennzeichen werden ausschließlich für Bezeichner verwendet. Trennzeichen können nicht für Schlüsselwörter verwendet werden, wobei es keine Rolle spielt, ob die Schlüsselwörter in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] als reserviert gekennzeichnet sind oder nicht.  
  
 Einen Begrenzungsbezeichner verwenden Sie in folgenden Zusammenhängen:  
  
-   Wenn der Name eines Objekts oder ein Teil des Namens ein reserviertes Wort ist.  
  
     Es wird empfohlen, dass reservierte Schlüsselwörter nicht als Objektnamen verwendet werden. Datenbanken, die ein Upgrade von früheren Versionen von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] enthalten möglicherweise Bezeichner, die in der früheren Version nicht reservierten Wörter enthalten, jedoch sind reservierte Wörter für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. So lange, bis Sie den Bezeichner des Objekts ändern können, können Sie mit dem Begrenzungsbezeichner auf das Objekt verweisen.  
  
-   Wenn für den Namen eines Objekts Zeichen verwendet werden, die nicht als qualifizierte Bezeichner aufgeführt sind.  
  
     In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] kann für einen Begrenzungsbezeichner jedes Zeichen verwendet werden, das zur aktuellen Codepage gehört. Ein unbedachtes Verwenden von Sonderzeichen in einem Objektnamen kann allerdings dazu führen, dass MDX-Anweisungen schwierig zu lesen und zu pflegen sind.  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>Formatierungsregeln für Begrenzungsbezeichner  
 Der Hauptteil eines Begrenzungsbezeichners kann jede Kombination aus Zeichen der aktuellen Codepage enthalten, einschließlich des Trennzeichens selbst. Enthält der Hauptteil eines Begrenzungsbezeichners Trennzeichen, kann ein spezieller Schritt erforderlich sein:  
  
-   Enthält der Hauptteil des Bezeichners nur eine linke eckige Klammer ([), ist kein zusätzlicher Schritt erforderlich.  
  
-   Enthält der Hauptteil des Bezeichners eine rechte eckige Klammer (]), müssen Sie zwei rechte eckige Klammern (]]) angeben.  
  
### <a name="examples-of-delimited-identifiers"></a>Beispiele zu Begrenzungsbezeichnern  
 In der folgenden hypothetischen Anweisung stellen `Sales Volume`, `Sales Cube` und `select` Begrenzungsbezeichner dar:  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 Im nächsten Beispiel hat ein Objekt den Namen `Total Profit [Domestic]`. Zum Verweisen auf dieses Objekt müssen Sie den folgenden Begrenzungsbezeichner verwenden:  
  
 `[Total Profit [Domestic]]]`  
  
 Wie Sie sehen, musste für die linke eckige Klammer vor `Domestic` keine Änderung vorgenommen werden, um den Begrenzungsbezeichner zu erstellen. Dagegen musste die rechte eckige Klammer hinter `Domestic` durch zwei rechte eckige Klammern ersetzt werden.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Begrenzen von mehrteiligen Bezeichnern  
 Wenn Sie vollqualifizierte Objektnamen verwenden, ist es eventuell erforderlich, mehr als einen der Bezeichner, aus denen sich der Objektname zusammensetzt, zu begrenzen. Der Bezeichner Front Brakes im folgenden Code muss beispielsweise begrenzt werden.  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 Außerdem ist im vorherigen Beispiel der Bezeichner Measures begrenzt, um zu zeigen, wie mehrere Bezeichner begrenzt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Sprachreferenz & #40; MDX & #41;](../mdx/mdx-language-reference-mdx.md)   
 [Grundlegendes zu MDX-Abfrage & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX-Syntaxelemente &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
