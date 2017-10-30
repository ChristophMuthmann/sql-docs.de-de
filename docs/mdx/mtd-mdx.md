---
title: MTd (MDX) | Microsoft Docs
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
- MTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Mtd function
ms.assetid: 07d8fd65-f9e6-42d4-868d-fccfac6bdb70
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b177ad5ade9a3c73299fa675674eb5c783df79d4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mtd-mdx"></a>Mtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Menge von gleichgeordneten Elementen zurück, die derselben Ebene angehören wie ein angegebenes Element. Die Menge beginnt mit dem ersten gleichgeordneten Element und endet mit dem angegebenen Element, entsprechend der Einschränkung durch die Year-Ebene in der Time-Dimension.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Elementausdruck nicht angegeben ist, wird die Standardeinstellung ist das aktuelle Element der ersten Hierarchie mit einer Ebene des Typs *Monate* in der ersten Dimension des Typs *Zeit* in der Measuregruppe.  
  
 Die **Mtd** Funktion ist eine Verknüpfungsfunktion für die [PeriodsToDate](../mdx/periodstodate-mdx.md) -Funktion, wenn die Typeigenschaft der Attributhierarchie, eine Ebene auf dem basiert, um festgelegt ist *Monate*. Somit ist `Mtd(Member_Expression)` äquivalent zu `PeriodsToDate(Month_Level_Expression,Member_Expression)`.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Summe der Monat bis Datum Frachtkosten für Internetverkäufe für den Monat Juli 2002 bis einschließlich 20. Juli zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Summe &#40; MDX &#41;](../mdx/sum-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

