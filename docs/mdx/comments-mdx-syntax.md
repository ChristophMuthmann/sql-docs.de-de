---
title: Kommentare (MDX-Syntax) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- remarks [MDX]
- MDX [Analysis Services], comments
- commenting characters
- nonexecuting text strings [MDX]
- Multidimensional Expressions [Analysis Services], comments
- comments [MDX]
ms.assetid: 9c00b30c-28f6-4f23-b812-ccc0e900daa5
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 372ef0470c32b4bb7fc6f6b2094a1e3b4d1a7013
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="comments-mdx-syntax"></a>Kommentare (MDX-Syntax)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Kommentare sind Textzeichenfolgen im Programmcode, die nicht ausgeführt werden. (Kommentare werden auch als Anmerkungen bezeichnet.) Sie können Kommentare dazu verwenden, Code zu dokumentieren oder Teile von MDX-Anweisungen (Multidimensional Expressions) und Skripts, für die eine Fehlerdiagnose vorgenommen wird, vorübergehend zu deaktivieren. Durch Verwenden von Kommentaren zum Dokumentieren von Code können Sie die künftige Wartung des Programmcodes vereinfachen. In Kommentaren werden häufig der Programmname, der Verfassername sowie Datumsangaben wichtiger Codeänderungen festgehalten. Sie können auch Kommentare zum Beschreiben komplexer Berechnungen oder zum Erklären einer Programmiermethode verwenden.  
  
 Für Kommentare in MDX gelten folgende Richtlinien:  
  
-   Im Kommentar können sämtliche alphanumerischen Zeichen oder Symbole verwendet werden. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignoriert alle Zeichen innerhalb eines Kommentars.  
  
-   Es gibt keine Längenbeschränkung für einen Kommentar innerhalb einer Anweisung oder eines Skripts. Ein Kommentar kann aus einer oder mehreren Zeilen bestehen.  
  
 MDX unterstützt drei Arten von Kommentarzeichen:  
  
 // (doppelte Schrägstriche)  
 Diese Kommentarzeichen können in derselben Zeile wie der auszuführende Code oder in einer gesonderten Zeile verwendet werden. Der gesamte Text ab den beiden Schrägstrichen bis zum Ende der Zeile ist Teil des Kommentars. Bei einem Kommentar, der sich über mehrere Zeilen erstreckt, muss jede der Kommentarzeilen mit doppelten Schrägstrichen beginnen. Weitere Informationen finden Sie unter [&#40; Kommentar &#41; &#40; MDX &#41; ](../mdx/comment-mdx-double-slash.md).  
  
 -- (doppelte Bindestriche)  
 Diese Kommentarzeichen können in derselben Zeile wie der auszuführende Code oder in einer gesonderten Zeile verwendet werden. Der gesamte Text zwischen den doppelten Bindestrichen und dem Ende der Zeile ist Teil des Kommentars. Bei einem Kommentar, der sich über mehrere Zeilen erstreckt, muss jede der Kommentarzeilen mit doppelten Bindestrichen beginnen. Weitere Informationen finden Sie unter [--&#40; Kommentar &#41; &#40; MDX &#41; ](../mdx/comment-mdx-operator-reference.md).  
  
 /* ... \*/ (Schrägstrich/Sternchen-Zeichenpaare)  
 Diese Kommentarzeichen können in derselben Zeile wie Code ausgeführt werden, auf Zeilen selbst oder sogar innerhalb des ausführbaren Codes verwendet werden. Sämtliche Zeichen ab dem öffnenden kommentarzeichenpaar (/\*), zum schließenden kommentarzeichenpaar (\*/) als Teil des Kommentars. Für einen mehrzeiligen Kommentar, die Open Kommentarzeichen (/\*) muss der Kommentar und die schließen Kommentarzeichen beginnen (\*/) Enden des Kommentars. Die Zeilen des Kommentars dürfen keine anderen Kommentarzeichen enthalten. Weitere Informationen finden Sie unter [/ *... \*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage zeigt Beispiele für alle drei Kommentartypen:  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Syntaxelemente &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

