---
title: "+ (Hinzufügen) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- +
dev_langs:
- kbMDX
helpviewer_keywords:
- + (add)
- add operator (+)
ms.assetid: f076d5bf-3ff3-4009-887a-28072fd599ca
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d8c878b0b91e6bb97538b5b5181fb9d4f3f0c646
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="-add-mdx"></a>+ (Addition) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine arithmetische Operation aus, die zwei Zahlen addiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parameter  
 *Numerische Ausdrücke*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Wert vom Datentyp des Parameters, der in der Rangfolge höher eingestuft ist.  
  
## <a name="remarks"></a>Hinweise  
 Beide Ausdrücke müssen denselben Datentyp haben, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren. Hat ein Ausdruck als Ergebnis den Wert NULL, gibt der Operator das Ergebnis des anderen Ausdrucks zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

