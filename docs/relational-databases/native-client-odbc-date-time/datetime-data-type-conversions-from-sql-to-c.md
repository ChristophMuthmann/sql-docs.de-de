---
title: Konvertierungen von SQL-in C | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 784a1b9453faa39bac3171905c88f829f77d5f50
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="datetime-data-type-conversions-from-sql-to-c"></a>DateTime-Datentypkonvertierungen von SQL-in C
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In der folgenden Tabelle werden Probleme aufgelistet, die zu berücksichtigen sind, wenn Sie Datum-/Uhrzeit-Typen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in C-Typen konvertieren.  
  
## <a name="conversions"></a>Konvertierungen  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_TYPE_DATE|OK|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|OK|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|OK|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|OK|21|16|16|  
  
## <a name="key-to-symbols"></a>Aufschlüsselung der Symbole  
  
|Symbol|Bedeutung|  
|------------|-------------|  
|OK|Keine Konvertierungsprobleme|  
|1|Es gelten die Regeln vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|2|Führende und nachfolgende Leerzeichen werden ignoriert.|  
|3|Die Zeichenfolge wird in Datum, Uhrzeit, Zeitzone oder Zeitunterschied der Zeitzone zerlegt und kann bis zu 9 Stellen für Sekundenbruchteile enthalten. Wenn die Angabe des Zeitunterschieds einer Zeitzone analysiert wird, wird die Zeitangabe in die Clientzeitzone konvertiert. Wenn während dieser Konvertierung ein Fehler auftritt, wird ein Diagnosedatensatz mit SQLSTATE 22018 und der Meldung "Überlauf im DateTime-Wert Feld" generiert.|  
|4|Wenn der Wert kein gültiger DATE-, timestamp- oder timestampoffset-Wert ist, wird ein Diagnosedatensatz mit SQLSTATE 22018 und der Meldung "Ungültiger Zeichenwert für Konvertierungsangabe" generiert.|  
|5|Wenn die Zeitangabe ungleich Null ist, dann wird ein Diagnosedatensatz mit SQLSTATE 01S07 und der Meldung "Teilbereiche wurden abgeschnitten" generiert.|  
|6|Wenn der Wert kein gültiger Time-, timestamp- oder timestampoffset-Wert ist, wird ein Diagnosedatensatz mit SQLSTATE 22018 und der Meldung "Ungültiger Zeichenwert für Konvertierungsangabe" generiert.|  
|7|Die Datumskomponente wird ignoriert.|  
|8|Wenn die Sekundenbruchteile ungleich Null sind, dann wird ein Diagnosedatensatz mit SQLSTATE 01S07 und der Meldung "Teilbereiche wurden abgeschnitten" generiert.|  
|9|Wenn der Wert kein gültiger DATE-, Time-, timestamp- oder timestampoffset-Wert ist, wird ein Diagnosedatensatz mit SQLSTATE 22018 und der Meldung "Ungültiger Zeichenwert für Konvertierungsangabe" generiert.|  
|10|Wenn der Wert eine gültige Zeitangabe ist, wird die Datumskomponente auf das aktuelle Clientdatum festgelegt.|  
|11|Wenn der Wert ein gültiges Datum ist, wird die Uhrzeitkomponente auf Null festgelegt.|  
|12|Es wird ein Diagnosedatensatz mit SQLSTATE 07006 und der Meldung "Attributverletzung beschränkter Datentypen" generiert.|  
|13|Die Uhrzeit wird auf 0 (Null) festgelegt.|  
|14|Wenn der Puffer nicht groß genug zum Speichern eines SQL_DATE_STRUCT-Werts ist, wird ein Diagnosedatensatz mit SQLSTATE 22003 und der Meldung "Numerischer Wert außerhalb des Gültigkeitsbereichs" generiert.|  
|15|Das Datum wird auf das aktuelle Clientdatum festgelegt.|  
|16|Wenn der Puffer nicht groß genug zum Speichern des konvertierten Zeichenfolgenwerts ist, sondern nur die Sekundenbruchteile aufnehmen kann, dann wird ein Diagnosedatensatz mit SQLSTATE 01004 und der Meldung "Die Zeichenfolgedaten wurden rechts abgeschnitten" generiert. Wenn der Puffer nicht groß genug zum Speichern des Zeichenfolgenwerts ist, ohne dass die Datums-, Uhrzeit- oder Offsetkomponenten abgeschnitten werden, dann wird ein Diagnosedatensatz mit SQLSTATE 22003 und der Meldung "Numerischer Wert außerhalb des Gültigkeitsbereichs" generiert. Beachten Sie, dass für Date- und timestampoffset-Werte SQLSTATE 01004 nicht ausgegeben werden kann, weil sich am rechten Ende der konvertierten Zeichenfolge keine Sekundenbruchteile befinden. Deshalb verursacht jedes Abschneiden Datenverluste.|  
|17|Wenn der Puffer nicht groß genug zum Speichern eines SQL_SS_TIME2_STRUCT-Werts ist, wird ein Diagnosedatensatz mit SQLSTATE 22003 und der Meldung "Numerischer Wert außerhalb des Gültigkeitsbereichs" generiert.|  
|18|Wenn die Zeitangabe ungleich Null ist, dann wird ein Diagnosedatensatz mit SQLSTATE 01S07 und der Meldung "Teilbereiche wurden abgeschnitten" generiert.|  
|19|Wenn der Servertyp datetime oder smalldatetime lautet, entspricht der Wert dem TDS-Übertragungsformat. Für smalldatetime handelt es sich um einen 4-Byte-Wert, für datetime handelt es sich um einen 8-Byte-Wert.<br /><br /> Wenn der Servertyp datetime2 ist, wird der Wert als SQL_TIMESTAMP_STRUCT zurückgegeben. Wenn der Puffer nicht groß genug zum Speichern des zurückgegebenen Werts ist, wird ein Diagnosedatensatz mit SQLSTATE 22003 und der Meldung "Numerischer Wert außerhalb des Gültigkeitsbereichs" generiert.|  
|20|Die Zeitangabe wird in die Clientzeitzone konvertiert. Tritt während dieser Konvertierung ein Fehler auf, wird ein Diagnosedatensatz mit SQLSTATE 22008 und der Meldung "Überlauf im Datetime-Feld" generiert.|  
|21|Wenn der Puffer groß genug ist, um einen SQL_SS_TIMESTAMPOFFSET_STRUCT-Wert aufzunehmen, wird der Wert als SQL_SS_TIMESTAMPOFFSET_STRUCT zurückgegeben. Andernfalls wird ein Diagnosedatensatz mit SQLSTATE 22003 und der Meldung "Numerischer Wert außerhalb des Gültigkeitsbereichs" generiert.|  
|22|Der Wert wird in die Clientzeitzone konvertiert, bevor das Datum extrahiert wird. Dadurch wird für die Konsistenz mit anderen Konvertierungen mit timestampoffset-Typen gesorgt. Tritt während dieser Konvertierung ein Fehler auf, wird ein Diagnosedatensatz mit SQLSTATE 22008 und der Meldung "Überlauf im Datetime-Feld" generiert. Dies könnte in einem Datum resultieren, das sich von dem Wert unterscheidet, der sich durch einfaches Abschneiden ergibt.|  
  
 Die Tabelle in diesem Thema beschreibt die Konvertierung der Typen, die an den Client zurückgegeben werden, aus den in der Bindung verwendeten Typen. Für Output-Parameter Wenn der Servertyp in angegeben SQLBindParameter entspricht nicht dem tatsächlichen Typ auf dem Server, wird eine implizite Konvertierung vom Server ausgeführt werden und die an den Client zurückgegebene Typ entspricht des Typs über SQLBindParameter angegeben. Dies kann zu unerwarteten konvertierungsergebnissen führen, wenn Konvertierungsregeln des Servers aus, die in der obigen Tabelle aufgeführten unterscheiden. Wenn beispielsweise ein Standarddatum bereitgestellt werden muss, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 1900-1-1 statt des aktuellen Datums.  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
