---
title: 'Anhang D: Datentypen | Microsoft Docs'
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
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a543430479a33953e087fd50c91f7f2a307fc204
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-d-data-types"></a>Anhang D:-Datentypen
ODBC definiert zwei Sätze von Datentypen: SQL-Datentypen und C-Datentypen. SQL-Datentypen geben Sie den Datentyp, der in der Datenquelle gespeicherten Daten an. C-Datentypen geben Sie den Datentyp, der in der Anwendungspuffer gespeicherten Daten an.  
  
 SQL-Datentypen werden von jedem DBMS in Übereinstimmung mit der SQL-92-Standard definiert. Für jeden SQL-Datentyp, der in der SQL-92-Standard angegeben wird, ODBC definiert einen Typbezeichner, also eine **#define** Wert, der als Argument in ODBC-Funktionen übergeben oder in den Metadaten als Resultset zurückgegeben. Die einzige SQL-92 nicht von ODBC unterstützte Datentypen sind BIT (ODBC SQL_BIT Typ verfügt über unterschiedliche Eigenschaften), BIT_VARYING, TIME_WITH_TIMEZONE, TIMESTAMP_WITH_TIMEZONE und NATIONAL_CHARACTER. Treiber sind verantwortlich für die ODBC-SQL-Datentypbezeichner und treiberspezifischen SQL-Datentypbezeichner Data Source-spezifische SQL-Datentypen zuordnen. Im Feld SQL_DESC_CONCISE_TYPE ein Deskriptor für die Implementierung ist die SQL-Datentyp angegeben.  
  
 ODBC definiert die C-Datentypen und ihre entsprechenden ODBC-Typ-IDs. Eine Anwendung gibt der C-Datentyp des Puffers, der Resultsetdaten erhält durch Übergeben der entsprechenden C-Typ-ID in der *TargetType* Argument in einem Aufruf von **SQLBindCol** oder  **SQLGetData**. Es gibt den C-Typ, der den Puffer mit einer Anweisungsparameter durch Übergeben der entsprechenden C-Typ-ID in der *ValueType* Argument in einem Aufruf von **SQLBindParameter**. Die C-Datentyp wird im Feld SQL_DESC_CONCISE_TYPE ein Anwendungsdiensts angegeben.  
  
> [!NOTE]  
>  Es gibt keine Treiber-spezifischen C-Datentypen.  
  
 Jeder SQL-Datentyp entspricht einer ODBC-C-Datentyp. Vor der Rückgabe von Daten aus der Datenquelle, konvertiert der Treiber es in den angegebenen C-Datentyp. Vor dem Senden von Daten an die Datenquelle, konvertiert der Treiber es aus der angegebenen C-Datentyp.  
  
 Dieser Anhang enthält die folgenden Themen.  
  
-   [Mithilfe von-Datentypbezeichner](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [-Datentypbezeichnungen und Deskriptoren](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [Pseudo-Typ-IDs](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [Übertragen von Daten in seiner binären Form](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [Richtlinien für das Intervall und numerische Datentypen](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [Einschränkungen des gregorianischen Kalenders](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [Spaltengröße, Dezimalstellen, Oktettlänge Übertragung und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [Konvertieren von Daten von SQL-in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [Konvertieren von Daten von C-in SQL-Datentypen](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 Eine Erläuterung der ODBC-Datentypen, finden Sie unter [Datentypen in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md). Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.

