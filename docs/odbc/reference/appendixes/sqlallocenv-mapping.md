---
title: SQLAllocEnv Zuordnung | Microsoft Docs
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
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01618081862172fb951cfc21c0c7cc5675bb1062
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv-Zuordnung
Wenn eine Anwendung ruft **SQLAllocEnv** über einen ODBC 3.*.x* Treiber, den Aufruf von **SQLAllocEnv**(*Phenv*) zugeordnet**SQLAllocHandle** wie folgt:  
  
1.  Der Treiber-Manager weist ein Umgebungshandle und an die Anwendung zurückgegeben. Der Treiber-Manager ruft **SQLSetEnvAttr** für SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION Umgebung Attributs fest.  
  
2.  Wenn die Anwendung die erste Verbindung mit einem Treiber hergestellt wird, ruft der Treiber-Manager  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     in den Treiber mit *OutputHandlePtr* festgelegt *Phenv*.
