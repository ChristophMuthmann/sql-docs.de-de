---
title: Abrufen von Fehlerinformationen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- retrieving error information
- errors [OLE DB], examples
- OLE DB error handling, retrieving information
- errors [OLE DB], retrieving information
- OLE DB error handling, examples
ms.assetid: 687b3c27-1a00-4122-8276-ea0f8fed895a
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 94af5d04b4ef10c37753bd37dc1e9c848129e102
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-error-information"></a>Abrufen von Fehlerinformationen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Beispiel enthält die Informationen aus den verschiedenen fehlerschnittstellen verfügbar gemacht werden, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.  
  
```  
// DumpErrorInfo queries SQLOLEDB error interfaces, retrieving available  
// status or error information.  
void DumpErrorInfo  
    (  
    IUnknown* pObjectWithError,  
    REFIID IID_InterfaceWithError  
    )  
    {  
  
    // Interfaces used in the example.  
    IErrorInfo*             pIErrorInfoAll          = NULL;  
    IErrorInfo*             pIErrorInfoRecord       = NULL;  
    IErrorRecords*          pIErrorRecords          = NULL;  
    ISupportErrorInfo*      pISupportErrorInfo      = NULL;  
    ISQLErrorInfo*          pISQLErrorInfo          = NULL;  
    ISQLServerErrorInfo*    pISQLServerErrorInfo    = NULL;  
  
    // Number of error records.  
    ULONG                   nRecs;  
    ULONG                   nRec;  
  
    // Basic error information from GetBasicErrorInfo.  
    ERRORINFO               errorinfo;  
  
    // IErrorInfo values.  
    BSTR                    bstrDescription;  
    BSTR                    bstrSource;  
  
    // ISQLErrorInfo parameters.  
    BSTR                    bstrSQLSTATE;  
    LONG                    lNativeError;  
  
    // ISQLServerErrorInfo parameter pointers.  
    SSERRORINFO*            pSSErrorInfo = NULL;  
    OLECHAR*                pSSErrorStrings = NULL;  
  
    // Hard-code an American English locale for the example.  
    DWORD                   MYLOCALEID = 0x0409;  
  
    // Only ask for error information if the interface supports  
    // it.  
   if (FAILED(pObjectWithError->QueryInterface(IID_ISupportErrorInfo,  
        (void**) &pISupportErrorInfo)))  
       {  
        wprintf_s(L"SupportErrorErrorInfo interface not supported");  
        return;  
        }  
   if (FAILED(pISupportErrorInfo->  
        InterfaceSupportsErrorInfo(IID_InterfaceWithError)))  
        {  
        wprintf_s(L"InterfaceWithError interface not supported");  
        return;  
        }  
  
    // Do not test the return of GetErrorInfo. It can succeed and return  
    // a NULL pointer in pIErrorInfoAll. Simply test the pointer.  
    GetErrorInfo(0, &pIErrorInfoAll);  
  
    if (pIErrorInfoAll != NULL)  
        {  
        // Test to see if it's a valid OLE DB IErrorInfo interface   
        // exposing a list of records.  
        if (SUCCEEDED(pIErrorInfoAll->QueryInterface(IID_IErrorRecords,  
            (void**) &pIErrorRecords)))  
            {  
            pIErrorRecords->GetRecordCount(&nRecs);  
  
            // Within each record, retrieve information from each  
            // of the defined interfaces.  
            for (nRec = 0; nRec < nRecs; nRec++)  
                {  
                // From IErrorRecords, get the HRESULT and a reference  
                // to the ISQLErrorInfo interface.  
                pIErrorRecords->GetBasicErrorInfo(nRec, &errorinfo);  
                pIErrorRecords->GetCustomErrorObject(nRec,  
                    IID_ISQLErrorInfo, (IUnknown**) &pISQLErrorInfo);  
  
                // Display the HRESULT, then use the ISQLErrorInfo.  
                wprintf_s(L"HRESULT:\t%#X\n", errorinfo.hrError);  
  
                if (pISQLErrorInfo != NULL)  
                    {  
                    pISQLErrorInfo->GetSQLInfo(&bstrSQLSTATE,   
                        &lNativeError);  
  
                    // Display the SQLSTATE and native error values.  
                    wprintf_s(L"SQLSTATE:\t%s\nNative Error:\t%ld\n",  
                        bstrSQLSTATE, lNativeError);  
  
                    // SysFree BSTR references.  
                    SysFreeString(bstrSQLSTATE);  
  
                    // Get the ISQLServerErrorInfo interface from  
                    // ISQLErrorInfo before releasing the reference.  
                    pISQLErrorInfo->QueryInterface(  
                        IID_ISQLServerErrorInfo,  
                        (void**) &pISQLServerErrorInfo);  
  
                    pISQLErrorInfo->Release();  
                    }  
  
                // Test to ensure the reference is valid, then  
                // get error information from ISQLServerErrorInfo.  
                if (pISQLServerErrorInfo != NULL)  
                    {  
                    pISQLServerErrorInfo->GetErrorInfo(&pSSErrorInfo,  
                        &pSSErrorStrings);  
  
                    // ISQLServerErrorInfo::GetErrorInfo succeeds  
                    // even when it has nothing to return. Test the  
                    // pointers before using.  
                    if (pSSErrorInfo)  
                        {  
                        // Display the state and severity from the  
                        // returned information. The error message comes  
                        // from IErrorInfo::GetDescription.  
                        wprintf_s(L"Error state:\t%d\nSeverity:\t%d\n",  
                                pSSErrorInfo->bState,  
                                pSSErrorInfo->bClass);  
  
                        // IMalloc::Free needed to release references  
                        // on returned values. For the example, assume  
                        // the g_pIMalloc pointer is valid.  
                        g_pIMalloc->Free(pSSErrorStrings);  
                        g_pIMalloc->Free(pSSErrorInfo);  
                        }  
  
                    pISQLServerErrorInfo->Release();  
                    }  
  
                if (SUCCEEDED(pIErrorRecords->GetErrorInfo(nRec,  
                    MYLOCALEID, &pIErrorInfoRecord)))  
                    {  
                    // Get the source and description (error message)  
                    // from the record's IErrorInfo.  
                    pIErrorInfoRecord->GetSource(&bstrSource);  
                    pIErrorInfoRecord->GetDescription(&bstrDescription);  
  
                    if (bstrSource != NULL)  
                        {  
                        wprintf_s(L"Source:\t\t%s\n", bstrSource);  
                        SysFreeString(bstrSource);  
                        }  
                    if (bstrDescription != NULL)  
                        {  
                        wprintf_s(L"Error message:\t%s\n",  
                            bstrDescription);  
                        SysFreeString(bstrDescription);  
                        }  
  
                    pIErrorInfoRecord->Release();  
                    }  
                }  
  
            pIErrorRecords->Release();  
            }  
        else  
            {  
            // IErrorInfo is valid; get the source and  
            // description to see what it is.  
            pIErrorInfoAll->GetSource(&bstrSource);  
            pIErrorInfoAll->GetDescription(&bstrDescription);  
  
            if (bstrSource != NULL)  
                {  
                wprintf_s(L"Source:\t\t%s\n", bstrSource);  
                SysFreeString(bstrSource);  
                }  
            if (bstrDescription != NULL)  
                {  
                wprintf_s(L"Error message:\t%s\n", bstrDescription);  
                SysFreeString(bstrDescription);  
                }  
            }  
  
        pIErrorInfoAll->Release();  
        }  
    else  
        {  
        wprintf_s(L"GetErrorInfo failed.");  
        }  
  
    pISupportErrorInfo->Release();  
  
    return;  
    }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
