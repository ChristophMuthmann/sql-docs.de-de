---
title: ClosingPeriod (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CLOSINGPERIOD
dev_langs: kbMDX
helpviewer_keywords: ClosingPeriod function
ms.assetid: ae709017-219d-43e1-a98a-a85bd365b4cd
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fe7c4c827706f45b5258b5c2738ada30d131a4c4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das letzte gleichgeordnete Element unter den nachfolgenden Werten eines angegebenen Elements auf einer angegebenen Ebene zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion ist hauptsächlich zur Verwendung mit einer Dimension des Typ Time vorgesehen, kann jedoch auch mit beliebigen anderen Dimensionen verwendet werden.  
  
-   Wenn ein Ebenenausdruck angegeben wird, die **ClosingPeriod** -Funktion verwendet die Dimension, die die angegebene Ebene enthält, und gibt das letzte gleichgeordnete Element unter den nachfolgenden Werten des Standardelements auf der angegebenen Ebene zurück.  
  
-   Wenn sowohl ein Ebenenausdruck als auch ein Elementausdruck angegeben sind, die **ClosingPeriod** Funktion gibt das letzte gleichgeordnete Element unter den nachfolgenden Werten eines angegebenen Elements auf der angegebenen Ebene zurück.  
  
-   Wenn weder ein Ebenenausdruck noch ein Elementausdruck angegeben ist, die **ClosingPeriod** Funktion verwendet die Standardebene und Mitglied der Dimension (sofern vorhanden) in den Cube mit den Typ Time.  
  
 Die **ClosingPeriod** -Funktion ist gleichbedeutend mit der folgenden MDX-Anweisung:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  Die [OpeningPeriod](../mdx/openingperiod-mdx.md) Funktion ist vergleichbar mit der **ClosingPeriod** -Funktion, außer dass die **OpeningPeriod** Funktion gibt das erste gleichgeordnete Element statt des letzten gleichgeordneten zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das FY2007-Element der Date-Dimension (die den semantischen Typ Time aufweist) zurückgegeben. Dieses Element wird zurückgegeben, weil die Fiscal Year-Ebene der erste nachfolgende Wert der [All]-Ebene ist. Die Fiscal-Hierarchie ist die Standardhierarchie, weil sie die erste benutzerdefinierte Hierarchie in der Hierarchie-Auflistung darstellt, und das FY 2007-Element ist das letzte gleichgeordnete Element in dieser Hierarchie auf dieser Ebene.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das Element "30. November 2006" auf der Date.Date.Date-Ebene für die Date.Date-Attributhierarchie zurückgegeben. Dieses Element ist das letzte gleichgeordnete Element des nachfolgenden Wertes der [All]-Ebene in der Date.Date-Attributhierarchie.  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das December, 2003-Element zurückgegeben. Dieses Element ist das letzte gleichgeordnete Element des nachfolgenden Wertes des 2003-Elements auf der Year-Ebene in der benutzerdefinierten Calendar-Hierarchie.  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das June, 2003-Element zurückgegeben. Dieses Element ist das letzte gleichgeordnete Element des nachfolgenden Wertes des 2003-Elements auf der Year-Ebene in der benutzerdefinierten Fiscal-Hierarchie.  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OpeningPeriod &#40; MDX &#41;](../mdx/openingperiod-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40; MDX &#41;](../mdx/lastsibling-mdx.md)  
  
  
