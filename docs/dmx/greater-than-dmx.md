---
title: "&gt;(Größer als) (DMX) | Microsoft Docs"
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
dev_langs:
- DMX
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: a1485c02-8d10-4722-b8cd-b747c472741b
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 515b8b3dfe8f08b57adaadb6e945baa0a685e38a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="gt-greater-than-dmx"></a>&gt;(Größer als) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine Vergleichsoperation aus, bei der ermittelt wird, ob der Wert eines DMX-Ausdrucks (Data Mining Extensions) größer als der Wert eines anderen DMX-Ausdrucks ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DMX_Expression > DMX_Expression  
```  
  
#### <a name="parameters"></a>Parameter  
 *DMX_Expression*  
 Ein gültiger DMX-Ausdruck.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der TRUE enthält, wenn beide Parameter ungleich NULL sind und der erste Parameter einen Wert hat, der größer als der Wert des zweiten Parameters ist. Der boolesche Wert enthält FALSE, wenn beide Parameter ungleich NULL sind und der erste Parameter einen Wert aufweist, der gleich dem oder kleiner als der Wert des zweiten Parameters ist. Der boolesche Wert enthält einen NULL-Wert, wenn einer der Parameter oder beide Parameter ausgewertet einen NULL-Wert haben.  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichsoperatoren &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

