---
title: ODBC-API-Funktionen unterstützt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC, API functions
- ODBC SQL grammar, API functions mapped to driver (table) [ODBC]
ms.assetid: b28a8ed6-09b1-4acf-bf3e-f90bb32422de
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5d7044cb0a4e963fdea39852593112c33fa8908
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="supported-odbc-api-functions"></a>Unterstützte ODBC-API-Funktionen
Der Zweck der Abgleich ist auf die Anwendung darüber zu informieren, welche Funktionen, aus dem Treiber verfügbar sind. Microsoft ODBC-Desktop-Datenbanktreiber unterstützen alle Core und Level 1-Funktionen.  
  
 Weitere Informationen zu Übereinstimmungsebenen für Funktionen und -Grammatik, finden Sie unter [Übereinstimmungsebenen](../../odbc/reference/develop-app/conformance-levels.md) in der *ODBC Programmer's Reference*.  
  
 Unterstützung des ODBC-API-Funktionen kann abhängig von der Treiber verwendet werden. In der folgenden Tabelle werden die Unterstützung für Funktionen zusammengefasst. Die äußerste linke Spalte enthält einen Link auf der Seite "Allgemeine Referenz" für jede Funktion. Diese Referenzseiten zu den aufgelisteten in alphabetischer Reihenfolge in der [ODBC-API-Referenz](../../odbc/reference/syntax/odbc-api-reference.md) -Abschnitt unter [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md). Die Spalten in den rechten geben Links treiberspezifische Notizen über die einzelnen unterstützten Funktionen. Diese treiberspezifische Themen sind im Abschnitt "Weitere Details Programmieren" für jeden Treiber aufgeführt. Wenn die gleiche "Hinweise" zu einer Funktion auf alle ODBC-Desktop-Datenbanktreiber anwenden, stellt die äußersten rechten Spalte alternativ einen Link zu einem Thema, das die Desktop-Datenbanktreiber-Unterstützung für diese Funktion zusammengefasst. Diese Themen sind am Ende des aktuellen Bereichs ("unterstützt ODBC-API-Funktionen") aufgeführt.  
  
|ODBC-Funktion|Access-Treiber-spezifische Hinweise|dBASE-Treiber-spezifischen Anmerkungen zu dieser|Paradox treiberspezifische Hinweise|Treiber-spezifischen Anmerkungen|Excel-Treiber-spezifische Hinweise|Hinweise, die relevant für alle Treiber|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Zugriff](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[DBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[Zugriff](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[DBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[Zugriff](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[DBASE](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[Zugriff](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[DBASE](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[Zugriff](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[DBASE](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)||  
GetStmtOption] (.. / Topic/SQLGetStmtOption%20Function.md)|[Alle Treiber](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)||||||  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[Zugriff](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[DBASE](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)||||||[Zugriff](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)|  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[Zugriff](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[DBASE](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursorName](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[Alle Treiber](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[Zugriff](../../odbc/microsoft/sqlstatistics-access-driver.md)|[DBASE](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[Zugriff](../../odbc/microsoft/sqltables-access-driver.md)|[DBASE](../../odbc/microsoft/sqltables-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltables-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)||  
Transact] (.. / Topic/SQLTransact%20Function.md)|[Zugriff](../../odbc/microsoft/sqltransact-access-driver.md)|[DBASE](../../odbc/microsoft/sqltransact-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltransact-paradox-driver.md)|[Textdatei](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 Die folgenden Themen enthalten Hinweise zum ODBC-Funktionen. Diese Hinweise gelten für alle ODBC-Datenbanktreiber Desktop.  
  
-   [SQLGetData (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (Desktop-Datenbanktreiber)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
