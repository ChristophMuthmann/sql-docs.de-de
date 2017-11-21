---
title: "Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Die folgenden Abschnitte in diesem Thema enthalten eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)].
-   [Datum und Uhrzeit-Datentypen](#DateandTimeDataTypes)  
-   [Datums- und Zeitfunktionen](#DateandTimeFunctions)  
    -   [Funktion, die Systemdatums- und Systemzeitwerte Werte](#GetSystemDateandTimeValues)  
    -   [Funktionen, die Datum abrufen und Uhrzeitteile](#GetDateandTimeParts)  
    -   [Funktionen, die Datums- und Uhrzeitwerte aus ihren Teilen abrufen](#fromParts)  
    -   [Funktionen, Abrufen von Datum, und Uhrzeit Unterschied](#GetDateandTimeDifference)  
    -   [Funktionen, die geändert werden Datum und Uhrzeit-Werte](#ModifyDateandTimeValues)  
    -   [Funktionen, die festlegen oder Abrufen von Sitzungsformatfunktionen](#SetorGetSessionFormatFunctions)  
    -   [Funktionen, mit denen überprüft Datum und Uhrzeit-Werte](#ValidateDateandTimeValues)  
-   [Datums- und Uhrzeitbezogene Themen](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>Datum und Uhrzeit-Datentypen
Die [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Zeitdatentypen sind in der folgenden Tabelle aufgeführt:
  
|Datentyp|Format|Bereich|Genauigkeit|Speichergröße (Bytes)|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|Zeitzonenoffset|  
|---|---|---|---|---|---|---|
|[Uhrzeit](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 bis 23:59:59.9999999|100 Nanosekunden|3 bis 5|ja|Nein|  
|[Datum](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 bis 9999-12-31|1 Tag|3|Nein|Nein|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 bis 2079-06-06|1 Minute|4|Nein|Nein|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 bis 9999-12-31|0,00333 Sekunden|8|Nein|Nein|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 bis 9999-12-31 23:59:59.9999999|100 Nanosekunden|6 bis 8|ja|Nein|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|JJJJ-MM-TT HH: mm: [.nnnnnnn] [+ &#124;-] hh: mm|0001-01-01 00:00:00.0000000 bis 9999-12-31 23:59:59.9999999 (in UTC)|100 Nanosekunden|8 bis 10|ja|ja|  
  
> [!NOTE]  
>  Die [!INCLUDE[tsql](../../includes/tsql-md.md)] [Rowversion](../../t-sql/data-types/rowversion-transact-sql.md) Datentyp ist nicht mit einem Datentyp Datum oder Uhrzeit. **Zeitstempel** ist ein veraltetes Synonym für **Rowversion**.  
  
##  <a name="DateandTimeFunctions"></a>Datums- und Zeitfunktionen  
In den folgenden Tabellen werden die Datums- und Uhrzeitfunktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgelistet. Weitere Informationen zum Determinismus finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
###  <a name="GetSystemDateandTimeValues"></a>Funktionen, die System Datums-und Uhrzeitwerte abrufen 
Alle Systemdatums- und Systemzeitwerte werden aus dem Betriebssystem des Computers abgeleitet, auf dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ausgeführt wird.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Systemdatums- und Systemuhrzeitfunktionen mit höherer Genauigkeit  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Ruft das Datum und Uhrzeit-Werte mithilfe der Windows-API für GetSystemTimeAsFileTime() ab. Die Genauigkeit hängt von der Computerhardware und der Windows-Version ab, unter der die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Die Genauigkeit dieser API liegt bei 100 Nanosekunden. Die Genauigkeit kann mithilfe der Windows-API für GetSystemTimeAdjustment() ermittelt werden.
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Gibt eine **datetime2(7)** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime2(7)**|Nicht deterministisch|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Gibt eine **datetimeoffset(7)** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird einbezogen.|**DateTimeOffset(7)**|Nicht deterministisch|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Gibt eine **datetime2(7)** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Das Datum und die Uhrzeit wird als UTC-Zeit (Coordinated Universal Time) zurückgegeben.|**datetime2(7)**|Nicht deterministisch|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>Mit geringerer Genauigkeit Datums- und Zeitfunktionen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Gibt eine **"DateTime"** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime**|Nicht deterministisch|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Gibt eine **"DateTime"** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird nicht einbezogen.|**datetime**|Nicht deterministisch|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Gibt eine **"DateTime"** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Das Datum und die Uhrzeit wird als UTC-Zeit (Coordinated Universal Time) zurückgegeben.|**datetime**|Nicht deterministisch|  
  
###  <a name="GetDateandTimeParts"></a>Funktionen, die Datums- und Uhrzeitteile abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *Datepart* , *Datum* )|Gibt eine Zeichenfolge, die den angegebenen darstellt *Datepart* des angegebenen Datums.|**nvarchar**|Nicht deterministisch|  
|[DATEPART-WERT](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *Datepart* , *Datum* )|Gibt eine ganze Zahl, die den angegebenen darstellt *Datepart* des angegebenen *Datum*.|**int**|Nicht deterministisch|  
|[TAG](../../t-sql/functions/day-transact-sql.md)|Tag ( *Datum* )|Gibt eine ganze Zahl, die den Tagesteil des angegebenen darstellt *Datum*.|**int**|Deterministisch|  
|[MONAT](../../t-sql/functions/month-transact-sql.md)|Monat ( *Datum* )|Gibt eine ganze Zahl, die die Monatsangabe eines angegebenen darstellt *Datum*.|**int**|Deterministisch|  
|[JAHR](../../t-sql/functions/year-transact-sql.md)|Jahr ( *Datum* )|Gibt eine ganze Zahl, die für die Jahresangabe eines angegebenen *Datum*.|**int**|Deterministisch|  
  
###  <a name="fromParts"></a>Funktionen, die Datums-und Uhrzeitwerte aus ihren Teilen abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS ( *Jahr*, *Monat*, *Tag* )|Gibt eine **Datum** Wert für den angegebenen Werten für Jahr, Monat und Tag.|**Datum**|Deterministisch|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS ( *Jahr*, *Monat*, *Tag*, *Stunde*, *Minute*, *Sekunden* , *Brüche*, *Genauigkeit*)|Gibt eine **datetime2** -Wert für das angegebene Datum und die Uhrzeit mit der angegebenen Genauigkeit.|**datetime2 (** *Genauigkeit* **)**|Deterministisch|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS ( *Jahr*, *Monat*, *Tag*, *Stunde*, *Minute*, *Sekunden* , *Millisekunden*)|Gibt eine **"DateTime"** Wert für das angegebene Datum und die Uhrzeit.|**datetime**|Deterministisch|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS ( *Jahr*, *Monat*, *Tag*, *Stunde*, *Minute*,  *Sekunden*, *Brüche*, *Hour_offset*, *Minute_offset*, *Genauigkeit*)|Gibt eine **"DateTimeOffset"** -Wert für das angegebene Datum und die Uhrzeit mit den angegebenen Offsets und die Genauigkeit.|**"DateTime" (** *Genauigkeit* **)**|Deterministisch|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS ( *Jahr*, *Monat*, *Tag*, *Stunde*, *Minute* )|Gibt eine **Smalldatetime** Wert für das angegebene Datum und die Uhrzeit.|**smalldatetime**|Deterministisch|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS ( *Stunde*, *Minute*, *Sekunden*, *Brüche*, *Genauigkeit* )|Gibt eine **Zeit** Wert für die angegebene Zeit und mit der angegebenen Genauigkeit.|**Zeit (** *Genauigkeit* **)**|Deterministisch|  
  
###  <a name="GetDateandTimeDifference"></a>Funktionen, die Datums- und Zeitunterschiede abrufen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *Datepart* , *"StartDate"* , *Enddate* )|Gibt die Anzahl der Datums- oder Zeitangabe *Datepart* Grenzen, die zwischen zwei angegebenen Daten überschritten wurden.|**int**|Deterministisch|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *Datepart* , *"StartDate"* , *Enddate* )|Gibt die Anzahl der Datums- oder Zeitangabe *Datepart* Grenzen, die zwischen zwei angegebenen Daten überschritten wurden.|**bigint**|Deterministisch|  
  
###  <a name="ModifyDateandTimeValues"></a>Funktionen, die Datums-und Uhrzeitwerte ändern
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*Datepart* , *Anzahl* , *Datum* )|Gibt eine neue **"DateTime"** Wert durch Hinzufügen eines Intervalls zum angegebenen *Datepart* des angegebenen *Datum*.|Der Datentyp der *Datum* Argument|Deterministisch|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *Start_date* [, *Month_to_add* ])|Gibt den letzten Tag des Monats, der das angegebene Datum enthält, mit einem optionalen Versatz zurück.|Rückgabetyp ist der Typ der *Start_date* oder **Datum**.|Deterministisch|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCH*OFFSET* (*"DateTimeOffset"* , *Time_zone*)|SWITCH*OFFSET* ändert den Zeitzonenoffset eines DATETIMEOFFSET-Werts und behält den UTC-Wert.|**"DateTimeOffset"** mit der Genauigkeit von Bruchteilen der *"DateTimeOffset"*|Deterministisch|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*Ausdruck* , *Time_zone*)|TODATETIMEOFFSET wandelt einen datetime2-Wert in einen datetimeoffset-Wert um. Der datetime2-Wert wird in Ortszeit für die angegebene time_zone interpretiert.|**"DateTimeOffset"** mit der Genauigkeit von Bruchteilen der *"DateTime"* Argument|Deterministisch|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>Funktionen, die sitzungsformat abrufen oder festlegen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Gibt den für die Sitzung aktuellen Wert von SET DATEFIRST zurück.|**tinyint**|Nicht deterministisch|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *Anzahl* &#124;  **@**  *Number_var* }|Legt den ersten Wochentag auf eine Zahl von 1 bis 7 fest.|Nicht verfügbar|Nicht verfügbar|  
|[SET DATEFORMAT-EINSTELLUNG](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *Format* &#124;  **@**  *Format_var* }|Legt die Reihenfolge der Datumsbestandteile (Tag/Monat/Jahr) für das Eingeben von **"DateTime"** oder **Smalldatetime** Daten.|Nicht verfügbar|Nicht verfügbar|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Gibt den Namen der Sprache, die derzeit verwendet wird. @@LANGUAGE ist keine Datums- oder Funktion. Die Spracheinstellung kann sich jedoch auf die Ausgabe von Datumsfunktionen auswirken.|Nicht verfügbar|Nicht verfügbar|  
|[SET-SPRACHE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] **"***Sprache***"** &#124;  **@**  *Language_var* }|Legt die Sprachumgebung für die Sitzung und die Systemmeldungen fest. SET LANGUAGE ist keine Datums- oder Uhrzeitfunktion. Die Spracheinstellung wirkt sich jedoch auf die Ausgabe von Datumsfunktionen aus.|Nicht verfügbar|Nicht verfügbar|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**Sp_helplanguage** [[  **@language =** ] **"***Sprache***"** ]|Gibt Informationen den Datumsformaten aller unterstützten Sprachen zurück. **Sp_helplanguage** ist kein Datum oder Uhrzeit gespeicherten Prozedur. Die Spracheinstellung wirkt sich jedoch auf die Ausgabe von Datumsfunktionen aus.|Nicht verfügbar|Nicht verfügbar|  
  
###  <a name="ValidateDateandTimeValues"></a>Funktionen, die Datums-und Uhrzeitwerte überprüfen
  
|Funktion|Syntax|Rückgabewert|Rückgabedatentyp|Determinismus|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *Ausdruck* )|Bestimmt, ob eine **"DateTime"** oder **Smalldatetime** -Eingabeausdruck ein gültiger Datums- oder Zeitwert.|**int**|ISDATE ist nur deterministisch bei Verwendung mit der CONVERT-Funktion, wenn der style-Parameter von CONVERT angegeben wird und style nicht den Wert 0, 100, 9 oder 109 aufweist.|  
  
##  <a name="DateandTimeRelatedTopics"></a>Datum und Uhrzeit-Themen 
  
|Thema|Description|  
|-----------|-----------------|  
|[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Stellt Informationen zur Konvertierung von Datums- und Uhrzeitwerten in und aus Zeichenfolgenliteralen und anderen Datums- und Uhrzeitformaten bereit.|  
|[Schreiben internationaler Transact-SQL-Anweisungen](../../relational-databases/collations/write-international-transact-sql-statements.md)|Enthält Richtlinien für die Portabilität von Datenbanken und datenbankanwendungen, mit denen [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen von einer Sprache in eine andere bzw. unterstützen mehrere Sprachen.|  
|[ODBC-Skalarfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Enthält Informationen zu ODBC-Skalarfunktionen aufgelistet, die in zu verwendenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen. Dies schließt ODBC-Funktionen für Datum und Uhrzeit.|  
|[ZEITZONE &AMP; #40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Stellt die Konvertierung der Zeitzone.|  
  
## <a name="see-also"></a>Siehe auch
[Funktionen](../../t-sql/functions/functions.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

