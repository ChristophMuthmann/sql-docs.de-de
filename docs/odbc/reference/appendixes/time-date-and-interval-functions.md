---
title: Uhrzeit-, Datums- und Intervallfunktionen | Microsoft Docs
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
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3d32dc500c2f57919757224d64b3f5c21c6f6423
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="time-date-and-interval-functions"></a>Uhrzeit-, Datums- und Intervallfunktionen
Die folgende Tabelle enthält Datum und Uhrzeit-Funktionen, die in der ODBC-Skalarfunktion Menge enthalten sind. Eine Anwendung kann bestimmen, welche Funktionen für Datum und Uhrzeit durch Aufrufen von einem-Treiber unterstützt werden **SQLGetInfo** mit einem *Informationstyp* von SQL_TIMEDATE_FUNCTIONS.  
  
 Als Argumente bezeichnet *Timestamp_exp* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *ODBC-Zeit-Escape*, *ODBC-Datum-Escape*, oder *ODBC-Zeitstempel-Escape*, in denen die zugrunde liegenden Datentyp als SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE oder SQL_TYPE_TIMESTAMP dargestellt werden konnte.  
  
 Als Argumente bezeichnet *"date_exp"* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *ODBC-Datum-Escape* oder *ODBC-Zeitstempel-Escape*, wobei die zugrunde liegende Datentyp kann als SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE oder SQL_TYPE_TIMESTAMP dargestellt werden.  
  
 Als Argumente bezeichnet *"time_exp"* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *ODBC-Zeit-Escape* oder *ODBC-Zeitstempel-Escape*, wobei die zugrunde liegende Datentyp kann als SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP dargestellt werden.  
  
 CURRENT_DATE, aktuelle_zeit und CURRENT_TIMESTAMP timedate skalare Funktionen wurden in ODBC 3.0 SQL-92 veröffentlichungshäufigkeit hinzugefügt.  
  
