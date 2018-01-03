---
title: SQLError Zuordnung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 518814868a7fafe91a166564771af51fd8a49505
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlerror-mapping"></a>SQLError-Zuordnung
Wenn eine Anwendung ruft **SQLError** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 wird zugeordnet  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 mit der *HandleType* Argument auf SQL_HANDLE_ENV auf SQL_HANDLE_DBC oder SQL_HANDLE_STMT auf, den Wert nach Bedarf, festgelegt und die *behandeln* Argument festgelegt wird, auf den Wert in *Henv*, *Hdbc*, oder *Befehls beschäftigt*je nach Bedarf. Die *RecNumber* -Argument wird vom Treiber-Manager bestimmt.
