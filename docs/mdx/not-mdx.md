---
title: KEINE (MDX) | Microsoft Docs
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
- NOT
dev_langs:
- kbMDX
helpviewer_keywords:
- NOT operator [MDX]
ms.assetid: c11bd3b0-54b3-4a6d-babc-6067722194db
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6e8b509d70bbc3a16935d69217a703faed18b871
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="not-mdx"></a>NOT (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine logische Negation für einen numerischen Ausdruck aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der zurückgibt **"false"** , wenn das Argument ergibt **"true"** ist, andernfalls **"true"**.  
  
## <a name="remarks"></a>Hinweise  
 Die **nicht** -Operator behandelt den Ausdruck als booleschen Wert (null, 0, als **"false"** ist, andernfalls **"true"**), bevor der Operator die logische Negation ausführt. Die folgende Tabelle verdeutlicht, wie die **nicht** Operator die logische Negation ausführt.  
  
|*Expression1*|Rückgabewert|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
