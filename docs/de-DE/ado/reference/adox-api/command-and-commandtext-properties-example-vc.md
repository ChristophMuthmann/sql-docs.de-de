---
title: Befehl "und" CommandText Eigenschaften (VC++-Beispiel) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CommandText property [ADOX], VC++ example
- Command property [ADOX], VC++ example
ms.assetid: 5a007b9a-be11-4fba-96db-6252993f97b8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb9f916a66e2183fd32be8d1d8659e81f68843d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="command-and-commandtext-properties-example-vc"></a>Befehl "und" CommandText Eigenschaften (VC++-Beispiel)
Der folgende Code veranschaulicht, wie die [Befehl](../../../ado/reference/adox-api/command-property-adox.md) Eigenschaft, um den Text einer Prozedur zu aktualisieren.  
  
```  
// BeginCommandTextCpp  
// This sample runs correctly only if procedure 'CustomerById' exists.  
  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ProcedureTextX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADOX namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define ADODB object pointers.  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
   ADODB::_CommandPtr m_pCommand = NULL;  
  
   try {  
      // Open the Connection  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      TESTHR(hr = m_pCommand.CreateInstance(__uuidof(ADODB::Command)));  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';", "", "", NULL);  
  
      // Open the catalog  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      // Get the Command  
      m_pCommand = m_pCatalog->Procedures->GetItem("CustomerById")->GetCommand();  
  
      // Update the CommandText  
      m_pCommand->PutCommandText("PARAMETERS [CustId] Text;select "  
         "CustomerId, CompanyName, ContactName "  
         "from Customers where CustomerId = [CustId]");  
      printf("CommandText is updated.\n");  
  
      // Update the Procedure  
      m_pCatalog->Procedures->GetItem("CustomerById")->PutCommand(_variant_t((IDispatch *)m_pCommand));  
      printf("Procedure 'CustomerById' is updated.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in ProcedureTextX...."<< endl;  
   }  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Eigenschaft (ADOX)](../../../ado/reference/adox-api/command-property-adox.md)
