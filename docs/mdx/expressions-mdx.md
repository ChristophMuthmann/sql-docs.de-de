---
title: Ausdrücke (MDX) | Microsoft Docs
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
- identifiers [MDX]
- expressions [MDX]
- expressions [MDX], about expressions
- MDX [Analysis Services], expressions
- Multidimensional Expressions [Analysis Services], expressions
ms.assetid: e20c34bc-30fa-4ac5-b896-9d4c9925ef59
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 0fbb0f5d2b1b9699cd468cbcbd81a528c217bd3a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="expressions-mdx"></a>Ausdrücke (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ein Ausdruck ist eine Kombination aus Bezeichnern, Werten und Operatoren, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] auswerten kann, um ein Ergebnis zu erhalten. Die Daten können an verschiedenen Stellen beim Zugriff oder Ändern von Daten verwendet werden. Beispielsweise können Sie einen Ausdruck als Teil der Daten, die von einer Abfrage abgerufen werden sollen, oder als Suchbedingung verwenden, um nach Daten zu suchen, die bestimmte Kriterien erfüllen.  
  
## <a name="simple-and-complex-expressions"></a>Einfache und komplexe Ausdrücke  
 Ein Ausdruck in MDX kann einfach oder komplex sein.  
  
 Ein einfacher Ausdruck kann einer der folgenden Ausdrücke sein:  
  
 Konstante  
 Eine Konstante ist ein Symbol, das einen bestimmten Datenwert in MDX darstellt. Zeichenfolgen-, numerische und Datumswerte können als Konstanten gerendert werden. Im Gegensatz zu numerischen Konstanten müssen Zeichenfolgen- und Datumskonstanten in einfache Anführungszeichen (') eingeschlossen werden.  
  
 Skalarfunktion  
 Eine Skalarfunktion gibt einen einzelnen Wert im Kontext einer Auswertung in MDX zurück. Zum Verständnis, wie Skalarfunktionen von MDX ausgewertet werden, muss der Unterschied zu den anderen MDX-Ausdrücken klar sein, denn die meisten MDX-Ausdrücke, -Anweisungen und -Skripts werden nicht für ein einzelnes Datenelement, sondern iterativ für eine Gruppe von Datenelementen (z. B. Zellen oder Elemente) ausgewertet. Zu dem Zeitpunkt, zu dem eine Skalarfunktion ausgewertet wird, ermittelt die Funktion üblicherweise nur den Wert für ein einzelnes Datenelement.  
  
 Objektbezeichner  
 MDX ist wegen der Beschaffenheit der mehrdimensionalen Daten objektorientiert. Objektbezeichner werden in MDX als einfache Ausdrücke angesehen. Weitere Informationen zu Bezeichnern finden Sie unter [-IDs &#40; MDX &#41; ](../mdx/identifiers-mdx.md).  
  
 Ein komplexer Ausdruck kann aus Kombinationen dieser Entitäten erstellt werden, die durch Operatoren verknüpft sind.  
  
## <a name="expression-results"></a>Ergebnisse von Ausdrücken  
 Bei einfachen Ausdrücken, die aus einer einzelnen Konstanten, Variablen, Skalarfunktion oder einem Spaltennamen bestehen, entsprechen Datentyp, Sortierung, Genauigkeit, Anzahl der Dezimalstellen und Wert des Ausdrucks den jeweiligen Eigenschaften (Datentyp, Sortierung, Genauigkeit usw.) des Elements, auf das verwiesen wird. Da MDX direkt nur den OLE VARIANT-Datentyp unterstützt, tritt keine Koersion auf, wenn einfache Ausdrücke verwendet werden.  
  
 Bei einem komplexen Ausdruck kann eine Koersion auftreten, wenn mehrere einfache Ausdrücke mit unterschiedlichen Datentypen verwendet werden.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Die folgende Abfrage zeigt Beispiele berechneter Measures, deren Definitionen einfache Ausdrücke sind:  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Bei einem Ausdruck kann es sich auch um eine Berechnung handeln, wie z. B. `[Measures].[Discount Amount] * 1.5`. Im folgenden Beispiel wird gezeigt, wie eine Berechnung dazu verwendet wird, ein Element in einer MDX-SELECT-Anweisung zu definieren:  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Using Cube and Subcube Expressions (Verwenden von Cube- und Teilcubeausdrücken)](../mdx/using-cube-and-subcube-expressions.md)|Definiert Cube- und Teilcubeausdrücke.|  
|[Using Dimension Expressions (Verwenden von Dimensionsausdrücken)](../mdx/using-dimension-expressions.md)|Definiert Dimensionsausdrücke.|  
|[Using Member Expressions (Verwenden von Elementausdrücken)](../mdx/using-member-expressions.md)|Definiert Elementausdrücke.|  
|[Using Tuple Expressions (Verwenden von Tupelausdrücken)](../mdx/using-tuple-expressions.md)|Definiert Tupelausdrücke.|  
|[Using Set Expressions (Verwenden von Mengenausdrücken)](../mdx/using-set-expressions.md)|Definiert Mengenausdrücke.|  
|[Using Scalar Expressions (Verwenden von Skalarausdrücken)](../mdx/using-scalar-expressions.md)|Definiert skalare Ausdrücke.|  
|[Working with Empty Values (Arbeiten mit leeren Werten)](../mdx/working-with-empty-values.md)|Beschreibt, was ein leerer Wert ist und wie leere Werte gehandhabt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Sprachreferenz &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)   
 [Grundlegendes zu MDX-Abfrage &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
