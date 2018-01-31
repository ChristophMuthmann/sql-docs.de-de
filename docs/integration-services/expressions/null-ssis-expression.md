---
title: NULL (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b8b9f8e703b402b55bef24b30977b086b75d1f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="null-ssis-expression"></a>NULL (SSIS-Ausdruck)
  Gibt einen NULL-Wert eines angeforderten Datentyps zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>Argumente  
 *typespec*  
 Ein gültiger Datentyp. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 Ein beliebiger gültiger Datentyp mit einem NULL-Wert.  
  
## <a name="remarks"></a>Remarks  
 NULL gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Parameter sind erforderlich, um einen NULL-Wert für bestimmte Datentypen anzufordern. In der folgenden Tabelle sind diese Datentypen und die zugehörigen Parameter aufgelistet.  
  
|Datentyp|Parameter|Beispiel|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) wandelt 30 Zeichen mithilfe der 1252-Codepage in den DT_STR-Datentyp um.|  
|DT_WSTR|*charcount*|(DT_WSTR,20) wandelt 20 Zeichen in den DT_WSTR-Datentyp um.|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) wandelt 50 Bytes in den DT_BYTES-Datentyp um.|  
|DT_DECIMAL|*scale*|(DT_DECIMAL,2) wandelt einen numerischen Wert mithilfe von 2 Dezimalstellen in den DT_DECIMAL-Datentyp um.|  
|DT_NUMERIC|*precision*<br /><br /> *scale*|(DT_NUMERIC,10,3) wandelt einen numerischen Wert mithilfe einer Genauigkeit von 10 und 3 Dezimalstellen in den DT_NUMERIC-Datentyp um.|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) wandelt einen Wert mithilfe der 1252-Codepage in den DT_TEXT-Datentyp um.|  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesen Beispielen wird der NULL-Wert der Datentypen zurückgegeben: DT_STR, DT_DATE und DT_BOOL.  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ISNULL &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/isnull-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
