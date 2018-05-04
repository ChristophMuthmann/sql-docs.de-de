---
title: DateTime-Datentypen | Microsoft Docs
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
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 730d72fecb5b452949d7336a59586f877cb09b40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="datetime-data-types"></a>DateTime-Datentypen
In ODBC 3.*.x*, die Bezeichner für das Datum, Zeit und Zeitstempel SQL-Datentypen von SQL_DATE, SQL_TIME und SQL_TIMESTAMP geändert haben (mit Instanzen von **#define** in der Headerdatei 9, 10 und 11) an den SQL_ TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP (mit Instanzen von **#define** in der Headerdatei von 91, 92 und 93) zugeordnet. Der entsprechende Bezeichner haben sich seit geändert SQL_C_DATE SQL_C_TIME und SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME und SQL_C_TYPE_TIMESTAMP bzw. C-Typ und die Instanzen von **#define** wurden geändert entsprechend.  
  
 Die Spaltengröße und Dezimalstellen zurückgegeben, für die SQL-Datetime-Datentypen in ODBC 3.*.x* sind identisch mit der Genauigkeit und Dezimalstellenanzahl dafür in ODBC 2. zurückgegeben. *X*. Diese Werte unterscheiden sich die Werte in die deskriptorfelder SQL_DESC_PRECISION und SQL_DESC_SCALE zur Verfügung. (Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.)  
  
 Diese Änderungen wirken sich auf **SQLDescribeCol**, **SQLDescribeParam**, und **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**, und **SQLGetData**; und **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, und **SQLSpecialColumns**.  
  
 Eine ODBC 3.*.x* Treiber verarbeitet, die Funktionsaufrufe, die im vorherigen Absatz gemäß der Einstellung des Attributs SQL_ATTR_ODBC_VERSION Umgebung aufgeführt. Für **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**, und **SQLStatistics** , wenn SQL_ATTR_ODBC_VERSION auf SQL_OV_ODBC3 fest, die Funktionen return SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP im Feld "DATA_TYPE" festgelegt ist. Die COLUMN_SIZE-Spalte (im zurückgegebenes Resultset **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, und **SQLSpecialColumns**) enthält die Genauigkeit für den ungefähren numerischen Typ an. Die Spalte NUM_PREC_RADIX (im zurückgegebenes Resultset **SQLColumns**, **SQLGetTypeInfo**, und **SQLProcedureColumns**) den Wert 2 enthält. Wenn SQL_ATTR_ODBC_VERSION auf SQL_OV_ODBC2, und klicken Sie dann auf die Funktionen return SQL_DATE, SQL_TIME und SQL_TIMESTAMP im Feld "DATA_TYPE" festgelegt ist, enthält die COLUMN_SIZE-Spalte die dezimale Genauigkeit für den ungefähren numerischen Typ und die NUM_PREC_RADIX-Spalte enthält einen Wert von 10.  
  
 Bei der Anforderung von alle Datentypen in einem Aufruf von **SQLGetTypeInfo**, die von der Funktion zurückgegebene Resultset enthält sowohl SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP gemäß Definition in ODBC 3.*.x*, und SQL_DATE, SQL_TIME und SQL_TIMESTAMP gemäß Definition in ODBC 2. *x*.  
  
 Aufgrund wie die ODBC 3.*.x* -Treiber-Manager führt die Zuordnung der Date, Time und Timestamp-Datentypen, ODBC 3.*.x* Treiber müssen nur erkennen **#defines** von 91, 92, und 93 für Datum, Uhrzeit und Timestamp-C-Datentypen eingegeben wird, der *TargetType* Argumente des **SQLBindCol** und **SQLGetData** oder  *ValueType* Argument **SQLBindParameter**, und Sie müssen nur erkennen **#defines** von 91, 92 und 93 für das Datum, Uhrzeit und Timestamp SQL-Datentypen in der eingegeben*ParameterType* Argument **SQLBindParameter** oder *DataType* Argument **SQLGetTypeInfo**. Weitere Informationen finden Sie unter [Änderungen des Datentyps "DateTime"](../../../odbc/reference/develop-app/datetime-data-type-changes.md).
