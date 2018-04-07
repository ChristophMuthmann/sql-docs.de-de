---
title: Massenkopieren von Daten mithilfe von IRowsetFastLoad (OLE DB) | Microsoft Docs
description: Massenkopieren von Daten in eine SQL Server Tabelle mithilfe von IRowsetFastLoad-Schnittstelle von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [OLE DB], text data
- bulk copy [OLE DB]
- bulk copy [OLE DB], data files
- bulk copy [OLE DB], about bulk copy
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc3476252a2142cd84dea7c96c89aed1c97c7bbd
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="bulk-copy-data-using-irowsetfastload-ole-db"></a>Massenkopieren von Daten mithilfe von IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Beispiel wird die Verwendung von IRowsetFastLoad für das Massenkopieren von Datensätzen in eine Tabelle gezeigt.  
  
 Der Consumer benachrichtigt den OLE DB-Treiber für SQL Server über die Anforderung zum Massenkopieren, indem der OLE DB-Treiber für SQL Server-Treiber-spezifische Eigenschaft SSPROP_ENABLEFASTLOAD auf VARIANT_TRUE festlegen. Mit der Eigenschaft für die Datenquelle festgelegt wurde erstellt der Consumer einen OLE DB-Treiber für SQL Server-Sitzung an. Die neue Sitzung lässt den Consumerzugriff auf **IRowsetFastLoad**.  
  
 Ein vollständiges Beispiel zur Verfügung steht, die veranschaulicht die Verwendung der **IRowsetFastLoad** zum Massenkopieren der Datensätze in einer Tabelle. In diesem Beispiel werden der Tabelle 10 Datensätze hinzugefügt **IRFLTable**. Sie müssen zum Erstellen der Tabelle **IRFLTable** in der Datenbank.  
  
 Dieses Beispiel erfordert die AdventureWorks-Beispieldatenbank, die Sie von der Homepage [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) herunterladen können.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn die Windows-Authentifizierung nicht verfügbar ist, fordern Sie die Benutzer auf, ihre Anmeldeinformationen zur Laufzeit einzugeben. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Sie die Anmeldeinformationen permanent speichern müssen, verschlüsseln Sie sie mit der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=64532).  
  
### <a name="to-bulk-copy-data-into-a-sql-server-table"></a>So massenkopieren Sie Daten in eine SQL Server-Tabelle  
  
1.  Stellen Sie eine Verbindung mit der Datenquelle her.  
  
2.  Der OLE DB-Treiber für SQL Server-Treiber-spezifische Datenquelleneigenschaft SSPROP_ENABLEFASTLOAD auf VARIANT_TRUE festgelegt. Diese Eigenschaft auf VARIANT_TRUE festgelegt ist, lässt die neu erstellte Sitzung den Consumerzugriff auf **IRowsetFastLoad**.  
  
3.  Erstellen einer Sitzung anfordert der **IOpenRowset** Schnittstelle.  
  
4.  Rufen Sie **IOpenRowset:: OPENROWSET** zum Öffnen eines Rowsets, die alle Zeilen aus der Tabelle enthält (in der Daten ist mit der Massenkopiervorgang kopiert werden soll).  
  
5.  Führen Sie die notwendigen Bindungen und erstellen Sie einen Accessor mithilfe **IAccessor:: CreateAccessor**.  
  
6.  Richten Sie den Arbeitsspeicherpuffer ein, aus dem die Daten in die Tabelle kopiert werden.  
  
7.  Rufen Sie **IRowsetFastLoad:: InsertRow** zum Massenkopieren von Daten in der Tabelle.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel werden der Tabelle IRFLTable 10 Datensätze hinzugefügt. Sie müssen die Tabelle IRFLTable in der Datenbank erstellen. Dieses Beispiel wird nicht auf IA64-basierten Systemen unterstützt.  
  
 Führen Sie das erste Codelisting ([!INCLUDE[tsql](../../../includes/tsql-md.md)]) aus, um die von der Anwendung verwendete Tabelle zu erstellen.  
  
 Kompilieren Sie mit ole32.lib und oleaut32.lib, und führen Sie das folgende C++-Codelisting aus. Diese Anwendung stellt eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Standardinstanz des Computers her. Bei einigen Windows-Betriebssystemen müssen Sie (localhost) oder (local) in den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz ändern. Um eine Verbindung mit einer benannten Instanz herzustellen, ändern Sie die Verbindungszeichenfolge von l"(Local)" "zu l"(Local)"\\\name", wobei der Name der benannten Instanz ist. Standardmäßig wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express in einer benannten Instanz installiert. Stellen Sie sicher, dass die INCLUDE-Umgebungsvariable das Verzeichnis einschließt, das msoledbsql.h enthält.  
  
 Führen Sie das dritte Codelisting ([!INCLUDE[tsql](../../../includes/tsql-md.md)]) aus, um die von der Anwendung verwendete Tabelle zu löschen.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'IRFLTable')  
     DROP TABLE IRFLTable  
