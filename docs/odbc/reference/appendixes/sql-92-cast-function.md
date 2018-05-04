---
title: SQL-92-CAST-Funktion | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce0ff593f8f381efb6d54ea73a8dea04f99823ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
