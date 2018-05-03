---
title: AbsolutePage "PageCount" und PageSize Eigenschaften (VC++-Beispiel) | Microsoft Docs
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
- PageCount property [ADO], VC++ example
- AbsolutePage property [ADO], VC++ example
- PageSize property [ADO], VC++ example
ms.assetid: 38ca4e1b-c109-4fba-b590-bdd6994f770e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 309fc83f73cb4413f19483932f450619b28df506
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="absolutepage-pagecount-and-pagesize-properties-example-vc"></a>AbsolutePage "PageCount" und PageSize Eigenschaften (VC++-Beispiel)
Dieses Beispiel verwendet die [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), ["PageCount"](../../../ado/reference/ado-api/pagecount-property-ado.md), und [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) Eigenschaften Anzeigenamen und Einstellungsdaten aus der ***Mitarbeiter*** Tabelle fünf Datensätzen zu einem Zeitpunkt.  
  
```  
// BeginAbsolutePageCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <stdio.h>  
#include <ole2.h>  
#include "conio.h"  
#include "icrsint.h"  
  
// This Class extracts only fname,lastname and hire_date  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
      // Column fname is the 2nd field in the table     
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szau_fname,   
      sizeof(m_szau_fname), lau_fnameStatus, FALSE)  
  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_szau_lname,   
      sizeof(m_szau_lname), lau_lnameStatus, TRUE)  
  
      ADO_VARIABLE_LENGTH_ENTRY2(8, adVarChar, m_szau_hiredate,   
      sizeof(m_szau_hiredate), lau_hiredateStatus, TRUE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR   m_szau_lname[41];  
   ULONG  lau_lnameStatus;  
   CHAR   m_szau_fname[41];  
   ULONG  lau_fnameStatus;  
   CHAR   m_szau_hiredate[40];  
   ULONG  lau_hiredateStatus;  
  
};  
  
// Function Declarations.  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void AbsolutePageX();  
void PrintProviderError(_ConnectionPtr pConnection);   
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   AbsolutePageX();  
   ::CoUninitialize();  
}  
  
void AbsolutePageX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _RecordsetPtr pRstEmployees = NULL;  
  
   // Define Other Variables.    Interface Pointer declared.(VC++ Extensions)  
   IADORecordBinding *picRs = NULL;  
   CEmployeeRs emprs;   // C++ class object   
   HRESULT hr = S_OK;  
   _bstr_t strMessage;  
  
   // Open a recordset using a Client Cursor for the Employee Table  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open a recordset.  
      TESTHR(hr = pRstEmployees.CreateInstance(__uuidof(Recordset)));  
  
      // Use client cursor to enable Absoluteposition property.  
      pRstEmployees->CursorLocation = adUseClient;  
  
      // Explicitly pass the default Cursor type  and LockType to the Recordset here   
      TESTHR(hr = pRstEmployees->Open("employee", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable));  
  
      // Open an IADORecordBinding interface pointer for Binding Recordset to a class      
      TESTHR(hr = pRstEmployees->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here      
      TESTHR(hr = picRs->BindToRecordset(&emprs));  
  
      // Display Names and hire dates, five records at a time  
      pRstEmployees->PageSize = 5;  
  
      int intPageCount = pRstEmployees->PageCount;  
  
      for (int intPage = 1 ; intPage <= intPageCount ; intPage++ ) {  
         pRstEmployees->put_AbsolutePage((enum PositionEnum)intPage);  
         strMessage = "";  
  
         for ( int intRecord = 1 ; intRecord <= pRstEmployees->PageSize ; intRecord++ ) {  
            printf("\t%s %s %.10s\n",   
               emprs.lau_fnameStatus == adFldOK ?   
               emprs.m_szau_fname : "<NULL>",  
               emprs.lau_lnameStatus == adFldOK ?   
               emprs.m_szau_lname : "<NULL>",  
               emprs.lau_hiredateStatus == adFldOK ?   
               emprs.m_szau_hiredate : "<NULL>");  
  
            pRstEmployees->MoveNext();  
  
            if (pRstEmployees->EndOfFile)  
               break;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _variant_t vtConnect = pRstEmployees->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         printf("Error:\n");  
         printf("Code = %08lx\n", e.Error());  
         printf("Message = %s\n", e.ErrorMessage());  
         printf("Source = %s\n", (LPCSTR) e.Source());  
         printf("Description = %s\n", (LPCSTR) e.Description());  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
   // Clean up objects before exit.  Release the IADORecordset Interface here  
   if (picRs)   
      picRs->Release();  
  
   if (pRstEmployees)  
      if (pRstEmployees->State == adStateOpen)  
         pRstEmployees->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      printf("Error:\n");  
      for ( long iError = 0 ; iError < nCount ; iError++) {  
         pErr = pConnection->Errors->GetItem(iError);  
         printf("\t Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 ["PageCount"-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Die Eigenschaft PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
