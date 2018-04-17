---
title: SQLAllocConnect Zuordnung | Microsoft Docs
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
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9271b975e1359212d1c1142ffda93f1f6c834ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect-Zuordnung
Wenn eine Anwendung ruft **SQLAllocConnect** über einen ODBC 3. *X* Treiber, den Aufruf von **SQLAllocConnect**(*Henv*, *Phdbc*) zugeordnet ist **SQLAllocHandle** wie folgt:  
  
1.  Der Treiber-Manager weist eine Verbindung und gibt ihn an die Anwendung zurück.  
  
2.  Wenn die Anwendung eine Verbindung hergestellt wird, ruft der Treiber-Manager  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     in den Treiber mit *InputHandle* festgelegt *Henv*, und *OutputHandlePtr* festgelegt *Phdbc*.
