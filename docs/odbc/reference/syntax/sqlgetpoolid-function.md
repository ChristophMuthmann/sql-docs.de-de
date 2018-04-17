---
title: SQLGetPoolID Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e665ceedb5faec816a6e17a763dad0b3d1ba360
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID-Funktion
**Konformität**  
 Version eingeführt: ODBC 3,81 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLGetPoolID** Ruft die Pool-ID ab  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Argumente  
 *hDbcInfoToken*  
 [Eingabe] Token-Handle, das alle Verbindungsinformationen enthält.  
  
 *pPoolID*  
 [Ausgabe] Die Anwendungspool-ID, die verwendet wird, um einen Satz von Verbindungen zu identifizieren, das Synonym verwendet werden kann (möglicherweise muss eine zusätzliche zurückgesetzt).  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetPoolID** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO der Treiber-Manager verwendet eine **HandleType** von SQL_HANDLE_DBC_INFO_TOKEN und ein **behandeln** von *hDbcInfoToken*.  
  
## <a name="remarks"></a>Hinweise  
 **SQLGetPoolID** verwendet, um die Pool-ID, die anhand eines Satzes von Verbindungsinformationen abzurufen (aus **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, und  **SQLSetConnectInfo**). Dieser Pool-ID wird verwendet, um einen Satz von Verbindungen zu identifizieren, das Synonym verwendet werden kann (möglicherweise muss eine zusätzliche zurückgesetzt). Die Anwendungspool-ID wird verwendet werden, um den Verbindungspool für diese Gruppe von Verbindungen zu identifizieren.  
  
 Immer ein Treiber SQL_ERROR oder SQL_INVALID_HANDLE zurückgibt, gibt der Treiber-Manager den Fehler an die Anwendung (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oder [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Immer ein Treiber SQL_SUCCESS_WITH_INFO zurückgegeben wird, erhält der Treiber-Manager die Diagnoseinformationen aus *hDbcInfoToken*, und geben Sie an die Anwendung in SQL_SUCCESS_WITH_INFO zurück [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)und [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Developing Connection-Pool Awareness in an ODBC Driver (Entwickeln von Verbindungspool-Unterstützung in einem ODBC-Treiber)](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
