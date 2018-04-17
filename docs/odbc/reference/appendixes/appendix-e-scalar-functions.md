---
title: 'Anhang E: Skalarfunktionen | Microsoft Docs'
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
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ee9e2ab75f22ae3090d87d5c232f88423df9360
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="appendix-e-scalar-functions"></a>Anhang E: Skalarfunktionen
ODBC gibt die folgenden Typen von Skalarfunktionen mit detaillierten Informationen zu den einzelnen von dieser Funktionstypen, die in den entsprechenden Abschnitten in diesem Anhang bereitgestellt. Zugeordnete Syntax einschließen, die die Beschreibungen der Funktion.  
  
 Dieser Anhang enthält die folgenden Themen.  
  
-   [Zeichenfolgenfunktionen](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Numerische Funktionen](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Uhrzeit-, Datums- und Intervallfunktionen](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Systemfunktionen](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Explicit Data Type Conversion Function (Explizite Datentyp-Konvertierungsfunktion)](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST-Funktion](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC ist keinen Datentyp für die Rückgabewerte von Skalarfunktionen vorgeben, da die Funktionen häufig Daten datenquellenspezifischen sind. Anwendungen sollten die CONVERT-Skalarfunktion nach Möglichkeit zwingen datentypkonvertierung verwenden.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC und SQL-92-Skalarfunktionen  
 Die Tabellen in diesem Anhang enthalten Funktionen, die in ODBC 3.0 SQL-92 veröffentlichungshäufigkeit hinzugefügt wurden. Diese Funktionen, die für einen bestimmten Typ der skalaren Funktion hinzugefügt wird, gemäß der Definition in ODBC werden in jedem Abschnitt angezeigt.  
  
 ODBC und SQL-92 klassifizieren ihre Skalarfunktionen unterschiedlich. ODBC klassifiziert Skalarfunktionen von Argumenttyp; SQL-92 klassifiziert werden nach Wert zurückgegeben. Beispielsweise ist die EXTRACT-Funktion als Funktion Timedate durch ODBC, klassifiziert, da das Argument Extract-Feld ein Datetime-Schlüsselwort ist und die Extract-Source-Argument ein Ausdruck "DateTime" oder ein Zeitintervall ist. SQL-92 klassifiziert EXTRAHIEREN andererseits, als eine numerische Skalarfunktion, ist der Rückgabewert eine numerische.  
  
 Eine Anwendung kann bestimmen, welche Skalarfunktionen ein Treiber, durch den Aufruf unterstützt **SQLGetInfo**. Typen von Informationen sind für ODBC und SQL-92-Klassifikationen von Skalarfunktionen enthalten. Da diese Klassifizierungen unterschiedlich sind, kann die Unterstützung für einige skalaren Funktionen in Typen von Informationen angegeben werden, die nicht mit ODBC und SQL-92 übereinstimmen. Unterstützung für die EXTRAHIERUNG in ODBC ist z. B. den Informationstyp SQL_TIMEDATE_FUNCTIONS ersichtlich; Unterstützung für die EXTRAHIERUNG in SQL-92, wird durch den Informationstyp SQL_SQL92_NUMERIC_VALUE_FUNCTIONS andererseits, angegeben.
