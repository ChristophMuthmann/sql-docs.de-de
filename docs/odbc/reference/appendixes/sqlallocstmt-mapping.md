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
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0601202316dd8fec60b428639bc9ad4c6c7b377
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
