---
title: UND (DMX) | Microsoft Docs
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
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AND
dev_langs:
- DMX
helpviewer_keywords:
- AND, DMX
ms.assetid: d337b20c-f80e-48be-9354-371367e53735
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bcb67e3b5c16a9bee84271eebc2083a065e924d9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine logische Konjunktion zweier numerischer Ausdrücke aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger DMX-Ausdruck (Data Mining-Erweiterungen), der einen numerischen Wert zurückgibt.  
  
 *Expression2*  
 Ein gültiger DMX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der TRUE zurückgibt, wenn beide Argumente zu TRUE ausgewertet werden; anderenfalls FALSE.  
  
## <a name="remarks"></a>Hinweise  
 Beide Parameter werden als boolesche Werte (0 als FALSE, anderenfalls TRUE) behandelt, bevor der Operator die logische Konjunktion ausführt. In der folgenden Tabelle sind die Werte aufgeführt, die entsprechend den unterschiedlichen Kombinationen der Parameterwerte zurückgegeben werden.  
  
|Expression1|Expression2|Rückgabewert|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Logische Operatoren &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

