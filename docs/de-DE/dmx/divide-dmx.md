---
title: (Division) (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 7afc06cd-054b-48c3-9c3c-9a0c17d15e63
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9b24f49594003f453f3258c431881bd0ddda0f70
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="divide-dmx"></a>(Division) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine arithmetische Operation aus, die eine Zahl durch eine andere dividiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parameter  
 *Dividend*  
 Ein gültiger DMX-Ausdruck (Data Mining-Erweiterungen), der einen numerischen Wert zurückgibt.  
  
 *Divisor*  
 Ein gültiger DMX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Wert, der den Datentyp des Parameters aufweist, der in der Rangfolge höher eingestuft ist.  
  
## <a name="remarks"></a>Hinweise  
 Der Wert, den dieser Operator zurückgibt, entspricht dem Quotienten des ersten und des zweiten Ausdrucks.  
  
 Beide Ausdrücke müssen denselben Datentyp haben, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren. Wenn der Divisor ausgewertet den Wert NULL hat, löst der Operator einen Fehler aus. Wenn sowohl der Divisor als auch der Dividend ausgewertet den Wert NULL haben, gibt der Operator den Wert NULL zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Arithmetische Operatoren &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatoren &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Teilen Sie &#40;SSIS-Ausdruck&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;Teilen Sie&#41; &#40;Transact-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
