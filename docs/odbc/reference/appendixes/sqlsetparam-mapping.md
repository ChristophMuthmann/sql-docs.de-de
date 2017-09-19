---
title: SQLSetParam Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd23345c0e403e6f4f16419e539c2b5ae277c9d4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetparam-mapping"></a>SQLSetParam-Zuordnung
**SQLSetParam** weiterhin auf der Basis von zuzuordnenden **SQLBindParameter** wie ODBC 2.* X*. Obwohl vom Konzept her ähnlich ist **SQLBindParam**, ordnet der Treiber-Manager nicht **SQLSetParam** auf **SQLBindParam**. Grund hierfür ist, bestimmte vorhandene ODBC 2. *x* Treiber verwenden, den speziellen Wert der *Pufferlänge* (SQL_SETPARAM_VALUE_MAX), die der Treiber-Manager generiert, wenn er zuordnet **SQLSetParam** auf der Basis von ** SQLBindParameter** um zu bestimmen, wenn sie mit 1 aufgerufen wird.* X* ODBC-Anwendung.  
  
 Ein Aufruf von  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 führt zu folgendem:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
