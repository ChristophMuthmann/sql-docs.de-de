---
title: Verbindungsresilienz im Windows ODBC-Treiber | Microsoft Docs
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
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dda329540bd228920e88a12c69a4a6f2b8a8327
ms.sourcegitcommit: e904c2a85347a93dcb15bb6b801afd39613d3ae7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/16/2017
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Verbindungsresilienz im Windows ODBC-Treiber
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Um sicherzustellen, dass Anwendungen mit verbunden bleiben ein [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], die ODBC-Treiber unter Windows Verbindungen im Leerlauf wiederherstellen kann.  
  
> [!IMPORTANT]  
>  Das Verbindungsstabilitätsfeature wird von Microsoft Azure SQL-Datenbanken und den Server-Versionen SQL Server 2014 (und neuer) unterstützt.  
  
 Weitere Informationen zu verbindungsstabilität im Leerlauf finden Sie unter [technischer Artikel – Verbindungsstabilität im Leerlauf](http://go.microsoft.com/fwlink/?LinkId=393996).  
  
 Um das Verhalten bei der Verbindungswiederherstellung zu steuern, bietet der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows zwei Optionen:  
  
-   Anzahl Verbindungsversuche.  
  
     Die Anzahl der Verbindungsversuche steuert die Anzahl der erneuten Versuche zur Verbindungsherstellung, wenn ein Verbindungsfehler vorhanden ist. Gültige Werte reichen von 0 bis 255. Null (0) bedeutet, keinen Versuch zu unternehmen, um die Verbindung wiederherzustellen. Der Standardwert ist ein (1) Verbindungsversuch.  
  
     Sie können die Anzahl der Verbindungsversuche ändern, wenn Sie:  
  
    -   Eine Datenquelle definieren oder ändern, die den ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit **ConnectionRetryCount** -Kontrolle verwendet.  
  
    -   Verwenden Sie das Schlüsselwort für Verbindungszeichenfolgen **ConnectionRetryCount** .  
  
     Verwenden Sie zum Abrufen der Anzahl der Verbindungsherstellungsversuche der **SQL_COPT_SS_CONNECT_RETRY_COUNT** (schreibgeschützt) Verbindungsattribut. Wenn eine Anwendung mit einem Server verbunden ist, der keine verbindungsresilienz unterstützt **SQL_COPT_SS_CONNECT_RETRY_COUNT** gibt 0 zurück.  
  
-   Intervall für Wiederholungen der Verbindungen  
  
     Das Intervall der Verbindungsversuche gibt die Anzahl der Sekunden zwischen jedem Verbindungsversuch an. Gültige Werte sind 1-60. Die Gesamtzeit für die Verbindung darf das Verbindungstimeout (in SQLSetStmtAttr SQL_ATTR_QUERY_TIMEOUT) nicht überschreiten. Der Standardwert beträgt 10 Sekunden.  
  
     Sie können das Intervall für Verbindungsversuche ändern, wenn Sie:  
  
    -   Definieren oder ändern Sie eine Datenquelle die den ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit dem Steuerelement **ConnectionRetryCount** verwendet.  
  
    -   Verwenden Sie das Schlüsselwort **ConnectionRetryInterval** für Verbindungszeichenfolgen.  
  
     Verwenden Sie zum Abrufen der Länge der das Intervall für Verbindungsversuche das **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (schreibgeschützt) Verbindungsattribut.  
  
 Wenn eine Anwendung eine Verbindung mit SQL_DRIVER_COMPLETE_REQUIRED herstellt und dann versucht, eine Anweisung über eine unterbrochene Verbindung ausführen, zeigt der ODBC-Treiber das Dialogfeld nicht erneut an. Darüber hinaus während der Wiederherstellung,  
  
-   Während der Wiederherstellung muss jeder Aufruf von **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)**, zurückgeben **SQL_CD_FALSE**.  
  
-   Bei Wiederherstellungsfehlern jeder Aufruf von **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)**, zurückgeben **SQL_CD_TRUE**.  
  
 Die folgenden Statuscodes werden von jeder Funktion zurückgegeben, die auf dem Server einen Befehl ausführt:  
  
|Status|MessageBox|  
|-----------|-------------|  
|IMC01|Die Verbindung ist unterbrochen und kann nicht wiederhergestellt werden. Der Client-Treiber hat versucht, die Verbindung ein oder mehrere Male wiederherzustellen und alle Versuche sind fehlgeschlagen. Erhöhen Sie den Wert der Verbindungszeichenfolgen von ConnectRetryCount, um die Anzahl der Wiederherstellungsversuche zu erhöhen.|  
|IMC02|Der Server hat einen Wiederherstellungsversuch nicht bestätigt. Die Wiederherstellung der Verbindung ist nicht möglich.|  
|IMC03|Der Server hat nicht die genaue Client TDS-Version beibehalten, die bei einem Wiederherstellungsversuch gefordert war. Die Wiederherstellung der Verbindung ist nicht möglich.|  
|IMC04|Der Server hat nicht die genaue Serverhauptversion beibehalten, die bei einem Wiederherstellungsversuch gefordert war. Die Wiederherstellung ist nicht möglich.|  
|IMC05|Die Verbindung ist unterbrochen und kann nicht wiederhergestellt werden. Die Verbindung wird vom Server als nicht behebbar markiert. Es wurde nicht versucht, die Verbindung wiederherzustellen.|  
|IMC06|Die Verbindung ist unterbrochen und kann nicht wiederhergestellt werden. Die Verbindung wird vom Clienttreiber als nicht behebbar markiert. Es wurde nicht versucht, die Verbindung wiederherzustellen.|  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel enthält zwei Funktionen. **func1** wird gezeigt, wie Sie mit einem Datenquellennamen (DSN) eine Verbindung herstellen können, die für die ODBC-Treiber verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows. Der DSN verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Authentifizierung und gibt die Benutzer-ID an. **func1** ruft anschließend die Anzahl der Verbindungsversuche mit **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
 **func2** verwendet **SQLDriverConnect**, **ConnectRetryCount** -Schlüsselwort der Verbindungszeichenfolge sowie die Verbindungsattribute, um die Einstellung für Verbindungsversuche und das Wiederholungsintervall aufzurufen.  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
