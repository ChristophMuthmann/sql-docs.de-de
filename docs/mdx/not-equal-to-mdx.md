---
title: '&lt;&gt; (Ungleich) (MDX) | Microsoft Docs'
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
- <>
dev_langs:
- kbMDX
helpviewer_keywords:
- not equal to operator (<>)
- <> (not equal to operator)
ms.assetid: b4eb3f1c-8b68-4530-a8f3-e3b8414ac789
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dea54629c9a1e1d5add6659e0eaaca2dc9d91c92
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (Ungleich) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks (Multidimensional Expressions) ungleich dem Wert eines anderen MDX-Ausdrucks ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parameter  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der auf den folgenden Bedingungen basiert:  
  
-   **"true"** Wenn beide Parameter ungleich Null sind und der erste Parameter nicht gleich dem zweiten Parameter ist.  
  
-   **"false"** Wenn beide Parameter ungleich Null sind und der erste Parameter der zweite Parameter gleich ist.  
  
-   NULL, wenn mindestens einer der Parameter zu einem NULL-Wert ausgewertet wird.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
