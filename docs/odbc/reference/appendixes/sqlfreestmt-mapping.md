---
title: SQLFreeStmt Zuordnung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: df3cfba17f19074fbe00f33ef7fba098a4fe8184
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt-Zuordnung
Wenn eine Anwendung aufruft **SQLFreeStmt** mit einem *Option* Argument SQL_DROP über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 wird zugeordnet  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 mit der *behandeln* Argument festgelegt wird, auf den Wert in *Befehls beschäftigt*.

