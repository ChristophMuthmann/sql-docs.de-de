---
title: Effektiver boolescher Wert (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93c3ecaf4a4ded90a4b65aed08c6112fd9b670f1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="effective-boolean-value-xquery"></a>Effektiver boolescher Wert (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Folgende Werte sind effektive boolesche Werte:  
  
-   False, wenn der Operand eine leere Sequenz oder ein boolesches False ist.  
  
-   Anderenfalls ist der Wert True.  
  
 Der effektive boolesche Wert kann für Ausdrücke berechnet werden, die einen einzelnen booleschen Wert, eine Knotensequenz oder eine leere Sequenz zurückgeben. Beachten Sie, dass der boolesche Wert implizit berechnet wird, wenn folgende Typen von Ausdrücken verarbeitet werden:  
  
-   Logische Ausdrücke  
  
-   Die [funktioniert nicht](../xquery/functions-on-boolean-values-not-function.md)  
  
-   Die WHERE-Klausel eines FLWOR-Ausdrucks  
  
-   [Bedingte Ausdrücke](../xquery/conditional-expressions-xquery.md)  
  
-   [QuantifiedeExpressions](../xquery/quantified-expressions-xquery.md)  
  
 Das folgende Beispiel zeigt einen effektiven booleschen Wert. Wenn die **Wenn** -Ausdruck verarbeitet wird, wird der effektive boolesche Wert der Bedingung bestimmt. Da `/a[1]` eine leere Sequenz zurückgibt, ist der effektive boolesche Wert False. Das Ergebnis wird als XML mit einem Textknoten (false) zurückgegeben.  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 Im folgenden Beispiel ist der effektive boolesche Wert True, weil der Ausdruck eine nicht leere Sequenz zurückgibt.  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 Bei Abfragen typisierter **Xml** -Spalten oder-Variablen können Knoten vom booleschen Typ. Die **data()** in diesem Fall einen booleschen Wert zurückgibt. Wenn der Abfrageausdruck einen booleschen Wert zurückgibt, ist der effektive boolesche Wert True, was im nächsten Beispiel dargestellt ist. Das Beispiel zeigt außerdem Folgendes:  
  
-   Es wird eine XML-Schemaauflistung erstellt. Das Element \<b > in der Auflistung befindet, einen Boolean-Typ.  
  
-   Eine typisierte **Xml** Variable wird erstellt und abgefragt werden.  
  
-   Der Ausdruck `data(/b[1])` gibt einen booleschen True-Wert zurück. Der effektive boolesche Wert ist deshalb in diesem Fall True.  
  
-   Der Ausdruck `data(/b[2])` gibt einen booleschen Wert "false" zurück. Der effektive boolesche Wert ist deshalb in diesem Fall False.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Grundlagen](../xquery/xquery-basics.md)   
 [FLWOR-Anweisung und Iteration &#40; XQuery &#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
