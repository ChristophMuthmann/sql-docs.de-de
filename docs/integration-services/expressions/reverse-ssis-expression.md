---
title: REVERSE (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2a20cd5329e2d94cb4da44208e6811fd076d6cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="reverse-ssis-expression"></a>REVERSE (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck in umgekehrter Reihenfolge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Der Zeichenausdruck, dessen Reihenfolge umgekehrt werden soll.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 Das *character_expression* -Argument muss den Datentyp „DT_WSTR“ aufweisen.  
  
 REVERSE gibt ein NULL-Ergebnis zurück, wenn *character_expression* NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Als Ergebnis wird "ekiB niatnuoM" zurückgegeben.  
  
```  
REVERSE("Mountain Bike")  
```  
  
 In diesem Beispiel wird eine Variable verwendet. Falls **Name** Touring Bike enthält, wird als Ergebnis "ekiB gniruoT" zurückgegeben.  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
