---
title: Erstellen im Bereich einer Sitzung berechnete Zellen | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b4b43145a59c557c4efd981b5a8013dcedd501bd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>MDX-Zellenberechnungen - berechneter Zellen im Bereich einer Sitzung
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
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
  
|Kategorie|Description|  
|--------------|-----------------|  
|Leere Menge|Ein MDX-Mengenausdruck, der zu einer leeren Menge aufgelöst wird. In diesem Fall ist der Gültigkeitsbereich der berechneten Zelle gleich dem gesamten Cube.|  
|Menge mit einem einzelnen Element|Ein MDX-Mengenausdruck, der zu einem einzelnen Element aufgelöst wird.|  
|Menge von Ebenenelementen|Ein MDX-Mengenausdruck, der zu den Elementen einer einzelnen Ebene aufgelöst wird. Ein Beispiel hierfür ist die MDX-Funktion *Level_Expression*.**Members** . Um berechnete Elemente einzuschließen, verwenden Sie die MDX-Funktion *Level_Expression*.**AllMembers**.<br /><br /> Weitere Informationen finden Sie unter [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Menge nachfolgender Werte|Ein MDX-Mengenausdruck, der zu den nachfolgenden Werten eines angegebenen Elements aufgelöst wird. Ein Beispiel hierfür ist die MDX-Funktion **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Weitere Informationen finden Sie unter [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Zellenberechnungen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
