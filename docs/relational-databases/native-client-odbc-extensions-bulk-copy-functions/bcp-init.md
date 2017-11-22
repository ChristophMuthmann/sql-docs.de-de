---
title: Bcp_init | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_init
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ae86d774a168a3e68ca4cb0bbcec1f3a741f801b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="bcpinit"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Initialisiert den Massenkopiervorgang.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *szTable*  
 Name der Datenbanktabelle, in die bzw. aus der kopiert werden soll. Dieser Name kann auch den Namen der Datenbank oder den Namen des Besitzers enthalten. Beispielsweise **pubs.gracie.titles**, **Pubs... Titel**, **gracie.titles**, und **Titel** sind gültige Tabellennamen.  
  
 Wenn *eDirection* DB_OUT ist, *SzTable* kann auch der Name einer Datenbanksicht sein.  
  
 Wenn *eDirection* DB_OUT ist und mit eine SELECT-Anweisung angegeben werden [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) vor [Bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) aufgerufen wird, **Bcp_init** *SzTable* muss auf NULL festgelegt werden.  
  
 *szDataFile*  
 Name der Benutzerdatei, in die bzw. aus der kopiert werden soll. Wenn Sie Daten direkt aus Variablen mit kopiert wird [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)legen *SzDataFile* auf NULL.  
  
 *szErrorFile*  
 Der Name der Fehlerdatei, in die Statusmeldungen, Fehlermeldungen und Kopien von Zeilen geschrieben werden sollen, die aus einem bestimmten Grund nicht von einer Benutzerdatei in eine Tabelle kopiert werden konnten. Wenn NULL, als übergeben wird *SzErrorFile*, wird keine Fehlerdatei verwendet.  
  
 *eDirection*  
 Die Richtung der Kopie, entweder DB_IN oder DB_OUT. DB_IN bedeutet eine Kopie aus Programmvariablen oder aus einer Benutzerdatei in eine Tabelle. DB_OUT bedeutet eine Kopie von einer Datenbanktabelle in eine Benutzerdatei an. Sie müssen einen Benutzerdateinamen mit DB_OUT angeben.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Rufen Sie **Bcp_init** vor dem Aufruf aller anderen Massenkopierfunktionen-Funktionen. **Bcp_init** führt die erforderlichen Initialisierungen für einen Massenkopiervorgang von Daten zwischen der Arbeitsstation und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Die **Bcp_init** Funktion muss mit einem ODBC-Verbindungshandle für die Verwendung mit Funktionen zum Massenkopieren aktiviert angegeben werden. Verwenden Sie zum Aktivieren des Handles [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) mit SQL_COPT_SS_BCP auf SQL_BCP_ON fest auf ein zugeordnetes, aber nicht verbundenes Verbindungshandle festgelegt. Wenn Sie versuchen, das Attribut einem bereits verbundenen Verbindungshandle zuzuweisen, tritt ein Fehler auf.  
  
 Wenn eine Datendatei angegeben wird, **Bcp_init** untersucht die Struktur der Quell- oder Zieltabelle Datenbanktabelle, nicht in der Datendatei. **Bcp_init** gibt die datenformatwerte für die Datendatei basierend auf den einzelnen Spalten in der Datenbanktabelle, Sicht oder SELECT-Resultset an. Diese Spezifikation enthält unter anderem den Datentyp jeder Spalte, das Vorhandensein bzw. Nichtvorhandensein eines Längen- oder NULL-Wertindikators und von Bytezeichenfolgen des Abschlusszeichens der Daten, sowie die Breite von Datentypen fester Länge. **Bcp_init** legt diese Werte wie folgt fest:  
  
-   Der angegebene Datentyp entspricht dem Datentyp der Spalte in der Datenbanktabelle, der Sicht oder dem SELECT-Resultset. Der Datentyp wird von den in der Datei sqlncli.h angegebenen systemeigenen Datentypen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgelistet. Die Daten selbst werden in computereigenem Format dargestellt, D. h. Daten aus einer Spalte mit **Ganzzahl** -Datentyp wird durch eine vier-Byte-Sequenz, die Groß dargestellt- oder die little-Endian-basierend auf dem Computer, der die Datendatei erstellt.  
  
-   Wenn ein Datenbankdatentyp eine feste Länge hat, haben auch die Daten der Datendatei eine feste Länge. Massenkopieren Funktionen, die Daten zu verarbeiten (z. B. [Bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)) werden die Datenzeilen erwartet wird die Länge der Daten in der Datendatei identisch mit der Länge der Daten in der Datenbanktabelle, Sicht oder SELECT-Spaltenliste angegeben werden analysiert. Beispielsweise Daten für eine Datenbankspalte, die als definiert **char(13)** muss für jede Zeile der Daten in der Datei 13 Zeichen dargestellt werden. Für Daten mit fester Länge kann ein NULL-Indikator verwendet werden, wenn die Datenbankspalte NULL-Werte zulässt.  
  
-   Wenn eine Bytesequenz für Abschlusszeichen definiert ist, wird deren Länge auf 0 festgelegt.  
  
-   Zum Kopieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss die Datendatei für jede Spalte der Datenbanktabelle Daten aufweisen. Beim Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Daten aus allen Spalten in der Datenbanktabelle, Sicht oder SELECT-Resultset in die Datendatei kopiert werden.  
  
-   Beim Kopieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss die Ordnungsposition einer Spalte in der Datendatei der Ordnungsposition einer Spalte in der Datenbanktabelle genau entsprechen. Beim Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **Bcp_exec** Daten auf Grundlage der Ordnungsposition der Spalte in der Datenbanktabelle platziert.  
  
-   Wenn eine Datenbank-Datentypen variabler Länge ist (z. B. **varbinary(22)**) oder wenn eine Datenbankspalte null-Werte enthalten kann, Daten in der Datendatei ein Längen-/Null-Indikator vorangestellt werden. Die Breite des Indikators ändert sich auf der Grundlage des Datentyps und der Version der Massenkopierfunktion.  
  
 Um für eine Datendatei angegebenen datenformatwerte zu ändern, rufen [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) und [Bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
 Massenkopiervorgänge in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können für Tabellen, die keine Indizes enthalten, optimiert werden, indem das Datenbank-Wiederherstellungsmodul auf SIMPLE oder BULK_LOGGED festgelegt wird. Weitere Informationen finden Sie unter [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md) und [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Wenn keine Datendatei verwendet wird, müssen Sie aufrufen [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) um das Format und den Speicherort im Arbeitsspeicher, der die Daten Fsor jede Spalte anzugeben, klicken Sie dann Kopieren von Datenzeilen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel zeigt, wie die ODBC-Funktion bcp_init mit einer Formatdatei verwendet wird.  
  
 Bevor Sie den C++-Code kompilieren und ausführen, sind folgende Schritte erforderlich:  
  
-   Erstellen einer ODBC-Datenquelle mit dem Namen "Test". Sie können diese Datenquelle einer beliebigen Datenbank zuordnen.  
  
-   Führen Sie für die Datenbank die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aus:  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   Fügen Sie dem Verzeichnis, in dem Sie die Anwendung ausführen, eine Datei namens Bcpfmt.fmt hinzu, und fügen Sie Folgendes in die Datei ein:  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   Fügen Sie dem Verzeichnis, in dem Sie die Anwendung ausführen, eine Datei namens Bcpodbc.bcp hinzu, und fügen Sie Folgendes in die Datei ein:  
  
    ```  
    1  
    2  
    ```  
  
 Nun sind Sie bereit, C++-Code zu kompilieren und auszuführen.  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
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
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
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
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
