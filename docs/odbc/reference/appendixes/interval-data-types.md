---
title: Intervalldatentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6a1b1a7320feef3cff6d63ce5ca6a22be6329169
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-types"></a>Interval-Datentypen
Ein Intervall wird als Differenz zwischen zwei Datumsangaben und Uhrzeiten definiert. Intervalle werden in zwei unterschiedliche Arten ausgedrückt werden. Ist eine *Jahr-Monat* Intervall, in der Intervalle in Jahren und einer ganzzahligen Anzahl von Monaten formuliert. Das andere ist eine *Tag* Intervall, in der Intervalle in Tagen, Minuten und Sekunden formuliert. Diese beiden Arten von Intervallen zielteilmengen verschieden und können nicht kombiniert werden, da Monate unterschiedliche Anzahl von Tagen haben können.  
  
 Ein Intervall besteht aus einem Satz von Feldern. Es gibt eine implizite Sortierung zwischen den Feldern. Z. B. in einem Intervall Jahr-Monat-Jahr welches Ereignis zuerst eintritt, gefolgt von den Monat. Auf ähnliche Weise sind die Felder in einem Tag-Minuten-Intervall, in der Reihenfolge Tag, Stunde und Minute. Das erste Feld in einem Intervalltyp wird aufgerufen, die *führende* Feld oder die *höherwertigen* Feld. Wird aufgerufen, das letzte Feld der *nachfolgende* Feld.  
  
 In alle Intervalle ist die führende Feld nicht durch Regeln des gregorianischen Kalenders eingeschränkt. Beispielsweise wird in einem Zeitintervall Stunde-Minute-dem Stundenfeld nicht eingeschränkt, werden zwischen 0 und 23 (einschließlich) liegt, als es normalerweise der Fall ist. Die nachfolgende Felder nach dem Feld führende führen Sie die üblichen Einschränkungen des gregorianischen Kalenders. Weitere Informationen finden Sie unter [Einschränkungen des gregorianischen Kalenders](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)weiter unten in diesem Anhang.  
  
 Es gibt 13 Intervall SQL-Datentypen und 13 Intervall C-Datentypen. Jede der Intervalldatentypen C verwendet die gleiche Struktur SQL_INTERVAL_STRUCT, die Intervalldaten enthalten. (Weitere Informationen finden Sie im nächsten Abschnitt [C-Intervall-Struktur](../../../odbc/reference/appendixes/c-interval-structure.md).) Weitere Informationen zu den SQL-Datentypen finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md); Weitere Informationen zu den C-Datentypen finden Sie unter [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Typ-ID|Klasse|Description|  
|---------------------|-----------|-----------------|  
|MONTH|Jahr-Monat|Anzahl der Monate zwischen zwei Datumsangaben.|  
|YEAR|Jahr-Monat|Anzahl der Jahre zwischen zwei Datumsangaben.|  
|YEAR_TO_MONTH|Jahr-Monat|Anzahl der Jahre oder Monate zwischen zwei Datumsangaben.|  
|DAY|Tag-Zeit|Die Anzahl von Tagen zwischen zwei Datumsangaben.|  
|HOUR|Tag-Zeit|Anzahl von Stunden zwischen zwei Datumsangaben und Uhrzeiten.|  
|MINUTE|Tag-Zeit|Anzahl der Minuten zwischen zwei Datumsangaben und Uhrzeiten.|  
|SECOND|Tag-Zeit|Anzahl der Sekunden zwischen zwei Datumsangaben und Uhrzeiten.|  
|DAY_TO_HOUR|Tag-Zeit|Anzahl der Tage/Stunden zwischen zwei Datumsangaben und Uhrzeiten.|  
|DAY_TO_MINUTE|Tag-Zeit|Anzahl der Tage/Stunden/Minuten zwischen zwei Datumsangaben und Uhrzeiten.|  
|DAY_TO_SECOND|Tag-Zeit|Anzahl der Tage/Stunden/Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten.|  
|HOUR_TO_MINUTE|Tag-Zeit|Anzahl der Stunden/Minuten zwischen zwei Datumsangaben und Uhrzeiten.|  
|HOUR_TO_SECOND|Tag-Zeit|Anzahl der Stunden/Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten.|  
|MINUTE_TO_SECOND|Tag-Zeit|Anzahl von Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten.|  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [C-Intervall-Struktur](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Datentypgenauigkeit Intervall](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Datentyplänge Intervall](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Intervall-Literale](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Overriding Default Leading and Seconds Precision for Interval Data Types (Überschreiben von standardmäßigen anführender Präzision und Genauigkeit in Sekunden für Intervalldatentypen)](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
