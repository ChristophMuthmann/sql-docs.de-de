---
title: Batches von Anweisungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
caps.latest.revision: "36"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f9e5a1416170b7b1cf2516ec25bc578141dfd36
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="batches-of-statements"></a>Batches von Anweisungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Ein Batch von [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisungen enthält zwei oder mehr Anweisungen, getrennt durch ein Semikolon (;) in einer einzigen Zeichenfolge an **SQLExecDirect** oder [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360). Beispiel:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 Batches können effizienter als das Senden getrennter Anweisungen sein, da der Netzwerkdatenverkehr dadurch meist reduziert wird. Verwendung [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) auf positioniert wird, auf das nächste Resultset, wenn das aktuelle Resultset abgeschlossen.  
  
 Batches können immer dann verwendet werden, wenn die ODBC-Cursorattribute auf die Standardeinstellungen eines schreibgeschützten Vorwärtscursors mit der Rowsetgröße 1 festgelegt wurden.  
  
 Wenn ein Batch ausgeführt wird und Servercursor für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet werden, dann wird der Servercursor implizit in ein Standardresultset umgewandelt. **SQLExecDirect** oder **SQLExecute** zurückgeben SQL_SUCCESS_WITH_INFO und ein Aufruf von **SQLGetDiagRec** zurückgibt:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Anweisungen &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
