---
title: LEN (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b110c6b9a20a216e50d1acbf9e207e5812e17e6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="len-ssis-expression"></a>LEN (SSIS-Ausdruck)
  Gibt die Anzahl von Zeichen in einem Zeichenausdruck zurück. Wenn die Zeichenfolge führende und nachfolgende Leerzeichen enthält, werden sie von der Funktion für die Anzahl berücksichtigt. LEN gibt identische Werte für dieselbe Zeichenfolge mit Einzelbyte- und Doppelbytezeichen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Der auszuwertende Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Das *character_expression* -Argument kann den Datentyp DT_WSTR, DT_TEXT, DT_NTEXT oder DT_IMAGE aufweisen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Wenn *character_expression* ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird dieses bzw. diese implizit in den DT_WSTR-Datentyp umgewandelt, bevor LEN ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Umwandlung &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Falls das an die LEN-Funktion übergebene Argument einen BLOB-Datentyp (Binary Large Object Block) aufweist, wie z. B. DT_TEXT, DT_NTEXT oder DT_IMAGE, gibt die Funktion die Anzahl der Bytes zurück.  
  
 LEN gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird die Länge eines Zeichenfolgenliterals zurückgegeben. Als Ergebnis wird 12 zurückgegeben.  
  
```  
LEN("Ball Bearing")  
```  
  
 In diesem Beispiel wird die Differenz zwischen der Länge von Werten in den Spalten **FirstName** und **LastName** zurückgegeben.  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 Gibt die Länge eines Computernamens mithilfe der **MachineName**-Systemvariablen zurück.  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
