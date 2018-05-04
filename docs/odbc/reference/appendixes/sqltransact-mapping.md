---
title: SQLTransact Zuordnung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e938a4eb7c605d1ed9cf71c038bcc7187e1a8cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
