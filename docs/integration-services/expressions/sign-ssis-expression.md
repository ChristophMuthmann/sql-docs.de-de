---
title: SIGN (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a926bddda6c86a7930a349915cc2a77602448b4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sign-ssis-expression"></a>SIGN (SSIS-Ausdruck)
  Gibt das positive (+1) oder negative (-1) Vorzeichen oder Null (0) für einen numerischen Ausdruck zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck mit Vorzeichen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_I4  
  
## <a name="remarks"></a>Hinweise  
 SIGN gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird das Vorzeichen eines numerischen Literals zurückgegeben. Als Ergebnis wird -1 zurückgegeben.  
  
```  
SIGN(-123.45)  
```  
  
 In diesem Beispiel wird das Vorzeichen aus der Subtraktion der **StandardCost** -Spalte von der **DealerPrice** -Spalte zurückgegeben.  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

