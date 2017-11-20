---
title: "DateTime-Datentyp ändert | Microsoft Docs"
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
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b09a6daa19b7a8b22ac5f4b3147e6cefde6ffc60
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="datetime-data-type-changes"></a>Änderungen des Datentyps "DateTime"
In ODBC 3. *x*, die Bezeichner für das Datum, Zeit und Zeitstempel SQL-Datentypen von SQL_DATE, SQL_TIME und SQL_TIMESTAMP geändert haben (mit Instanzen von **#define** in der Headerdatei 9, 10 und 11) zu SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP (mit Instanzen von **#define** in der Headerdatei von 91, 92 und 93) zugeordnet. Die entsprechenden C-Typ-IDs haben bzw. von SQL_C_DATE SQL_C_TIME und SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME und SQL_C_TYPE_TIMESTAMP geändert.  
  
 Die Spaltengröße und die Dezimalstellen für die SQL-Datetime-Datentypen in ODBC 3. zurückgegeben. *x* sind identisch mit der Genauigkeit und Dezimalstellenanzahl dafür in ODBC 2. zurückgegeben.* X*. Diese Werte unterscheiden sich die Werte in die deskriptorfelder SQL_DESC_PRECISION und SQL_DESC_SCALE zur Verfügung. (Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Diese Änderungen wirken sich auf **SQLDescribeCol**, **SQLDescribeParam**, und **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, und **SQLGetData**; und **SQLColumns**, **SQLGetTypeInfo **, **SQLProcedureColumns**, **SQLStatistics**, und **SQLSpecialColumns**.  
  
 Die folgende Tabelle zeigt, wie die ODBC 3.*.x* -Treiber-Manager führt die Zuordnung von der Date, Time und Timestamp C-Datentypen in eingegeben der *TargetType* Argumente **SQLBindCol**und **SQLGetData** oder in der *ValueType* Argument **SQLBindParameter**.  
  
|Datentyp<br /><br /> Code eingegeben|2.*x* -app<br /><br /> 2.*x* Treiber|2.*x* -app<br /><br /> 3.*x* Treiber|3.*x* -app<br /><br /> 2.*x* Treiber|3.*x* -app<br /><br /> 3.*x* Treiber|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Keine Zuordnung|SQL_C_TYPE_DATE (91)|Keine Zuordnung [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Fehler (DM)|Fehler (DM)|SQL_C_DATE (9)|Keine Zuordnung [2]|  
|SQL_C_TIME (10)|Keine Zuordnung|SQL_C_TYPE_TIME (92)|Keine Zuordnung [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Fehler (DM)|Fehler (DM)|SQL_C_TIME (10)|Keine Zuordnung [2]|  
|SQL_C_TIMESTAMP (11)|Keine Zuordnung|SQL_C_TYPE_TIMESTAMP (93)|Keine Zuordnung [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Fehler (DM)|Fehler (DM)|SQL_C_TIMESTAMP (11)|Keine Zuordnung [2]|  
  
 [1] als Ergebnis des hierzu ein ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2..* X* Treiber können auf das Datum, Uhrzeit oder Zeitstempel zurückgegebenem in den Resultsets, die durch die Katalogfunktionen zurückgegeben werden.  
  
 [2] von Ereignishandleraufrufen dieser, eine ODBC-3. *x* Anwendung arbeiten mit einem ODBC 3..* X* Treiber können auf das Datum, Uhrzeit oder Zeitstempel zurückgegebenem in den Resultsets, die durch die Katalogfunktionen zurückgegeben werden.  
  
 Die folgende Tabelle zeigt, wie die ODBC 3.*.x* -Treiber-Manager führt Zuordnung der eingegebene Date, Time und Timestamp SQL Datentypen der *ParameterType* Argument **SQLBindParameter ** oder in der *DataType* Argument **SQLGetTypeInfo**.  
  
|Datentyp<br /><br /> Code eingegeben|2.*x* -app<br /><br /> 2.*x* Treiber|2.*x* -app<br /><br /> 3.*x* Treiber|3.*x* -app<br /><br /> 2.*x* Treiber|3.*x* -app<br /><br /> 3.*x* Treiber|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Keine Zuordnung|SQL_TYPE_DATE (91)|Keine Zuordnung [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Fehler (DM)|Fehler (DM)|SQL_DATE (9)|Keine Zuordnung [2]|  
|SQL_TIME (10)|Keine Zuordnung|SQL_TYPE_TIME (92)|Keine Zuordnung [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Fehler (DM)|Fehler (DM)|SQL_TIME (10)|Keine Zuordnung [2]|  
|SQL_TIMESTAMP (11)|Keine Zuordnung|SQL_TYPE_TIMESTAMP (93)|Keine Zuordnung [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Fehler (DM)|Fehler (DM)|SQL_TIMESTAMP (11)|Keine Zuordnung [2]|  
  
 [1] als Ergebnis des hierzu ein ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2..* X* Treiber können auf das Datum, Uhrzeit oder Zeitstempel zurückgegebenem in den Resultsets, die durch die Katalogfunktionen zurückgegeben werden.  
  
 [2] von Ereignishandleraufrufen dieser, eine ODBC-3. *x* Anwendung arbeiten mit einem ODBC 3..* X* Treiber können auf das Datum, Uhrzeit oder Zeitstempel zurückgegebenem in den Resultsets, die durch die Katalogfunktionen zurückgegeben werden.

