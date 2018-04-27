---
title: REPLACE (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- replacing string expression
- REPLACE function
ms.assetid: a6837043-ea70-4c6a-9c7a-6868b02b2adc
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7d502c8c0a4e8305f9e8f19b28e550c7f102cef9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="replace-ssis-expression"></a>REPLACE (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck zurück, nachdem eine Zeichenfolge im Ausdruck durch eine andere Zeichenfolge oder durch eine leere Zeichenfolge ersetzt wurde.  
  
> [!NOTE]  
>  Von der REPLACE-Funktion werden häufig lange Zeichenfolgen verwendet. Die Folgen der Kürzung können unauffällig behandelt werden oder eine Warnung oder einen Fehler verursachen. Weitere Informationen finden Sie unter [Syntax &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REPLACE(character_expression,searchstring,replacementstring)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein gültiger Zeichenausdruck, den die Funktion durchsucht.  
  
 *searchstring*  
 Ein gültiger Zeichenausdruck, nach dem die Funktion sucht.  
  
 *replacementstring*  
 Ein gültiger Zeichenausdruck, der den zu ersetzenden Ausdruck darstellt.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 Die Länge von *searchstring* darf nicht Null sein.  
  
 Die Länge von *replacementstring* darf Null sein.  
  
 Für die Argumente *searchstring* und *replacementstring* sind Variablen und Spalten möglich.  
  
 REPLACE kann nur mit dem DT_WSTR-Datentyp verwendet werden. Das*character_expression1, character_expression2,* -Argument und das *character_expression3* -Argument, die Zeichenfolgenliterale oder Datenspalten mit dem DT_STR-Datentyp sind, werden implizit in den DT_WSTR-Datentyp umgewandelt, bevor REPLACE die Operation ausführt. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Umwandlung &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 REPLACE gibt ein NULL-Ergebnis zurück, wenn eines der Argumente NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Als Ergebnis wird "All Terrain Bike" zurückgegeben.  
  
```  
REPLACE("Mountain Bike", "Mountain","All Terrain")  
```  
  
 In diesem Beispiel wird die Zeichenfolge "Bike" aus der **Product** -Spalte entfernt.  
  
```  
REPLACE(Product, "Bike","")  
```  
  
 In diesem Beispiel werden Werte in der **DaysToManufacture** -Spalte ersetzt. Die Spalte weist einen Integer-Datentyp auf, und der Ausdruck enthält die Umwandlung von **DaysToManufacture** in den DT_WSTR-Datentyp.  
  
```  
REPLACE((DT_WSTR,8)DaysToManufacture,"6","5")  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SUBSTRING &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/substring-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
