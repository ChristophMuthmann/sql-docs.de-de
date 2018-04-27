---
title: REVERSE (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1daa8f608a6b99c384f6c8f2c9b6b657a30333c7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
