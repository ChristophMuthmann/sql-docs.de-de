---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56b902d8be50a1ce0a69c273d195659c3d835030
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfreestmt"></a>'SQLFreeStmt'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Im Allgemeinen   
      **SQLFreeStmt** wird nicht empfohlen, in ODBC 3.0 und höher. Wenn die Anwendung die Anweisung erneut verwenden muss Sie jedoch weiterhin verwenden sollten **SQLFreeStmt** mit der **SQL_RESET_PARAMS** und **SQL_UNBIND** Optionen). Sie können auch [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md), und [ SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) ersetzen oder duplizieren die Funktion des **SQLFreeStmt** und sollte stattdessen diese verwendet werden.  
  
 Im Allgemeinen ist es effizienter, wiederverwenden Anweisungen als zum Löschen und neu zuzuordnen. Jedoch in einigen Situationen, z. B. das Wiederverwenden von Anweisungen die, SQLFreeStmt weiterhin verwendet werden muss.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLFreeStmt-Funktion](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
