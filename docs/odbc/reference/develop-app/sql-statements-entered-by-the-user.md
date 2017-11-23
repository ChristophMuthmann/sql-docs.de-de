---
title: SQL-Anweisungen, die vom Benutzer eingegebenen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91ae086fd7be4222c55a8fad9b8383846cc59949
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sql-statements-entered-by-the-user"></a>SQL-Anweisungen, die vom Benutzer eingegebenen
Anwendungen, die häufig auch ad-hoc-Analysen ermöglicht dem Benutzer, SQL-Anweisungen direkt einzugeben. Beispiel:  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 Dieser Ansatz vereinfacht die Anwendung zu codieren; die Anwendung benötigt für den Benutzer aus, um die SQL-Anweisung zu erstellen und für die Datenquelle, um die Anweisung Gültigkeit zu überprüfen. Da es schwierig ist, eine grafische Benutzeroberfläche zu schreiben, die die Komplexität von SQL Server ausreichend verfügbar macht, möglicherweise die einfach den Benutzer auffordert, geben Sie den Text der SQL-Anweisung, dass eine Alternative vorzuziehen. Allerdings erfordert dies die Benutzer wissen, nicht nur SQL, sondern auch das Schema der Datenquelle abgefragt wird. Einige Anwendungen bieten eine grafische Benutzeroberfläche der Benutzer kann nach der Erstellen einer einfachen SQL-Anweisung und geben Sie auch eine Text-Schnittstelle, die mit der der Benutzer sie ändern kann.
