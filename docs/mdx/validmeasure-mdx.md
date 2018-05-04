---
title: ValidMeasure (MDX) | Microsoft Docs
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
- VALIDMEASURE
dev_langs:
- kbMDX
helpviewer_keywords:
- ValidMeasure function
ms.assetid: ecf20a86-c45e-4521-84ce-3a466e0c1136
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c3c2bb7aa20794d7de9a3eeaa208377736af653e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Wert eines Measures in einem Cube zurück, indem beim Zurückgeben des Ergebnisses für ein angegebenes Tupel für nicht passende Dimensionen ihre Alle-Ebene (oder, wenn nicht aggregierbar, ihr Standardelement) erzwungen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **ValidMeasure** Funktion gibt den Wert eines Tupels, ignoriert Attribute, die keine Beziehung mit der Measuregruppe des Measures, dessen Wert verfügen das Tupel zurückgibt. Ein Attribut kann aus zwei Gründen mit einem Measure nicht verbunden sein:  
  
-   Die Dimension des Attributs verfügt über keine Beziehung mit der Measuregruppe des Measure im Tupel.  
  
-   Die Dimension des Attributs verfügt über keine Beziehung mit der Measuregruppe im Measure, aber das Granularitätsattribut ist nicht das Schlüsselattribut, und das Granularitätsattribut verfügt über keine direkte Beziehung mit dem Attribut im Tupel.  
  
 Das Verhalten dieser Funktion ist das Standardverhalten für die serverseitige und wird gesteuert, indem die **IgnoreUnrelatedDimensions** -Eigenschaft für das measuregruppenobjekt.  
  
 Für alle Attribute im angegebenen Tupel mit Granularität (wenn das Element im Tupel nicht das Alle-Element ist) wird die aktuelle Koordinate für jedes einzelne dieser Attribute wie folgt verschoben:  
  
-   Mit dem angegebenen Attributelement verknüpfte Attribute werden zu dem zusammen mit dem aktuellen Element vorhandenen Element verschoben.  
  
-   Mit dem angegebenen Attributelement verknüpfende Attribute werden zum Alle-Element verschoben (oder zum Standardelement, wenn die Hierarchie nicht aggregierbar ist).  
  
-   Nicht verknüpfte Attribute werden (Measure-basiert) zum Alle-Element verschoben.  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage zeigt, wie die ValidMeasure-Funktion verwendet werden kann, um das Verhalten der IgnoreUnrelatedDimensions-Eigenschaft zu überschreiben. Im Adventure Works-Cube ist IgnoreUnrelatedDimensions für die Sales Targets-Measuregruppe auf False festgelegt; da die Date-Dimension bei der Kalenderquartalsgranularität zu dieser Measuregruppe verknüpft, bedeutet dies, dass das Sales Quota-Measure unter Kalenderquartal standardmäßig NULL zurückgibt (obwohl es auch eine Berechnung im MDX-Skript gibt, das Werte bis hinunter zur Monatsebene zuordnet). Die ValidMeasure-Funktion in einem berechneten Measure kann verwendet werden, um ein Verhalten für das Sales Quota-Measure zu bewirken, als ob IgnoreUnrelatedDimensions auf True festgelegt wurde und Sales Quota zwingt, den Wert des aktuellen Kalenderquartals anzuzeigen.  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 Auf ähnliche Weise hat das Sales Targets-Measure keine Beziehung mit der Promotion-Dimension; unterhalb des Alle-Elements jeder Hierarchie auf Promotion gibt es NULL zurück. Dieses Verhalten kann ebenfalls mittels ValidMeasure geändert werden:  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
