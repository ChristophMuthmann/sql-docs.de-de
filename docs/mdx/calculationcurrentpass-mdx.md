---
title: CalculationCurrentPass (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CALCULATIONCURRENTPASS
dev_langs: kbMDX
helpviewer_keywords: CalculationCurrentPass function
ms.assetid: 7069f7a0-8ec8-4293-8db3-b35b9327f437
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 675c708517d2624919c926248a91455842111ac4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="calculationcurrentpass-mdx"></a>CalculationCurrentPass (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den aktuellen Berechnungsdurchlauf eines Cubes für den angegebenen Abfragekontext zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CalculationCurrentPass()  
```  
  
## <a name="remarks"></a>Hinweise  
 Die **CalculationCurrentPass** Funktion gibt den nullbasierten Index des Berechnungsdurchlaufs für den aktuellen Abfragekontext zurück. Durch die automatische rekursionsauflösung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], diese Funktion hat kaum noch praktischen nutzen.  
  
## <a name="see-also"></a>Siehe auch  
 [CalculationPassValue &#40; MDX &#41;](../mdx/calculationpassvalue-mdx.md)   
 [IIf &#40; MDX &#41;](../mdx/iif-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
