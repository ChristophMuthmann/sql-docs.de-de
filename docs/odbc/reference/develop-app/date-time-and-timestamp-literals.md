---
title: Date, Time und Timestamp-Literale | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 132377c8578ae4a403753d71dc82cd12b8be3c80
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="date-time-and-timestamp-literals"></a>Date, Time und Timestamp-Literale
Die Escapesequenz für Datum, Uhrzeit und timestampliterale lautet  
  
 **{***-Typ* **"** *Wert* **'}**   
  
 wobei *Literal vom Typ* ist einer der Werte in der folgenden Tabelle aufgeführt.  
  
|*Literal-Typ*|Bedeutung|Formatieren von *Wert*|  
|---------------------|-------------|-----------------------|  
|**d**|date|*JJJJ*-*mm*-*TT*|  
|**t**|Zeit *|*"hh"*:*mm*:*ss*[1]|  
|**TS**|Timestamp|*JJJJ*-*mm*-*Dd* *"hh"*:*mm*:*ss* [. *f...* ] [1]|  
  
 [1] die Anzahl der Ziffern rechts vom Dezimaltrennzeichen in einem Zeichenfolgenliteral, eine Komponente für Sekunden enthält, Uhrzeit oder Zeitstempel Zeitraum ist abhängig von der Genauigkeit Sekunden, wie in der SQL_DESC_PRECISION Deskriptorfeld enthalten. (Weitere Informationen finden Sie unter [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Weitere Informationen zu Datum, Uhrzeit und Timestamp-Escapesequenzen finden Sie unter [Date, Time und Timestamp-Escapesequenzen](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) in Anhang C: SQL-Grammatik.  
  
 Aktualisieren Sie sowohl die folgenden SQL-Anweisungen z. B. das öffnende Datum Auftrags 1023 in der Orders-Tabelle. Die erste Anweisung verwendet der Escape-Sequence-Syntax. Die zweite Anweisung verwendet die systemeigene Oracle Rdb-Syntax für die Datumsspalte und ist nicht interoperabel.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 Die Escapesequenz für Datum, Uhrzeit oder Zeitstempel Zeichenfolgenliteral kann auch in eine Zeichenvariable auf ein Datum, Uhrzeit oder Zeitstempel-Parameter gebunden eingefügt werden. Der folgende Code verwendet beispielsweise einen Date-Parameter gebunden werden, um eine Zeichenvariable offene Datum Auftrags 1023 in der Orders-Tabelle zu aktualisieren:  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Allerdings ist es i. d. r. effizienter, den Parameter direkt auf eine Datumsstruktur binden:  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Um zu bestimmen, ob ein Treiber die ODBC-Escapesequenzen für Datum, Uhrzeit oder Zeitstempel Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle einen Datentyp Datum, Uhrzeit oder Zeitstempel unterstützt, muss es auch die entsprechende Escapesequenz unterstützen.  
  
 Datenquellen können auch die Datetime-Literale in der ANSI SQL-92-Spezifikation definiert unterstützen, die sich von der ODBC-Escapesequenzen für Datum, Uhrzeit oder Zeitstempel-Literale sind. Um zu bestimmen, ob eine Datenquelle die ANSI-Literale unterstützt, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Um zu bestimmen, ob ein Treiber die ODBC-Escapesequenzen für Intervall Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle einen Datetime-Intervall-Datentyp unterstützt, muss es auch die entsprechende Escapesequenz unterstützen.  
  
 Datenquellen unterstützen auch die Datetime-Literale in der ANSI SQL-92-Spezifikation definiert die unterscheiden sich von den ODBC-Escapesequenzen für Datetime-Intervall-Literale. Um zu bestimmen, ob eine Datenquelle die ANSI-Literale unterstützt, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_ANSI_SQL_DATETIME_LITERALS.
