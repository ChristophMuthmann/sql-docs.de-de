---
title: Dividieren (MDX) | Microsoft Docs
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
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4bff8fd59df9aa01e88fcd5d8a71f209f48332eb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="divide-mdx"></a>Dividieren (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine Division aus und gibt ein alternatives Ergebnis oder BLANK() bei Division durch 0 zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumente  
 *Zähler*  
 Der Dividend oder Zahl dividiert werden soll.  
  
 *Nenner*  
 Der Divisor oder Zahl, durch die dividiert werden soll.  
  
 *alternateresult*  
 (Optional) Der Rückgabewert, wenn die Division durch null zu einem Fehler führt. Der Standardwert ist BLANK(), wenn nichts angegeben ist.  
  
## <a name="remarks"></a>Hinweise  
 Das alternative Ergebnis für eine Division durch 0 muss eine Konstante sein.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
