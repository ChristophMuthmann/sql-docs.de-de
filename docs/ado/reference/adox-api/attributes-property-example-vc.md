---
title: Attribute-Eigenschaft (VC++-Beispiel) | Microsoft Docs
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
- Attributes property [ADOX], VC++ example
ms.assetid: 1057b57b-5ace-4830-9a20-562e88aeef86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfb2d50d571095e12e2923858197fe4f6b14ace5
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="attributes-property-example-vc"></a>Attribute-Eigenschaft (VC++-Beispiel)
Dieses Beispiel zeigt die [Attribute](../../../ado/reference/adox-api/attributes-property-adox.md) Eigenschaft eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md). Bei der Einstellung **eine** ermöglicht es dem Benutzer zum Festlegen des Werts von einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) [Feld](../../../ado/reference/ado-api/field-object.md) auf eine leere Zeichenfolge. In diesem Fall kann der Benutzer unterscheiden, zwischen einer, in dem Daten nicht bekannt ist, und ein Datensatz, in dem die Daten nicht gilt.  
  
```  
// Attributes_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
#include "icrsint.h"  
using namespace std;  
  
// class extracts LastName, FirstName, FaxPhone from Employees table  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
   // Column LastName is the 2nd field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(2,   
                              adVarChar,   
                              m_szemp_LastName,   
                              sizeof(m_szemp_LastName),   
                              lemp_LastNameStatus,   
                              TRUE)  
  
   // Column FirstName is the 17th field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(17,   
                              adVarChar,   
                              m_szemp_FirstName,   
                              sizeof(m_szemp_FirstName),   
                              lemp_FirstNameStatus,   
                              TRUE)  
  
   // Column FaxPhone is the 18th field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(18,   
                              adVarChar,   
                              m_szemp_Faxphone,   
                              sizeof(m_szemp_Faxphone),   
                              lemp_FaxphoneStatus,   
                              TRUE)  
  
END_ADO_BINDING()  
  
public:  
   CHAR m_szemp_LastName[21];  
   ULONG lemp_LastNameStatus;  
   CHAR m_szemp_FirstName[11];  
   ULONG lemp_FirstNameStatus;  
   CHAR m_szemp_Faxphone[25];  
   ULONG lemp_FaxphoneStatus;  
};  
  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
  
int main() {  
   if ( FAILED( ::CoInitialize(NULL) ) )  
      return -1;  
  
   HRESULT hr = S_OK;  
   char * token;  
  
   // Define ADOX object pointers, initialize pointers.  These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _ColumnPtr m_pColumn = NULL;  
   _TablePtr m_pTable = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
   ADODB::_RecordsetPtr m_pRstEmployees = NULL;  
  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared  
   CEmployeeRs emprs;   // C++ Class Object  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';");  
  
   try {  
      // Connect the catalog.  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof (ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pColumn.CreateInstance(__uuidof(Column)));  
      TESTHR(hr = m_pRstEmployees.CreateInstance(__uuidof(ADODB::Recordset)));  
  
      m_pCnn->Open(strcnn, "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *) m_pCnn));  
      m_pTable= m_pCatalog->Tables->GetItem("Employees");  
  
      // Create a new Field object and append it to the Fields  
      // collection of the Employees table.  
      m_pColumn->Name = "FaxPhone";  
      m_pColumn->Type = adVarWChar;  
      m_pColumn->DefinedSize = 24;  
      m_pColumn->Attributes = adColNullable;  
  
      m_pCatalog->Tables->GetItem("Employees")->Columns->Append(m_pColumn->Name, adVarWChar, 24);  
      // Append("FaxPhone", adVarWChar, 24);  
  
      // Open the Employees table for updating as a Recordset.  
      m_pRstEmployees->Open("Employees",   
         _variant_t((IDispatch *) m_pCnn),   
         ADODB::adOpenKeyset,   
         ADODB::adLockOptimistic,   
         ADODB::adCmdTable);  
  
      // Get user input.  
      printf("Enter fax number for : %s %s\n",   
         (LPSTR)(_bstr_t) m_pRstEmployees->Fields->GetItem("LastName")->Value,  
         (LPSTR) (_bstr_t) m_pRstEmployees->Fields->GetItem("FirstName")->Value);  
      printf("[? - unknown, X - has no fax] : \n");  
  
      // Skip user input routine, just supply a value.  
      char* strTemp = strtok_s("X", " \t", &token);  
      _variant_t vNull;  
      vNull.vt = VT_BSTR;  
      vNull.bstrVal = NULL;  
  
      if (strTemp != NULL) {  
         if (strcmp(strTemp, "?") == 0)  
            m_pRstEmployees->Fields->GetItem("FaxPhone")->PutValue(vNull);  
         else if( (strcmp(strTemp,"X") == 0) | (strcmp(strTemp,"x") == 0) )  
            m_pRstEmployees->Fields->GetItem("FaxPhone")->PutValue("");  
         else  
            m_pRstEmployees->Fields->GetItem("FaxPhone")->PutValue(strTemp);  
  
         m_pRstEmployees->Update();  
  
         // Open IADORecordBinding interface pointer for binding Recordset to a class  
         TESTHR(hr = m_pRstEmployees->QueryInterface(__uuidof(IADORecordBinding),(LPVOID*)&picRs));  
  
         // Bind the Recordset to a C++ class here  
         TESTHR(hr = picRs->BindToRecordset(&emprs));  
  
         // Print report.  
         printf("\nName - Fax number\n");  
         printf("%s %s ", emprs.lemp_LastNameStatus == adFldOK ?   
            emprs.m_szemp_LastName : "<NULL>",  
            emprs.lemp_FirstNameStatus == adFldOK ?   
            emprs.m_szemp_FirstName : "<NULL>");  
  
         if (emprs.lemp_FaxphoneStatus == adFldNull)  
            printf("- [Unknown]\n");  
         else if (strcmp((LPSTR)emprs.m_szemp_Faxphone, "") == 0)  
            printf("- [Has no fax]\n");  
         else  
            printf("- %s\n", emprs.m_szemp_Faxphone);  
      }  
  
      // Delete new field because this is a demonstration.    
      // m_pTable->Columns->Delete(m_pColumn->Name);  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in AttributesX...." << endl;  
   }  
  
   if (m_pRstEmployees)  
      if (m_pRstEmployees->State == 1)  
         m_pRstEmployees->Close();  
  
   // Delete new field because this is a demonstration.  
   if (m_pTable != NULL)  
      m_pTable->Columns->Delete(m_pColumn->Name);  
  
   if (m_pCnn)  
      if (m_pCnn->State == 1)  
         m_pCnn->Close();  
  
   // Release the IADORecordset Interface here  
   if (picRs)  
      picRs->Release();  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute-Eigenschaft (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md)   
 [Column-Objekt (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
