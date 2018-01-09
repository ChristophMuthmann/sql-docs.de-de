---
title: Teilmenge (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: subset
dev_langs: kbMDX
helpviewer_keywords: Subset function
ms.assetid: 49a7cd28-cd6f-4ae7-8c91-94a8652a97a5
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6f461f979c9d064305b0004fb906673e97f2ab5f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="subset-mdx"></a>Subset (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Teilmenge von Tupeln aus einer angegebenen Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Starten*  
 Ein gültiger numerischer Ausdruck, der die Position des ersten zurückzugebenden Tupels angibt.  
  
 *Anzahl*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Aus dem angegebenen Satz der **Teilmenge** Funktion gibt eine Teilmenge, die angegebene Anzahl von Tupeln enthält, beginnend an der angegebenen Startposition, zurück. Die Startposition basiert auf einem nullbasierten Index, d. h., null (0) entspricht dem ersten Tupel in der Menge, 1 entspricht dem zweiten Tupel usw.  
  
 Wenn *Anzahl* nicht angegeben ist, wird die Funktion gibt alle Tupel von *starten* bis zum Ende des Satzes.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Reseller Sales-Measure für die fünf bestverkauften Produktunterkategorien unabhängig von der Hierarchie basierend auf Reseller Gross Profit zurückgegeben. Die **Teilmenge** Funktion wird verwendet, um nur die ersten fünf Mengen aus dem Ergebnis zurückzugeben, nach dem Sortieren des Ergebnisses mithilfe der **Reihenfolge** Funktion.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
