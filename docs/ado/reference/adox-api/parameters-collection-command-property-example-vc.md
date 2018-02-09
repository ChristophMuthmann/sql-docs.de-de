---
title: Parameters-Auflistung, Befehlsbeispiel-Eigenschaft (VC++) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- Parameters collection [ADOX], VC++ example
- Command property [ADOX], VC++ example
ms.assetid: 8636fa08-b3db-4e9a-a918-585e76dd59c8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 674bf858215fc2d6f5b1c0384e368d2100ca1c25
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="parameters-collection-command-property-example-vc"></a>Parameters-Auflistung, Befehl-Eigenschaft (VC++-Beispiel)
Der folgende Code veranschaulicht, wie die [Befehl](../../../ado/reference/adox-api/command-property-adox.md) Eigenschaft mit dem [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Parameterinformationen für die Prozedur abzurufenden Objekts.  
  
```  
// BeginProcedureParametersCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ProcedureParametersX(void);  
  
int main() {  
    if ( FAILED(::CoInitialize(NULL)) )  
        return -1;  
  
    ProcedureParametersX();  
  
    ::CoUninitialize();  
}  
  
void ProcedureParametersX() {  
    HRESULT hr = S_OK;  
  
    // Define and initialize ADOX object pointers. These are in ADODB namespace.  
    _CatalogPtr m_pCatalog = NULL;  
  
    //Define ADODB object pointers.  
    ADODB::_ConnectionPtr m_pCnn = NULL;  
    ADODB::_CommandPtr m_pCommand = NULL;  
    ADODB::_ParameterPtr m_pParameter = NULL;  
  
    try {  
        TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
  
        // Open the Connection  
        m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source='c:\\Northwind.mdb';", "", "", NULL);  
  
        TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
        // Open the catalog  
        m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
        // Get the command object  
        m_pCommand = m_pCatalog->Procedures->GetItem("CustomerById")->GetCommand();  
  
        _variant_t vIndex;  
  
        // Retrieve Parameter information  
        m_pCommand->Parameters->Refresh();  
        for ( long lIndex = 0 ; lIndex < m_pCommand->Parameters->Count ; lIndex ++ ) {  
            vIndex = lIndex;  
            m_pParameter = m_pCommand->Parameters->GetItem(vIndex);  
            cout << m_pParameter->Name << ":" << m_pParameter->Type << "\n" << endl;  
        }  
    }  
    catch(_com_error &e) {  
        // Notify the user of errors if any.  
        _bstr_t bstrSource(e.Source());  
        _bstr_t bstrDescription(e.Description());  
  
        printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
    }  
    catch(...) {  
        cout << "Error occured in ProcedureParametersX...." << endl;  
    }  
}  
```
