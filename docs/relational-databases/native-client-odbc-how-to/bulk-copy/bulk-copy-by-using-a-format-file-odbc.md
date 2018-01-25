---
title: Massenkopieren mithilfe einer Formatdatei (ODBC) | Microsoft Docs
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
helpviewer_keywords:
- bulk copy using format file [ODBC]
- ODBC, bulk copy operations
ms.assetid: 970fd3af-f918-4fc3-a5b1-92596515d4de
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39817debb4c61657af78127c22e6bca498680786
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bulk-copy-by-using-a-format-file-odbc"></a>Massenkopieren mithilfe einer Formatdatei (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Dieses Beispiel zeigt, wie die ODBC-Funktion bcp_init mit einer Formatdatei verwendet wird.  
  
### <a name="to-bulk-copy-by-using-a-format-file"></a>So führen Sie einen Massenkopiervorgang mithilfe einer Formatdatei aus  
  
1.  Ordnen Sie ein Umgebungshandle und ein Verbindungshandle zu.  
  
2.  Legen Sie SQL_COPT_SS_BCP und SQL_BCP_ON fest, um Massenkopiervorgänge zu aktivieren.  
  
3.  Stellen Sie eine Verbindung zu Microsoft® SQL Server™ her.  
  
4.  Rufen Sie [bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) auf, um die folgenden Informationen festzulegen:  
  
    -   Name der Tabelle oder Sicht, aus der bzw. in die massenkopiert werden soll  
  
    -   Name der Datendatei, welche die in die Datenbank zu kopierenden Daten enthält bzw. in welche die Daten eingefügt werden sollen, die aus der Datenbank kopiert werden  
  
    -   Name der Datendatei, in die Fehlermeldungen zum Massenkopiervorgang ausgegeben werden sollen (geben Sie NULL an, wenn keine Meldungsdatei erstellt werden soll)  
  
    -   Kopierrichtung: DB_IN, wenn Daten aus der Datei in die Tabelle oder Sicht kopiert werden sollen  
  
5.  Rufen Sie [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) auf, um eine Formatdatei zu lesen, welche die vom Massenkopiervorgang verwendete Datendatei beschreibt.  
  
6.  Rufen Sie [bcp_exec](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) auf, um den Massenkopiervorgang auszuführen.  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel wird nicht auf IA64-basierten Systemen unterstützt.  
  
 Sie benötigen eine ODBC-Datenquelle mit dem Namen AdventureWorks, deren Standarddatenbank die AdventureWorks-Beispieldatenbank ist. (Sie können die AdventureWorks-Beispieldatenbank von der Homepage [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) herunterladen.) Diese Datenquelle muss auf dem ODBC-Treiber basieren, der vom Betriebssystem bereitgestellt wird (der Treibername lautet "SQL Server"). Wenn Sie dieses Beispiel als 32-Bit-Anwendung entwickeln und unter einem 64-Bit-Betriebssystem ausführen, müssen Sie die ODBC-Datenquelle mit dem ODBC-Administrator in %windir%\SysWOW64\odbcad32.exe erstellen.  
  
 In diesem Beispiel wird eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Standardinstanz des Computers hergestellt. Ändern Sie zum Herstellen einer Verbindung mit einer benannten Instanz die Definition der ODBC-Datenquelle, um die Instanz im folgenden Format anzugeben: Server\benannteInstanz. Standardmäßig wird [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] in einer benannten Instanz installiert.  
  
 Führen Sie das erste Codelisting ([!INCLUDE[tsql](../../../includes/tsql-md.md)]) aus, um die im Beispiel verwendete Tabelle zu erstellen.  
  
 Kopieren Sie das zweite Codelisting, und fügen Sie es in eine Datei mit dem Namen Bcpfmt.fmt ein. Jede Spalte in der Tabelle wird durch ein Tabstoppzeichen getrennt.  
  
 Kopieren Sie das dritte Codelisting, und fügen Sie es in eine Datei mit dem Namen Bcpodbc.bcp ein. Jedem Wagenrücklauf in der Datei ist ein Tabstoppzeichen vorangestellt.  
  
 Kompilieren Sie das vierte Codelisting (C++) mit odbc32.lib und odbcbcp.lib. Wenn Sie das Beispiel mit MSBuild.exe erstellt haben, kopieren Sie zuerst Bcpfmt.fmt und Bcpodbc.bcp aus dem Projektverzeichnis in das Verzeichnis mit der EXE-Datei, und rufen Sie dann die EXE-Datei auf.  
  
 Führen Sie das fünfte Codelisting ([!INCLUDE[tsql](../../../includes/tsql-md.md)]) aus, um die im Beispiel verwendete Tabelle zu löschen.  
  
```  
use AdventureWorks  
CREATE TABLE BCPDate (cola int, colb datetime)  
```  
  
```  
8.0  
2  
1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
```  
  
```  
1  
2  
  
```  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Das Massenkopieren mit der SQL Server-ODBC-Treiber Themen zur Vorgehensweise &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [Verwenden von Datendateien und Formatdateien](../../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
  
