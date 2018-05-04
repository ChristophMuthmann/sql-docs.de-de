---
title: Uhrzeit und Datumsfunktionen (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b47cd46b93878b6b394d302ff4493a6ec5bbd032
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Uhrzeit und Datumsfunktionen (Visual FoxPro-ODBC-Treiber)
Die folgende Tabelle listet die ODBC-Datum und die Funktionen von der Visual FoxPro-ODBC-Treiber unterstützt; Wenn die Visual FoxPro-Grammatik für dieselbe Funktion aus der ODBC-Syntax unterscheidet, wird der entsprechende Visual FoxPro aufgeführt.  
  
|ODBC-Grammatik|Visual FoxPro-Grammatik|  
|------------------|---------------------------|  
|CURDATE *)*|DATUM *)*|  
|CURTIME *)*|ZEIT *)*|  
|DAYNAME *("date_exp")*|CDOW *("date_exp")*|  
|DAYOFMONTH (*"date_exp")*|TAG *)*|  
|Stunde *("time_exp")*||  
|MINUTE *("time_exp")*||  
|Monat *("time_exp")*||  
|"MonthName"*("date_exp")*|CMONTH *("date_exp")*|  
|JETZT *)*|"DATETIME"*)*|  
|ZWEITE *("time_exp")*|S *("time_exp")*|  
|Woche *("date_exp")*||  
|Jahr *("date_exp")*||  
  
 Die folgenden Funktionen für Datum und Uhrzeit werden nicht unterstützt:  
  
 DAYOFYEAR *("date_exp")*  
  
 Quartal *("date_exp")*  
  
 TIMESTAMPADD *(Intervall, Integer_exp, Timestamp_exp)*  
  
 TIMESTAMPDIFF *(Intervall, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Escapesequenzen für ODBC  
 Der Treiber unterstützt auch die ODBC-Escapesequenz für Datums- und Zeitstempel. Die Escape-Klausel-Syntax lautet wie folgt:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 In dieser Syntax **d** gibt an, dass *Wert* ein Datum in der *jjjj-mm-tt* Format und **ts** gibt an, dass *Wert*  ist ein Zeitstempel in der *jjjj-mm-tt hh: mm:*[.*f...*] Format. Die kurznotationssyntax für Datums- und Zeitstempel lautet wie folgt:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Jede der folgenden Anweisungen aktualisiert z. B. die ALLTYPES-Tabelle mithilfe von Kurzsyntax Datums- und Zeitstempel in einem unterstützten SQL-UPDATE-Befehl:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zu Escapesequenzen finden Sie unter [in ODBC-Escapesequenzen](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) in der *ODBC Programmer's Reference*.
