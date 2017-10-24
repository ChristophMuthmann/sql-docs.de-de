---
title: Erstellen im Bereich einer Sitzung berechnete Zellen | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0953df9aa142ce6826e96a3715970d51ec15158
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>MDX-Zellenberechnungen - berechneter Zellen im Bereich einer Sitzung
    
> [!IMPORTANT]  
>  Diese Syntax wurde als veraltet markiert. Sie sollten stattdessen MDX-Zuweisungen verwenden. Weitere Informationen zu Zuweisungen finden Sie unter [Grundlegendes MDX-Skript &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Wenn Sie berechnete Zellen erstellen möchten, die für alle Abfragen in derselben Sitzung verfügbar sind, verwenden Sie entweder die [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) -Anweisung oder die [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) -Anweisung. Beide Anweisungen führen zum selben Ergebnis.  
  
## <a name="create-cell-calculation-syntax"></a>Syntax von CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Diese Syntax wurde als veraltet markiert. Sie sollten stattdessen MDX-Zuweisungen verwenden. Weitere Informationen zu Zuweisungen finden Sie unter [Grundlegendes MDX-Skript &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Verwenden Sie folgende Syntax, wenn Sie mit der CREATE CELL CALCULATION-Anweisung eine berechnete Zelle im Bereich einer Sitzung definieren möchten:  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>Syntax von ALTER CUBE  
  
> [!IMPORTANT]  
>  Diese Syntax wurde als veraltet markiert. Sie sollten stattdessen MDX-Zuweisungen verwenden. Weitere Informationen zu Zuweisungen finden Sie unter [Grundlegendes MDX-Skript &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Verwenden Sie folgende Syntax, wenn Sie mit der ALTER CUBE -Anweisung eine berechnete Zelle im Bereich einer Sitzung definieren möchten:  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 Der `String_Expression` -Wert enthält eine Liste der orthogonalen, eindimensionalen MDX-Mengenausdrücke, von denen jeder aufgelöst zu einer der Mengenkategorien gehören muss, die in der folgenden Tabelle aufgelistet sind.  
  
|Kategorie|Beschreibung|  
|--------------|-----------------|  
|Leere Menge|Ein MDX-Mengenausdruck, der zu einer leeren Menge aufgelöst wird. In diesem Fall ist der Gültigkeitsbereich der berechneten Zelle gleich dem gesamten Cube.|  
|Menge mit einem einzelnen Element|Ein MDX-Mengenausdruck, der zu einem einzelnen Element aufgelöst wird.|  
|Menge von Ebenenelementen|Ein MDX-Mengenausdruck, der zu den Elementen einer einzelnen Ebene aufgelöst wird. Ein Beispiel hierfür ist die MDX-Funktion *Level_Expression*.**Members** . Um berechnete Elemente einzuschließen, verwenden Sie die MDX-Funktion *Level_Expression*.**AllMembers**.<br /><br /> Weitere Informationen finden Sie unter [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Menge nachfolgender Werte|Ein MDX-Mengenausdruck, der zu den nachfolgenden Werten eines angegebenen Elements aufgelöst wird. Ein Beispiel hierfür ist die MDX-Funktion **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Weitere Informationen finden Sie unter [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Zellenberechnungen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  

