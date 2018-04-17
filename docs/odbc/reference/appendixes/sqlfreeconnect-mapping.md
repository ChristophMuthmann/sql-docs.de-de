---
title: SQLFreeConnect Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e22a01271bab030fa0036bb5669a2bf7ef15c00
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect-Zuordnung
Wenn eine Anwendung ruft **SQLFreeConnect** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 wird zugeordnet  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 mit der *behandeln* Argument festgelegt wird, auf den Wert in *Hdbc*.
