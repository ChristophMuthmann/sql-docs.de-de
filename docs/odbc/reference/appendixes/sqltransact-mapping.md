---
title: SQLTransact Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 252339f7fcd2a3893f030c0ffbc4485ab5441152
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
