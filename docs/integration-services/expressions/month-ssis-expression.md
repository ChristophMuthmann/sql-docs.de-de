---
title: MONTH (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2a75f2f611519d38e168748b703a1e80e1c8e2a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="month-ssis-expression"></a>MONTH (SSIS-Ausdruck)
  Gibt eine ganze Zahl zurück, die den datepart-Wert für die Monatsangabe in einem Datum darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>Argumente  
 *Datum*  
 Ein Datum in einem beliebigen Datumsformat.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 MONTH gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Ein Datumsliteral muss explizit in einen der date-Datentypen umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  Der Ausdruck wird nicht überprüft, wenn ein Datumsliteral explizit in einen der folgenden Datumsdatentypen umgewandelt wird: DT_DBTIMESTAMPOFFSET oder DT_DBTIMESTAMP2.  
  
 Die MONTH-Funktion entspricht bezüglich der Verwendung der DATEPART("Month", date)-Funktion, ist jedoch schneller.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird der Monat eines Datumsliterals zurückgegeben. Falls das Datum das Format "mm/dd/yyyy" aufweist, wird 11 zurückgegeben.  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Monat in der **ModifiedDate** -Spalte darstellt.  
  
```  
MONTH(ModifiedDate)  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Monat des aktuellen Datums darstellt.  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DATEADD &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [YEAR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
