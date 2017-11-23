---
title: SQLFreeConnect Zuordnung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e04891841ab2c934c13f0296c9560754363f9aa9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
