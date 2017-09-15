---
title: SQLAllocEnv Zuordnung | Microsoft Docs
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
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 66261c8fd8236a4abc35ac70e29f63b49f646daf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv-Zuordnung
Wenn eine Anwendung ruft **SQLAllocEnv** über einen ODBC 3.*.x* Treiber, den Aufruf von **SQLAllocEnv**(*Phenv*) zugeordnet**SQLAllocHandle** wie folgt:  
  
1.  Der Treiber-Manager weist ein Umgebungshandle und an die Anwendung zurückgegeben. Der Treiber-Manager ruft **SQLSetEnvAttr** für SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION Umgebung Attributs fest.  
  
2.  Wenn die Anwendung die erste Verbindung mit einem Treiber hergestellt wird, ruft der Treiber-Manager  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     in den Treiber mit *OutputHandlePtr* festgelegt *Phenv*.
