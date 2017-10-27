---
title: SQLSetConnectInfo Funktion | Microsoft Docs
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
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e4c974a8cf4bb46f955ec8f2bae0a766f58f692
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo-Funktion
**Konformität**  
 Version eingeführt: ODBC 3,81 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLSetConnectInfo** wird verwendet, um die Datenquelle, Benutzer-ID und Kennwort in das Verbindungstoken für die Informationen für einer Anwendungsverzeichnis festgelegt [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) aufrufen.  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>Argumente  
 *TokenHandle*  
 [Eingabe] Tokenhandle.  
  
 *ServerName*  
 [Eingabe] Datenquellenname. Daten können sich auf demselben Computer wie das Programm oder auf einem anderen Computer an einer beliebigen Stelle in einem Netzwerk sein. Weitere Informationen dazu, wie eine Anwendung eine Datenquelle auswählt, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Eingabe] Länge des **ServerName* in Zeichen.  
  
 *UserName*  
 [Eingabe] Benutzer-ID.  
  
 *NameLength2*  
 [Eingabe] Länge des **Benutzername* in Zeichen.  
  
 *Authentifizierung*  
 [Eingabe] Authentifizierungszeichenfolge (in der Regel das Kennwort).  
  
 *NameLength3*  
 [Eingabe] Länge des **Authentifizierung* in Zeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Identisch mit [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) für Eingabe von Validierungsfehlern, mit dem Unterschied, dass der Treiber-Manager verwendet eine **HandleType** von SQL_HANDLE_DBC_INFO_TOKEN und ein **behandeln** von *hDbcInfoToken*.  
  
## <a name="remarks"></a>Hinweise  
 Immer ein Treiber SQL_ERROR oder SQL_INVALID_HANDLE zurückgibt, gibt der Treiber-Manager den Fehler an die Anwendung (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oder [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Immer ein Treiber SQL_SUCCESS_WITH_INFO zurückgegeben wird, erhält der Treiber-Manager die Diagnoseinformationen aus *hDbcInfoToken*, und geben Sie an die Anwendung in SQL_SUCCESS_WITH_INFO zurück [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)und [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Entwickeln von Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

