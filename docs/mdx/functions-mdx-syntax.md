---
title: Funktionen (MDX-Syntax) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- MDX [Analysis Services], functions
- Multidimensional Expressions [Analysis Services], functions
- functions [MDX]
ms.assetid: 74ca5e79-1f33-4795-9d68-98eff9c190c1
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 88195fd4841c7fbc7135ad44c531d508912e58f0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="functions-mdx-syntax"></a>Funktionen (MDX-Syntax)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  MDX (Multidimensional Expressions) verfügt über verschiedene Kategorien systeminterner Funktionen, mit denen bestimmte Vorgänge ausgeführt werden können. In der folgenden Tabelle werden die in MDX verfügbaren Funktionskategorien aufgelistet.  
  
> [!NOTE]  
>  Weitere Informationen zu einzelnen Funktionen finden Sie unter [MDX-Funktionsreferenz &#40; MDX &#41; ](../mdx/mdx-function-reference-mdx.md).  
  
|Funktionskategorie|Description|  
|-----------------------|-----------------|  
|Arrayfunktionen|Stellen Arrays bereit, die in gespeicherten Prozeduren verwendet werden können.<br /><br /> Weitere Informationen finden Sie unter [Verwendung von gespeicherten Prozeduren &#40; MDX &#41; ](../mdx/using-stored-procedures-mdx.md).|  
|Dimensionsfunktionen|Geben einen Verweis auf eine Dimension aus einer Hierarchie, einer Ebene oder einem Element zurück.<br /><br /> Weitere Informationen finden Sie unter [mithilfe von Dimensions-, Hierarchie- und Funktionen der Ebene](../mdx/using-dimension-hierarchy-and-level-functions.md).|  
|Hierarchiefunktionen|Geben einen Verweis auf eine Hierarchie aus einer Ebene oder einem Element zurück.<br /><br /> Weitere Informationen finden Sie unter [mithilfe von Dimensions-, Hierarchie- und Funktionen der Ebene](../mdx/using-dimension-hierarchy-and-level-functions.md).|  
|Ebenenfunktionen|Geben einen Verweis auf eine Ebene aus einem Element, einer Dimension, einer Hierarchie oder einem Zeichenfolgenausdruck zurück.<br /><br /> Weitere Informationen finden Sie unter [mithilfe von Dimensions-, Hierarchie- und Funktionen der Ebene](../mdx/using-dimension-hierarchy-and-level-functions.md).|  
|Logische Funktionen|Führen logische Operationen und Vergleiche für Objekte und Ausdrücke aus.<br /><br /> Weitere Informationen finden Sie unter [logische Funktionen mithilfe von](../mdx/using-logical-functions.md).|  
|Memberfunktionen|Geben einen Verweis auf ein Element aus anderen Objekten oder aus einem Zeichenfolgenausdruck zurück.<br /><br /> Weitere Informationen finden Sie unter [Memberfunktionen verwenden](../mdx/using-member-functions.md).|  
|Numerische Funktionen|Führen mathematische und statistische Funktionen für Objekte und Ausdrücke aus.<br /><br /> Weitere Informationen finden Sie unter [Verwenden von mathematischen Funktionen](../mdx/using-mathematical-functions.md).|  
|Set-Funktionen|Geben einen Verweis auf eine Menge aus anderen Objekten oder aus einem Zeichenfolgenausdruck zurück.<br /><br /> Weitere Informationen finden Sie unter [mithilfe von Set-Funktion](../mdx/using-set-functions.md).|  
|Zeichenfolgenfunktionen|Geben Zeichenfolgenwerte aus anderen Objekten oder vom Server zurück.<br /><br /> Weitere Informationen finden Sie unter [mithilfe von Zeichenfolgenfunktionen](../mdx/using-string-functions.md).|  
|Tupelfunktionen|Geben einen Verweis auf ein Tupel aus einer Menge oder aus einem Zeichenfolgenausdruck zurück.<br /><br /> Weitere Informationen finden Sie im Abschnitt über das Verwenden von Tupelfunktionen.|  
  
## <a name="uses-of-functions"></a>Verwendungsweisen der Funktionen  
 Funktionen können in jedem MDX-Ausdruck verwendet werden. Funktionen können außerdem geschachtelt werden (d. h., eine Funktion kann innerhalb einer anderen Funktion verwendet werden).  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Syntaxelemente &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
