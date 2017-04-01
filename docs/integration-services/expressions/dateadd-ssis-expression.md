---
title: "DATEADD (SSIS-Ausdruck) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datumsangaben [Integration Services], DATEADD"
  - "Datumsangaben [Integration Services]"
  - "DATEADD-Funktion"
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# DATEADD (SSIS-Ausdruck)
  Gibt einen neuen DT_DBTIMESTAMP-Wert zurück, nachdem einem angegebenen datepart-Wert in einem Datum eine Zahl hinzugefügt wurde, die ein Datums- oder Zeitintervall darstellt. Der number-Parameter muss zu einer ganzen Zahl ausgewertet werden, und der date-Parameter muss zu einem gültigen Datum ausgewertet werden.  
  
## Syntax  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## Argumente  
 *datepart*  
 Der Parameter, der angibt, welcher Datumseinheit eine Zahl hinzugefügt werden soll.  
  
 *number*  
 Der Wert, um den *datepart* inkrementiert wird. Dieser Wert muss ein ganzzahliger Wert sein, der beim Analysieren des Ausdrucks bekannt ist.  
  
 *Datum*  
 Ein Ausdruck, der ein gültiges Datum oder eine Zeichenfolge im Datumsformat zurückgibt.  
  
## Ergebnistypen  
 DT_DBTIMESTAMP  
  
## Hinweise  
 In der folgenden Tabelle sind die datepart-Werte und Abkürzungen aufgeführt, die von der Ausdrucksauswertung erkannt werden. Bei datepart-Namen wird die Groß-/Kleinschreibung nicht berücksichtigt.  
  
|Datumseinheit|Abkürzungen|  
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
  
 Ein Datumsliteral muss explizit in einen der date-Datentypen umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 DATEADD gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Fehler treten auf, wenn ein Datum ungültig, die Datums- oder Zeiteinheit keine Zeichenfolge oder das Inkrement keine statische ganze Zahl ist.  
  
## Beispiele für SSIS-Ausdrücke  
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
  
## Siehe auch  
 [DATEDIFF &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  