---
title: DATEADD (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9f730b37d29a33c9a0c5248760203862a8470e7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="dateadd-ssis-expression"></a>DATEADD (SSIS-Ausdruck)
  Gibt einen neuen DT_DBTIMESTAMP-Wert zurück, nachdem einem angegebenen datepart-Wert in einem Datum eine Zahl hinzugefügt wurde, die ein Datums- oder Zeitintervall darstellt. Der number-Parameter muss zu einer ganzen Zahl ausgewertet werden, und der date-Parameter muss zu einem gültigen Datum ausgewertet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>Argumente  
 *datepart*  
 Der Parameter, der angibt, welcher Datumseinheit eine Zahl hinzugefügt werden soll.  
  
 *number*  
 Der Wert, um den *datepart*inkrementiert wird. Dieser Wert muss ein ganzzahliger Wert sein, der beim Analysieren des Ausdrucks bekannt ist.  
  
 *Datum*  
 Ein Ausdruck, der ein gültiges Datum oder eine Zeichenfolge im Datumsformat zurückgibt.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Tabelle sind die datepart-Werte und Abkürzungen aufgeführt, die von der Ausdrucksauswertung erkannt werden. Bei datepart-Namen wird die Groß-/Kleinschreibung nicht berücksichtigt.  
  
|datepart|Abkürzungen|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Arbeitstag|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|Zweimal|ss, s|  
|Millisekunde|Ms|  
  
 Das *number* -Argument muss beim Analysieren des Ausdrucks verfügbar sein. Bei diesem Argument kann es sich um eine Konstante oder eine Variable handeln. Spaltenwerte können nicht verwendet werden, weil diese Werte beim Analysieren des Ausdrucks nicht bekannt sind.  
  
 Das *datepart* -Argument muss in Anführungszeichen eingeschlossen werden.  
  
 Ein Datumsliteral muss explizit in einen der date-Datentypen umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 DATEADD gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Fehler treten auf, wenn ein Datum ungültig, die Datums- oder Zeiteinheit keine Zeichenfolge oder das Inkrement keine statische ganze Zahl ist.  
  
## <a name="ssis-expression-examples"></a>Beispiele für SSIS-Ausdrücke  
 In diesem Beispiel wird dem aktuellen Datum ein Monat hinzugefügt.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 In diesem Beispiel werden den Datumsangaben in der **ModifiedDate** -Spalte 21 Tage hinzugefügt.  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 In diesem Beispiel werden einem Datumsliteral 2 Jahre hinzugefügt.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DATEDIFF &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
