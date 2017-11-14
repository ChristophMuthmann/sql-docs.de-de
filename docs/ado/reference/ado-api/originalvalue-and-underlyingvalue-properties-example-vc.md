---
title: OriginalValue und OriginalValue Eigenschaften (VC++-Beispiel) | Microsoft Docs
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
- UnderlyingValue property [ADO], VC++ example
- OriginalValue property [ADO]
ms.assetid: c5762ad2-f43b-453d-b44a-9c70210eb00f
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e73d970163aba564c6ed199a2024511db7579a89
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="originalvalue-and-underlyingvalue-properties-example-vc"></a>OriginalValue und OriginalValue Eigenschaften (VC++-Beispiel)
Dieses Beispiel zeigt die [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) und [OriginalValue](../../../ado/reference/ado-api/underlyingvalue-property.md) Eigenschaften, die über eine Meldung angezeigt, wenn ein Datensatz Daten liegenden wurde geändert, während ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) BatchUpdate.  
  
## <a name="example"></a>Beispiel  
  
```  
// BeginOriginalValueCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// class extracts title_id and type from titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
   // Column title_id is the 1st field in the Recordset  
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szau_Title_id, sizeof(m_szau_Title_id), lau_Title_idStatus, FALSE)  
  
   // Column type is the 3rd field in the Recordset  
   ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szau_Type, sizeof(m_szau_Type), lau_TypeStatus, TRUE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title_id[7];  
   ULONG lau_Title_idStatus;  
   CHAR m_szau_Type[13];  
   ULONG lau_TypeStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void OriginalValueX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   OriginalValueX();  
   ::CoUninitialize();  
}  
  
void OriginalValueX() {  
   // Define ADO object pointers, initialize pointers on define.  These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   FieldPtr pFldType = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
  
   // Define string variables.  
   _bstr_t strSQLChange("UPDATE Titles SET Type = 'sociology' WHERE Type = 'psychology'");  
   _bstr_t strSQLRestore("UPDATE Titles SET Type = 'psychology' WHERE Type = 'sociology'");  
  
   // Define Other Variables  
   HRESULT hr = S_OK;  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared  
   CTitleRs titlers;   // C++ Class object  
   char * token1;  
  
   try {  
      _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open Recordset for batch update.  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->PutActiveConnection(_variant_t((IDispatch *)pConnection, true));  
      pRstTitles->CursorType = adOpenKeyset;  
      pRstTitles->LockType = adLockBatchOptimistic;  
  
      // Cast connection pointer to IDispatch type; convert to correct variant type.  
      pRstTitles->Open("Titles", _variant_t((IDispatch *)pConnection,true),  
         adOpenKeyset, adLockBatchOptimistic, adCmdTable);  
  
      // Open IADORecordBinding interface pointer for Binding Recordset to a class.  
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here    
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Set field object variable for Type field.  
      pFldType = pRstTitles->Fields->GetItem("type");  
  
      // Change the type of psychology titles.  
      while ( !(pRstTitles->EndOfFile) ) {  
         if (!strcmp(strtok_s((char *)titlers.m_szau_Type, " ", &token1), "psychology"))  
            pFldType->Value = "self_help";  
         pRstTitles->MoveNext();  
      }  
  
      // Simulate a change by another user by updating data using a command string.  
      pConnection->Execute(strSQLChange, NULL, 0);  
  
      // Check for changes.  
      pRstTitles->MoveFirst();  
      while (!(pRstTitles->EndOfFile)) {  
         if (strcmp(pFldType->OriginalValue.pcVal, pFldType->UnderlyingValue.pcVal)) {  
            printf("Data has changed!");  
  
            printf("\nTitle ID: %s", titlers.lau_Title_idStatus ==   
               adFldOK ? titlers.m_szau_Title_id : "<NULL>");  
  
            printf("\nCurrent Value: %s", (LPCSTR) (_bstr_t) pFldType->Value);  
  
            printf("\nOriginal Value: %s", (LPCSTR) (_bstr_t) pFldType->OriginalValue);  
  
            printf("\nUnderlying Value: %s\n\n", (LPCSTR) (_bstr_t) pFldType->UnderlyingValue);  
         }  
         pRstTitles->MoveNext();  
      }  
   }  
   catch (_com_error &e)  {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Connection.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen) {  
         // Cancel the update because this is a demonstration.  
         pRstTitles->CancelBatch(adAffectAll);  
         pRstTitles->Close();  
      }  
      if (pConnection)  
         if (pConnection->State == adStateOpen) {  
            // Restore Original Values.  
            pConnection->Execute(strSQLRestore, NULL, 0);  
            pConnection->Close();  
         }  
};  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **Daten wurde geändert!**  
**Title-ID: PS1372**  
**Aktueller Wert: Self_help**   
**Ursprünglicher Wert: Psychologie**   
**Zugrunde liegenden Wert: Soziologie**   
**Daten wurde geändert!**  
**Title-ID: PS2091**  
**Aktueller Wert: Self_help**   
**Ursprünglicher Wert: Psychologie**   
**Zugrunde liegenden Wert: Soziologie**   
**Daten wurde geändert!**  
**Title-ID: PS2106**  
**Aktueller Wert: Self_help**   
**Ursprünglicher Wert: Psychologie**   
**Zugrunde liegenden Wert: Soziologie**   
**Daten wurde geändert!**  
**Title-ID: PS3333**  
**Aktueller Wert: Self_help**   
**Ursprünglicher Wert: Psychologie**   
**Zugrunde liegenden Wert: Soziologie**   
**Daten wurde geändert!**  
**Title-ID: PS7777**  
**Aktueller Wert: Self_help**   
**Ursprünglicher Wert: Psychologie**   
**Zugrunde liegenden Wert: Soziologie**    
## <a name="see-also"></a>Siehe auch  
 [OriginalValue-Eigenschaft (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [OriginalValue-Eigenschaft](../../../ado/reference/ado-api/underlyingvalue-property.md)

