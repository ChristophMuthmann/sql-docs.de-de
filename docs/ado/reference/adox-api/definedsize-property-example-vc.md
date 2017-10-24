---
title: DefinedSize-Eigenschaft (VC++-Beispiel) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- DefinedSize property [ADOX], VC++ example
ms.assetid: cc752ae4-58c4-4a7b-bfb2-0454e90fe2e7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3601e69350096d3fae0104e5d43c6d7e4abb5237
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="definedsize-property-example-vc"></a>DefinedSize-Eigenschaft (VC++-Beispiel)
Dieses Beispiel zeigt die [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) Eigenschaft eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md). Der Code wird die Größe der Spalte "FirstName" der definieren die **Mitarbeiter** Tabelle mit den *Northwind* Datenbank. Klicken Sie dann die Änderung in den Werten der FirstName [Feld](../../../ado/reference/ado-api/field-object.md) von einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) basierend auf der **Mitarbeiter** Tabelle wird angezeigt. Beachten Sie, dass standardmäßig das Feld FirstName mit Leerzeichen aufgefüllt wird, nachdem Sie neu definieren die **DefinedSize** Eigenschaft.  
  
```  
// BeginDefinedSizeCpp.cpp  
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
  
   // Define ADOX object pointers, initialize pointers. These are in the ADODB namespace.  
   _CatalogPtr m_pCatNorthwind = NULL;  
   _ColumnPtr m_pColFirstName = NULL;  
   _ColumnPtr m_pColNewFirstName = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_RecordsetPtr m_pRstEmployees = NULL;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
   _bstr_t aryFirstName[10];  
  
   try {  
      // Open a Recordset for the Employees table.  
      TESTHR(hr = m_pRstEmployees.CreateInstance(__uuidof(ADODB::Recordset)));  
      TESTHR(hr = m_pCatNorthwind.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pColNewFirstName.CreateInstance(__uuidof(Column)));  
  
      m_pRstEmployees->Open("Employees", strCnn,ADODB::adOpenKeyset, ADODB::adLockReadOnly, ADODB::adCmdTable);  
  
      long lngSize = m_pRstEmployees->RecordCount;  
      aryFirstName[lngSize];  
  
      // Open a catalog for the Northwind database, using same connection as rstEmployees.  
      m_pCatNorthwind->PutActiveConnection(m_pRstEmployees->GetActiveConnection());  
  
      // Loop through the recordset displaying the contents, of the FirstName field, the field's defined size,  
      // and its actual size.  Also store FirstName values in aryFirstName array.  
      m_pRstEmployees->MoveFirst();  
      printf("\nOriginal Defined Size and Actual Size");  
      int iCount = 0;  
      while (!(m_pRstEmployees->EndOfFile)) {  
         printf("\nEmployee Name:");  
         printf("%s ", (LPSTR)(_bstr_t)m_pRstEmployees->Fields->GetItem("FirstName")->Value);  
         printf("%s\n", (LPSTR)(_bstr_t)m_pRstEmployees->Fields->GetItem("LastName")->Value);  
         printf("  FirstName Defined size: %d\n", m_pRstEmployees->Fields->GetItem("FirstName")->DefinedSize);  
         printf("  FirstName Actual size: %d\n", m_pRstEmployees->Fields->GetItem("FirstName")->ActualSize);  
         aryFirstName[iCount] = (_bstr_t) m_pRstEmployees->Fields->GetItem("FirstName")->Value;  
         m_pRstEmployees->MoveNext();  
      }  
      m_pRstEmployees->Close();  
  
      // Redefine the DefinedSize of FirstName in the catalog.  
      m_pColFirstName = m_pCatNorthwind->Tables->GetItem("Employees")->Columns->GetItem("FirstName");  
      m_pColNewFirstName->Name = m_pColFirstName->Name;  
      m_pColNewFirstName->Type = m_pColFirstName->Type;  
      m_pColNewFirstName->DefinedSize = (m_pColFirstName->DefinedSize) + 1;  
  
      // Append new FirstName column to catalog.  
      m_pCatNorthwind->Tables->GetItem("Employees")->Columns->Delete(m_pColFirstName->Name);  
      m_pCatNorthwind->Tables->GetItem("Employees")->Columns->Append(_variant_t((IDispatch*)m_pColNewFirstName, true),   
         adVarWChar,  
         m_pColNewFirstName->DefinedSize);  
  
      // Open Employee table in Recordset for updating.  
      m_pRstEmployees->Open("Employees",  
         m_pCatNorthwind->GetActiveConnection(),   
         ADODB::adOpenKeyset,  
         ADODB::adLockOptimistic,  
         ADODB::adCmdTable);  
  
      // Loop through the recordset displaying the contents of the FirstName field,the field's defined size,  
      // and its actual size. Also restore FirstName values from aryFirstName.  
      m_pRstEmployees->MoveFirst();  
      printf("\n\nNew Defined Size and Actual Size");  
      iCount = 0;  
      while (!(m_pRstEmployees->EndOfFile)) {  
         m_pRstEmployees->Fields->GetItem("FirstName")->Value = aryFirstName[iCount];  
         printf("\nEmployee Name: ");  
         printf("%s ", (LPSTR) (_bstr_t)m_pRstEmployees->Fields->GetItem("FirstName")->Value);  
         printf("%s\n", (LPSTR)(_bstr_t)m_pRstEmployees->Fields->GetItem("LastName")->Value);  
         printf("  FirstName Defined size: %d\n", m_pRstEmployees->Fields->GetItem("FirstName")->DefinedSize);  
         printf("  FirstName Actual size: %d\n", m_pRstEmployees->Fields->GetItem("FirstName")->ActualSize);  
         m_pRstEmployees->MoveNext();  
      }  
      m_pRstEmployees->Close();  
  
      // Restore original FirstName column to catalog  
      m_pCatNorthwind->Tables->GetItem("Employees")->Columns->Delete(m_pColNewFirstName->Name);  
  
      m_pCatNorthwind->Tables->GetItem("Employees")->Columns->Append(_variant_t((IDispatch*)m_pColFirstName,   
         true),   
         adVarWChar,  
         m_pColFirstName->DefinedSize);  
  
      // Restore original FirstName values to Employees table.  
      m_pRstEmployees->Open("Employees",   
         m_pCatNorthwind->GetActiveConnection(),   
         ADODB::adOpenKeyset,   
         ADODB::adLockOptimistic,  
         ADODB::adCmdTable);  
  
      m_pRstEmployees->MoveFirst();  
      iCount = 0;  
      while ( !(m_pRstEmployees->EndOfFile) ) {  
         m_pRstEmployees->Fields->GetItem("FirstName")->Value = aryFirstName[iCount];  
         m_pRstEmployees->MoveNext();  
         iCount++;  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in DefinedSizeX...." << endl;  
   }  
  
   if (m_pRstEmployees)  
      if (m_pRstEmployees->State == 1)  
         m_pRstEmployees->Close();  
  
   m_pCatNorthwind = NULL;  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Column-Objekt (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [DefinedSize-Eigenschaft (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)

