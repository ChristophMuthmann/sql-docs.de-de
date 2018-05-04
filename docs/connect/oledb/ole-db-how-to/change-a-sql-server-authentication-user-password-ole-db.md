---
title: Ändern Sie eine SQL Server-Authentifizierungsbenutzerkennworts (OLE DB) | Microsoft Docs
description: Ändern eines SQL Server-authentifizierungsbenutzerkennworts (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: bac201886dd19f9e1ee05170cdbca93bbbf22a34
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="change-a-sql-server-authentication-user-password-ole-db"></a>Ändern eines SQL Server-Authentifizierungsbenutzerkennworts (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Beispiel wird gezeigt, wie OLE DB-verwenden Sie zum Ändern des Kennworts eines Benutzerkontos unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn die Windows-Authentifizierung nicht verfügbar ist, fordern Sie die Benutzer auf, ihre Anmeldeinformationen zur Laufzeit einzugeben. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Sie die Anmeldeinformationen permanent speichern müssen, verschlüsseln Sie sie mit der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Beispiel  
 Aktualisieren Sie vor dem Erstellen den C++-Code, um die Benutzer-ID, das alte Kennwort und das neue Kennwort anzugeben.  
  
 Diese Anwendung stellt eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Standardinstanz des Computers her. Bei einigen Windows-Betriebssystemen müssen Sie (localhost) oder (local) in den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz ändern. Um eine Verbindung mit einer benannten Instanz herzustellen, ändern Sie die Verbindungszeichenfolge von l"(Local)" "zu l"(Local)"\\\name", wobei der Name der benannten Instanz ist. Standardmäßig wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express in einer benannten Instanz installiert. Stellen Sie sicher, dass die INCLUDE-Umgebungsvariable das Verzeichnis einschließt, das msoledbsql.h enthält.  
  
 Kompilieren Sie mit ole32.lib und oleaut32.lib.  
  
 Um dieses Beispiel zu erstellen, müssen Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] authentifizierungsbenutzerkonto, für das Sie das Kennwort kennen. Wenn Sie Anmeldungen unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung zulassen möchten, öffnen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Knoten Server, und wählen Sie Eigenschaften aus. Wählen Sie Sicherheit aus, und aktivieren Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und Windows-Authentifizierungsmodus. Hinzufügen ein Benutzerkontos unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Authentifizierung, klicken Sie mit der mit der rechten Maustaste auf den Knoten "Sicherheit" im Objekt-Explorer, und wählen Sie hinzufügen.  
  
 Auf dem Server, auf dem Sie dieses Beispiel ausführen, muss mindestens eine Anmeldung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung aktiviert sein. Der Server muss außerdem Anmeldungen über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung zulassen.  
  
```  
// compile with: ole32.lib oleaut32.lib  
void InitializeAndEstablishConnection();  
  
#define STATUSDUMP(status)  case status : wprintf(L"status"); break;  
  
#define UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
  
#include <assert.h>  
#include <windows.h>  
#include <stdio.h>  
#include <stddef.h>  
#include <IOSTREAM>  
#include <cguid.h>  
#include <oledb.h>  
#include <oledberr.h>  
  
#include <msoledbsql.h>  
  
LPMALLOC pMalloc = NULL;  
IDBInitialize * pIDBInitialize = NULL;  
HRESULT hr;  
  
void DumpErrorInfo (IUnknown* pObjectWithError, REFIID IID_InterfaceWithError);  
void DumpErrorInfo (IUnknown* pObjectWithError, REFIID IID_InterfaceWithError, BOOL &has_sql_errors);  
  
int main() {  
   // All the initialization activities in a separate function.  
   InitializeAndEstablishConnection();  
  
   if ( FAILED( pIDBInitialize->Uninitialize() ) )  
      // Uninitialize is not required, but fails if an interface was not released.  
      printf("Problem uninitializing.\n");  
  
   pIDBInitialize->Release();  
   CoUninitialize();  
};  
  
void InitializeAndEstablishConnection() {  
   IDBProperties * pIDBProperties = NULL;  
   const ULONG nInitProps = 4;  
   DBPROP InitProperties[nInitProps];  
   const ULONG nSSInitProps = 1;  
   DBPROP SSInitProperties[nSSInitProps];  
  
   const ULONG nPropSet = 2;  
   DBPROPSET rgInitPropSet[nPropSet];  
  
   // Initialize the COM library.  
   CoInitialize(NULL);  
   CoGetMalloc(1, &pMalloc);  
  
   CLSID clsid;  
   CLSIDFromProgID(L"MSOLEDBSQL", &clsid);  
  
   // Obtain access to the SQLOLEDB provider.  
   hr = CoCreateInstance( clsid, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void **) &pIDBInitialize);  
   if (FAILED(hr))  
      printf("Failed in CoCreateInstance().\n");  
  
   // Initialize the property values needed to establish the connection.  
   for (int i = 0; i < nInitProps; i++)  
      VariantInit(&InitProperties[i].vValue);  
  
   // Specify database name.  
   InitProperties[0].dwPropertyID = DBPROP_INIT_CATALOG;  
   InitProperties[0].vValue.vt = VT_BSTR;  
   // Change the following line to use any database on your server  
   InitProperties[0].vValue.bstrVal = SysAllocString(L"master");  
   InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid = DB_NULLID;  
  
   InitProperties[1].dwPropertyID = DBPROP_AUTH_USERID;  
   InitProperties[1].vValue.vt = VT_BSTR;  
   // Modify the following line to add the user ID of a SQL Server Authentication account on your server  
   InitProperties[1].vValue.bstrVal = SysAllocString(L"");  
   InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid = DB_NULLID;  
  
   InitProperties[2].dwPropertyID = DBPROP_AUTH_PASSWORD;  
   InitProperties[2].vValue.vt = VT_BSTR;  
   // Modify the following line to add the new SQL Server Authentication password  
   InitProperties[2].vValue.bstrVal = SysAllocString(L"");  
   InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid = DB_NULLID;  
  
   InitProperties[3].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   InitProperties[3].vValue.vt = VT_BSTR;  
   InitProperties[3].vValue.bstrVal = SysAllocString(L"(local)");  
   InitProperties[3].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[3].colid = DB_NULLID;  
  
   SSInitProperties[0].dwPropertyID = SSPROP_AUTH_OLD_PASSWORD;  
   SSInitProperties[0].vValue.vt = VT_BSTR;  
   // Modify the following line to specify the existing SQL Server Authentication password  
   SSInitProperties[0].vValue.bstrVal = SysAllocString(L"");  
   SSInitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   SSInitProperties[0].colid = DB_NULLID;  
  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties = nInitProps;  
   rgInitPropSet[0].rgProperties = InitProperties;  
  
   rgInitPropSet[1].guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
   rgInitPropSet[1].cProperties = nSSInitProps;  
   rgInitPropSet[1].rgProperties = SSInitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface( IID_IDBProperties, (void **)&pIDBProperties);  
  
   if (FAILED(hr))  
      printf("Failed to obtain IDBProperties interface.\n");  
  
   hr = pIDBProperties->SetProperties( nPropSet, rgInitPropSet);  
  
   if (FAILED(hr))  
      printf("Failed to set initialization properties.\n");  
  
   pIDBProperties->Release();  
  
   // establish connection to the data source.  
   DWORD now = GetTickCount();  
  
   if ( FAILED(pIDBInitialize->Initialize()) ) {  
      printf("Problem in initializing.\n");  
      DumpErrorInfo(pIDBInitialize, IID_IDBInitialize);  
   }  
  
   DWORD tookms = GetTickCount() - now;  
   printf("Connection took %d ms.\n", tookms);  
}  
  
// DumpErrorInfo queries SQLOLEDB error interfaces, retrieving available status  
// or error information. This version is called when SQL Server errors are not expected.  
void DumpErrorInfo (IUnknown* pObjectWithError, REFIID IID_InterfaceWithError) {  
   BOOL has_sql_errors;  
   DumpErrorInfo (pObjectWithError, IID_InterfaceWithError, has_sql_errors);  
}  
  
// DumpErrorInfo queries SQLOLEDB error interfaces, retrieving available status   
// or error information. This version is called when an SQL Server error could occur.  
void DumpErrorInfo (IUnknown* pObjectWithError, REFIID IID_InterfaceWithError, BOOL &has_sql_errors ) {  
   // Interfaces used in the example.  
   IErrorInfo * pIErrorInfoAll = NULL;  
   IErrorInfo * pIErrorInfoRecord = NULL;  
   IErrorRecords * pIErrorRecords = NULL;  
   ISupportErrorInfo * pISupportErrorInfo = NULL;  
   ISQLErrorInfo * pISQLErrorInfo = NULL;  
   ISQLServerErrorInfo * pISQLServerErrorInfo = NULL;  
  
   // Number of error records.  
   ULONG nRecs;  
   ULONG nRec;  
  
   // Basic error information from GetBasicErrorInfo.  
   ERRORINFO errorinfo;  
  
   // IErrorInfo values.  
   BSTR bstrDescription;  
   BSTR bstrSource;  
  
   // ISQLErrorInfo parameters.  
   BSTR bstrSQLSTATE;  
   LONG lNativeError;  
  
   // ISQLServerErrorInfo parameter pointers.  
   SSERRORINFO * pSSErrorInfo = NULL;  
   OLECHAR * pSSErrorStrings = NULL;  
  
   // Hard-code an American English locale for the example.  
   DWORD MYLOCALEID = 0x0409;  
  
   has_sql_errors = 0;  
  
   // Only ask for error information if the interface supports it.  
   if (FAILED(pObjectWithError->QueryInterface(IID_ISupportErrorInfo, (void**) &pISupportErrorInfo)))     
      wprintf(L"SupportErrorErrorInfo interface not supported\n");  
   else if (FAILED(pISupportErrorInfo->InterfaceSupportsErrorInfo(IID_InterfaceWithError)))     
      wprintf(L"InterfaceWithError interface not supported\n");  
  
   // Do not test the return of GetErrorInfo. It can succeed and return  
   // a NULL pointer in pIErrorInfoAll. Simply test the pointer.  
   GetErrorInfo(0, &pIErrorInfoAll);  
  
   // Test to see if it's a valid OLE DB IErrorInfo interface exposing a list of records.  
   if (pIErrorInfoAll != NULL)  {  
      if (SUCCEEDED(pIErrorInfoAll->QueryInterface(IID_IErrorRecords, (void**) &pIErrorRecords))) {  
         pIErrorRecords->GetRecordCount(&nRecs);  
  
         // Within each record, retrieve information from each of the defined interfaces.  
         for (nRec = 0; nRec < nRecs; nRec++) {  
            ULONG errorno = nRecs - nRec - 1;  
            // From IErrorRecords, get the HRESULT and a reference to the ISQLErrorInfo interface.  
            pIErrorRecords->GetBasicErrorInfo(errorno, &errorinfo);  
            pIErrorRecords->GetCustomErrorObject(errorno,IID_ISQLErrorInfo, (IUnknown**) &pISQLErrorInfo);  
  
            // Display the HRESULT, then use the ISQLErrorInfo.  
            wprintf(L"HRESULT:\t%#X\n", errorinfo.hrError);  
  
            if (pISQLErrorInfo != NULL) {  
               pISQLErrorInfo->GetSQLInfo(&bstrSQLSTATE, &lNativeError);  
               // Display SQLSTATE and native error values.  
               wprintf(L"SQLSTATE:\t%s\nNative Error:\t%ld\n", bstrSQLSTATE, lNativeError);  
  
               // SysFree BSTR references.  
               SysFreeString(bstrSQLSTATE);  
  
               // Get the ISQLServerErrorInfo interface from  
               // ISQLErrorInfo before releasing the reference.  
               pISQLErrorInfo->QueryInterface(IID_ISQLServerErrorInfo, (void**) &pISQLServerErrorInfo);  
  
               pISQLErrorInfo->Release();  
            }  
  
            // Test to ensure the reference is valid, then get error information from ISQLServerErrorInfo.  
            if (pISQLServerErrorInfo != NULL) {  
               pISQLServerErrorInfo->GetErrorInfo(&pSSErrorInfo, &pSSErrorStrings);  
  
               // ISQLServerErrorInfo::GetErrorInfo succeeds even when it  
               // has nothing to return. Test the pointers before using.  
               if (pSSErrorInfo) {  
                  // Display the state and severity from the returned  
                  // information. The error message comes from  
                  // IErrorInfo::GetDescription.  
                  wprintf(L"Error state:\t%d\nSeverity:\t%d\n", pSSErrorInfo->bState, pSSErrorInfo->bClass);  
                  wprintf(L"Procedure:\t%s\nLine:\t%d\n", pSSErrorInfo->pwszProcedure, pSSErrorInfo->wLineNumber);  
  
                  has_sql_errors++;  
  
                  // IMalloc::Free needed to release references on returned values.  
                  pMalloc->Free(pSSErrorStrings);  
                  pMalloc->Free(pSSErrorInfo);  
               }  
  
               pISQLServerErrorInfo->Release();  
            }  
  
            if (SUCCEEDED(pIErrorRecords->GetErrorInfo(errno, MYLOCALEID, &pIErrorInfoRecord))) {  
               // Get the source and description (error message) from the record's IErrorInfo.  
               pIErrorInfoRecord->GetSource(&bstrSource);  
               pIErrorInfoRecord->GetDescription(&bstrDescription);  
  
               if (bstrSource != NULL) {  
                  wprintf(L"Source:\t\t%s\n", bstrSource);  
                  SysFreeString(bstrSource);  
               }  
  
               if (bstrDescription != NULL) {  
                  wprintf(L"Error message:\t%s\n", bstrDescription);  
                  SysFreeString(bstrDescription);  
               }  
  
               pIErrorInfoRecord->Release();  
            }  
         }  
  
         pIErrorRecords->Release();  
      }  
      else {  
         // IErrorInfo is valid; get the source and  
         // description to see what it is.  
         pIErrorInfoAll->GetSource(&bstrSource);  
         pIErrorInfoAll->GetDescription(&bstrDescription);  
  
         if (bstrSource != NULL) {  
            wprintf(L"Source:\t\t%s\n", bstrSource);  
            SysFreeString(bstrSource);  
         }  
  
         if (bstrDescription != NULL) {  
            wprintf(L"Error message:\t%s\n", bstrDescription);  
            SysFreeString(bstrDescription);  
         }  
      }  
  
      pIErrorInfoAll->Release();  
   }  
   else  
      wprintf(L"GetErrorInfo failed.\n");  
  
   if (pISupportErrorInfo != NULL)  
      pISupportErrorInfo->Release();  
}  
```  
  
  
