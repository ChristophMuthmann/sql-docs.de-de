---
title: KEINE (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: NOT
dev_langs: DMX
helpviewer_keywords: NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c242a6767e60b04249d69d340806d0cf78a374e2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ein logischer Operator, der eine logische Negation für einen numerischen Ausdruck ausführt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger DMX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der FALSE zurückgibt, wenn das Argument zu TRUE ausgewertet wird; anderenfalls FALSE.  
  
## <a name="remarks"></a>Hinweise  
 Das Argument wird als boolescher Wert (0 als FALSE, anderenfalls TRUE) behandelt, bevor der Operator die logische Negation ausführt. Wenn *Expression1* ist "true", gibt der Operator "false" zurück. Wenn *Expression1* ist "false", der Operator gibt "true" zurück. Die folgende Tabelle verdeutlicht, wie die logische Konjunktion ausgeführt wird.  
  
|Expression1|Rückgabewert|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Logische Operatoren &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
