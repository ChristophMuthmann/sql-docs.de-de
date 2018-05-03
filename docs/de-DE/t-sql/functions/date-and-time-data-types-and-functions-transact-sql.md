---
title: Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7dae37763b4a4ef372964ad3990fa77adaae1f0d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Die folgenden Abschnitte in diesem Thema enthalten eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)].
-   [Datums- und Uhrzeitdatentypen:](#DateandTimeDataTypes)  
-   [Datums- und Uhrzeitfunktionen](#DateandTimeFunctions)  
    -   [Funktion, die Systemdatums- und Systemzeitwerte abruft](#GetSystemDateandTimeValues)  
    -   [Funktionen, die Datums- und Uhrzeitteile abrufen](#GetDateandTimeParts)  
    -   [Funktionen, die Datums- und Uhrzeitwerte aus ihren Teilen abrufen](#fromParts)  
    -   [Funktionen, die Datums- und Uhrzeitdifferenzen abrufen](#GetDateandTimeDifference)  
    -   [Funktionen, die Datums- und Uhrzeitwerte ändern](#ModifyDateandTimeValues)  
    -   [Funktionen, die Sitzungsformatfunktionen festlegen oder abrufen](#SetorGetSessionFormatFunctions)  
    -   [Funktionen, die Datums- und Uhrzeitwerte überprüfen](#ValidateDateandTimeValues)  
-   [Datums- und uhrzeitbezogene Themen](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a> Datums- und Uhrzeitdatentypen
In der folgenden Tabelle werden die Datums- und Uhrzeitdatentypen von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgelistet:
  
|Datentyp|Format|Bereich|Genauigkeit|Speichergröße (Bytes)|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|Zeitzonenoffset|  
|---|---|---|---|---|---|---|
|[Uhrzeit](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 bis 23:59:59.9999999|100 Nanosekunden|3 bis 5|ja|nein|  
|[Datum](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 bis 9999-12-31|1 Tag|3|nein|nein|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 bis 2079-06-06|1 Minute|4|nein|nein|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 bis 9999-12-31|0,00333 Sekunden|8|nein|nein|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 bis 9999-12-31 23:59:59.9999999|100 Nanosekunden|6 bis 8|ja|nein|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|0001-01-01 00:00:00.0000000 bis 9999-12-31 23:59:59.9999999 (in UTC)|100 Nanosekunden|8 bis 10|ja|ja|  
  
> [!NOTE]  
>  Der [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md)-Datentyp ist kein Datums- oder Uhrzeitdatentyp. **timestamp** ist ein veraltetes Synonym für **rowversion**.  
  
##  <a name="DateandTimeFunctions"></a> Datums- und Uhrzeitfunktionen  
In den folgenden Tabellen werden die Datums- und Uhrzeitfunktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgelistet. Weitere Informationen zu deterministischen Funktionen finden Sie unter [Deterministische und nicht deterministische Funktionen](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
###  <a name="GetSystemDateandTimeValues"></a> Funktionen, die Systemdatums- und Systemzeitwerte abrufen 
Alle Systemdatums- und Systemzeitwerte werden aus dem Betriebssystem des Computers abgeleitet, auf dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ausgeführt wird.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Systemdatums- und Systemuhrzeitfunktionen mit höherer Genauigkeit  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ruft die Datums- und Zeitwerte mithilfe der GetSystemTimeAsFileTime()-Windows-API ab. Die Genauigkeit hängt von der Computerhardware und der Windows-Version ab, unter der die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Die Genauigkeit dieser API liegt bei 100 Nanosekunden. Die Genauigkeit kann mithilfe der GetSystemTimeAdjustment()-Windows-API festgestellt werden.
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Gibt einen **datetime2(7)**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime2(7)**|Nicht deterministisch|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Gibt einen **datetimeoffset(7)**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird einbezogen.|**datetimeoffset(7)**|Nicht deterministisch|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Gibt einen **datetime2(7)**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Das Datum und die Uhrzeit werden als UTC-Zeit (Koordinierte Weltzeit) zurückgegeben.|**datetime2(7)**|Nicht deterministisch|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>Systemdatums- und Systemuhrzeitfunktionen mit geringerer Genauigkeit
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Gibt einen **datetime**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime**|Nicht deterministisch|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Gibt einen **datetime**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime**|Nicht deterministisch|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Gibt einen **datetime**-Wert zurück, der das Datum und die Uhrzeit des Computers enthält, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Das Datum und die Uhrzeit werden als UTC-Zeit (Koordinierte Weltzeit) zurückgegeben.|**datetime**|Nicht deterministisch|  
  
###  <a name="GetDateandTimeParts"></a> Funktionen, die Datums- und Uhrzeitteile abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *date* )|Gibt eine Zeichenfolge zurück, die den angegebenen *datepart*-Wert des angegebenen Datums darstellt.|**nvarchar**|Nicht deterministisch|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *date* )|Gibt einen Integer zurück, der den angegebenen *datepart*-Wert des angegebenen *date*-Werts darstellt.|**int**|Nicht deterministisch|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|Gibt eine ganze Zahl zurück, die die Tagesangabe des angegebenen *date*-Werts darstellt.|**int**|Deterministisch|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|Gibt einen Integer zurück, der den Monatsteil des angegebenen *Datums* darstellt.|**int**|Deterministisch|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|Gibt einen Integer zurück, der den Jahresteil des angegebenen *Datums* darstellt.|**int**|Deterministisch|  
  
###  <a name="fromParts"></a> Funktionen, die Datums- und Uhrzeitwerte aus ihren Teilen abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS  ( *year*, *month*, *day* )|Gibt einen **date**-Wert für das angegebene Jahr, den Monat und den Tag zurück.|**Datum**|Deterministisch|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *precision*)|Gibt einen **datetime2**-Wert für das angegebene Datum und die angegebene Uhrzeit mit der angegebenen Genauigkeit zurück.|**datetime2(** *precision* **)**|Deterministisch|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *milliseconds*)|Gibt einen **datetime**-Wert für das angegebene Datum und die Uhrzeit zurück.|**datetime**|Deterministisch|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *hour_offset*, *minute_offset*, *precision*)|Gibt einen **datetimeoffset**-Wert für das angegebene Datum und die angegebene Uhrzeit mit dem angegebenen Offset und der angegebenen Genauigkeit zurück.|**datetimeoffset(** *Genauigkeit* **)**|Deterministisch|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute* )|Gibt einen **smalldatetime**-Wert für das angegebene Datum und die Uhrzeit zurück.|**smalldatetime**|Deterministisch|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS  ( *hour*, *minute*, *seconds*, *fractions*, *precision* )|Gibt einen **time**-Wert für die angegebene Uhrzeit mit der angegebenen Genauigkeit zurück.|**time(** *precision* **)**|Deterministisch|  
  
###  <a name="GetDateandTimeDifference"></a> Funktionen, die Datums- und Uhrzeitdifferenzen abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|Gibt die Anzahl der Datums- oder Zeitbegrenzungen von *datepart* zurück, die zwischen zwei angegebenen Daten überschritten wurden.|**int**|Deterministisch|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|Gibt die Anzahl der Datums- oder Zeitbegrenzungen von *datepart* zurück, die zwischen zwei angegebenen Daten überschritten wurden.|**bigint**|Deterministisch|  
  
###  <a name="ModifyDateandTimeValues"></a> Funktionen, die Datums- und Uhrzeitwerte ändern
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *number* , *date* )|Gibt einen neuen **datetime**-Wert zurück. Dazu wird dem angegebenen *datepart*-Wert des angegebenen *date*-Werts ein Intervall hinzugefügt.|Der Datentyp des *date*-Arguments|Deterministisch|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH  ( *start_date* [, *month_to_add* ] )|Gibt den letzten Tag des Monats, der das angegebene Datum enthält, mit einem optionalen Versatz zurück.|Der Rückgabetyp ist der Typ von *start_date* oder **date**.|Deterministisch|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCH*OFFSET* (*DATETIMEOFFSET* , *time_zone*)|SWITCH*OFFSET* ändert den Zeitzonenoffset eines DATETIMEOFFSET-Werts und behält den UTC-Wert bei.|**datetimeoffset** mit der Genauigkeit von Bruchteilen von *DATETIMEOFFSET*|Deterministisch|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression* , *time_zone*)|TODATETIMEOFFSET wandelt einen datetime2-Wert in einen datetimeoffset-Wert um. Der datetime2-Wert wird in Ortszeit für die angegebene time_zone interpretiert.|**datetimeoffset** mit der Genauigkeit von Bruchteilen des *datetime*-Arguments|Deterministisch|  
  
###  <a name="SetorGetSessionFormatFunctions"></a> Funktionen, die das Sitzungsformat festlegen oder abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Gibt den für die Sitzung aktuellen Wert von SET DATEFIRST zurück.|**tinyint**|Nicht deterministisch|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *number* &#124; **@***number_var* }|Legt den ersten Wochentag auf eine Zahl von 1 bis 7 fest.|Nicht verfügbar|Nicht verfügbar|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *format* &#124; **@***format_var* }|Legt die Reihenfolge der Datumsbestandteile (Tag, Monat, Jahr) für die Eingabe von **datetime**- oder **smalldatetime**-Daten fest.|Nicht verfügbar|Nicht verfügbar|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Gibt den Namen der zurzeit verwendeten Sprache zurück. @@LANGUAGE ist keine Datums- oder Uhrzeitfunktion. Die Spracheinstellung kann sich jedoch auf die Ausgabe von Datumsfunktionen auswirken.|Nicht verfügbar|Nicht verfügbar|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE { [ N ] **'***language***'** &#124; **@***language_var* }|Legt die Sprachumgebung für die Sitzung und die Systemmeldungen fest. SET LANGUAGE ist keine Datums- oder Uhrzeitfunktion. Die Spracheinstellung wirkt sich jedoch auf die Ausgabe von Datumsfunktionen aus.|Nicht verfügbar|Nicht verfügbar|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [ [ **@language =** ] **'***language***'** ]|Gibt Informationen den Datumsformaten aller unterstützten Sprachen zurück. **sp_helplanguage** ist keine gespeicherte Prozedur für Datum oder Uhrzeit. Die Spracheinstellung wirkt sich jedoch auf die Ausgabe von Datumsfunktionen aus.|Nicht verfügbar|Nicht verfügbar|  
  
###  <a name="ValidateDateandTimeValues"></a> Funktionen, die Datums- und Uhrzeitwerte überprüfen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expression* )|Bestimmt, ob ein **datetime** oder **smalldatetime**-Eingabeausdruck ein gültiger Datums- oder Uhrzeitwert ist.|**int**|ISDATE ist nur deterministisch bei Verwendung mit der CONVERT-Funktion, wenn der style-Parameter von CONVERT angegeben wird und style nicht den Wert 0, 100, 9 oder 109 aufweist.|  
  
##  <a name="DateandTimeRelatedTopics"></a> Datums- und uhrzeitbezogene Themen 
  
|Thema|Description|  
|-----------|-----------------|  
|[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Stellt Informationen zur Konvertierung von Datums- und Uhrzeitwerten in und aus Zeichenfolgenliteralen und anderen Datums- und Uhrzeitformaten bereit.|  
|[Schreiben internationaler Transact-SQL-Anweisungen](../../relational-databases/collations/write-international-transact-sql-statements.md)|Stellt Richtlinien für die sprachübergreifende Portabilität von Datenbanken und Datenbankanwendungen bereit, die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwenden bzw. mehrere Sprachen unterstützen.|  
|[ODBC-Skalarfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Stellt Informationen zu ODBC-Skalarfunktionen bereit, die in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwendet werden können. Dies schließt ODBC-Datums- und -Uhrzeitfunktionen ein.|  
|[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Stellt den Zeitzonenwechsel zur Verfügung.|  
  
## <a name="see-also"></a>Siehe auch
[Funktionen](../../t-sql/functions/functions.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
