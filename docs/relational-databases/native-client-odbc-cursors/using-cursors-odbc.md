---
title: Verwenden von Cursorn (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f4fd700f6642f2cbb6fae33115229a323689686e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-cursors-odbc"></a>Verwenden von Cursorn (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC unterstützt ein Cursormodell, das Folgendes zulässt:  
  
-   Mehrere Typen von Cursorn  
  
-   Das Durchführen eines Bildlaufs und Positionieren innerhalb eines Cursors  
  
-   Mehrere Parallelitätsoptionen  
  
-   Positionierte Updates.  
  
 ODBC-Anwendungen deklarieren und öffnen Cursor oder verwenden cursorspezifische [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nur selten. ODBC öffnet automatisch einen Cursor für jedes Resultset, das von einer SQL-Anweisung zurückgegeben wird. Die Charakteristika der Cursor werden von Anweisungsattribute festlegen mit gesteuert [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) vor der SQL-Anweisung ausgeführt wird. Die ODBC-API-Funktionen zum Verarbeiten der Resultsets unterstützen sämtliche Cursorfunktionalitäten einschließlich Abrufen, Durchführen eines Bildlaufs und positionierte Updates.  
  
 Dies ist ein Vergleich der Funktionsweise von Cursorn in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skripts und ODBC-Anwendungen.  
  
|Aktion|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definieren des Cursorverhaltens|Angeben durch DECLARE CURSOR-Parameter|Festlegen der Cursorattribute mithilfe [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|Öffnen eines Cursors|DECLARE CURSOR OPEN *Cursorname*|**SQLExecDirect** oder **SQLExecute**|  
|Abrufen von Zeilen|FETCH|**SQLFetch** oder [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|Positioniertes Update|WHERE CURRENT OF-Klausel mit UPDATE oder DELETE|**SQLSetPos**|  
|Schließen eines Cursors|Schließen *Cursor_name* DEALLOCATE|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 Die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementierten Servercursor unterstützen die Funktionalität des ODBC-Cursormodells. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Treiber verwendet Servercursor, um die Cursorfunktionalität der ODBC-API zu unterstützen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Implementieren von Cursorn](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [Cursortypen](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [Verhalten von Cursorn](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [Cursoreigenschaften](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [Details zum Programmieren von Cursorn &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [Scrollen und Fetchen von Zeilen](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [Positionierte Updates &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursor](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
