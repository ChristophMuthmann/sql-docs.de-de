---
title: FINDSTRING (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
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
- FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 56520a56a70622e23e7c407ed788f8f8f0ba3dc6
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="findstring-ssis-expression"></a>FINDSTRING (SSIS-Ausdruck)
  Gibt den Speicherort für das angegebene Auftreten einer Zeichenfolge innerhalb eines Zeichenausdrucks zurück. Das Ergebnis ist der einsbasierte Index für das Auftreten. Der string-Parameter muss zu einem Zeichenausdruck und der occurrence-Parameter zu einer ganzen Zahl ausgewertet werden. Wenn die Zeichenfolge nicht gefunden wird, wird 0 zurückgegeben. Wenn die Zeichenfolge weniger auftritt als im occurrence-Argument angegeben, wird ebenfalls 0 zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Die Zeichenfolge, in der gesucht werden soll.  
  
 *searchstring*  
 Die Zeichenfolge, nach der gesucht werden soll.  
  
 *occurrence*  
 Eine ganze Zahl mit oder ohne Vorzeichen, die angibt, welches Auftreten von *searchstring* gemeldet werden soll.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 FINDSTRING kann nur mit dem DT_WSTR-Datentyp verwendet werden.  Das*character_expression* -Argument und das *searchstring* -Argument, die Zeichenfolgenliterale oder Datenspalten mit dem DT_STR-Datentyp sind, werden implizit in den DT_WSTR-Datentyp umgewandelt, bevor FINDSTRING die Operation ausführt. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md) und [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 FINDSTRING gibt NULL zurück, wenn *character_expression* oder *searchstring* NULL sind.  
  
 Verwenden Sie den Wert 1 für das *occurrence* -Argument, um den Index des ersten Vorkommens abzurufen, 2 für das zweite Vorkommen usw.  
  
 *occurrence* muss eine ganze Zahl mit einem Wert größer als 0 sein.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Der Wert 11 wird zurückgegeben.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Da die Zeichenfolge "NY" nur zweimal auftritt, wird 0 zurückgegeben.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 In diesem Beispiel wird die **Name** -Spalte verwendet. Der Speicherort des zweiten „n“ in der Spalte **Name** wird zurückgegeben. Das Ergebnis hängt vom Wert in **Name**ab. Wenn die **Name** -Spalte „Anderson“ enthält, gibt die Funktion den Wert 8 zurück.  
  
```  
FINDSTRING(Name, "n", 2)   
```  
  
 In diesem Beispiel werden die Spalten **Name** und **Size** verwendet. Der Speicherort des äußeren linken Zeichens des **Size** -Arguments in der **Name** -Spalte wird zurückgegeben. Das Ergebnis hängt von den Spaltenwerten ab. Falls **Name** „Mountain,500Red,42“ und **Size** „42“ enthält, wird 17 zurückgegeben.  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [REPLACE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/replace-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
