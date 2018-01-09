---
title: Unorder (MDX) | Microsoft Docs
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
f1_keywords: UNORDER
dev_langs: kbMDX
helpviewer_keywords: Unorder function
ms.assetid: a805df2a-6320-45bc-989f-90e85faf027f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2593c6f22915cbe5615f8d104b718fd4b3a7d6a5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="unorder-mdx"></a>Unorder (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Entfernt eine erzwungene Reihenfolge von einer angegebenen Menge.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Unorder** -Funktion entfernt jede Sortierung, die auf den Tupeln in der Menge durch eine andere Funktion oder Anweisung, wie z. B. die [Reihenfolge](../mdx/order-mdx.md) Funktion. Die Reihenfolge der Tupel in der Menge zurückgegebenes der **Unorder** Funktion unbestimmt ist.  
  
 Die **Unorder** Funktion dient als Hinweis für [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zur abfrageoptimierung bei der mengenverarbeitung. Wenn die Reihenfolge der Tupel in einer Menge für eine Berechnung oder Abfrage unwichtig ist, mithilfe der **Unorder** -Funktion einen Leistungsvorteil in solchen Fällen bieten kann. Z. B. die [NonEmpty (MDX)](../mdx/nonempty-mdx.md) Funktion möglicherweise eine bessere Leistung bei der für diese Funktion bereitgestellte Satz ungeordnet ist, als If ist [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Reihenfolge beibehalten muss, obwohl mit [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], der Abfrageprozessor versucht, die automatisch für viele Funktionen, wie z. B. verarbeitetes **Summe** und **aggregieren**. Der Leistungsvorteil mit **Unorder** wahrscheinlich nur bei sehr großen Mengen, die aus Millionen von Tupeln bestehen, bemerkbar.  
  
## <a name="example"></a>Beispiel  
 Der folgende Pseudocode veranschaulicht die Syntax für diese Funktion.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
