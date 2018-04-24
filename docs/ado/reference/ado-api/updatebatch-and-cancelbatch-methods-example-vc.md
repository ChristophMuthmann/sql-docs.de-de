---
title: UpdateBatch und CancelBatch Methoden (VC++-Beispiel) | Microsoft Docs
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
- UpdateBatch method [ADO]
- CancelBatch method [ADO]
ms.assetid: bcb1468e-18bb-41b8-8902-6ee05b786eec
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a6de943e01fe3fc092c13c19368151678831e49f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="updatebatch-and-cancelbatch-methods-example-vc"></a>UpdateBatch und CancelBatch Methoden (VC++-Beispiel)
Dieses Beispiel zeigt die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode in Verbindung mit der [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methode.  
  
```  
// BeginUpdateBatchCpp.cpp  
// compile with: /EHsc /c  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// class extracts titles and type from Titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
   // Column title is the 2nd field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szt_Title, sizeof(m_szt_Title), lt_TitleStatus, FALSE)  
  
   // Column type is the 3rd field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szt_Type, sizeof(m_szt_Type), lt_TypeStatus, TRUE)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szt_Title[81];  
   ULONG lt_TitleStatus;  
   CHAR m_szt_Type[13];  
   ULONG lt_TypeStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void UpdateBatchX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   UpdateBatchX();  
   ::CoUninitialize();  
}  
  
void UpdateBatchX() {  
   HRESULT  hr = S_OK;  
  
   // Define ADO object pointers.    // Initialize pointers on define.   
   // These are in the ADODB::  namespace.  
   _RecordsetPtr pRstTitles = NULL;  
   char * token1;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared  
   CTitleRs titlers;   // C++ Class Object  
  
   try {  
      // Open titles table.  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->CursorType = adOpenKeyset;  
      pRstTitles->LockType = adLockBatchOptimistic;  
      pRstTitles->Open ("titles", strCnn, adOpenKeyset, adLockBatchOptimistic, adCmdTable);  
  
      // Open IADORecordBinding interface pointer for binding recordset to a class  
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Binding the Recordset to a C++ Class  
      TESTHR(picRs->BindToRecordset(&titlers));  
      pRstTitles->MoveFirst();  
  
      // Loop through recordset and ask user if she wants,  
      // to change the type for a specified title.  
      while (!(pRstTitles->EndOfFile)) {  
         // Compare type with psychology  
         if (!strcmp( (char *)strtok_s(titlers.m_szt_Type, " ", &token1), "psychology" )) {   
               printf("\n\nTitle: %s \nChange type to self_help?(y/n):", titlers.m_szt_Title);  
               char chKey;  
               chKey = _getch();  
               if (toupper(chKey) == 'Y') {  
                  // Change type to self_help.  
                  pRstTitles->Fields->GetItem("type")->Value = (_bstr_t)("self_help");  
               }  
         }  
         pRstTitles->MoveNext();  
      }  
  
      // commit all the changes made above?  
      printf("\n\nSave all changes?");  
      char chKey;  
      chKey = _getch();  
      if (toupper(chKey) == 'Y')  
         pRstTitles->UpdateBatch(adAffectAll);  
      else  
         pRstTitles->CancelBatch(adAffectAll);  
  
      // Print current data in recordset.  
      pRstTitles->Requery(adOptionUnspecified);  
  
      // Open IADORecordBinding interface pointer for Binding Recordset to a class      
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // ReBinding the Recordset to a C++ Class.  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Move to the first record of the title table  
      pRstTitles->MoveFirst();  
  
      system("cls");  
  
      while (!pRstTitles->EndOfFile) {  
         printf("%s -  %s\n",  
            titlers.lt_TitleStatus == adFldOK ?   
            titlers.m_szt_Title :"<NULL>",  
            titlers.lt_TypeStatus == adFldOK ?   
            titlers.m_szt_Type :"<NULL>");  
         pRstTitles->MoveNext();  
      }  
  
      pRstTitles->MoveFirst();  
  
      // Restore original data because this is demonstration.  
      while (!(pRstTitles->EndOfFile)) {  
         // Compare type with psychology  
         if (!strcmp( (char *)strtok_s(titlers.m_szt_Type, " ", &token1), "self_help" )) {  
            // Change type to psychology.  
            pRstTitles->Fields->GetItem("type")->Value = (_bstr_t)("psychology");  
         }  
         pRstTitles->MoveNext();  
      }  
   }  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTitles->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
         case VT_BSTR:  
            PrintComError(e);  
            break;  
         case VT_DISPATCH:  
            PrintProviderError(vtConnect);  
            break;  
         default:  
            printf("Errors occured.");  
            break;  
      }  
   }  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen) {  
         pRstTitles->UpdateBatch(adAffectAll);  
         pRstTitles->Close();  
      }  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.  
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
