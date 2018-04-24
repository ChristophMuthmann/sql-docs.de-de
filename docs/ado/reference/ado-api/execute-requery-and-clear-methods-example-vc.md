---
title: Ausführen, abzufragen und deaktivieren Sie die Methoden (VC++-Beispiel) | Microsoft Docs
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
- Requery method [ADO], VC++ example
- Clear method [ADO], VC++ example
- Execute method [ADO], VC++ example
ms.assetid: ada6acc1-82eb-4cfa-8f2f-617a916ffd8d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed534461e3f0305cc0dd017abbb508d6322aa77e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="execute-requery-and-clear-methods-example-vc"></a>Führen Sie Requery und deaktivieren Sie die Methoden (VC++-Beispiel)
In diesem Beispiel wird veranschaulicht, die **Execute** Methode, die sowohl beim Ausführen einer [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt und ein [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Darüber hinaus verwendet der [Requery](../../../ado/reference/ado-api/requery-method.md) Methode zum Abrufen von aktuellen Daten in einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und die [deaktivieren](../../../ado/reference/ado-api/clear-method-ado.md) Methode, um den Inhalt der Löschen der [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md)Auflistung. Die Funktionen "ExecuteCommand" und PrintOutput sind erforderlich, damit dieses Beispiel ausführen.  
  
```  
// Execute_Requery_Clear_Method_Sample.cpp  
// compile with: /EHsc  
#include <ole2.h>  
#include <stdio.h>  
  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void ExecuteX();  
void ExecuteCommand(_CommandPtr pCmdTemp, _RecordsetPtr pRstTemp);  
void PrintOutput(_RecordsetPtr pRstTemp);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   ExecuteX();  
   ::CoUninitialize();  
}  
  
void ExecuteX() {  
   // Define string variables.  
   _bstr_t strSQLChange("UPDATE Titles SET Type = 'self_help' WHERE Type = 'psychology'");  
   _bstr_t strSQLRestore("UPDATE Titles SET Type = 'psychology' WHERE Type = 'self_help'");  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _CommandPtr pCmdChange = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
  
   try {  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Create command object.  
      TESTHR(pCmdChange.CreateInstance(__uuidof(Command)));  
      pCmdChange->ActiveConnection = pConnection;  
      pCmdChange->CommandText = strSQLChange;  
  
      // Open titles table, casting Connection pointer to an   
      // IDispatch type so converted to correct type of variant.  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->Open ("Titles", _variant_t((IDispatch *) pConnection, true),   
         adOpenStatic, adLockOptimistic, adCmdTable);  
  
      // Print report of original data.  
      printf("\n\nData in Titles table before executing the query: \n");  
  
      // Call function to print loop recordset contents.  
      PrintOutput(pRstTitles);  
  
      // Clear extraneous errors from the Errors collection.  
      pConnection->Errors->Clear();  
  
      // Call ExecuteCommand subroutine to execute pCmdChange command.  
      ExecuteCommand(pCmdChange, pRstTitles);  
  
      // Print report of new data.  
      printf("\n\n\tData in Titles table after executing the query: \n");  
      PrintOutput(pRstTitles);  
  
      // Use Connection object's Execute method to execute SQL statement to restore data.  
      pConnection->Execute(strSQLRestore, NULL, adExecuteNoRecords);  
  
      // Retrieve the current data by requerying the recordset.  
      pRstTitles->Requery(adCmdUnknown);  
  
      // Print report of restored data.  
      printf("\n\n\tData after exec. query to restore original info: \n");  
      PrintOutput(pRstTitles);  
   }  
   catch (_com_error &e) {  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void ExecuteCommand(_CommandPtr pCmdTemp, _RecordsetPtr pRstTemp) {  
   try {  
      // CommandText property already set before function was called.  
      pCmdTemp->Execute(NULL, NULL, adCmdText);  
  
      // Retrieve the current data by requerying the recordset.  
      pRstTemp->Requery(adCmdUnknown);  
   }  
  
   catch(_com_error &e) {  
      // Notify user of any errors that result from executing the query.  
      // Pass a connection pointer accessed from the Recordset.  
      PrintProviderError(pRstTemp->GetActiveConnection());  
      PrintComError(e);  
   }  
}  
  
void PrintOutput(_RecordsetPtr pRstTemp) {  
   // Ensure at top of recordset.  
   pRstTemp->MoveFirst();  
  
   // If EOF is true, then no data and skip print loop.  
   if ( pRstTemp->EndOfFile )  
      printf("\tRecordset empty\n");  
   else {  
      // Define strings for output conversions.  Initialize to first record's values.  
      _bstr_t bstrTitle;  
      _bstr_t bstrType;  
  
      // Enumerate Recordset and print from each.  
      while ( !(pRstTemp->EndOfFile) ) {  
         // Convert variant string to convertable string type.  
         bstrTitle = pRstTemp->Fields->GetItem("Title")->Value;  
         bstrType  = pRstTemp->Fields->GetItem("Type")->Value;  
         printf("\t%s, %s \n", (LPCSTR) bstrTitle, (LPCSTR) bstrType);  
  
         pRstTemp->MoveNext();  
      }  
   }  
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
  
## <a name="see-also"></a>Siehe auch  
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Execute-Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Requery-Methode](../../../ado/reference/ado-api/requery-method.md)
