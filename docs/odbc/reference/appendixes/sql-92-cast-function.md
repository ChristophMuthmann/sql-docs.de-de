---
title: SQL-92-CAST-Funktion | Microsoft Docs
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
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8389ff0812c91ca5a35007a21d70a2a1ca0baee8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-92-cast-function"></a>SQL-92-CAST-Funktion
Die **Umwandlung** in SQL-92 definierten Funktion entspricht der **konvertieren** in ODBC definierte Funktion. Die Syntax der entsprechenden Funktionen lautet wie folgt:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 Die SQL-92 **Umwandlung** Funktion festlegen, welche Datentypen in die andere Datentypen konvertiert werden können. (Weitere Informationen finden Sie in der SQL-92-Spezifikation.) Die **Umwandlung** -Funktion wird auf der FIPS-Transitional Ebene unterstützt.  
  
 Eine Anwendung kann bestimmen, Unterstützung für die **Umwandlung** -Funktion wie folgt:  
  
1.  Rufen Sie **SQLGetInfo** mit dem Typ der SQL_SQL_CONFORMANCE-Informationen. Wenn der Rückgabewert für den Informationstyp SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE oder SQL_SC_SQL92_FULL, ist die **Umwandlung** -Funktion unterstützt wird.  
  
2.  Wenn der Rückgabewert des Typs Informationen SQL_SQL_CONFORMANCE SQL_SC_ENTRY_LEVEL oder 0 ist, rufen Sie **SQLGetInfo** mit dem Typ der SQL_SQL92_VALUE_EXPRESSIONS-Informationen. Wenn das SQL_SVE_CAST Bit festgelegt ist, die **Umwandlung** -Funktion unterstützt wird.

