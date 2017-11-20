---
title: C-Intervall-Struktur | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 146e16608f0f2f790bf49a84de2ef4610df33d0f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-interval-structure"></a>C-Intervall-Struktur
Jede C-Intervall-Datentypen aufgeführt, der [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) Abschnitt verwendet die gleiche Struktur, um die Intervalldaten enthalten. Wenn **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData** wird aufgerufen, der Treiber gibt Daten zurück, in der Struktur SQL_INTERVAL_STRUCT, verwendet den Wert, der durch angegeben wurde, die Anwendung für die C-Datentypen (im Aufruf **SQLBindCol**, **SQLGetData**, oder **SQLBindParameter**) zum Interpretieren des Inhalts der SQL_INTERVAL_STRUCT , und füllt die *Interval_type* -Feld der Struktur mit den *Enum* -Wert, des C-Typs entspricht. Beachten Sie, dass der Treiber kein Lesevorgang der *Interval_type* zum Bestimmen des Typs des Intervalls Feld; sie den Wert des Felds Deskriptor SQL_DESC_CONCISE_TYPE abrufen. Wenn die Struktur für Parameterdaten verwendet wird, der Treiber verwendet den angegebenen Wert durch die Anwendung in das Feld SQL_DESC_CONCISE_TYPE APD zum Interpretieren des Inhalts der SQL_INTERVAL_STRUCT, auch wenn die Anwendung den Wert für setzt die  *Interval_type* Feld auf einen anderen Wert.  
  
 Diese Struktur ist folgendermaßen definiert:  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 Die *Interval_type* -Feld von der SQL_INTERVAL_STRUCT gibt an, an die Anwendung in welcher Struktur in der Union aufrechterhalten wird und welche Member der Struktur sind auch relevant. Die *Interval_sign* Feld hat den Wert SQL_FALSE aus, wenn die für anführenden Intervallwert, Feld nicht signiert ist, ist dies SQL_TRUE, das führende Feld ist ein negativer Wert. Der Wert im Feld führende selbst ist immer ohne Vorzeichen, unabhängig vom Wert der *Interval_sign*. Die *Interval_sign* Feld fungiert als Vorzeichenbit.

