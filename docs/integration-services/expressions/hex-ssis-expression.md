---
title: HEX (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- hexadecimal data
- HEX function
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 566bdd1b9aebb84fa9d76de5b3cb9a6a55346bb8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="hex-ssis-expression"></a>HEX (SSIS-Ausdruck)
  Gibt eine Zeichenfolge zurück, die den hexadezimalen Wert einer ganzen Zahl darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HEX(integer_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression*  
 Eine ganze Zahl mit oder ohne Vorzeichen.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 HEX gibt NULL zurück, wenn *integer_expression* NULL ist.  
  
 Das *integer_expression* -Argument muss zu einer ganzen Zahl ausgewertet werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Das zurückgegebene Ergebnis schließt keine Qualifizierer ein, wie z. B. das 0x-Präfix. Verwenden Sie den + (Verketten)-Operator, um ein Präfix einzuschließen. Weitere Informationen finden Sie unter [+ &#40;Verketten, SSIS-Ausdruck&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Die Buchstaben A bis F, die für die HEX-Schreibweise verwendet werden, werden in Großbuchstaben angezeigt.  
  
 Integer-Datentypen weisen für die sich ergebende Zeichenfolge die folgende Länge auf:  
  
-   DT_I1 und DT_UI1 geben eine Zeichenfolge mit einer maximalen Länge von 2 zurück.  
  
-   DT_I2 und DT_UI2 geben eine Zeichenfolge mit einer maximalen Länge von 4 zurück.  
  
-   DT_I4 und DT_UI4 geben eine Zeichenfolge mit einer maximalen Länge von 8 zurück.  
  
-   DT_I8 und DT_UI8 geben eine Zeichenfolge mit einer maximalen Länge von 16 zurück.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein numerisches Literal verwendet. Die Funktion gibt den Wert 190 zurück.  
  
```  
HEX(400)   
```  
  
 In diesem Beispiel wird die **ReorderPoint** -Spalte verwendet. Der Datentyp der Spalte ist **smallint**. Falls **ReorderPoint** gleich 750 ist, gibt die Funktion 2EE zurück.  
  
```  
HEX(ReorderPoint)   
```  
  
 In diesem Beispiel wird **LocaleID**als Systemvariable verwendet. Falls **LocaleID** gleich 1033 ist, gibt die Funktion 409 zurück.  
  
```  
HEX(@LocaleID)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
