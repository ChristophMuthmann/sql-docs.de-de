---
title: SQLTransact Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4742829b5df9d99007181109f68d020a2f4af98
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqltransact-mapping"></a>SQLTransact-Zuordnung
**SQLTransact** ersetzt durch **SQLEndTran**. Der Hauptunterschied zwischen den beiden Funktionen besteht, die **SQLEndTran** enthält ein Argument *HandleType*, gibt den Bereich der Arbeit durchgeführt werden. Die *HandleType* -Argument kann der Umgebung oder das Verbindungshandle angeben. Beim folgenden Aufruf **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 wird zugeordnet  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Wenn *Verbindungshandle* stimmt nicht mit SQL_NULL_HDBC. Die *Verbindungshandle* Argument wird festgelegt, auf den Wert der *Hdbc*.  
  
 **SQL_Transact** zugeordnet ist  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Wenn *Verbindungshandle* SQL_NULL_HDBC entspricht. Die *EnvironmentHandle* Argument wird festgelegt, auf den Wert der *Henv*.  
  
 Sowohl der vorangegangenen Fälle, in der *' CompletionType '* Argument wird festgelegt, auf den gleichen Wert wie *fType*.
