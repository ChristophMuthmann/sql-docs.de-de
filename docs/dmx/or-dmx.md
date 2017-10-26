---
title: ODER (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- DMX
helpviewer_keywords:
- OR operator
ms.assetid: 727a38a9-7f75-4963-8e8a-aa703c129d30
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41cdd1638dc31eefa9cb034db33ef9d30162d617
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ein logischer Operator, der eine logische Disjunktion zweier numerischer Ausdrücke ausführt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger DMX-Ausdruck (Data Mining-Erweiterungen), der einen numerischen Wert zurückgibt.  
  
 *Expression2*  
 Ein gültiger DMX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der TRUE zurückgibt, wenn eines der Argumente oder beide Argumente zu TRUE ausgewertet werden; anderenfalls FALSE.  
  
## <a name="remarks"></a>Hinweise  
 Beide Argumente werden als boolesche Werte (0 als FALSE, anderenfalls TRUE) behandelt, bevor der Operator die logische Disjunktion ausführt. Wird eines der Argumente oder werden beide Argumente zu TRUE ausgewertet, gibt der Operator TRUE zurück Wenn *Expression1* auf "true" ausgewertet und *Expression2* zu FALSE ausgewertet wird, gibt der Operator "true" zurück.  
  
 Die folgende Tabelle verdeutlicht, wie die logische Disjunktion ausgeführt wird.  
  
|Expression1|Expression2|Rückgabewert|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Logische Operatoren &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

