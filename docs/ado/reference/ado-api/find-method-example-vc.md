---
title: Suchen Sie die (VC++-Methodenbeispiel) | Microsoft Docs
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
- Find method [ADO], VC++ example
ms.assetid: 594c51cb-1157-4417-802b-d91b875ba020
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8277c4fb811be2d0ae61ded434643aeda835a6a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="find-method-example-vc"></a>Suchen Sie die (VC++-Methodenbeispiel)
Dieses Beispiel verwendet die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) des Objekts [suchen](../../../ado/reference/ado-api/find-method-ado.md) -Methode zum Suchen und die Anzahl der Business Titel in die **Pubs** Datenbank. Im Beispiel wird davon ausgegangen, dass der zugrunde liegende Anbieter eine ähnliche Funktionalität nicht unterstützt.  
  
```  
// BeginFindCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This Class extracts only titleId from Titles table.  
class CTitlesRs : public CADORecordBinding {  
BEGIN_ADO_BINDING(CTitlesRs)  
  
   // Column title_id is the first field in the recordset from Titles table.  
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szt_titleid, sizeof(m_szt_titleid), lt_titleidStatus, FALSE)  
  
END_ADO_BINDING()  
  
public:  
   CHAR m_szt_titleid[150];  
   ULONG lt_titleidStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void FindX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
   FindX();  
   ::CoUninitialize();  
}  
  
void FindX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared.  
   CTitlesRs titlers;   // C++ class object  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open title Table  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
  
      pRstTitles->Open("SELECT title_id FROM titles",   
         _variant_t((IDispatch *)pConnection),   
         adOpenStatic, adLockReadOnly, adCmdText);  
  
      // The default parameters are sufficient to search forward through a Recordset.  
  
      pRstTitles->Find ("title_id LIKE 'BU%'", 0, adSearchForward, "");  
  
      // Open an IADORecordBinding interface pointer for Binding Recordset to a class      
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here      
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Skip the current record to avoid finding the same row repeatedly.   
      // The bookmark is redundant because Find searches from the current position.  
      int count = 0;  
  
      // Continue if last find succeeded.  
      while (!(pRstTitles->EndOfFile)) {  
         printf("Title ID: %s\n", titlers.lt_titleidStatus == adFldOK ?  
            titlers.m_szt_titleid : "<NULL>");  
         count++;   // Count the last title found.  
  
         _variant_t mark = pRstTitles->Bookmark;   // Note current pos.  
         pRstTitles->Find("title_id LIKE 'BU%'", 1, adSearchForward, mark);  
      }  
      printf("The number of business titles is %d\n", count);  
   }  
   catch(_com_error &e) {  
      // Display errors, if any. Pass connection pointer accessed from the Recordset.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }      
  
   // Clean up objects before exit. Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, (LPCSTR)pErr->Description);  
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
 [Find-Methode (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
