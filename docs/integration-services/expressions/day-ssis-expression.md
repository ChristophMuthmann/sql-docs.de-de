---
title: DAY (SSIS-Ausdruck) | Microsoft Docs
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
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e297f7021239ded4aa76ad61e75fddba528ccf6
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="day-ssis-expression"></a>DAY (SSIS-Ausdruck)
  Gibt eine ganze Zahl zurück, die den datepart-Wert für den Tag eines Datums darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>Argumente  
 *Datum*  
 Ein Ausdruck, der ein gültiges Datum oder eine Zeichenfolge im Datumsformat zurückgibt.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_I4  
  
## <a name="remarks"></a>Hinweise  
 DAY gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Ein Datumsliteral muss explizit in einen der date-Datentypen umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  Der Ausdruck wird nicht überprüft, wenn ein Datumsliteral explizit in einen der folgenden Datumsdatentypen umgewandelt wird: DT_DBTIMESTAMPOFFSET oder DT_DBTIMESTAMP2.  
  
 Die DAY-Funktion entspricht bezüglich der Verwendung der DATEPART("Day", date)-Funktion, ist jedoch schneller.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird der Tag eines Datumsliterals zurückgegeben. Falls das Datum das Format "mm/dd/yyyy" aufweist, wird 23 zurückgegeben.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Tag in der **ModifiedDate** -Spalte darstellt.  
  
```  
DAY(ModifiedDate)  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Tag des aktuellen Datums darstellt.  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DATEADD &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [Monat &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [Jahr &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

