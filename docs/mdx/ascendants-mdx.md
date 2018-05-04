---
title: Vorgänger (MDX) | Microsoft Docs
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
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7eb0bff443065cff7a279320d85d848ae303f5dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
