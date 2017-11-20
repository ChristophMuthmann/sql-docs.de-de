---
title: "Spaltengröße, Dezimalstellen, Übertragung Oktett lang und Anzeigegröße | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19f505751d63f07dbd5eb2d1d53b9c191307e9b2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße - ODBC
Datentypen sind gekennzeichnet durch ihre Größe Spalte (oder Parameter), Dezimalstellen, Länge und Größe anzuzeigen. Die folgenden ODBC-Funktionen geben diese Attribute für einen Parameter in einer SQL­Anweisung oder eines SQL-Datentyps auf einer Datenquelle zurück. Jede ODBC-Funktion gibt einen anderen Satz dieser Attribute wie folgt aus:  
  
-   **SQLDescribeCol** gibt die Spalte zurück, Größe und Dezimalstelle Ziffern der Spalten beschrieben.  
  
-   **SQLDescribeParam** Größe und Dezimalstelle Ziffern der Parameter, es wird beschrieben, für den Parameter zurück. **SQLBindParameter** legt den Parameter Größe und Dezimalstelle Ziffern für einen Parameter in einer SQL­Anweisung.  
  
-   Die Katalogfunktionen **SQLColumns**, **SQLProcedureColumns**, und **SQLGetTypeInfo** Attribute für eine Spalte in einer Tabelle, Resultsets oder einen Prozedurparameter zurück und die Katalogattribute der Datentypen in der Datenquelle. **SQLColumns** gibt die Spaltengröße, Dezimalstellen und Länge einer Spalte in der angegebenen Tabellen (z. B. die Basistabelle, Sicht oder eine Systemtabelle). **SQLProcedureColumns** gibt die Spaltengröße, Dezimalstellen und Länge einer Spalte in einer Prozedur. **SQLGetTypeInfo** gibt die maximale Spaltengröße und die minimalen und maximalen Dezimalzahlen eines SQL-Datentyps auf einer Datenquelle zurück.  
  
 Die Werte, die von diesen Funktionen für die Spalte zurückgegeben oder Parametergröße entsprechen "Precision" als in ODBC 2. definiert. *x*. Allerdings die Werte nicht unbedingt in SQL_DESC_PRECISION oder alle eine Deskriptorfeld zurückgegebenen Werte entsprechen. Dasselbe gilt für die Dezimalstellen "Scale" als definiert, in ODBC 2. entsprechen. *x*. Entspricht nicht unbedingt mit den Werten in SQL_DESC_SCALE oder ein anderes einen Deskriptorfeld zurückgegeben, aber unterschiedliche deskriptorfelder je nach Datentyp stammt. Weitere Informationen finden Sie unter [Spaltengröße](../../../odbc/reference/appendixes/column-size.md) und [Dezimalstellen](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Auf ähnliche Weise die Werte für die Übertragung Oktettlänge nicht SQL_DESC_LENGTH stammen. Sie stammen aus den SQL_DESC_OCTET_LENGTH eines Felds einen Deskriptor für alle Zeichen- und Binärtypen. Es gibt keine Deskriptorfeld, die diese Informationen für andere Typen enthält.  
  
 Der Anzeigewert der Größe für alle Datentypen entspricht dem Wert in einem einzelnen Beschreibungsfeld SQL_DESC_DISPLAY_SIZE.  
  
 Deskriptorfelder beschreiben die Merkmale eines Resultsets. Deskriptorfelder enthalten keine gültigen Werte zu Daten, die vor der anweisungsausführung. Die Werte für die Spalte Größe, Dezimalstellen, und Anzeigegröße zurückgegebenes **SQLColumns**, **SQLProcedureColumns**, und **SQLGetTypeInfo**, auf dem anderen andererseits, zurückgeben Merkmale der Datenbankobjekte, z. B. Spalten und Datentypen, die im Katalog der Datenquelle vorhanden sein. Ebenso im Resultset **SQLColAttribute** gibt die Spaltengröße, den Dezimalstellen und Übertragung Oktettlänge von Spalten in der Datenquelle; diese Werte sind nicht unbedingt identisch mit den Werten in der SQL_DESC_PRECISION SQL_ DESC_SCALE und deskriptorfelder SQL_DESC_OCTET_LENGTH.  
  
 Weitere Informationen zu diesen deskriptorfelder finden Sie unter [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Verwandte Themen:  
  
-   [Spaltengröße](../../../odbc/reference/appendixes/column-size.md)  
-   [Dezimalstellen](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Oktettlänge übertragen](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Die Anzeigegröße](../../../odbc/reference/appendixes/display-size.md)

