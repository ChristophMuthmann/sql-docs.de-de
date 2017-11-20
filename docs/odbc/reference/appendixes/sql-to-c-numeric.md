---
title: SQL in "c:" numerischen | Microsoft Docs
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
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5513983bcd8d7858629bb1a9f45ff5489ad46246
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-numeric"></a>SQL in numerischen Wert "c:"
Der Bezeichner für die numerische ODBC SQL-Datentypen sind:  
  
 SQL_DECIMAL  
  
 SQL_BIGINT  
  
 SQL_NUMERIC  
  
 SQL_REAL  
  
 SQL_TINYINT  
  
 SQL_FLOAT  
  
 SQL_SMALLINT  
  
 SQL_INTEGER SQL_DOUBLE  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in die numerische SQL-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Zeichenlänge des Byte < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Zeichenlänge des < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|Daten konvertiert werden, ohne Abschneiden [a]<br /><br /> Daten konvertiert, wobei das Abschneiden von Dezimalstellen [a]<br /><br /> Konvertierung von Daten führt zu einem Verlust von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern [a]|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22003|  
_C_FLOAT<br /><br /> SQL_C_DOUBLE|Daten sind innerhalb des Bereichs des Datentyps in den die Anzahl konvertiert [a]<br /><br /> Daten sind außerhalb des Bereichs des Datentyps in den die Anzahl konvertiert [a]|data<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_BIT|Daten sind 0 oder 1 [a]<br /><br /> Daten sind größer als 0 (null) kleiner als 2, und nicht gleich 1 [a]<br /><br /> Daten ist kleiner als 0 oder größer als oder gleich 2 [a]|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|1 [b]<br /><br /> 1 [b]<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|Daten wurden nicht abgeschnitten.<br /><br /> Die Sekundenbruchteile abgeschnitten<br /><br /> Ganze Zahl gekürzt-Teil|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22015|  
_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|Ganze Zahl gekürzt-Teil|Nicht definiert|Nicht definiert|22015|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 [c] diese Konvertierung wird nur für die genaue numerische Datentypen (SQL_DECIMAL, SQL_NUMERIC SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER und SQL_BIGINT) unterstützt. Es ist nicht für die ungefähre numerische Datentypen (SQL_REAL, SQL_FLOAT oder SQL_DOUBLE) unterstützt.  
  
## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC und SQLSetDescField  
 Die [SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ist erforderlich, um manuelle Bindung mit SQL_C_NUMERIC Werten ausführen. (Beachten Sie, dass SQLSetDescField in ODBC 3.0 hinzugefügt wurde.) Zum manuellen Bindung durchführen zu können, müssen Sie zuerst die Deskriptorhandles abrufen.  
  
```  
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```

