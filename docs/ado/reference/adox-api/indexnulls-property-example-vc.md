---
title: IndexNulls-Eigenschaft (VC++-Beispiel) | Microsoft Docs
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
- IndexNulls property [ADOX], VC++ example
ms.assetid: ee407e03-4889-4a22-b031-ca542d637c96
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb57364ac272720ac82dceee65f195157e0b3e0e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="indexnulls-property-example-vc"></a>IndexNulls-Eigenschaft (VC++-Beispiel)
Dieses Beispiel zeigt die [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) Eigenschaft ein [Index](../../../ado/reference/adox-api/index-object-adox.md). Der Code erstellt einen neuen Index und legt den Wert des **IndexNulls** basierend auf Benutzereingaben. Anschließend wird die **Index** wird angefügt, um die **Mitarbeiter** [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) in der *Northwind* [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md). Die neue **Index** wird angewendet, um eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) basierend auf der **Mitarbeiter** Tabelle, und die **Recordset** wird geöffnet. Ein neuer Datensatz hinzugefügt wird die **Mitarbeiter** Tabelle mit einer **Null** Wert des indizierten Felds. Gibt an, ob diese neue Datensatz angezeigt wird, hängt davon ab, die Einstellung von der **IndexNulls** Eigenschaft.  
  
```  
// BeignIndexNullCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
#include "icrsint.h"  
using namespace std;  
  
// This class extracts LastName,Country,FirstName from Employees table  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
      // Column LastName is the 2nd field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szemp_LastName, sizeof(m_szemp_LastName), lemp_LastNameStatus, TRUE)  
  
      // Column Country is the 11th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(11, adVarChar, m_szemp_Country, sizeof(m_szemp_Country), lemp_CountryStatus, TRUE)  
  
      // Column Country is the 17th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(17, adVarChar, m_szemp_FirstName, sizeof(m_szemp_FirstName), lemp_FirstNameStatus, TRUE)  
      END_ADO_BINDING()  
  
public:  
   CHAR m_szemp_LastName[21];  
   ULONG lemp_LastNameStatus;  
   CHAR m_szemp_Country[16];  
   ULONG lemp_CountryStatus;  
   CHAR m_szemp_FirstName[11];  
   ULONG lemp_FirstNameStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void IndexNullsX(_bstr_t);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;   
  
   printf("\nShow records having indexed field value = NULL? (Y/N):");  
   // char input = getche();  
   // Let's pretend you said Yes  
   char input = 'Y';  
  
   if ( toupper(input) == 'Y' )  
      IndexNullsX("Allow");  
   else if ( toupper(input) == 'N' )  
      IndexNullsX("Ignore");  
   else  
      exit(0);  
  
   ::CoUninitialize();  
}  
  
void IndexNullsX(_bstr_t strSel) {  
   HRESULT hr = S_OK;  
  
   // Define and initialie ADOX object pointers. These are in the ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _IndexPtr m_pIndexNew = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
   ADODB::_RecordsetPtr m_pRstEmployees = NULL;  
  
   // Define other variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared  
   CEmployeeRs emprs;   // C++ Class Object  
  
   // Define string variable.  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pIndexNew.CreateInstance(__uuidof(Index)));  
      TESTHR(hr = m_pRstEmployees.CreateInstance(__uuidof(ADODB::Recordset)));  
  
      // Connect the catalog.  
      m_pCnn->Open(strCnn, "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      // Append Country column to new index.  
      m_pIndexNew->Columns->Append("Country", adVarWChar, 0);  
      m_pIndexNew->Name = "NewIndex";  
  
      // Set IndexNulls based on user input  
      if (strcmp((LPSTR)strSel, "Allow") == 0 )  
         m_pIndexNew->IndexNulls = adIndexNullsAllow;  
      else if (strcmp((LPSTR)strSel, "Ignore") == 0 )  
         m_pIndexNew->IndexNulls = adIndexNullsIgnore;  
  
      // Append new index to Employees table  
      m_pCatalog->Tables->GetItem("Employees")->Indexes->Append(_variant_t((IDispatch *)m_pIndexNew));  
      m_pRstEmployees->Index = m_pIndexNew->Name;  
      m_pRstEmployees->Open("Employees",   
         _variant_t((IDispatch *)m_pCnn),   
         ADODB::adOpenKeyset,   
         ADODB::adLockOptimistic,  
         ADODB::adCmdTableDirect);  
  
      // Add a new record to the Employees table.  
      m_pRstEmployees->AddNew();  
      m_pRstEmployees->Fields->GetItem("FirstName")->Value = (_bstr_t) "Gary";  
      m_pRstEmployees->Fields->GetItem("LastName")->Value = (_bstr_t) "Haarsager";  
      m_pRstEmployees->Update();  
  
      // Bookmark the newly added record.  
      _variant_t varBookmark = m_pRstEmployees->Bookmark;  
  
      // Use the new index to set the order of the records.  
      m_pRstEmployees->MoveFirst();  
      printf("\n\nIndex = %s,", (LPSTR) m_pRstEmployees->Index);  
      printf("IndexNulls = %d\n\n", m_pIndexNew->IndexNulls);  
      cout<<"Country            -        Name" << endl;  
  
      // Open an IADORecordBinding interface pointer for binding Recordset to a class  
      TESTHR(hr = m_pRstEmployees->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here   
      TESTHR(hr = picRs->BindToRecordset(&emprs));  
  
      // Enumerate the Recordset.The value of the IndexNulls property will determine if the newly  
      // added record appears in the output.  
      while ( !(m_pRstEmployees->EndOfFile) ) {  
         printf("%s    -    %s %s\n",  
            emprs.lemp_CountryStatus == adFldOK ? emprs.m_szemp_Country :"[Null]",  
            emprs.lemp_FirstNameStatus == adFldOK ? emprs.m_szemp_FirstName :"<NULL>",  
            emprs.lemp_LastNameStatus == adFldOK ? emprs.m_szemp_LastName :"<NULL>");  
  
         m_pRstEmployees->MoveNext();  
      }  
  
      // Delete new record because this is a demonstration.  
      m_pRstEmployees->Bookmark = varBookmark;  
      m_pRstEmployees->Delete(ADODB::adAffectCurrent);  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in include files...." << endl;  
   }  
  
   if (m_pRstEmployees)  
      if (m_pRstEmployees->State == 1) {  
         m_pRstEmployees->Close();  
         m_pRstEmployees = NULL;  
      }  
  
      // Delete new Index because this is a demonstration.  
      if (m_pCatalog)  
         m_pCatalog->Tables->GetItem("Employees")->Indexes->Delete(m_pIndexNew->Name);  
  
      if (m_pCnn)  
         if (m_pCnn->State == 1) {  
            m_pCnn->Close();  
            m_pCnn = NULL;  
         }  
  
         m_pCatalog = NULL;  
}  
```
