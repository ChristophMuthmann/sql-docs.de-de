---
title: FLOOR (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10b5f2fe1ad7e1a474f960e51027d8675e2d690f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="floor-ssis-expression"></a>FLOOR (SSIS-Ausdruck)
  Gibt die größte ganze Zahl zurück, die kleiner oder gleich einem numerischen Ausdruck ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 Der numerische Datentyp des expression-Arguments. Das Ergebnis ist der ganzzahlige Teil des berechneten Werts mit dem gleichen Datentyp wie *numeric_expression*.  
  
## <a name="remarks"></a>Hinweise  
 FLOOR gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesen Beispielen wird die FLOOR-Funktion auf positive und negative Werte und auf Null angewendet.  
  
```  
FLOOR(123.45)  
```  
  
 Gibt 123.00 zurück.  
  
```  
FLOOR(-123.45)  
```  
  
 Gibt -124.00 zurück.  
  
```  
FLOOR(0.00)  
```  
  
 Gibt 0.00 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [CEILING &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
