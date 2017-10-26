---
title: CEILING (SSIS-Ausdruck) | Microsoft Docs
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
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce44f2297c19b62687ca097343dc970397ca28d6
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ceiling-ssis-expression"></a>CEILING (SSIS-Ausdruck)
  Gibt die kleinste ganze Zahl zurück, die größer oder gleich einem numerischen Ausdruck ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 Der Datentyp des numerischen Ausdrucks, der an die Funktion übergeben wird.  
  
## <a name="remarks"></a>Hinweise  
 CEILING gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesen Beispielen wird die CEILING-Funktion auf positive und negative Werte und auf Null angewendet.  
  
```  
CEILING(123.74)  
```  
  
 Gibt 124,00 zurück.  
  
```  
CEILING(-124.27)  
```  
  
 Gibt -124.00 zurück.  
  
```  
CEILING(0.00)  
```  
  
 Gibt 0.00 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [FLOOR &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

