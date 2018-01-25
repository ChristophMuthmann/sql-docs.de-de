---
title: 'Abrufen von Spalten mithilfe von IRow:: GetColumns (oder IRow:: Open) und ISequentialStream | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Open method
- ISequentialStream interface, samples
- GetColumns method
ms.assetid: 0761f469-9b6c-4fa6-bbd7-f0cb936e4f1c
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4388fa8499cef7b01a9adcd3e3a9754cfa1e261c
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="fetch-columns-using-irowgetcolumns-or-irowopen-and-isequentialstream"></a>Abrufen von Spalten mithilfe von IRow::GetColumns (oder IRow::Open) und ISequentialStream
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Umfangreiche Daten können gebunden oder abgerufen werden mithilfe der **ISequentialStream** Schnittstelle. Bei gebundenen Spalten gibt das Statusflag DBSTATUS_S_TRUNCATED an, dass die Daten abgeschnitten werden.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn die Windows-Authentifizierung nicht verfügbar ist, fordern Sie die Benutzer auf, ihre Anmeldeinformationen zur Laufzeit einzugeben. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Sie die Anmeldeinformationen permanent speichern müssen, verschlüsseln Sie sie mit der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=64532).  
  
### <a name="to-fetch-columns-using-irowgetcolumns-or-irowopen-and-isequentialstream"></a>So rufen Sie Spalten mithilfe von IRow::GetColumns (oder IRow::Open) und ISequentialStream ab  
  
1.  Stellen Sie eine Verbindung mit der Datenquelle her.  
  
2.  Führen Sie den Befehl (in diesem Beispiel **ICommandExecute** mit IID_IRow aufgerufen).  
  
3.  Die Spaltendaten mit FETCH **IRow::Open()** oder **IRow::GetColumns()**.  
  
    -   **IRow::Open()** dienen zum Öffnen einer **ISequentialStream** in der Zeile. Geben Sie DBGUID_STREAM an, dass die Spalte einen Strom von Binärdaten enthält (**IStream** oder **ISequentialStream** kann dann zum Lesen der Daten aus der Spalte verwendet werden).  
  
    -   Wenn **IRow::GetColumns()** verwendet wird, die **pData** -Element der DBCOLUMNACCESS-Struktur auf ein Datenstromobjekt festgelegt ist.  
  
4.  Verwendung **ISequentialStream::Read()** wiederholt, um die angegebene Anzahl von Bytes in den Consumerpuffer zu lesen.  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel zeigt, wie Sie mithilfe von IRow eine einzelne Zeile abrufen können. In diesem Beispiel wird jeweils eine Spalte aus der Zeile abgerufen. In diesem Beispiel wird die Verwendung von IRow::Open() sowie IRow::GetColumns() veranschaulicht. Im Beispiel werden die Spaltendaten mithilfe von ISequentialStream::Read gelesen.  
  
 Dieses Beispiel erfordert die AdventureWorks-Beispieldatenbank, die Sie von der Homepage [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) herunterladen können.  
  
 Das erste Codelisting ([!INCLUDE[tsql](../../includes/tsql-md.md)]) erstellt eine im Beispiel verwendete Tabelle.  
  
 Kompilieren Sie mit ole32.lib und oleaut32.lib, und führen Sie das zweite Codelisting (C++). Diese Anwendung stellt eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standardinstanz des Computers her. Bei einigen Windows-Betriebssystemen müssen Sie (localhost) oder (local) in den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz ändern. Um eine Verbindung mit einer benannten Instanz herzustellen, ändern Sie die Verbindungszeichenfolge von l"(Local)" "zu l"(Local)"\\\name", wobei der Name der benannten Instanz ist. Standardmäßig wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express in einer benannten Instanz installiert. Stellen Sie sicher, dass die INCLUDE-Umgebungsvariable das Verzeichnis einschließt, das sqlncli.h enthält.  
  
 Das dritte Codelisting ([!INCLUDE[tsql](../../includes/tsql-md.md)]) löscht die im Beispiel verwendete Tabelle.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'MyTable')  
     DROP TABLE MyTable  
GO  
  
CREATE TABLE MyTable  
(  
     col1  int,  
     col2  varchar(50),  
     col3  char(50),  
     col4  datetime,  
     col5  float,  
     col6  money,  
     col7  sql_variant,  
     col8  binary(50),  
     col9  text,  
     col10 image  
)  
GO  
  