GO  
  
CREATE TABLE IRFLTable (col_vchar varchar(30))  
```  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define DBINITCONSTANTS  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <oledb.h>  
#include <oledberr.h>  
#include <stdio.h>  
#include <stddef.h>   // for offsetof  
#include <msoledbsql.h>  
  
// @type UWORD    | 2 byte unsigned integer.  
typedef unsigned short UWORD;  
  
// @type SDWORD   | 4 byte signed integer.  
typedef signed long SDWORD;  
  
WCHAR g_wszTable[] = L"IRFLTable";  
WCHAR g_strTestLOC[100] = L"localhost";  
WCHAR g_strTestDBName[] = L"AdventureWorks";  
const UWORD g_cOPTION = 4;  
const UWORD MAXPROPERTIES = 5;  
const ULONG DEFAULT_CBMAXLENGTH = 20;  
IMalloc* g_pIMalloc = NULL;  
IDBInitialize* g_pIDBInitialize = NULL;  
  
// Given an ICommand pointer, properties, and query, a rowsetpointer is returned.  
HRESULT CreateSessionCommand( DBPROPSET* rgPropertySets, ULONG ulcPropCount, CLSID clsidProv );  
  
// Use to set properties and execute a given query.  
HRESULT ExecuteQuery ( IDBCreateCommand* pIDBCreateCommand,  
                       WCHAR* pwszQuery,  
                       DBPROPSET* rgPropertySets,  
                       ULONG ulcPropCount,   
                       LONG* pcRowsAffected,  
                       IRowset** ppIRowset,  
                       BOOL fSuccessOnly = TRUE );  
  
// Use to set up options for call to IDBInitialize::Initialize.  
void SetupOption ( DBPROPID PropID, WCHAR *wszVal, DBPROP * pDBProp );  
  
// Sets fastload property on/off for session.  
HRESULT SetFastLoadProperty(BOOL fSet);  
  
// IRowsetFastLoad inserting data.  
HRESULT FastLoadData();  
  
// How to lay out each column in memory.  
struct COLUMNDATA {  
   DBLENGTH dwLength;   // Length of data (not space allocated).  
   DWORD dwStatus;   // Status of column.  
   BYTE bData[1];   // Store data here as a variant.  
};  
  
#define COLUMN_ALIGNVAL 8  
  
#define ROUND_UP(Size, Amount)(((DWORD)(Size) + ((Amount)-1)) & ~((Amount)-1))  
  
int main() {  
   HRESULT hr = NOERROR;  
   HRESULT hr2 = NOERROR;  
  
   // OLE initialized?  
   BOOL fInitialized = FALSE;  
  
   // One property set for initializing.  
   DBPROPSET rgPropertySets[1];  
  
   // Properties within above property set.  
   DBPROP rgDBProperties[g_cOPTION];   
  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
   IRowset* pIRowset = NULL;  
   DBPROPSET* rgProperties = NULL;  
   IAccessor* pIAccessor = NULL;  
  
   // Basic initialization.  
   if ( FAILED(CoInitialize(NULL)) )  
      goto cleanup;  
   else  
      fInitialized = TRUE;  
  
   hr = CoGetMalloc(MEMCTX_TASK, &g_pIMalloc);  
   if ((!g_pIMalloc) || FAILED(hr))  
      goto cleanup;  
  
   // Set up property set for call to IDBInitialize in CreateSessionCommand.  
   rgPropertySets[0].rgProperties = rgDBProperties;  
   rgPropertySets[0].cProperties = g_cOPTION;  
   rgPropertySets[0].guidPropertySet = DBPROPSET_DBINIT;  
  
   SetupOption(DBPROP_INIT_CATALOG, g_strTestDBName, &rgDBProperties[0]);  
  
   SetupOption(DBPROP_AUTH_INTEGRATED, L"SSPI", &rgDBProperties[1]);  
  
   SetupOption(DBPROP_INIT_DATASOURCE, g_strTestLOC, &rgDBProperties[3]);  
  
   if (!SUCCEEDED( hr = CreateSessionCommand(rgPropertySets, 1, CLSID_MSOLEDBSQL)))  
      goto cleanup;  
  
   // Get IRowsetFastLoad and insert data into IRFLTable.  
   if (FAILED(hr = FastLoadData()))  
      goto cleanup;  
  
cleanup:  
   // Release memory.  
   if (rgProperties && rgProperties->rgProperties)  
      delete [](rgProperties->rgProperties);  
   if (rgProperties)  
      delete []rgProperties;  
   if (pIDBCreateCommand)  
      pIDBCreateCommand->Release();  
  
   if (pIAccessor)  
      pIAccessor->Release();  
  
   if (pIRowset)  
      pIRowset->Release();  
   if (g_pIMalloc)  
      g_pIMalloc->Release();  
  
   if (g_pIDBInitialize) {      
      hr2 = g_pIDBInitialize->Uninitialize();  
      if (FAILED(hr2))  
         printf("Uninitialize failed\n");  
   }  
  
   if (fInitialized)  
      CoUninitialize();  
  
   if (SUCCEEDED(hr))  
      printf("Test completed successfully.\n\n");  
   else  
      printf("Test failed.\n\n");  
}  
  
HRESULT FastLoadData() {  
   HRESULT hr = E_FAIL;  
   HRESULT hr2 = E_FAIL;  
   DBID TableID;  
  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IOpenRowset* pIOpenRowsetFL = NULL;  
   IRowsetFastLoad* pIFastLoad = NULL;  
  
   IAccessor* pIAccessor = NULL;  
   HACCESSOR hAccessor = 0;  
   DBBINDSTATUS oneStatus = 0;  
  
   DBBINDING oneBinding;  
   ULONG ulOffset = 0;  
   TableID.uName.pwszName = NULL;  
   LONG i = 0;  
   void* pData = NULL;  
   COLUMNDATA* pcolData = NULL;  
  
   TableID.eKind = DBKIND_NAME;  
   // if ( !(TableID.uName.pwszName = new WCHAR[wcslen(g_wszTable) + 2]) )  
   LPOLESTR x = TableID.uName.pwszName = new WCHAR[wcslen(g_wszTable) + 2];  
   if (!x)  
      return E_FAIL;  
   wcsncpy_s(TableID.uName.pwszName, wcslen(g_wszTable) + 2, g_wszTable, wcslen(g_wszTable)+1);  
   TableID.uName.pwszName[wcslen(g_wszTable)+1] = (WCHAR) NULL;  
  
   // Get the fastload pointer.  
   if (FAILED(hr = SetFastLoadProperty(TRUE)))  
      goto cleanup;  
  
   if ( FAILED( hr =   
      g_pIDBInitialize->QueryInterface( IID_IDBCreateSession, (void **) &pIDBCreateSession )))  
      goto cleanup;  
  
   if ( FAILED( hr =   
      pIDBCreateSession->CreateSession( NULL, IID_IOpenRowset, (IUnknown **) &pIOpenRowsetFL )))  
      goto cleanup;  
  
   // Get IRowsetFastLoad initialized to use the test table.  
   if (FAILED(hr =   
      pIOpenRowsetFL->OpenRowset(NULL,   
                                 &TableID,   
                                 NULL,   
                                 IID_IRowsetFastLoad,   
                                 0,   
                                 NULL,   
                                 (LPUNKNOWN *)&pIFastLoad)))  
      goto cleanup;  
  
   // Set up custom bindings.  
   oneBinding.dwPart = DBPART_VALUE | DBPART_LENGTH | DBPART_STATUS;  
   oneBinding.iOrdinal = 1;  
   oneBinding.pTypeInfo = NULL;  
   oneBinding.obValue = ulOffset + offsetof(COLUMNDATA,bData);  
   oneBinding.obLength = ulOffset + offsetof(COLUMNDATA,dwLength);  
   oneBinding.obStatus = ulOffset + offsetof(COLUMNDATA,dwStatus);  
   oneBinding.cbMaxLen = 30;   // Size of varchar column.  
   oneBinding.pTypeInfo = NULL;  
   oneBinding.pObject = NULL;  
   oneBinding.pBindExt = NULL;  
   oneBinding.dwFlags = 0;  
   oneBinding.eParamIO = DBPARAMIO_NOTPARAM;  
   oneBinding.dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
   oneBinding.bPrecision= 0;     
   oneBinding.bScale = 0;    
   oneBinding.wType = DBTYPE_STR;    
   ulOffset = oneBinding.cbMaxLen + offsetof(COLUMNDATA, bData);  
   ulOffset = ROUND_UP( ulOffset, COLUMN_ALIGNVAL );  
  
   if ( FAILED( hr =   
      pIFastLoad->QueryInterface(IID_IAccessor, (void **) &pIAccessor)))   
      return hr;  
  
   if (FAILED(hr = pIAccessor->CreateAccessor( DBACCESSOR_ROWDATA,   
                                               1,   
                                               &oneBinding,   
                                               ulOffset,   
                                               &hAccessor,   
                                               &oneStatus)))  
      return hr;  
  
   // Set up memory buffer.  
   pData = new BYTE[40];  
   if (!(pData /* = new BYTE[40]*/ )) {  
      hr = E_FAIL;  
      goto cleanup;  
   }  
  
   pcolData = (COLUMNDATA*)pData;  
   pcolData->dwLength = (SDWORD)strlen("Show the data") + 1;  
   pcolData->dwStatus = 0;  
   memcpy(&(pcolData->bData), "Show the data", strlen("Show the data") + 1);  
  
   for ( i = 0 ; i < 10 ; i++ )  
      if (FAILED(hr = pIFastLoad->InsertRow(hAccessor, pData)))  
         goto cleanup;  
  
   if (FAILED(hr = pIFastLoad->Commit(TRUE)))  
      printf("Error on IRFL::Commit\n");  
  
cleanup:  
   if (FAILED(hr2 = SetFastLoadProperty(FALSE)))  
      printf("SetFastLoadProperty(FALSE) failed with %x", hr2);  
  
   if (pIAccessor && hAccessor)  
      if (FAILED(pIAccessor->ReleaseAccessor(hAccessor, NULL)))  
         hr = E_FAIL;  
  
   if (pIAccessor)  
      pIAccessor->Release();  
  
   if (pIFastLoad)  
      pIFastLoad->Release();  
  
   if (pIOpenRowsetFL)  
      pIOpenRowsetFL->Release();  
  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
  
   if (TableID.uName.pwszName)  
      delete []TableID.uName.pwszName;  
  
   return hr;  
}  
  
HRESULT SetFastLoadProperty(BOOL fSet) {  
   HRESULT hr = S_OK;  
   IDBProperties* pIDBProps = NULL;  
   DBPROP rgProps[1];  
   DBPROPSET PropSet;  
  
   VariantInit(&rgProps[0].vValue);  
  
   rgProps[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgProps[0].colid = DB_NULLID;  
   rgProps[0].vValue.vt = VT_BOOL;  
   rgProps[0].dwPropertyID = SSPROP_ENABLEFASTLOAD;  
  
   if (fSet == TRUE)  
      rgProps[0].vValue.boolVal = VARIANT_TRUE;  
   else  
      rgProps[0].vValue.boolVal = VARIANT_FALSE;  
  
   PropSet.rgProperties = rgProps;  
   PropSet.cProperties = 1;  
   PropSet.guidPropertySet = DBPROPSET_SQLSERVERDATASOURCE;  
  
   if (SUCCEEDED(hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (LPVOID *)&pIDBProps)))  
      hr = pIDBProps->SetProperties(1, &PropSet);  
  
   VariantClear(&rgProps[0].vValue);   
  
   if (pIDBProps)  
      pIDBProps->Release();  
  
   return hr;  
}  
  
HRESULT CreateSessionCommand( DBPROPSET* rgPropertySets,// @parm [in] property sets  
                              ULONG ulcPropCount,   // @parm [in] count of prop sets.  
                              CLSID clsidProv) {  // @parm [in] Provider CLSID.  
  
   HRESULT hr = NOERROR;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBProperties* pIDBProperties = NULL;  
   UWORD i = 0, j = 0;   // indexes.  
  
   if (ulcPropCount && !rgPropertySets) {  
      hr = E_INVALIDARG;  
      return hr;  
   }  
  
   if (!SUCCEEDED(hr = CoCreateInstance(clsidProv,   
                                        NULL,CLSCTX_INPROC_SERVER,  
                                        IID_IDBInitialize,  
                                        (void **)&g_pIDBInitialize)))  
      goto CLEANUP;  
  
   if (!SUCCEEDED(hr = g_pIDBInitialize->QueryInterface( IID_IDBProperties,  
                                                         (void **)&pIDBProperties)))  
      goto CLEANUP;  
  
   if (!SUCCEEDED(hr = pIDBProperties->SetProperties(ulcPropCount, rgPropertySets)))  
      goto CLEANUP;  
  
   if (!SUCCEEDED(hr = g_pIDBInitialize->Initialize())) {  
      printf("Call to initialize failed.\n");  
      goto CLEANUP;  
   }  
  
CLEANUP:  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
  
   for (i = 0 ; i < ulcPropCount ; i++)  
      for (j = 0 ; j < rgPropertySets[i].cProperties ; j++)  
         VariantClear(&(rgPropertySets[i].rgProperties[j]).vValue);  
   return hr;  
}  
  
void SetupOption (DBPROPID PropID, WCHAR *wszVal, DBPROP * pDBProp ) {  
   pDBProp->dwPropertyID = PropID;  
   pDBProp->dwOptions = DBPROPOPTIONS_REQUIRED;  
   pDBProp->colid = DB_NULLID;  
   pDBProp->vValue.vt = VT_BSTR;  
   pDBProp->vValue.bstrVal = SysAllocStringLen(wszVal, wcslen(wszVal));  
}  
```  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'IRFLTable')  
     DROP TABLE IRFLTable  
GO  
```  
  
  
