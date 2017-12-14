---
title: CEILING (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 971c7038c0b144ac4073162e0d14b519e263328f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
 [FLOOR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
