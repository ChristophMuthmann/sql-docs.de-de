---
title: "Vorgehensweise: Einfügen von Zeilen in eine Geografiespalte (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0b6516f7-1fc0-4b01-a2d0-add0571070d5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fa3374c0f60a43a9ddff566b11c4554c66ac7a0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="how-to-insert-rows-into-geography-column-odbc"></a>Vorgehensweise: Einfügen von Zeilen in eine Geografiespalte (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Beispiel werden unter Verwendung zweier verschiedener Bindungen (SQLCCHAR und SQLCBINARY) zwei Zeilen in eine Tabelle mit einer geography-Spalte aus einem WellKnownBinary (WKB) eingefügt. Daraufhin wird im Beispiel eine Zeile aus der Tabelle ausgewählt und mit ::STAsText() angezeigt. Das WKB ist 0x01010000000700ECFAD03A4C4001008000B5DF07C0, und die Anwendung gibt POINT(56.4595 -2.9842) auf der Konsole aus.  
  
 Dieses Beispiel erfordert keine ODBC-Datenquelle, es wird jedoch standardmäßig auf der lokalen Instanz von SQL Server ausgeführt.  
  
 In einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]kann das Beispiel nicht ausgeführt werden.  
  
 Weitere Informationen zu räumlicher Speicherung finden Sie unter [räumliche Daten &#40; SQLServer &#41; ](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
## <a name="example"></a>Beispiel  
 Das erste Codelisting ([!INCLUDE[tsql](../../includes/tsql-md.md)]) erstellt eine im Beispiel verwendete Tabelle.  
  
 Kompilieren Sie das zweite Codelisting (C++) mit odbc32.lib und user32.lib. Stellen Sie sicher, dass die INCLUDE-Umgebungsvariable das Verzeichnis einschließt, das sqlncli.h enthält.  
  
 Wenn Sie dieses Beispiel als 32-Bit-Anwendung entwickeln und unter einem 64-Bit-Betriebssystem ausführen, müssen Sie die ODBC-Datenquelle mit dem ODBC-Administrator in %windir%\SysWOW64\odbcad32.exe erstellen.  
  
 In diesem Beispiel wird eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standardinstanz des Computers hergestellt. Ändern Sie zum Herstellen einer Verbindung mit einer benannten Instanz die Definition der ODBC-Datenquelle, um die Instanz im folgenden Format anzugeben: Server\benannteInstanz. Standardmäßig wird [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in einer benannten Instanz installiert.  
  
 Mit dem dritten Codelisting ([!INCLUDE[tsql](../../includes/tsql-md.md)]) wird die im Beispiel verwendete Tabelle gelöscht.  
  
```  
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'SpatialSample')  
   DROP TABLE SpatialSample  
  
CREATE TABLE SpatialSample (Name varchar(10), Geog Geography)  
GO  
```  
  
```  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <Sqlext.h>  
#include <mbstring.h>  
#include "sqlncli.h"  
#include <string.h>  
#include <stdio.h>  
  
#define MAX_DATA 1024  
#define MYSQLSUCCESS(rc) ( (rc == SQL_SUCCESS) || (rc == SQL_SUCCESS_WITH_INFO) )  
  
SQLCHAR szDSN[] = "Driver={SQL Server Native Client 10.0};Server=.;Database=tempdb;Trusted_Connection=Yes;";  
  
class direxec {  
      RETCODE rc;   // ODBC return code  
      HENV henv;   // Environment  
      HDBC hdbc;   // Connection Handle  
      HSTMT hstmt;   // Statement Handle  
      SQLHDESC hdesc;   // Descriptor handle  
      SQLCHAR szData[MAX_DATA];   // Returned Data Storage  
      SDWORD cbData;   // Output Lenght of data   
  
      SQLCHAR szConnStrOut[MAX_DATA + 1];  
      SWORD swStrLen;  
  
public:  
      void sqlconn();   // Allocate env, stat and conn  
      void sqldisconn();   // Free pointers to env, stat, conn and disconnect  
      void error_out();   // Display errors  
      void check_rc(RETCODE rc);   // Checks for success of the return code  
      void SqlInsertFromChar();   // Insert a WKB in character form  
      void SqlInsertFromBinary();   // Insert a WKB in binary form   
      void SqlSelectGeogAsText(); // Retrieve the geography as Text.  
};   
  
// Allocate environment handles, connection handle, connect to data source, and allocate statement handle  
void direxec::sqlconn() {  
      // Allocate the enviroment handle  
      rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
      check_rc(rc);  
  
      // Set the ODBC version to version 3  
      rc = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
      check_rc(rc);  
  
      // Allocate the database connection handle  
      rc = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
      check_rc(rc);  
  
      // Connect to the database  
      rc = SQLDriverConnect(hdbc, NULL, szDSN, SQL_NTS, szConnStrOut, MAX_DATA, &swStrLen, SQL_DRIVER_NOPROMPT);  
      check_rc(rc);  
  
      // Allocate the statement handle  
      rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
      check_rc(rc);    
  
      // Allocate the descriptor handle  
      rc = rc = SQLAllocHandle(SQL_HANDLE_DESC, hdbc, &hdesc);  
      check_rc(rc);  
}   
  
// Display error message from the DiagRecord  
void direxec::error_out() {  
      // String to hold the SQL State  
      SQLCHAR szSQLSTATE[10];   
  
      // Error code  
      SDWORD nErr;  
  
      // The error message  
      SQLCHAR msg[SQL_MAX_MESSAGE_LENGTH + 1];  
  
      // Size of the message  
      SWORD cbmsg;  
  
      // If hstmt is not null use that for getting the DiagRec  
      if (hstmt)  
            rc = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
      // else get the diag record from the env  
      else  
            rc = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
  
      // If the rc is successful, show the message using a message box  
      if ( rc == SQL_SUCCESS) {  
            printf((char *)szData, "Error:\nSQLSTATE=%s,Native error=%ld, msg='%s'", szSQLSTATE, nErr, msg);  
            MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
      }  
}  
  
// Checks the return code.  If failure, displays the error, free the memory and exits the program  
void direxec::check_rc(RETCODE rc) {  
      if (!MYSQLSUCCESS(rc)) {  
            error_out();  
            SQLFreeEnv(henv);  
            SQLFreeConnect(hdbc);  
            exit(-1);  
      }   
}  
  
void direxec::SqlInsertFromBinary() {     
      rc = SQLPrepare(hstmt, (SQLCHAR*) "INSERT INTO SpatialSample(Name,Geog) values('Sample1',Geography::STGeomFromWKB(?,4326))", SQL_NTS);  
      check_rc(rc);  
  
      SQLCHAR szBytes [] = "\x01\x01\x00\x00\x00\x07\x00\xEC\xFA\xD0\x3A\x4C\x40\x01\x00\x80\x00\xB5\xDF\x07\xC0";  
      SQLLEN iDataLength = sizeof(szBytes)-1;  
  
      rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_VARBINARY, 100, 0, szBytes, sizeof(szBytes), &iDataLength);  
      check_rc(rc);  
  
      rc = SQLExecute(hstmt);  
      check_rc(rc);  
}  
  
void direxec::SqlInsertFromChar() {     
      rc = SQLPrepare(hstmt, (SQLCHAR*) "INSERT INTO SpatialSample(Name,Geog) values('Sample2',Geography::STGeomFromWKB(?,4326))", SQL_NTS);  
      check_rc(rc);  
  
      SQLCHAR szBytes [] = "01010000000700ECFAD03A4C4001008000B5DF07C0";  
  
      rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARBINARY, 100, 0, szBytes, sizeof(szBytes), NULL);  
      check_rc(rc);  
  
      rc = SQLExecute(hstmt);  
      check_rc(rc);  
}  
  
void direxec::SqlSelectGeogAsText() {  
      rc = SQLFreeStmt(hstmt, SQL_CLOSE);  
      check_rc(rc);   
  
      rc = SQLExecDirect(hstmt, (SQLCHAR*) "SELECT geog.STAsText() FROM SpatialSample", SQL_NTS);  
      check_rc(rc);   
  
      SQLCHAR rgcAsText[MAX_DATA];  
      SQLLEN cbAsText;   
  
      rc = SQLBindCol(hstmt, 1, SQL_C_CHAR, rgcAsText, sizeof(rgcAsText), &cbAsText);  
      check_rc(rc);  
  
      rc = SQLFetch(hstmt);  
      check_rc(rc);  
  
      rgcAsText[cbAsText] = '\0';  
      printf("%s\r\n", (LPSTR)rgcAsText);  
}   
  
int main() {  
      direxec x;  
  
      // Allocate handles, and connect.  
      x.sqlconn();    
  
      // Insert 2 samples into the table  
      x.SqlInsertFromChar();  
      x.SqlInsertFromBinary();  
  
      // Select 1 row from the table and display the geography as text  
      x.SqlSelectGeogAsText();  
}  
```  
  
```  
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'SpatialSample')  
   DROP TABLE SpatialSample  
GO  
```  
  
  
