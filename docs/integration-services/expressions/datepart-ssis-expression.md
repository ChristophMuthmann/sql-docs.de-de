---
title: "DATEPART (SSIS-Ausdruck) | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datumsangaben [Integration Services], DATEPART"
  - "DATEPART-Funktion"
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# DATEPART (SSIS-Ausdruck)
  Gibt eine ganze Zahl zurück, die einen datepart-Wert eines Datums darstellt.  
  
## Syntax  
  
```  
  
DATEPART(datepart, date)  
```  
  
## Argumente  
 *datepart*  
 Der Parameter, der angibt, für welche Datumseinheit ein neuer Wert zurückgegeben werden soll.  
  
 *Datum*  
 Ein Ausdruck, der ein gültiges Datum oder eine Zeichenfolge im Datumsformat zurückgibt.  
  
## Ergebnistypen  
 DT_I4  
  
## Hinweise  
 DATEPART gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Ein Datumsliteral muss explizit in einen der date-Datentypen umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 In der folgenden Tabelle sind die datepart-Werte und Abkürzungen aufgeführt, die von der Ausdrucksauswertung erkannt werden. Bei datepart-Namen wird die Groß-/Kleinschreibung nicht berücksichtigt.  
  
|Datumseinheit|Abkürzungen|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Week|wk, ww|  
|Arbeitstag|dw|  
|Hour|Hh|  
|Minute|mi, n|  
|Zweimal|ss, s|  
|Millisekunde|Ms|  
  
## Beispiele für SSIS-Ausdrücke  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Monat in einem Datumsliteral darstellt. Falls das Datum das Format „MM/TT/JJJJ“ aufweist, gibt dieses Beispiel „11“ zurück.  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die den Tag in der **ModifiedDate** -Spalte darstellt.  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 In diesem Beispiel wird die ganze Zahl zurückgegeben, die das Jahr des aktuellen Datums darstellt.  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## Siehe auch  
 [DATEADD &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DAY &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  