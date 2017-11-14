---
title: DeleteRule-Eigenschaft (VC++-Beispiel) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- DeleteRule property [ADOX], VC++ example
ms.assetid: 7a1def31-2b6f-4542-aac3-ec35b54c89ef
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41c740653886e95a8ee8cc949b5b2fe7190ddb85
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="deleterule-property-example-vc"></a>DeleteRule-Eigenschaft (VC++-Beispiel)
Dieses Beispiel zeigt die [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) Eigenschaft eine [Schlüssel](../../../ado/reference/adox-api/key-object-adox.md) Objekt. Der Code Fügt eine neue [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) und definiert dann einen neuen Primärschlüssel festlegen **DeleteRule** auf **AdRICascade**.  
  
```  
// BeginDeleteRuleCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _KeyPtr m_pKeyPrimary = NULL;  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTblNew = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
   try {  
      TESTHR(hr = m_pKeyPrimary.CreateInstance(__uuidof(Key)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pTblNew.CreateInstance(__uuidof(Table)));  
  
      // Connect the catalog.  
      m_pCatalog->PutActiveConnection(strcnn);  
  
      // Name new table.  
      m_pTblNew->Name = "NewTable";  
  
      // Append a numeric and a text field to new table.  
      m_pTblNew->Columns->Append("NumField", adInteger, 20);  
      m_pTblNew->Columns->Append("TextField", adVarWChar, 20);  
  
      // Append the new table.  
      m_pCatalog->Tables->Append(_variant_t((IDispatch*)m_pTblNew));  
      printf("Table 'NewTable' is added.\n");  
  
      // Define the Primary key.  
      m_pKeyPrimary->Name = "NumField";  
      m_pKeyPrimary->Type = adKeyPrimary;  
      m_pKeyPrimary->RelatedTable = "Customers";  
      m_pKeyPrimary->Columns->Append("NumField", adInteger,20);  
      m_pKeyPrimary->Columns->GetItem("NumField")->RelatedColumn = "CustomerId";  
      m_pKeyPrimary->DeleteRule = adRICascade;  
  
      // to pass an optional column parameter to Key's Apppend method  
      _variant_t vOptional;  
      vOptional.vt = VT_ERROR;  
      vOptional.scode = DISP_E_PARAMNOTFOUND;  
  
      // Append the primary key.  
      m_pCatalog->Tables->GetItem("NewTable")->Keys->Append( _variant_t((IDispatch*)m_pKeyPrimary),   
         adKeyPrimary,vOptional,   
         L"",   
         L"");  
  
      // Delete the table as this is a demonstration.  
      m_pCatalog->Tables->Delete(m_pTblNew->Name);  
      printf("Table 'NewTable' is deleted.\n");  
   }  
  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   catch(...) {  
      cout << "Error occured in include files...."<< endl;  
   }  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DeleteRule-Eigenschaft (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)   
 [Schlüsselobjekt (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)

