---
title: OpeningPeriod (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- OpeningPeriod function
ms.assetid: bebf55cf-e5c6-42b1-98f2-1d6e54093d4c
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 30100b2762d3365c1599e665db54e2446e392fb3
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das erste gleichgeordnete Element unter den nachfolgenden Werten einer angegebenen Ebene optional bei einem angegebenen Element zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion dient in erster Linie die Time-Dimension verwendet, jedoch mit beliebigen anderen Dimensionen verwendet werden können.  
  
-   Wenn ein Ebenenausdruck angegeben wird, die **OpeningPeriod** -Funktion verwendet die Hierarchie, die die angegebene Ebene enthält, und gibt das erste gleichgeordnete Element unter den nachfolgenden Werten des Standardelements auf der angegebenen Ebene zurück.  
  
-   Wenn sowohl ein Ebenenausdruck als auch ein Elementausdruck angegeben sind, die **OpeningPeriod** Funktion gibt das erste gleichgeordnete Element unter den nachfolgenden Werten eines angegebenen Elements auf der angegebenen Ebene innerhalb der Hierarchie, die mit der angegebenen Ebene zurück.  
  
-   Wenn weder ein Ebenenausdruck noch ein Elementausdruck angegeben sind, die **OpeningPeriod** Funktion verwendet die Standardebene und-Element der Dimension vom Typ Time.  
  
> [!NOTE]  
>  Die [ClosingPeriod](../mdx/closingperiod-mdx.md) Funktion ist vergleichbar mit der **OpeningPeriod** -Funktion, außer dass die **ClosingPeriod** Funktion gibt das letzte gleichgeordnete Element statt dem ersten gleichgeordneten Element zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das FY2002-Element der Date-Dimension (die den Typ Time aufweist) zurückgegeben. Dieses Element wird zurückgegeben, weil die Fiscal Year-Ebene der erste nachfolgende Wert der [All]-Ebene ist. Die Fiscal-Hierarchie ist die Standardhierarchie, weil sie die erste benutzerdefinierte Hierarchie in der Hierarchie-Auflistung darstellt, und das FY2002-Element ist das erste gleichgeordnete Element in dieser Hierarchie auf dieser Ebene.  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das July 1, 2001-Element auf der Date.Date.Date-Ebene für die Date.Date-Attributhierarchie zurückgegeben. Dieses Element ist das erste gleichgeordnete Element des nachfolgenden Wertes der [All]-Ebene in der Date.Date-Attributhierarchie.  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das January, 2003-Element zurückgegeben. Dieses Element ist das erste gleichgeordnete Element des nachfolgenden Wertes des 2003-Elements auf der Year-Ebene in der benutzerdefinierten Calendar-Hierarchie.  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird der Wert des Standardmeasures für das July, 2002-Element zurückgegeben. Dieses Element ist das erste gleichgeordnete Element des nachfolgenden Wertes des 2003-Elements auf der Year-Ebene in der benutzerdefinierten Fiscal-Hierarchie.  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [TopCount &#40; MDX &#41;](../mdx/topcount-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40; MDX &#41;](../mdx/firstsibling-mdx.md)  
  
  

