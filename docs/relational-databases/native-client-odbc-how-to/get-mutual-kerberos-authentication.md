---
title: Einrichten der gegenseitigen Kerberos-Authentifizierung | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 64149fd4-239b-40e4-91e2-f9011f7d9f66
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 775d451ed687ceae2a3e78f2bb8ddd3f6b76216e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="get-mutual-kerberos-authentication"></a>Einrichten der gegenseitigen Kerberos-Authentifizierung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dieses Beispiel zeigt, wie gegenseitige Kerberos-Authentifizierung mithilfe von ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client eingerichtet wird.  
  
 In einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]kann das Beispiel nicht ausgeführt werden.  
  
 Weitere Informationen finden Sie unter [Service Principal Name & #40; Dienstprinzipalnamen & #41; Unterstützung in Clientverbindungen](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md).  
  
## <a name="example"></a>Beispiel  
 Wenn Sie dieses Beispiel als 32-Bit-Anwendung entwickeln und unter einem 64-Bit-Betriebssystem ausführen, müssen Sie die ODBC-Datenquelle mit dem ODBC-Administrator in %windir%\SysWOW64\odbcad32.exe erstellen.  
  
 In diesem Beispiel wird eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standardinstanz des Computers hergestellt. Ändern Sie zum Herstellen einer Verbindung mit einer benannten Instanz die Definition der ODBC-Datenquelle, um die Instanz im folgenden Format anzugeben: Server\benannteInstanz. Standardmäßig wird [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in einer benannten Instanz installiert.  
  
 Ändern Sie "MyServer" in den Namen eines Computers, auf dem sich eine Instanz von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher) befindet.  
  
 Sie müssen auch einen vom Kunden bereitgestellten SPN angeben. Ändern Sie " CP_SPN " in einen vom Kunden bereitgestellten SPN.  
  
 Kompilieren Sie mit /EHsc, /D "_UNICODE", /D "UNICODE" und odbc32.lib. Stellen Sie sicher, dass die INCLUDE-Umgebungsvariable das Verzeichnis einschließt, das sqlncli.h enthält.  
  
```  
// compile with: /EHsc /D "_UNICODE" /D "UNICODE" odbc32.lib  
#define WIN32_LEAN_AND_MEAN  
#include <tchar.h>  
#include <windows.h>  
#include <stdio.h>  
#include <sql.h>  
#include <sqlext.h>  
  
#define _SQLNCLI_ODBC_  
#include <sqlncli.h>  
  
#define SUCCESS(x) (!((x) & 0xFFFE))  
  
#define CHKRC(stmt) do \  
                    { \  
                    rc = (stmt); \  
                    if (!SUCCESS(rc)) \  
                    throw (RETCODE) rc; \  
                    } while(0);  
  
void PrintError(SQLSMALLINT HandleType, SQLHANDLE Handle) {  
   RETCODE rc = SQL_SUCCESS;  
   SQLTCHAR szSqlState[6], szMessage[1024];  
   SQLSMALLINT i = 1, msgLen = 0;  
   SQLINTEGER NativeError;  
  
   do {  
      i = 1;  
      while (SQL_NO_DATA != (rc = SQLGetDiagRec(HandleType, Handle, i, szSqlState, &NativeError,   
         szMessage, sizeof(szMessage)/sizeof(SQLTCHAR), &msgLen)) && SUCCESS(rc)) {  
            _tprintf(_T("SQLState=%s, NativeError=%ld, Message=%s\r\n"), szSqlState, NativeError, szMessage);  
            i++;  
      }  
   }   
   while (SQL_NO_DATA != (rc = SQLMoreResults(Handle)) && SUCCESS(rc));  
}  
  
int _tmain(int argc, _TCHAR* argv[]) {  
   RETCODE rc = SQL_SUCCESS;  
   HENV henv = SQL_NULL_HENV;  
   HDBC hdbc = SQL_NULL_HDBC;  
   SQLHSTMT hstmt = SQL_NULL_HSTMT;  
   SQLTCHAR * pszConnection = _T("DRIVER={SQL Server Native Client 10.0};")  
      _T("Server=MyServer;")          // server with SQL Server 2008 (or later)  
      _T("Trusted_Connection=Yes;")  
      _T("ServerSPN=CP_SPN");    // customer-provided SPN  
  
   TCHAR szIntgAuthMethod[64];  
   SQLSMALLINT fMutuallyAuth = 0;  
  
   try {  
      CHKRC(SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HENV, &henv));  
      CHKRC(SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0));  
      CHKRC(SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc));  
      CHKRC(SQLDriverConnect( hdbc, NULL, pszConnection, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT));  
      CHKRC(SQLGetConnectAttr(hdbc, SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD, szIntgAuthMethod, sizeof(szIntgAuthMethod)/sizeof(szIntgAuthMethod[0]), NULL));  
      CHKRC(::SQLGetConnectAttrW(hdbc, SQL_COPT_SS_MUTUALLY_AUTHENTICATED, &fMutuallyAuth, SQL_IS_SMALLINT, NULL));  
  
      _tprintf(_T("Authentication method: %s\r\n"), szIntgAuthMethod);  
      _tprintf(_T("Mutually authenticated: %s\r\n"), fMutuallyAuth?_T("yes"):_T("no"));  
   }  
   catch (RETCODE retcode) {  
      rc = retcode;  
   }  
  
   if (!SUCCESS(rc)) {  
      if (hstmt)  
         PrintError(SQL_HANDLE_STMT, hstmt);  
      else if (hdbc)  
         PrintError(SQL_HANDLE_DBC, hdbc);  
      else if(henv)  
         PrintError(SQL_HANDLE_ENV, henv);  
   }  
  
   if (hstmt)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
   if (hdbc) {  
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
   }  
   if (henv)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
  
