---
title: Verarbeitung von Anweisungen, die Meldungen generieren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a9deaa7c1890c327de38663e99e83f6ce526491
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="processing-statements-that-generate-messages"></a>Verarbeiten von Anweisungen, die Meldungen generieren
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-SET-Anweisungsoptionen STATISTICS TIME und STATISTICS IO werden verwendet, um Informationen zur Unterstützung bei der Diagnose von Abfragen mit langer Ausführungszeit zu gewinnen. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen auch die SHOWPLAN-Option zur Analyse von Abfrageplänen. Eine ODBC-Anwendung kann diese Optionen festlegen, indem sie die folgenden Anweisungen ausführt:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Wenn SET STATISTICS TIME oder SET SHOWPLAN ON, **SQLExecute** und **SQLExecDirect** SQL_SUCCESS_WITH_INFO zurück, und an diesem Punkt kann die Anwendung die SHOWPLAN oder STATISTICS TIME-Ausgabe abrufen durch Aufrufen von **SQLGetDiagRec** bis SQL_NO_DATA zurückgegeben. Jede Zeile der SHOWPLAN-Daten wird im folgenden Format ausgegeben:  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0 wurde die SHOWPLAN-Option durch SHOWPLAN_ALL und SHOWPLAN_TEXT ersetzt. Beide Optionen geben die Ausgabe als Resultset, nicht wie zuvor als Meldungssätze, zurück.  
  
 Jede Zeile der STATISTICS TIME-Daten wird im folgenden Format ausgegeben:  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 Die Ausgabe von SET STATISTICS IO ist bis zum Ende eines Resultsets nicht verfügbar. Zum Abrufen der Ausgabe von STATISTICS IO, ruft die Anwendung **SQLGetDiagRec** Zeitpunkt **SQLFetch** oder [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) gibt SQL_NO_DATA zurück. Die Ausgabe der STATISTICS IO-Option erfolgt in folgendem Format:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Verwenden von DBCC-Anweisungen  
 DBCC-Anweisungen geben Daten als Meldungen, nicht als Resultsets, zurück. **SQLExecDirect** oder **SQLExecute** zurückgeben, SQL_SUCCESS_WITH_INFO, und die Anwendung ruft die Ausgabe von Aufrufen **SQLGetDiagRec** bis SQL_NO_DATA zurückgegeben.  
  
 Beispielsweise gibt die folgende Anweisung SQL_SUCCESS_WITH_INFO zurück:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Aufrufe von **SQLGetDiagRec** zurück:  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>Verwenden der Anweisungen PRINT und RAISERROR  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]Print- und RAISERROR-Anweisungen geben Daten auch durch den Aufruf zurück **SQLGetDiagRec**. PRINT-Anweisungen dazu führen, dass die SQL-anweisungsausführung SQL_SUCCESS_WITH_INFO und ein anschließender Aufruf zurückzugebenden **SQLGetDiagRec** gibt eine *SQLState* 01000. Ein RAISERROR mit einem Schweregrad bis einschließlich 10 zeigt dasselbe Verhalten wie PRINT. Ein RAISERROR mit einem Schweregrad von 11 oder höher wird bei der Ausführung SQL_ERROR zurückgegeben, und ein anschließender Aufruf zurückzugebenden **SQLGetDiagRec** gibt *SQLState* 42000. Beispielsweise gibt die folgende Anweisung SQL_SUCCESS_WITH_INFO zurück:  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 Aufrufen von **SQLGetDiagRec** zurückgibt:  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 Die folgende Anweisung gibt SQL_SUCCESS_WITH_INFO zurück:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 Aufrufen von **SQLGetDiagRec** zurückgibt:  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 Die folgende Anweisung gibt SQL_ERROR zurück:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 Aufrufen von **SQLGetDiagRec** zurückgibt:  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 Der Zeitpunkt des Aufrufs **SQLGetDiagRec** ist wichtig, wenn die Ausgabe von Print- oder RAISERROR-Anweisungen in einem Resultset enthalten ist. Der Aufruf von **SQLGetDiagRec** abzurufenden die Print- oder RAISERROR muss unmittelbar nach der Anweisung, die SQL_ERROR oder SQL_SUCCESS_WITH_INFO empfängt Ausgabe vorgenommen werden. Dies ist einfach, wenn nur eine einzelne SQL-Anweisung ausgeführt wird, wie in den oben stehenden Beispielen. In diesen Fällen ist der Aufruf von **SQLExecDirect** oder **SQLExecute** SQL_ERROR oder SQL_SUCCESS_WITH_INFO zurück und **SQLGetDiagRec** kann dann aufgerufen werden. Komplizierter wird es, wenn Schleifen zum Behandeln der Ausgabe einer Reihe von SQL-Anweisungen codiert, oder wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-gespeicherte Prozeduren ausgeführt werden müssen.  
  
 In diesem Fall gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Resultset für jede SELECT-Anweisung zurück, die in einem Batch oder in einer gespeicherten Prozedur ausgeführt wurde. Wenn der Batch bzw. die Prozedur PRINT- oder RAISERROR-Anweisungen enthält, ist die Ausgabe dieser Anweisungen mit den Resultsets der SELECT-Anweisungen verschachtelt. Wenn die erste Anweisung im Batch oder Prozedur einer Print- oder RAISERROR, ist die **SQLExecute** oder **SQLExecDirect** gibt SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurückgegeben, und die Anwendung muss Aufrufen**SQLGetDiagRec** bis SQL_NO_DATA zum Abrufen von Print- oder RAISERROR-Informationen zurückgegeben.  
  
 Wenn die Print- oder RAISERROR-Anweisung nach einer SQL­Anweisung (z. B. eine SELECT-Anweisung) stammt, und klicken Sie dann die Print- oder RAISERROR-Informationen, wenn zurückgegeben wird [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)auf dem Resultset positioniert festgelegt, die den Fehler enthält. **SQLMoreResults** SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurückgegeben, abhängig vom Schweregrad der Meldung. Diese Nachrichten werden durch den Aufruf abgerufen **SQLGetDiagRec** bis SQL_NO_DATA zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Behandlung von Fehlern und Meldungen](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
