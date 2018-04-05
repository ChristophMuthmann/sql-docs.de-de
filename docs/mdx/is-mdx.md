---
title: IST (MDX) | Microsoft Docs
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
- IS
dev_langs:
- kbMDX
helpviewer_keywords:
- IS operator
ms.assetid: dc8c0b91-3bb1-49e5-8d70-57545baaa8e0
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2851106b509cb3907b06b21adc0d08e850af4fdd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="is-mdx"></a>IS (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen logischen Vergleich zweier Objektausdrücke aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen MDX-Objektverweis zurückgibt.  
  
 *Expression2*  
 Ein gültiger MDX-Ausdruck, der einen MDX-Objektverweis zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der zurückgibt **"true"** , wenn beide Argumente für das gleiche Objekt verweisen, andernfalls **"false"**. Wenn die **NULL** Schlüsselwort angegeben ist, gibt der Operator **"true"** Wenn *Expression1* ist **null**ist, andernfalls **"false"**.  
  
## <a name="remarks"></a>Remarks  
 Die **IS** -Operator wird häufig verwendet, um zu bestimmen, ob Tupeln und Elemente Idempotent sind, was bedeutet, dass sie genau gleich sind.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie Sie die **IS** Operator zum Überprüfen, ob das aktuelle Element auf einer Achse ein spezifisches Element ist:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
