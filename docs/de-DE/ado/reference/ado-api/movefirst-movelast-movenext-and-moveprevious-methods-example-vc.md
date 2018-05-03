---
title: Mauszeiger Datensatz des Recordsets (VC++-Beispiel) | Microsoft Docs
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
- MoveLast method [ADO], VC++ example
- MoveNext method [ADO], VC++ example
- MovePrevious method [ADO], VC++ example
- MoveFirst method [ADO], VC++ example
ms.assetid: 7f8aea7b-9183-4b29-8ac0-a393ed2e8bd5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 330f06ef60f72d76f33ee439da0de7768b164dea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-example-vc"></a>MoveFirst, MoveLast, MoveNext und MovePrevious Methoden (VC++-Beispiel)
Dieses Beispiel verwendet die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), und [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) -Methoden verschieben die Zeiger für den Datensatz eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) basierend auf den angegebenen Befehl. Die MoveAny-Funktion ist erforderlich, damit dieses Beispiel ausführen.  
  
## <a name="example"></a>Beispiel  
  
```  
// MoveFirstMoveLastMoveNextSample.cpp  
// compile with: /EHsc  
#include <ole2.h>  
#include <stdio.h>  
  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void MoveFirstX();  
void MoveAny(int intChoice, _RecordsetPtr pRstTemp);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   MoveFirstX();  
   ::CoUninitialize();  
}  
  
void MoveFirstX() {  
   HRESULT hr = S_OK;  
   _RecordsetPtr pRstAuthors = NULL;  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
   _bstr_t strMessage("UPDATE Titles SET Type = "  
      "'psychology' WHERE Type = 'self_help'");  
   int intCommand = 0;  
  
   // Temporary string variable for type conversion for printing.  
   _bstr_t  bstrFName;  
   _bstr_t  bstrLName;  
  
   try {  
      // Open recordset from Authors table.  
      TESTHR(pRstAuthors.CreateInstance(__uuidof(Recordset)));  
      pRstAuthors->CursorType = adOpenStatic;  
  
      // Use client cursor to enable AbsolutePosition property.  
      pRstAuthors->CursorLocation = adUseClient;  
      pRstAuthors->Open("Authors", strCnn, adOpenStatic, adLockBatchOptimistic, adCmdTable);  
  
      // Show current record information and get user's method choice.  
      while (true) {   // Continuous loop.  
         // Convert variant string to convertable string type.  
         bstrFName = pRstAuthors->Fields->Item["au_fName"]->Value;  
         bstrLName = pRstAuthors->Fields->Item["au_lName"]->Value;  
  
         printf("Name: %s %s\n Record %d of %d\n\n",  
            (LPCSTR) bstrFName,  
            (LPCSTR) bstrLName,  
            pRstAuthors->AbsolutePosition,  
            pRstAuthors->RecordCount);  
         printf("[1 - MoveFirst, 2 - MoveLast, \n");  
         printf(" 3 - MoveNext, 4 - MovePrevious, 5 - Quit]\n");  
  
         scanf_s("%d", &intCommand);  
  
         if ((intCommand < 1) || (intCommand > 4))  
            break;   // Out of range entry exits program loop.  
  
         // Call method based on user's input.  
         MoveAny(intCommand, pRstAuthors);  
      }  
   }  
   catch (_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstAuthors->GetActiveConnection();  
  
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
  
   // Clean up objects before exit.  
   if (pRstAuthors)  
      if (pRstAuthors->State == adStateOpen)  
         pRstAuthors->Close();  
}  
  
void MoveAny(int intChoice, _RecordsetPtr pRstTemp) {  
   // Use specified method, trapping for BOF and EOF  
   try {  
      switch(intChoice) {  
         case 1:  
            pRstTemp->MoveFirst();  
            break;  
         case 2:  
            pRstTemp->MoveLast();  
            break;  
         case 3:  
            pRstTemp->MoveNext();  
            if (pRstTemp->EndOfFile) {  
               printf("\nAlready at end of recordset!\n");  
               pRstTemp->MoveLast();  
            }    // End If  
            break;  
         case 4:  
            pRstTemp->MovePrevious();  
            if (pRstTemp->BOF) {  
               printf("\nAlready at beginning of recordset!\n");  
               pRstTemp->MoveFirst();  
            }  
            break;  
         default:  
            ;  
      }  
   }  
  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTemp->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt)  {  
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
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount - 1.  
      for ( long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
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
  
 Eingabe  
  
```  
5  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
