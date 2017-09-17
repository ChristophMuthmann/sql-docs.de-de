---
title: Beispiel SQLGetTypeInfo Resultset | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b43138efe4c6540b12bbfeeb0185f61ad0e65861
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="example-sqlgettypeinfo-result-set"></a>SQLGetTypeInfo Beispielergebnis
Ruft die Anwendung **SQLGetTypeInfo** um zu bestimmen, welche Datentypen von einer Datenquelle und die Eigenschaften dieser Datentypen unterstützt werden. Die folgenden Tabellen zeigen ein beispielresultset zurückgegebenes **SQLGetTypeInfo** für eine Datenquelle, die SQL_CHAR, SQL_LONGVARCHAR SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR und SQL_INTERVAL_DAY_TO_SECOND unterstützt.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"Char"|SQL_CHAR|255|"'"|"'"|"Length"|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<NULL >|SQL_TRUE|  
|"decimal"|SQL_DECIMAL|28|\<NULL >|\<NULL >|"Precision,<br />Skala"|SQL_TRUE|  
|"real"|SQL_REAL|7|\<NULL >|\<NULL >|\<NULL >|SQL_TRUE|  
|"Datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<NULL >|SQL_TRUE|  
|"ZEITINTERVALL YEAR() JAHR"|SQL_INTERVAL_YEAR|9|"'"|"'"|"Precision"|SQL_TRUE|  
|"ZEITINTERVALL DAY() ZU FRACTION(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"Precision"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"Char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<NULL >|SQL_FALSE|\<NULL >|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"decimal"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"real"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"Datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"ZEITINTERVALL YEAR() JAHR"|  
TERVAL_DAY_TO_SECOND **|SQL_FALSE|SQL_PRED_BASIC|\<NULL >|SQL_FALSE|\<NULL >|"ZEITINTERVALL DAY() ZU FRACTION(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<NULL >|\<NULL >|SQL_CHAR|\<NULL >|\<NULL >|\<NULL >|  
|**SQL_LONGVARCHAR**|\<NULL >|\<NULL >|SQL_LONGVARCHAR|\<NULL >|\<NULL >|\<NULL >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<NULL >|10|\<NULL >|  
|**SQL_REAL**|\<NULL >|\<NULL >|SQL_REAL|\<NULL >|10|\<NULL >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<NULL >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<NULL >|9|  
ERVAL_DAY_TO_SECOND **|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<NULL >|9|