|Funktion|Description|  
|--------------|-----------------|  
|**CURRENT_DATE ()** (ODBC 3.0)|Gibt das aktuelle Datum zurück.|  
|**Aktuelle_zeit [(** *zeitgenauigkeit* **)]** (ODBC 3.0)|Gibt die aktuelle lokale Zeit zurück. Die *Zeit mit doppelter Genauigkeit* Argument bestimmt die Sekunden Genauigkeit des zurückgegebenen Werts.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *Zeitstempel mit doppelter Genauigkeit* **)]** (ODBC 3.0)|Gibt die aktuelle lokale Datums- und Ortszeit als eine Timestamp-Wert zurück. Die *Zeitstempel mit doppelter Genauigkeit* Argument bestimmt die Sekunden Genauigkeit des zurückgegebenen Zeitstempels.|  
|**CURDATE ()** (ODBC 1.0)|Gibt das aktuelle Datum zurück.|  
|**CURTIME ()** (ODBC 1.0)|Gibt die aktuelle lokale Zeit zurück.|  
|**DAYNAME (** *"date_exp"* **)** (ODBC 2.0)|Gibt eine Zeichenfolge mit der für die Datenquelle spezifischen Namen des Tags (z. B. Sonntag bis Samstag oder so. bis Sa. für eine Datenquelle, die Englisch oder Sunday bis Saturday für eine Datenquelle verwendet, die Deutsch verwendet) für den Tagteil von *"date_exp"*.|  
|**DAYOFMONTH (** *"date_exp"* **)** (ODBC 1.0)|Gibt den Tag des Monats basierend auf dem Monatsfeld in *"date_exp"* als ganze Zahl im Bereich von 1 bis 31.|  
|**DAYOFWEEK (** *"date_exp"* **)** (ODBC 1.0)|Gibt den Wochentag basierend auf dem wochenfeld in *"date_exp"* als ganze Zahl im Bereich von 1 bis 7, wobei 1 Sonntag darstellt.|  
|**DAYOFYEAR (** *"date_exp"* **)** (ODBC 1.0)|Gibt den Tag des Jahres basierend auf dem Feld "Year" in *"date_exp"* als ganze Zahl im Bereich von 1-366.|  
|**EXTRAHIEREN (** *Extract-Feld FROM* *Extract-Quelle* **)** (ODBC 3.0)|Gibt die *Extract-Feld* Teil der *Extract-Quelle*. Die *Extract-Quelle* Argument ist ein Ausdruck, "DateTime" oder ein Zeitintervall. Die *Extract-Feld* Argument kann eine der folgenden Schlüsselwörter:<br /><br /> JAHR-MONAT TAG STUNDE MINUTE, SEKUNDE<br /><br /> Die Genauigkeit des zurückgegebenen Werts wird die Implementierung definiert. Die Skalierung ist 0, wenn die zweite angegeben wird, in diesem Fall ist die Dezimalstellen nicht kleiner als die Genauigkeit der Sekundenbruchteile von der *Extract-Quelle* Feld.|  
|**Stunde (** *"time_exp"* **)** (ODBC 1.0)|Gibt die Stunde basierend auf dem Stundenfeld in *"time_exp"* als ganze Zahl im Bereich von 0 bis 23.|  
|**MINUTE (** *"time_exp"* **)** (ODBC 1.0)|Gibt die Minute basierend auf dem Minutenfeld in *"time_exp"* als ganze Zahl im Bereich von 0 bis 59.|  
|**Monat (** *"date_exp"* **)** (ODBC 1.0)|Gibt den Monat, basierend auf dem Monatsfeld in *"date_exp"* als ganze Zahl im Bereich von 1 bis 12.|  
|**"MonthName" (** *"date_exp"* **)** (ODBC 2.0)|Gibt eine Zeichenfolge mit der für die Datenquelle spezifischen Namen des Monats (z. B. Januar bis Dezember oder Jan. bis Dezember für eine Datenquelle, die Englisch verwendet, oder January bis December für eine Datenquelle, die Deutsch verwendet) für den Monatsteil von *"date_exp"*.|  
|**(JETZT)** (ODBC 1.0)|Gibt das aktuelle Datum und die Uhrzeit als ein Zeitstempelwert.|  
|**Quartal (** *"date_exp"* **)** (ODBC 1.0)|Gibt das Quartal *"date_exp"* als ganze Zahl im Bereich von 1 bis 4, wobei 1 vom 1. Januar bis 31. März darstellt.|  
|**ZWEITE (** *"time_exp"* **)** (ODBC 1.0)|Gibt die Sekunde basierend auf dem zweiten Feld *"time_exp"* als ganze Zahl im Bereich von 0 bis 59.|
|**TIMESTAMPADD (** *Intervall*, *Integer_exp*, *Timestamp_exp* **)** (ODBC 2.0)|Gibt den Zeitstempel des berechnet, indem *Integer_exp* Intervalle des Typs *Intervall* auf *Timestamp_exp*. Gültige Werte für *Intervall* sind die folgenden Schlüsselwörter:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> wobei Sekundenbruchteile milliardste Teil einer Sekunde ausgedrückt werden. Die folgende SQL-Anweisung gibt z. B. den Namen der einzelnen Mitarbeiter und seine einjähriges Jahrestag:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Wenn *Timestamp_exp* ist ein Zeitwert und *Intervall* gibt an, Tage, Wochen, Monate, Quartale oder Jahre, den Datumsteil des *Timestamp_exp* festgelegt ist, auf das aktuelle Datum vor den resultierenden Zeitstempel zu berechnen.<br /><br /> Wenn *Timestamp_exp* ist ein Datumswert und *Intervall* angegeben Sekundenbruchteile Sekunden, Sekunden, Minuten oder Stunden, den Zeitbereich *Timestamp_exp* auf 0 vor dem festgelegt wird den resultierenden Zeitstempel zu berechnen.<br /><br /> Eine Anwendung bestimmt, welche Intervallen eine Datenquelle, durch den Aufruf unterstützt **SQLGetInfo** mit der Option SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF (** *Intervall*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Gibt die ganze Zahl der Intervalle des Typs *Intervall* nach dem *timestamp_exp2* ist größer als *timestamp_exp1*. Gültige Werte für *Intervall* sind die folgenden Schlüsselwörter:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> wobei Sekundenbruchteile milliardste Teil einer Sekunde ausgedrückt werden. Die folgende SQL-Anweisung gibt z. B. den Namen der einzelnen Mitarbeiter und die Anzahl von Jahren, die er Ausgabeblöcke hat:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Wenn entweder Timestamp-Ausdruck einen Uhrzeitwert ist und *Intervall* Tage, Wochen, Monate, Quartale oder Jahre Datumsteil dieser Zeitstempel wird festgelegt, auf das aktuelle Datum vor dem Berechnen der Differenz zwischen dem Zeitstempel angibt.<br /><br /> Wenn entweder Timestamp-Ausdruck ein Datumswert ist und *Intervall* angegeben Sekundenbruchteile Sekunden Sekunden, Minuten oder Stunden, die Teil dieser Zeitstempel auf 0 festgelegt ist vor dem Berechnen der Differenz zwischen dem Zeitstempel.<br /><br /> Eine Anwendung bestimmt, welche Intervallen eine Datenquelle, durch den Aufruf unterstützt **SQLGetInfo** mit der Option SQL_TIMEDATE_DIFF_INTERVALS.|  
|**Woche (** *"date_exp"* **)** (ODBC 1.0)|Gibt die Woche des Jahres basierend auf dem wochenfeld in *"date_exp"* als ganze Zahl im Bereich von 1 bis 53.|  
|**Jahr (** *"date_exp"* **)** (ODBC 1.0)|Gibt die Jahresangabe basierend auf dem Feld "Year" in *"date_exp"* als ganze Zahl. Der Bereich ist datenquellenabhängig.|
