---
title: 'SQLAllocStmt: Zuordnung | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 936e7861da5aaccc9c5ca9c649524484640f5fb4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
