---
title: NumericScale und Genauigkeit Eigenschaften der Spalte (VC++-Beispiel) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Precision property [ADOX], VC++ example
- NumericScale property [ADOX], VC++ example
ms.assetid: 69653366-ebd7-4ff6-a654-761772223b0c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca11ba4800d0516b9a87c91fca4b4dd58f7ea42c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="numericscale-and-precision-properties-of-the-column-object-example-vc"></a>NumericScale und Genauigkeit Eigenschaften der Spalte Objekt (VC++-Beispiel)
In diesem Beispiel wird veranschaulicht, die [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) und [Genauigkeit](../../../ado/reference/adox-api/precision-property-adox.md) Eigenschaften der [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekt. Dieser Code zeigt an, deren Wert für die **Bestelldetails** Tabelle mit den *Northwind* Datenbank.  
  
```  
// BeginNumericScalePrecCpp.cpp  
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
  
   // Define and initialize ADOX object pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _ColumnPtr m_pColumn = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Declare string variables  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source='c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
  
      // Connect the catalog.  
      m_pCnn->Open (strCnn, "", "", NULL);  
  
      m_pCatalog->PutActiveConnection(variant_t((IDispatch *)m_pCnn));  
  
      // Retrieve the Order Details table  
      m_pTable = m_pCatalog->Tables->GetItem("Order Details");  
  
      // Display numeric scale and precision of small integer fields.  
      _variant_t vIndex;  
      for ( long lIndex = 0 ; lIndex < m_pTable->Columns->Count ; lIndex++ ) {  
         vIndex = lIndex ;  
         m_pColumn = m_pTable->Columns->GetItem(vIndex);  
         if (m_pColumn->Type == adSmallInt) {  
            cout << "Column: " << m_pColumn->GetName() << endl;  
            cout << "Numeric scale: " << (_bstr_t) m_pColumn->GetNumericScale() << endl;  
            cout << "Precision: " << m_pColumn->GetPrecision() << endl;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in NumericScalePrecX...." << endl;  
   }  
   ::CoUninitialize();  
}  
```
