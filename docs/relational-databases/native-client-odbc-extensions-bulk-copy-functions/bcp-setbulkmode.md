---
title: Bcp_setbulkmode | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bcp_setbulkmode function
ms.assetid: de56f206-1f7e-4c03-bf22-da9c7f9f4433
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1e0b8bdab13a6a937c6e97cec3ece700a685deb1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bcpsetbulkmode"></a>bcp_setbulkmode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bcp_setbulkmode ermöglicht die Angabe des Spaltenformats in einem Massenkopiervorgang alle Spaltenattribute in einem einzigen Funktionsaufruf festlegen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_setbulkmode (  
   HDBC hdbc,  
   INT property,  
   void * pField,  
   INT cbField,  
   void * pRow,  
   INT cbRow  
);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *Eigenschaft*  
 Eine Konstante vom Typ BYTE. Eine Liste der Konstanten finden Sie in der Tabelle im Abschnitt mit Hinweisen.  
  
 *pField*  
 Der Zeiger auf den Wert des Feldabschlusszeichens.  
  
 *cbField*  
 Die Länge (in Bytes) des Feldabschlusszeichenwerts.  
  
 *pRow*  
 Der Zeiger auf den Wert des Zeilenabschlusszeichens.  
  
 *cbRow*  
 Die Länge in Bytes des Zeilenabschlusszeichenwerts.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL  
  
## <a name="remarks"></a>Hinweise  
 Bcp_setbulkmode kann zum Massenkopieren aus einer Abfrage oder eine Tabelle verwendet werden. Wenn Bcp_setbulkmode für das Massenkopieren aus einer abfrageanweisung verwendet wird, muss er aufgerufen werden, vor dem Aufrufen von Bcp_control mit bcp_hint aufgerufen wird.  
  
 Bcp_setbulkmode ist eine Alternative zur Verwendung [Bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) und [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md), die nur können Sie angeben, das Format der eine Spalte pro Funktionsaufruf.  
  
 In der folgenden Tabelle sind die Konstanten für den *property* -Parameter aufgelistet.  
  
|property|Beschreibung|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|Gibt den Zeichenausgabemodus an.<br /><br /> Entspricht der – C-Option in BCP. EXE-Datei, und Bcp_setcolfmt mit **BCP_FMT_TYPE** -Eigenschaftensatz auf **SQLCHARACTER**.|  
|BCP_OUT_WIDE_CHARACTER_MODE|Gibt den Unicode-Ausgabemodus an.<br /><br /> Entspricht der – w-Option in BCP. EXE-Datei und Bcp_setcolfmt mit **BCP_FMT_TYPE** -Eigenschaftensatz auf **SQLNCHAR**.|  
|BCP_OUT_NATIVE_TEXT_MODE|Gibt systemeigene Typen für Nicht-Zeichen-Typen und Unicode für Zeichentypen an.<br /><br /> Entspricht der – N-Option in BCP. EXE-Datei und Bcp_setcolfmt mit **BCP_FMT_TYPE** -Eigenschaftensatz auf **SQLNCHAR** , wenn der Spaltentyp eine Zeichenfolge (Standard, wenn keine Zeichenfolge) ist.|  
|BCP_OUT_NATIVE_MODE|Gibt systemeigene Datenbanktypen an.<br /><br /> Entspricht der – n-Option in BCP. EXE-Datei und Bcp_setcolfmt mit **BCP_FMT_TYPE** -Eigenschaft auf den Standardwert festgelegt.|  
  
 Sie sollten nicht Bcp_setbulkmode verwenden, die mit einer Sequenz von Funktionsaufrufen, die bcp_setcolfmt Bcp_control und Bcp_readfmt enthält. Sie sollten z. B. nicht bcp_control(BCPTEXTFILE) und Bcp_setbulkmode aufrufen.  
  
 Sie können Bcp_control und Bcp_setbulkmode Bcp_control Optionen aufrufen, die nicht mit Bcp_setbulkmode in Konflikt stehen. Sie können z. B. bcp_control(BCPFIRST) und Bcp_setbulkmode aufrufen.  
  
 Wenn Sie versuchen, Bcp_setbulkmode mit einer Sequenz von Funktionsaufrufen aufzurufen, die Bcp_setcolfmt Bcp_control und Bcp_readfmt enthält, gibt einen der Funktionsaufrufe einen Sequenzfehler zurück. Falls gewünscht, um den Fehler zu beheben, rufen Sie Bcp_init, um alle Einstellungen zurücksetzen und erneut zu beginnen.  
  
 Im folgenden sind einige Beispiele für Funktionsaufrufe, die zu einem Fehler bei Funktionssequenz führen:  
  
