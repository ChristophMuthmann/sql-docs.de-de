---
title: Erstellen der Beispiel-Methode (VC++) | Microsoft Docs
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
- Create method [ADOX], VC++ example
ms.assetid: 57fcb0eb-5d40-4ad4-996d-380732de8a3d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d5621e9a74d063285306e9ab069557eb339884
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-method-example-vc"></a>Erstellen Sie die (VC++-Methodenbeispiel)
Der folgende Code veranschaulicht das Erstellen einer neuen Microsoft Jet-Datenbank mit der [erstellen](../../../ado/reference/adox-api/create-method-adox.md) Methode.  
  
```  
// BeginCreateDatabaseCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#define TESTHR(x) if FAILED(x) _com_issue_error(x);  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
void CreateDatabaseX(void);  
  
int main() {  
   HRESULT hr = S_OK;  
  
   hr = ::CoInitialize(NULL);  
   if (SUCCEEDED(hr)) {  
      CreateDatabaseX();  
      ::CoUninitialize();  
   }  
}  
  
// Create a new Jet database with the Create method  
void CreateDatabaseX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Set ActiveConnection of Catalog to this string  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = c:\\new.mdb");  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->Create(strcnn);  
      printf("Database 'c:\\new.mdb' is created.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CreateDatabaseX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Create-Methode (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
