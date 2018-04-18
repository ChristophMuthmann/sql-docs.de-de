---
title: SQLSetParam Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a784ec60a7b88f3ace601a8ce18ff05263803441
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam-Zuordnung
**SQLSetParam** weiterhin auf der Basis von zuzuordnenden **SQLBindParameter** wie ODBC 2. *X*. Obwohl vom Konzept her ähnlich ist **SQLBindParam**, ordnet der Treiber-Manager nicht **SQLSetParam** auf **SQLBindParam**. Grund hierfür ist, bestimmte vorhandene ODBC 2. *x* Treiber verwenden, den speziellen Wert der *Pufferlänge* (SQL_SETPARAM_VALUE_MAX), die der Treiber-Manager generiert, wenn er zuordnet **SQLSetParam** auf der Basis von  **SQLBindParameter** um zu bestimmen, wenn sie mit 1 aufgerufen wird. *X* ODBC-Anwendung.  
  
 Ein Aufruf von  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 führt zu folgendem:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
