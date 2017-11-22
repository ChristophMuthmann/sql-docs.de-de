---
title: "Vorgänger (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ASCENDANTS
dev_langs: kbMDX
helpviewer_keywords: Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2b81f8dffc10d5fa62c264814d3f1215c7f44c5a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Menge der vorausgehenden Elemente zu einem angegebenen Element zurück, einschließlich des Elements selbst.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Vorgänger** Funktion gibt alle Vorgänger eines Elements aus der Member selbst bis zum Anfang des Mitglieds der Hierarchie zurück; genauer gesagt, es führt einen Postorder-Durchlauf der Hierarchie für das angegebene Element und dann gibt alle Vorgänger der Elemente im Zusammenhang mit den Member auf, einschließlich selbst in einem Satz. Dies ist im Gegensatz zu den [Vorgänger](../mdx/ancestor-mdx.md) -Funktion, die ein bestimmtes vorausgehendes Element oder Vorgänger, auf einer bestimmten Ebene zurückgibt.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel gibt die Anzahl der Bestellungen des Wiederverkäufers für die `[Sales Territory].[Northwest]` Element und alle vorausgehenden Elemente des Elements aus der **Adventure Works** Cube. Die **Vorgänger** Funktion bildet die Menge der `[Sales Territory].[Northwest]` Element und seinen vorausgehenden Elementen für die ROWS-Achse.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