-- Enter data  
INSERT INTO MyTable  
values  
(  
     10,  
     'abcdefghijklmnopqrstuvwxyz',  
     'ABCDEFGHIJKLMNOPQRSTUVWXYZ',  
     '11/1/1999 11:52 AM',  
     3.14,  
     99.95,  
     CONVERT(nchar(50), N'AbCdEfGhIjKlMnOpQrStUvWxYz'),  
     0x123456789,  
     REPLICATE('AAAAABBBBB', 500),  
     REPLICATE(0x123456789, 500)  
)  
GO  
```  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define DBINITCONSTANTS  
#define INITGUID  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <stdio.h>  
#include <windows.h>  
#include <iostream>  
#include <oledb.h>  
#include <sqlncli.h>  
  
using namespace std;  
  
const int kMaxBuff = 50;  
int InitializeAndEstablishConnection();  
HRESULT GetColumnSize(IRow* pUnkRow, ULONG iCol);  
ULONG PrintData(ULONG iCols, ULONG iStart, DBCOLUMNINFO* prgInfo, DBCOLUMNACCESS* prgColumns);  
HRESULT GetColumns(IRow* pUnkRow, ULONG iStart, ULONG iEnd);  
HRESULT GetSequentialColumn(IRow* pUnkRow, ULONG iCol, BOOL fOpen = TRUE);  
  
IDBInitialize*       pIDBInitialize     = NULL;  
IDBProperties*       pIDBProperties     = NULL;  
IDBCreateSession*    pIDBCreateSession  = NULL;  
IDBCreateCommand*    pIDBCreateCommand  = NULL;  
ICommandText*        pICommandText      = NULL;  
IRow*                pIRow              = NULL;  
DBCOLUMNINFO*        pDBColumnInfo      = NULL;  
IAccessor*           pIAccessor         = NULL;  
DBPROP               InitProperties[4];  
DBPROPSET            rgInitPropSet[1];  
ULONG                i, j;  
HRESULT              hresult;  
DBROWCOUNT           cNumRows = 0;  
ULONG                lNumCols;  
WCHAR*               pStringsBuffer;  
DBBINDING*           pBindings;  
ULONG                ConsumerBufColOffset = 0;  
HACCESSOR            hAccessor;  
ULONG                lNumRowsRetrieved;  
HROW                 hRows[10];  
HROW*                pRows = &hRows[0];  
  
int main() {  
   ULONG iidx = 0;  
   WCHAR* wCmdString = OLESTR("SELECT * FROM MyTable ");    
  
   // Call a function to initialize and establish connection.   
   if (InitializeAndEstablishConnection() == -1) {  
      cout << "Failed to initialize and establish connection.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Create a session object.  
   if (FAILED(pIDBInitialize->QueryInterface( IID_IDBCreateSession, (void**) &pIDBCreateSession))) {  
      cout << "Failed to obtain IDBCreateSession interface.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   if (FAILED(pIDBCreateSession->CreateSession( NULL,  
                                                IID_IDBCreateCommand,  
                                                (IUnknown**) &pIDBCreateCommand))) {  
      cout << "pIDBCreateSession->CreateSession failed.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Access the ICommandText interface.  
   if (FAILED(pIDBCreateCommand->CreateCommand( NULL, IID_ICommandText, (IUnknown**) &pICommandText))) {  
      cout << "Failed to access ICommand interface.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Use SetCommandText() to specify the command text.  
   if (FAILED(pICommandText->SetCommandText(DBGUID_DBSQL, wCmdString))) {  
      cout << "Failed to set command text.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Execute the command.  
   if (FAILED(hresult = pICommandText->Execute( NULL, IID_IRow, NULL, &cNumRows, (IUnknown **) &pIRow))) {  
      cout << "Failed to execute command.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   DBORDINAL cColumns = 0;  
   DBCOLUMNINFO* prgInfo = 0;  
   OLECHAR* pColNames;  
  
   // Get column count  
   HRESULT hr;  
   IColumnsInfo* pIColumnsInfo;  
   hr = pIRow->QueryInterface(IID_IColumnsInfo, (void**) &pIColumnsInfo);  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   // Get columns (one at a time) using ISequentialStream and Open  
   // 3rd parameter is by default TRUE indicating use of ISequentialStream and Open.  
   DBCOLUMNINFO* colInfo;   
   for ( iidx = 1 ; iidx <= cColumns ; iidx++ ) {  
  colInfo = (DBCOLUMNINFO*)(prgInfo + (iidx - 1));  
  if (colInfo->dwFlags & DBCOLUMNFLAGS_ISLONG)  
  hresult = GetSequentialColumn(pIRow, iidx);  
  else  
  hresult = GetColumns(pIRow, iidx, iidx);  
   }  
  
   // Release the Row object.  
   pIRow->Release();  
  
   // Execute the command again.  
   if (FAILED(hresult = pICommandText->Execute(NULL,  
                                               IID_IRow,  
                                               NULL,  
                                               &cNumRows,  
                                               (IUnknown **) &pIRow))) {  
      cout << "Failed to execute command.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Now get columns (one at a time) using ISequentialStream and GetColumns.   
   // The 3rd parameter is by default TRUE indicating use of ISequentialStream   
   // and GetColumns  
   for ( iidx = 1 ; iidx <= cColumns ; iidx++ ) {  
  colInfo = (DBCOLUMNINFO*)(prgInfo + (iidx - 1));  
  if (colInfo->dwFlags & DBCOLUMNFLAGS_ISLONG)  
  hresult = GetSequentialColumn(pIRow, iidx, FALSE);  
  else  
  hresult = GetColumns(pIRow, iidx, iidx);  
   }  
  
CLEANUP:  
   // Release memory.  
   pICommandText->Release();  
   pIDBCreateCommand->Release();  
   pIDBCreateSession->Release();  
  
   if (FAILED(pIDBInitialize->Uninitialize())) {  
      // Uninitialize not required, but it fails if an interface has not been released, can be used for debugging.   
      // cout << "Problem uninitializing.\n";  
   }  
  
   pIDBInitialize->Release();  
  
   CoTaskMemFree(prgInfo);  
   CoTaskMemFree(pColNames);  
   if( pIColumnsInfo )  
      pIColumnsInfo->Release();  
  
   // Release the COM library.  
   CoUninitialize();  
}  
  
HRESULT GetSequentialColumn(IRow* pUnkRow, ULONG iCol, BOOL fOpen) {  
   HRESULT hr = NOERROR;  
   ULONG cbRead = 0;  
   ULONG cbTotal = 0;  
   DBORDINAL cColumns = 0;  
   ULONG cReads = 0;  
   ISequentialStream* pIStream = NULL;  
   WCHAR* pBuffer[kMaxBuff];   // 50 chars read by ISequentialStream::Read()  
   DBCOLUMNINFO* prgInfo = 0;  
   OLECHAR* pColNames = 0;  
   IColumnsInfo* pIColumnsInfo;  
   DBID columnid;  
   DBCOLUMNACCESS column;  
  
   wprintf(L"[RETRIEVING COLUMN %d SEQUENTIALLY]\n", iCol);  
  
   // Get column information (basically get column id).  
   hr = pUnkRow->QueryInterface(IID_IColumnsInfo, (void**) &pIColumnsInfo);  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   // Get Column ID.  
   columnid = (prgInfo + (iCol - 1))->columnid;  
   if (fOpen) {   // Get columns using ISequentialStream and IRow::Open  
      wprintf(L"[RETRIEVING COLUMNS USING ");  
      wprintf(L" ISequentialSteam and Open]\n");  
  
      // Open sequential stream.  
      hr = pUnkRow->Open(NULL,  
                         &columnid,  
                         DBGUID_STREAM,  
                         0,  
                         IID_ISequentialStream,  
                         (LPUNKNOWN *)&pIStream);  
  
      if (FAILED(hr)) {  
         wprintf(L"Unable to get ISequentialStream interface.\n");  
         goto CLEANUP;  
      }  
   }  
  
   else {   // Get Columns using IRow::GetColumns and ISequentialStream.  
      wprintf(L"[RETRIEVING COLUMNS USING ");  
      wprintf(L" GetColumns and ISequentialStream]\n");  
  
  IUnknown* pUnkStream = NULL;  
  
      ZeroMemory(&column, sizeof(column));  
      column.columnid = prgInfo[iCol - 1].columnid;  
      column.wType = DBTYPE_IUNKNOWN;  
      column.pData = (LPVOID*) &pUnkStream;  
  
      hr = pUnkRow->GetColumns(1, &column);  
      if (FAILED(hr)) {  
         wprintf(L"Error executing IRow::GetColumns.\n");  
         goto CLEANUP;  
      }  
  
      hr = pUnkStream->QueryInterface(IID_ISequentialStream, (LPVOID*) &pIStream);  
      if (FAILED(hr)) {  
         wprintf(L"Unable to get ISequentialStream interface ");  
         wprintf(L"via IRow::GetColumns.\n");  
         goto CLEANUP;  
      }  
  
      pUnkStream->Release();  
   }  
  
   ZeroMemory(pBuffer, kMaxBuff * sizeof(WCHAR));  
  
   // Read 50 chars at a time until no more data.  
   do {  
      hr = pIStream->Read(pBuffer, kMaxBuff, &cbRead);  
      if (FAILED(hr)) {  
         wprintf(L"Error reading data.\n");  
         goto CLEANUP;  
      }  
  
      cbTotal = cbTotal + cbRead;  
  
      // Print the data  
      wprintf(L"READ #%d: %-*S\n", ++cReads, kMaxBuff, pBuffer);  
   } while(cbRead > 0);  
  
   wprintf(L"[READ %d bytes for column %d.\n", cbTotal, iCol);  
  
CLEANUP:  
   if (pIColumnsInfo)  
      pIColumnsInfo->Release();  
  
   CoTaskMemFree(prgInfo);  
   CoTaskMemFree(pColNames);  
  
   if (pIStream)  
      pIStream->Release();  
  
   return hr;  
}  
  
BOOL InitColumn(DBCOLUMNACCESS* pCol, DBCOLUMNINFO* pInfo) {  
   // If maximum possible length of a value column is very large (text or image  
   //  column is read) limit that size to 512 bytes (for illustration purposes).  
  
   ULONG ulSize;  
   if (pInfo->wType == DBTYPE_WSTR || pInfo->wType == DBTYPE_STR)  
      ulSize = (pInfo->ulColumnSize < 0x7fffffff) ? pInfo->ulColumnSize : 512;  
   else  
      ulSize = 128; //default buffer to handle conversion to text of non-string data types  
  
   // Verify data buffer is large enough.  
   if (pCol->cbMaxLen < (ulSize + 1)) {  
      if (pCol->pData) {  
         delete [] pCol->pData;  
         pCol->pData = NULL;  
      }  
  
      // Allocate data buffer  
      void * p = pCol->pData = new WCHAR[ulSize + 1];  
      if (!(p /*pCol->pData = new WCHAR[ulSize + 1]*/ ))  
         return FALSE;  
  
      // set the max length of caller-initialized memory.  
      pCol->cbMaxLen = sizeof(WCHAR) * (ulSize + 1);  
  
      // In the above 2 steps, pData is pointing to memory (it is not NULL) and   
      // cbMaxLen has a value (not 0), so next call to IRow->GetData()   
      // will read the data from the column.  
   }  
  
   // Clear memory buffer  
   ZeroMemory((void*) pCol->pData, pCol->cbMaxLen);  
  
   // Set properties.  
   //pCol->wType = DBTYPE_WSTR;  
   pCol->wType = DBTYPE_WSTR;  
   pCol->columnid = pInfo->columnid;  
   pCol->cbDataLen = 0;  
   pCol->dwStatus = 0;  
   pCol->dwReserved = 0;  
   pCol->bPrecision = 0;  
   pCol->bScale = 0;  
  
   return TRUE;  
}  
  
HRESULT GetColumns(IRow* pUnkRow, ULONG iStart, ULONG iEnd) {  
// Start and end are same. Thus, get only one column.  
   HRESULT          hr = E_FAIL;  
   ULONG            iidx;          // loop counter  
   DBORDINAL        cColumns;      // Count of columns  
   ULONG            cUserCols;     // Count of user columns  
   DBCOLUMNINFO*    prgInfo;       // Column of info. array  
   OLECHAR*         pColNames;     // Array of column names  
   DBCOLUMNACCESS*  prgColumns;    // Ptr to column access structures array  
   DBCOLUMNINFO*    pCurrInfo;  
   DBCOLUMNACCESS*  pCurrCol;  
  
   IColumnsInfo* pIColumnsInfo = NULL;  
  
   // Initialize  
   cColumns    = 0;  
   prgInfo     = NULL;  
   pColNames   = NULL;  
   prgColumns  = NULL;  
  
   printf("Retrieving data with GetColumns\n");  
  
   // Get column info to build column access array  
   hr = pUnkRow->QueryInterface(IID_IColumnsInfo, (void**)&pIColumnsInfo);  
  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   // Determine no. of columns to retrieve.  Since iEnd and iStart is same,   
   // this is redundent step.  cUserCols will always be 1.  
   cUserCols = iEnd - iStart + 1;   
  
   // Walk list of columns and setup a DBCOLUMNACCESS structure  
   DBCOLUMNACCESS * x = (prgColumns = new DBCOLUMNACCESS[cUserCols]);  
   if (!(x /*prgColumns = new DBCOLUMNACCESS[cUserCols]*/ )) {   // cUserCols is only 1  
      hr = E_FAIL;  
      goto CLEANUP;  
   }  
  
   ZeroMemory((void*) prgColumns, sizeof(DBCOLUMNACCESS) * cUserCols);  
  
   for ( iidx = 0 ; iidx < cUserCols ; iidx++ ) {  
      pCurrInfo = prgInfo + iidx + iStart - 1;  
      pCurrCol = prgColumns + iidx;  
  
      // Here the values of pData and cbMaxLen elements of DBCOLUMNACCESS   
      // elements is set. Thus IRow->GetColumns() will return actual data.  
      if ( InitColumn(pCurrCol, pCurrInfo) == FALSE )  
         goto CLEANUP;  
   }  
  
   hr = pUnkRow->GetColumns(cUserCols, prgColumns);   // cUserCols = 1  
   if (FAILED(hr))  
      printf("Error occured\n");  
  
   // Show data.  
   PrintData(cUserCols, iStart, prgInfo, prgColumns);  
  
CLEANUP:  
   if (pIColumnsInfo)  
      pIColumnsInfo->Release();  
   if (prgColumns)  
      delete [] prgColumns;  
  
   return hr;  
}  
// This function returns the actual width of the data in the column (not the   
// columnwidth in DBCOLUMNFO structure which is the width of the column)  
HRESULT GetColumnSize(IRow* pUnkRow, ULONG iCol) {  
   HRESULT         hr = NOERROR;  
   DBORDINAL       cColumns = 0;   // Count the columns  
   DBCOLUMNINFO*   prgInfo;        // Column info array  
   OLECHAR*        pColNames;  
   DBCOLUMNACCESS  column;            
   DBCOLUMNINFO*   pCurrInfo;  
   IColumnsInfo*   pIColumnsInfo = NULL;  
  
   // Initialize  
   prgInfo = NULL;  
   pColNames = NULL;  
  
   printf("Checking column size\n");  
  
   // Get column info to build column access array  
   hr = pUnkRow->QueryInterface(IID_IColumnsInfo, (void**) &pIColumnsInfo);  
   if (FAILED(hr))  
      goto CLEANUP;  
  
   hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
   if (FAILED(hr))  
      goto CLEANUP;  
   printf("Value of cColumns is %d\n", cColumns);  
  
   // Setup a DBCOLUMNACCESS structure: pData is set to NULL and cbMaxLen is set   
   // to 0. Thus IRow->GetColumns() returns only the actual column length in  
   // cbDataLen member of DBCOLUMNACCESS structure.In this case you can call   
   // IRow->GetColumns() again for the same column to retrieve actual data in the second call.  
   ZeroMemory((void*) &column, sizeof(DBCOLUMNACCESS));  
   column.pData = NULL;  
  
   pCurrInfo = prgInfo + iCol - 1;  
   // Get column id in DBCOLUMNACCESS structure. It is then used in GetColumn().  
   column.columnid = pCurrInfo->columnid;   
  
   printf("column.columnid value is %d\n", column.columnid);  
   // We know which column to get.  The column.columnid gives the column number.  
   hr = pUnkRow->GetColumns(1, &column);   
   if (FAILED(hr))  
      printf("Errors occured\n");  
  
   // Show data  
   PrintData(1, iCol, prgInfo, &column);  
  
CLEANUP:  
   if (pIColumnsInfo)  
      pIColumnsInfo->Release();  
   return hr;  
}  
  
BOOL GetStatus(DWORD dwStatus, WCHAR* pwszStatus) {  
   switch (dwStatus) {  
   case DBSTATUS_S_OK:  
      wcscpy_s(pwszStatus, 255, L"DBSTATUS_S_OK");  
      break;  
   case DBSTATUS_E_CANTCONVERTVALUE:  
   wcscpy_s(pwszStatus, 255, L"DBSTATUS_E_CANTCONVERTVALUE");  
   break;  
   case DBSTATUS_S_ISNULL:  
   wcscpy_s(pwszStatus, 255, L"DBSTATUS_S_ISNULL");  
   break;  
   case DBSTATUS_E_UNAVAILABLE:  
      wcscpy_s(pwszStatus, 255, L"DBSTATUS_E_UNAVAILABLE");  
      break;  
   case DBSTATUS_S_TRUNCATED:  
      wcscpy_s(pwszStatus, 255, L"DBSTATUS_S_TRUNCATED");  
      break;  
   default:  
      swprintf_s(pwszStatus, sizeof(pwszStatus), L"OTHER STATUS VALUE: %d", dwStatus);  
   }  
   return TRUE;  
}  
  
ULONG PrintData(ULONG iCols,   
                ULONG iStart,   
                DBCOLUMNINFO* prgInfo,   
                DBCOLUMNACCESS* prgColumns) {  
  
   WCHAR wszStatus[255];  
   DBCOLUMNINFO* pCurrInfo;  
   DBCOLUMNACCESS* pCurrCol;  
   ULONG iidx = 0;       // Loop counter  
  
   printf("%-3s %-20s %-21s %-9s %-9s %-50s\n", "No.", "Name", "Status", "Length", "Max", "Data");  
  
   for ( iidx = 0 ; iidx < iCols ; iidx++ ) {  
      pCurrInfo = prgInfo + iidx + iStart - 1;  
      pCurrCol = prgColumns + iidx;  
  
      GetStatus(pCurrCol->dwStatus, wszStatus);   
      // was the data successfully retrieved?  
      wprintf(L"%-3d %-20s %-21s %-9d %-9d %-50s\n", iStart + iidx,  
                                                    pCurrInfo->pwszName,  
                                                    wszStatus,  
                                                    pCurrCol->cbDataLen,  
                                                    pCurrCol->cbMaxLen,  
pCurrCol->dwStatus == DBSTATUS_S_ISNULL ? L"(NULL)" : (WCHAR*) pCurrCol->pData);  
   }  
  
   wprintf(L"\n");  
   return iidx;  
}  
  
int InitializeAndEstablishConnection() {      
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the SQLNCLI provider.  
   hresult = CoCreateInstance(CLSID_SQLNCLI11,   
                              NULL,   
                              CLSCTX_INPROC_SERVER,  
                              IID_IDBInitialize,   
                              (void **) &pIDBInitialize);  
  
   if(FAILED(hresult)) {  
      printf("Failed to get IDBInitialize interface.\n");  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   // Initialize the property values needed to establish the connection.  
   for (i =  0 ; i < 4 ; i++ )  
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt = VT_BSTR;  
  
   InitProperties[0].vValue.bstrVal = SysAllocString(L"(local)");  
   InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid         = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt     = VT_BSTR;  
   InitProperties[1].vValue.bstrVal= SysAllocString(L"AdventureWorks");  
   InitProperties[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid         = DB_NULLID;  
  
   // connection  
   InitProperties[2].dwPropertyID  = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt     = VT_BSTR;  
   InitProperties[2].vValue.bstrVal= SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid         = DB_NULLID;  
  
   // Now that the properties are set, construct the DBPROPSET structure  
   // (rgInitPropSet). The DBPROPSET structure is used to pass an array   
   // of DBPROP structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties    = 4;  
   rgInitPropSet[0].rgProperties   = InitProperties;  
  
   // Set initialization properties.  
   hresult = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   if (FAILED(hresult)) {  
      cout << "Failed to get IDBProperties interface.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   hresult = pIDBProperties->SetProperties(1, rgInitPropSet);   
   if (FAILED(hresult)) {  
      cout << "Failed to set initialization properties.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   if (FAILED(pIDBInitialize->Initialize())) {  
      cout << "Problem establishing connection to the data source.\n";  
      // Insert your code for cleanup and error handling  
      return -1;  
   }  
  
   return 0;  
}  
```  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'MyTable')  
     DROP TABLE MyTable  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Themen zur Vorgehensweise](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
