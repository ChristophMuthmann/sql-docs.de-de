---
title: Festlegen von Cursoroptionen (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 357678adf4c5cba588c5d76dc9ca880e7f6d8cb5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-cursor-options-odbc"></a>Festlegen von Cursoroptionen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Zum Festlegen von Cursoroptionen rufen [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) festlegen oder [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) um die Anweisungsoptionen abzurufen, das Cursorverhalten gesteuert.  
  
|*Attribut*|Gibt an|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|Cursortyp, der einen Vorwärtscursor, einen statischen, dynamischen oder keyset-gesteuerten Cursor bezeichnen kann|  
|SQL_ATTR_CONCURRENCY|Option zur Steuerung der gleichzeitigen Ausführung, die Schreibschutz, Sperren, vollständige Parallelität mit Timestamps oder vollständige Parallelität mit Werten angeben kann|  
|SQL_ATTR_ROW_ARRAY_SIZE|Anzahl der Zeilen, die mit jedem Abrufvorgang abgerufen werden|  
|SQL_ATTR_CURSOR_SENSITIVITY|Cursor, der Cursorupdates, die von anderen Verbindungen an Cursorzeilen vorgenommen wurden, anzeigt oder nicht anzeigt|  
|SQL_ATTR_CURSOR_SCROLLABLE|Cursor, mit denen sowohl ein Vorwärts- als auch ein Rückwärtsbildlauf ausgeführt werden kann|  
  
 Bei Verwendung der Standardwerte dieser Attribute (forward-only, read-only, Rowsetgröße von 1) werden keine Servercursor verwendet. Die Verwendung von Servercursorn setzt voraus, dass mindestens eines dieser Attribute auf einen anderen Wert als den Standardwert festgelegt wird und dass es sich bei der auszuführenden Anweisungen um eine einzelne SELECT-Anweisung oder eine gespeicherte Prozedur handelt, die eine einzelne SELECT-Anweisung enthält. Beim Einsatz von Servercursorn können in SELECT-Anweisungen keine Klauseln angegeben werden, die von den Servercursorn nicht unterstützt werden: COMPUTE, COMPUTE BY, FOR BROWSE und INTO.  
  
 Sie können den Typ des Cursors entweder von SQL_ATTR_CURSOR_TYPE und SQL_ATTR_CONCURRENCY oder SQL_ATTR_CURSOR_SENSITIVITY und SQL_ATTR_CURSOR_SCROLLABLE steuern. Sie sollten die zwei Methoden zur Angabe des Cursorverhaltens nicht kombinieren.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden ein Anweisungshandle zugeordnet, ein dynamischer Cursortyp mit vollständiger Parallelität mit Zeilenversionsverwaltung festgelegt und anschließend eine SELECT-Anweisung ausgeführt.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden ein Anweisungshandle zugeordnet, ein bildlauffähiger Sensitivcursor festgelegt und anschließend eine SELECT-Anweisung ausgeführt.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Abfragen Gewusst-wie-Themen zur Vorgehensweise & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