```  
bcp_init(“table”, DB_IN);  
bcp_setbulkmode();  
```  
  
```  
bcp_init(“table”, DB_OUT);  
bcp_setbulkmode();  
bcp_readfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPHINTS, “select …”);  
bcp_setbulkmode();  
```  
  
```  
bcp_init(“table”, DB_OUT);  
bcp_setbulkmode();  
bcp_setcolfmt();  
```  
  
```  
bcp_init(“table”, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_readfmt();  
bcp_setcolfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setbulkmode();  
bcp_control(BCPHINTS, “select …”);  
bcp_readfmt();  
```  
  
```  
bcp_init(“table”, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_columns();  
```  
  
```  
bcp_init(“table”, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setcolfmt();  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden vier Dateien mit unterschiedlichen Einstellungen von bcp_setbulkmode erstellt.  
  
```  
// compile with: sqlncli11.lib odbc32.lib  
  
#include <windows.h>  
#include <stdio.h>  
#include <tchar.h>  
#include <sqlext.h>  
#include "sqlncli.h"  
  
// Global variables  
SQLHENV g_hEnv = NULL;  
SQLHDBC g_hDbc = NULL;  
  
void ODBCCleanUp() {  
   if (g_hDbc) {  
      SQLDisconnect(g_hDbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, g_hDbc);  
      g_hDbc = NULL;  
   }  
   if (g_hEnv) {  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      g_hEnv = NULL;  
   }  
}  
  
BOOL MakeODBCConnection(TCHAR * pszServer) {  
   TCHAR szConnectionString[500];  
   TCHAR szOutConnectionString[500];  
   SQLSMALLINT iLen;  
   SQLRETURN rc;  
  
   _sntprintf_s(szConnectionString, 500, TEXT("DRIVER={SQL Server Native Client 11.0};Server=%s;Trusted_connection=yes;"), pszServer);  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE,&g_hEnv);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_ENV...) failed\n");  
      return false;  
   }  
   rc = SQLSetEnvAttr(g_hEnv,SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, SQL_IS_UINTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetEnvAttr failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   rc = SQLAllocHandle( SQL_HANDLE_DBC, g_hEnv , &g_hDbc);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_DBC...) failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   // Enable BCP  
   rc = SQLSetConnectAttr(g_hDbc, SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON, SQL_IS_INTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetConnectAttr(.. SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON ...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // connecting ...  
   rc = SQLDriverConnect(g_hDbc,NULL, (SQLTCHAR*)szConnectionString, SQL_NTS, (SQLTCHAR*)szOutConnectionString, 500, &iLen, SQL_DRIVER_NOPROMPT);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLDriverConnect(SQL_HANDLE_DBC...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   return true;  
}  
  
BOOL BCPSetBulkMode(TCHAR * pszServer, TCHAR * pszQureryOut, char BCPType, TCHAR * pszDataFile) {  
   SQLRETURN rc;  
  
   if (!MakeODBCConnection(pszServer))  
      return false;  
   rc = bcp_init(g_hDbc, NULL, pszDataFile, NULL, DB_OUT);   // bcp init for queryout  
   if (SUCCEED != rc) {  
      printf("bcp_init failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if (BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if (BCPType == 'w') {   // bcp -w   
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               ODBCCleanUp();  
               return false;  
            }  
            rc = bcp_setbulkmode(g_hDbc, bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (SUCCEED != rc) {  
               printf("bcp_setbulkmode failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // set queryout TSQL statement  
            rc = bcp_control(g_hDbc, BCPHINTS , pszQureryOut);  
            if (SUCCEED != rc) {  
               printf("bcp_control(..BCP_OPTION_HINTS..) failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBINT nRowsInserted = 0;  
            rc = bcp_exec(g_hDbc, &nRowsInserted);  
            if (SUCCEED != rc) {  
               printf("bcp_exec failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            ODBCCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', TEXT("bcpc.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', TEXT("bcpw.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', TEXT("bcpn.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', TEXT("bcp_N.dat"));  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
