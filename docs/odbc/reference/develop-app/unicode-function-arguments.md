---
title: Unicode-Funktionsargumente | Microsoft Docs
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
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab660a9af95d6232f22c98a868da8fed9ebb0cae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-function-arguments"></a>Unicode-Funktionsargumente
Der ODBC 3.5 (oder höher)-Treiber-Manager unterstützt ANSI- und Unicode-Versionen aller Funktionen, die Zeiger auf Zeichenfolgen oder SQLPOINTER in ihrer Argumente akzeptieren. Die Unicode-Funktionen werden als Funktionen implementiert (mit dem Suffix *W*) und nicht als Makros. Die ANSI-Funktionen (aufgerufen werden können, mit oder ohne dem Suffix *ein*) sind identisch mit der aktuellen ODBC API-Funktionen.  
  
## <a name="remarks"></a>Hinweise  
 Unicode-Funktionen, die immer zurückgeben oder Zeichenfolgen oder Länge Argumente übernehmen, werden als Anzahl von Zeichen übergeben. Für Funktionen, die von Längeninformationen für Server-Daten zurückgeben, werden die Anzeigegröße und Genauigkeit in Anzahl von Zeichen beschrieben. Wenn eine Länge (Übertragungsgröße der Daten) auf Zeichenfolgen- oder Objektressourcen Daten verweisen kann, wird die Länge in Oktett Längen beschrieben. Beispielsweise **SQLGetInfoW** dauert noch die Länge als Anzahl von Bytes, aber **SQLExecDirectW** wird die Anzahl von Zeichen verwenden.  
  
 Anzahl von Zeichen bezieht sich auf die Anzahl der Bytes (Oktette) für ANSI-Funktionen und die Anzahl der WCHAR (16-Bit-Wörter) für Unicode-Funktionen. Insbesondere kann eine Sequenz Doppelbyte-Zeichensatz (DBCS) oder eine Sequenz Mehrbyte-Zeichensätzen (MBCS) aus mehreren Bytes bestehen. Eine Folge von UTF-16-Unicode-Zeichen kann aus mehreren WCHARs so lang wie bestehen.  
  
 Im folgenden finden eine Liste der ODBC-API-Funktionen, die Unicode (W) und ANSI (A) Versionen unterstützen:  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
  
 Im folgenden finden eine Liste der ODBC-Installer und ODBC-Konvertierungsprogramm Funktionen, die Unicode (W) und ANSI (A) Versionen unterstützen:  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]  
>  Als veraltet markierte Funktionen haben Unterstützung für Unicode in ANSI-Zuordnung aus, da die ODBC 3.*.x* -Treiber-Manager unterstützt ODBC 2. Neukompilierung. *X* Anwendungen mit dem Unicode- **#define**.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Unicode-Anwendungen](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode-Treiber](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Funktionszuordnung im Treiber-Manager](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
