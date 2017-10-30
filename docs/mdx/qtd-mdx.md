---
title: QTD (MDX) | Microsoft Docs
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
- QTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Qtd function
ms.assetid: c1fe47e0-9c2b-466f-8d6d-e2b1c16a69cb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d4fcbfa3ac5c02dc04181bb32c8baca10a56fa0e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt einen Satz von gleichgeordneten Elementen aus der gleichen Ebene wie ein angegebenes Element aus, beginnend mit dem ersten gleichgeordneten Element und endend mit dem angegebenen Element, entsprechend der Einschränkung durch die *Quartal* in der Zeitdimension.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Member-AusdruckIS nicht angegeben, wird standardmäßig das aktuelle Element der ersten Hierarchie mit einer Ebene des Typs *Quartale* in der ersten Dimension des Typs *Zeit* in der Measuregruppe.  
  
 Die **Qtd** Funktion ist eine Verknüpfungsfunktion für die [PeriodsToDate &#40; MDX &#41; ](../mdx/periodstodate-mdx.md) Funktion, deren Ebenenausdruck-Argument auf *Quartal*. Somit ist `Qtd(Member_Expression)` funktionell äquivalent zu `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel gibt die Summe aus der `Measures.[Order Quantity]` Elements, aggregiert über die ersten zwei Monate des dritten Quartals des Kalenderjahres 2003, die in enthaltenen der `Date` Dimension, aus der **Adventure Works** Cube.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

