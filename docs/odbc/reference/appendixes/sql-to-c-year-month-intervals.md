---
title: SQL in "c:" Jahr-Monat-Intervallen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 680143b9cc20b910e65218bfe222bd43654bcb21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-year-month-intervals"></a>SQL in Intervallen von "c:" Jahr-Monat
Der Bezeichner für die Jahr-Monat-Intervall ODBC SQL-Datentypen sind:  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in die Jahr-Monat-Intervall SQL-Daten konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|Nachfolgende Felder Teil nicht abgeschnitten.<br /><br /> Nachfolgende Felder Teil abgeschnitten<br /><br /> Führende Genauigkeit des Ziels ist nicht groß genug zum Speichern von Daten aus der Quelle|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> Der SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|Intervall Genauigkeit wurde ein einzelnes Feld und die Daten ohne Abschneiden konvertiert wurde<br /><br /> Intervall Genauigkeit wurde ein einzelnes Feld und das gesamte abgeschnittene<br /><br /> Intervall Genauigkeit war es sich nicht um ein einzelnes Feld|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Länge der Daten in bytes<br /><br /> Größe der C-Datentyp|–<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_CHAR|Zeichenlänge des Byte < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Zeichenlänge des < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
  
 [a] ein Jahr-Monat-Intervall SQL-Typ kann auf einen beliebigen Jahr-Monat-Intervall C-Typ konvertiert werden.  
  
 [b] Wenn die Intervall-Genauigkeit ein einzelnes Feld (eine Jahr oder Monat) ist, kann das Intervall für den SQL in einer beliebigen exakten numerischen (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG oder SQL_C_NUMERIC) konvertiert werden.  
  
 Die Standard-Konvertierung eines Intervalls SQL-Typ ist in den entsprechenden Datentyp der C-Intervall. Die Anwendung dann bindet die Spalte oder Parameter (oder legt das SQL_DESC_DATA_PTR-Feld in den entsprechenden Datensatz von der ARD), zeigen Sie auf die initialisierte SQL_INTERVAL_STRUCT-Struktur (oder übergibt einen Zeiger auf die SQL_ INTERVAL_STRUCT-Struktur wie die *TargetValuePtr* Argument in einem Aufruf von **SQLGetData**).
