---
title: Verwenden von SQLGetDiagRec und SQLGetDiagField | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db4a853206e402228eb9d76dca72a421444ed042
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Verwenden von SQLGetDiagRec und SQLGetDiagField
-Anwendungen rufen **SQLGetDiagRec** oder **SQLGetDiagField** Diagnoseinformationen abgerufen. Diese Funktionen akzeptieren eine Umgebung, Verbindung, Anweisung oder Deskriptor-Handle und Diagnose von der Funktion, die zuletzt dieses Handle zurück. Die Diagnose in einem bestimmten Handle protokolliert werden verworfen, wenn eine neue Funktion mit diesem Handle aufgerufen wird. Wenn die Funktion mehrere DiagnoseDatensätze zurückgegeben wird, ruft die Anwendung diese Funktionen mehrmals; Die Gesamtanzahl der Statusdatensätze wird durch den Aufruf abgerufen **SQLGetDiagField** für den Headerdatensatz (Datensatz 0), mit der Option SQL_DIAG_NUMBER.  
  
 Anwendungen einzelne Diagnosefelder abzurufen, durch den Aufruf **SQLGetDiagField** und Angeben des abzurufenden Felds. Bestimmte Diagnosefelder keine Bedeutung für bestimmte Arten von Handles. Eine Liste der Felder und ihre Bedeutungen, finden Sie unter der [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) funktionsbeschreibung.  
  
 Anwendungen abrufen SQLSTATE, systemeigener Fehlercode und diagnosemeldung in einem einzigen Aufruf durch den Aufruf **SQLGetDiagRec**; **SQLGetDiagRec** nicht zum Abrufen von Informationen aus den Headerdatensatz verwendet werden.  
  
 Beispielsweise wird der folgende Code fordert den Benutzer für eine SQL-Anweisung und ausgeführt. Wenn Diagnoseinformationen zurückgegeben wurde, ruft es **SQLGetDiagField** beim Abrufen der Anzahl der Statusdatensätze und **SQLGetDiagRec** SQLSTATE, systemeigener Fehlercode und diagnosemeldung von den abrufen Datensätze.  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
