---
title: 'SQLAllocStmt: Zuordnung | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocstmt-mapping"></a>Zuordnung von SQLAllocStmt:
Wenn eine Anwendung ruft **SQLAllocStmt:** über einen ODBC 3.*.x* Treiber, den Aufruf von:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 wird zugeordnet zu **SQLAllocHandle** vom Treiber-Manager im Treiber wie folgt:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 mit *InputHandle* festgelegt *Hdbc* und *OutputHandlePtr* festgelegt *Phstmt*.

