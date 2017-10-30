---
title: + (Verketten von Zeichenfolgen) (MDX) | Microsoft Docs
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
- +
dev_langs:
- kbMDX
helpviewer_keywords:
- string concatenation operators
- + (string concatenation)
ms.assetid: d77636b1-2973-4587-af35-54aba5700d9a
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b5c2fd213bffba6a9863f8b96f847e2d46df388e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="-string-concatenation-mdx"></a>+ (Verketten von Zeichenfolgen) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt eine Zeichenfolgenoperation aus, die mindestens zwei Zeichenfolgen, Tupel oder eine Kombination von Zeichenfolgen und Tupeln verkettet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parameter  
 *String_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen Zeichenfolgenwert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Wert vom Datentyp des Parameters, der in der Rangfolge höher eingestuft ist.  
  
## <a name="remarks"></a>Hinweise  
 Beide Ausdrücke müssen denselben Datentyp haben, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren. Hat ein Ausdruck als Ergebnis den Wert NULL, gibt der Operator das Ergebnis des anderen Ausdrucks zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

