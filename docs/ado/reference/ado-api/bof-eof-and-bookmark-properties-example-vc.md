---
title: BOF, EOF und Lesezeichen Eigenschaften (VC++-Beispiel) | Microsoft Docs
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
- Bookmark property [ADO], VC++ example
- EOF property [ADO], VC++ example
- BOF property [ADO], VC++ example
ms.assetid: bd2b9d85-e75e-4fc8-a392-076582019caa
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 309c33960737c855c4399832db5275461c5bf513
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bof-eof-and-bookmark-properties-example-vc"></a>BOF, EOF und Lesezeichen Eigenschaften (VC++-Beispiel)
Die erste Funktion in diesem Beispiel verwendet die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) und [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) eine Meldung angezeigt, wenn ein Benutzer versucht, verschieben Sie nach der ersten oder letzten Datensatz mit den Eigenschaften einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Verwendet die [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md) Eigenschaft der Benutzer einen Datensatz in ein flag einer **Recordset** und später zu ihr zurückkehren.  
  
 Die zweite Funktion verwendet die Lesezeicheneigenschaft platziert die **Lesezeichen** von jedem anderen Datensatz aus einer **Recordset** in ein Array, und klicken Sie dann unter Verwendung des Recordset-Filter.  
  
## <a name="example"></a>Beispiel  
  
```  
// BOF_EOF_Bookmark.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include "conio.h"  
#include "icrsint.h"  
  
// class extracts only author id,fname,lastname  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
   // Column au_id is the 1st field in the recordset     
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szau_id, sizeof(m_szau_id), lau_idStatus, TRUE)  
  
    ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szau_lname, sizeof(m_szau_lname), lau_lnameStatus, TRUE)  
  
    ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szau_fname, sizeof(m_szau_fname), lau_fnameStatus, TRUE)  
  
END_ADO_BINDING()  
  
public:  
   CHAR m_szau_id[20];  
   ULONG lau_idStatus;  
   CHAR m_szau_fname[40];  
   ULONG lau_fnameStatus;  
   CHAR   m_szau_lname[40];  
   ULONG  lau_lnameStatus;  
};  
  
// Function declaration  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void AppendX();  
void PrintProviderError(_ConnectionPtr pConnection);  
  
int main() {  
   HRESULT hr = S_OK;  
  
   if (FAILED(::CoInitialize(NULL)))  
        return -1;  
  
    AppendX();  
    ::CoUninitialize();   
}  
  
void AppendX() {  
   HRESULT hr = S_OK;  
  
   // Define ADO object pointers. Initialize pointers on define. These are in the ADODB::  namespace.  
   _RecordsetPtr pRstByRoyalty = NULL;  
   _RecordsetPtr pRstAuthors = NULL;    
   _CommandPtr pcmdByRoyalty = NULL;  
   _ParameterPtr pprmByRoyalty = NULL;  
   _ConnectionPtr pConnection = NULL;  
  
   //Define Other variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared.(VC++ Extensions)     
   CEmployeeRs emprs;   // C++ class object      
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   _bstr_t strMessage, strAuthorID;  
  
   int intRoyalty;  
   VARIANT vtRoyalty;  
  
   try {  
      // Open a Connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      hr = pConnection->Open(strCnn, "", "", adConnectUnspecified);  
      pConnection->CursorLocation = adUseClient;  
  
      // Open Command Object with one Parameter  
      TESTHR(pcmdByRoyalty.CreateInstance(__uuidof(Command)));  
      pcmdByRoyalty->CommandText = "byroyalty";  
      pcmdByRoyalty->CommandType = adCmdStoredProc;  
  
      // Get parameter value and append parameter  
      printf("Enter Royalty: ");  
      scanf_s("%d", &intRoyalty);  
  
      // Define Integer/variant.  
      vtRoyalty.vt = VT_I2;  
      vtRoyalty.iVal = intRoyalty;  
      pprmByRoyalty = pcmdByRoyalty->CreateParameter("percentage", adInteger, adParamInput, sizeof(int), vtRoyalty);  
      pcmdByRoyalty->Parameters->Append(pprmByRoyalty);  
  
      pprmByRoyalty->Value = vtRoyalty;  
  
      // Create Recordset by executing the command  
      pcmdByRoyalty->ActiveConnection = pConnection;  
      pRstByRoyalty = pcmdByRoyalty->Execute(NULL, NULL, adCmdStoredProc);  
  
      // Open the authors table to get author names for display  
      TESTHR(pRstAuthors.CreateInstance(__uuidof(Recordset)));  
  
      // You have to explicitly pass the default Cursor type and LockType to the Recordset here  
      hr = pRstAuthors->Open("authors", _variant_t((IDispatch*)pConnection, true), adOpenForwardOnly, adLockReadOnly, adCmdTable);   
  
      // Open an IADORecordBinding interface pointer which we'll use for Binding Recordset to a class      
      TESTHR(pRstAuthors->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here      
      TESTHR(picRs->BindToRecordset(&emprs));  
  
      // Print current data in the recordset, adding author names from author table.  
      printf("Authors with %d percent royalty ", intRoyalty);  
  
      while(!(pRstByRoyalty->EndOfFile)) {  
         strAuthorID = pRstByRoyalty->Fields->Item["au_id"]->Value;  
         pRstAuthors->Filter = "au_id = '"+strAuthorID+"'";  
  
         printf("\n"  "%s, %s  %s",emprs.lau_idStatus == adFldOK ? emprs.m_szau_id : "<NULL>",\  
            emprs.lau_fnameStatus == adFldOK ? emprs.m_szau_fname : "<NULL>",\  
            emprs.lau_lnameStatus == adFldOK ? emprs.m_szau_lname : "<NULL>");  
  
         pRstByRoyalty->MoveNext();   
      }  
   }  
   catch(_com_error &e) {  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
      PrintProviderError(pConnection);  
      printf("\n Source : %s \n Description : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   // Clean up objects before exit.  Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstByRoyalty)  
      if (pRstByRoyalty->State == adStateOpen)  
         pRstByRoyalty->Close();  
   if (pRstAuthors)  
      if (pRstAuthors->State == adStateOpen)  
         pRstAuthors->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
    // Print Provider Errors from Connection object.  
    // pErr is a record object in the Connection's Error collection.  
    ErrorPtr pErr = NULL;  
    long nCount = 0;  
    long i = 0;  
  
    if ( (pConnection->Errors->Count) > 0) {  
        nCount = pConnection->Errors->Count;  
        // Collection ranges from 0 to nCount -1.  
        for (i = 0 ; i < nCount ; i++) {  
            pErr = pConnection->Errors->GetItem(i);  
            printf("Error number: %x\n Error Description: %s\n", pErr->Number, (LPCSTR) pErr->Description);  
        }  
    }  
}  
```  
  
## <a name="input"></a>Eingabe  
  
```  
25  
```  
  
## <a name="sample-output"></a>Beispielausgabe  
  
```  
Authors with 25 percent royalty  
724-80-9391, Stearns  MacFeather  
899-46-2035, Anne  Ringer  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BOF, EOF-Eigenschaften (ADO)](../../../ado/reference/ado-api/bof-eof-properties-ado.md)   
 [Bookmark-Eigenschaft (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
