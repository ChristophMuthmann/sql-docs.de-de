---
title: NextRecordset-Methode (VC++-Beispiel) | Microsoft Docs
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
- NextRecordset method [ADO], VC++ example
ms.assetid: 8bb72817-0cf5-4ce9-9fb8-043c89da941c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efe33b6537c149dccab20f664a36c02b0b78c9d9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="nextrecordset-method-example-vc"></a>NextRecordset-Methode (VC++-Beispiel)
Dieses Beispiel verwendet die [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) Methode, um die Daten in einem Recordset anzuzeigen, die einen zusammengesetzten befehlsanweisung setzt sich aus drei Separate verwendet **wählen** Anweisungen.  
  
```  
// BeginNextRecordsetCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <stdio.h>  
#include <ole2.h>  
#include <conio.h>  
#include <stdlib.h>  
  
//Function Declaration.  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void NextRecordsetX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   NextRecordsetX();  
   ::CoUninitialize();  
}  
  
void NextRecordsetX() {  
   // Define ADO object pointers.  Initialize pointers on define.  These are in the ADODB::  namespace.  
   _RecordsetPtr pRstCompound = NULL;  
  
   // Define Other Variables  
   _variant_t index;  
   index.vt = VT_I2;  
  
   // Assign connection string to a variable.  
   _bstr_t strCnn("Provider='sqloledb';Data Source='(local)';Initial Catalog='pubs';Integrated Security='SSPI';");  
  
   try {  
      // Open recordset from Authors table.  
      TESTHR(pRstCompound.CreateInstance(__uuidof(Recordset)));  
  
      // Pass the Cursor type and Lock type to the Recordset.  
      pRstCompound->Open("SELECT * FROM authors; SELECT * FROM stores;SELECT * FROM jobs",   
         strCnn, adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Display results from each SELECT statement.  
      int intCount = 1;  
      while (!(pRstCompound == NULL)) {  
         printf("\n\nContents of recordset #%d\n", intCount);  
  
         while (!pRstCompound->EndOfFile) {  
            index.iVal = 0;  
            printf("%s\t", (LPCSTR)(_bstr_t)pRstCompound->GetFields()->GetItem(& index)->Value);  
            index.iVal = 1;  
            printf("%s\n", (LPCSTR)(_bstr_t)pRstCompound->Fields->GetItem(& index)->Value);  
  
            pRstCompound->MoveNext();  
  
         }  
         long lngRec = 0;  
         pRstCompound = pRstCompound->NextRecordset((VARIANT *)lngRec);  
  
         intCount = intCount + 1;  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstCompound->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection is not open, else returns Connection object.  
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
  
   // Clean up objects before exit.  
   if (pRstCompound)  
      if (pRstCompound->State == adStateOpen)  
         pRstCompound->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, (LPCSTR) pErr->Description);  
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
 [NextRecordset-Methode (ADO)](../../../ado/reference/ado-api/nextrecordset-method-ado.md)
