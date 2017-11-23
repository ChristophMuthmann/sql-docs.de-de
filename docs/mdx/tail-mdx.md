---
title: Tail (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: TAIL
dev_langs: kbMDX
helpviewer_keywords: Tail function
ms.assetid: d62a1bb2-55c0-4939-8526-cdc3d444ffe2
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 72466a551ccf2cf159d6c041cd94ac32ad3ca20a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="tail-mdx"></a>Tail (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Teilmenge vom Ende einer Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Anzahl*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Die **Tail** Funktion gibt die angegebene Anzahl von Tupeln vom Ende der angegebenen Menge zurück. Die Reihenfolge der Elemente wird beibehalten. Der Standardwert von *Anzahl* ist 1. Wenn die angegebene Anzahl der Tupel kleiner als 1 ist, gibt die Funktion die leere Menge zurück. Wenn die angegebene Anzahl der Tupel größer ist als die Anzahl der Tupel in der Menge, gibt die Funktion die ursprüngliche Menge zurück.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Reseller Sales-Measure für die fünf bestverkauften Produktunterkategorien unabhängig von der Hierarchie basierend auf Reseller Gross Profit zurückgegeben. Die **Tail** Funktion wird verwendet, um nur die letzten fünf Mengen aus dem Ergebnis zurückzugeben, nachdem das Ergebnis in umgekehrter Reihenfolge sortiert wird mithilfe der **Reihenfolge** Funktion.  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
