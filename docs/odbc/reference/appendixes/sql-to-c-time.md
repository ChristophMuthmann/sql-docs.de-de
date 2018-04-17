---
title: SQL in "c:" Zeit | Microsoft Docs
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
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f8db10d126eab69546b2d81eaf4d93743a63238
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-time"></a>SQL in "c:" Zeit
Der Bezeichner für die Zeit, die ODBC-SQL-Datentyp ist:  
  
 SQL_TYPE_TIME  
  
 Die folgende Tabelle zeigt ODBC C-Datentypen in die SQL-Zeitdaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Pufferlänge* > Byte Zeichenlänge<br /><br /> *9* <= *Pufferlänge* < = Byte Zeichenlänge<br /><br /> *Pufferlänge* < 9|data<br /><br /> Abgeschnittene Daten [a]<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Pufferlänge* > Zeichenlänge<br /><br /> *9* <= *Pufferlänge* < = Zeichenlänge<br /><br /> *Pufferlänge* < 9|data<br /><br /> Abgeschnittene Daten [a]<br /><br /> Nicht definiert|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Keine [b]|data|6 [d]|–|  
|SQL_C_TYPE_TIMESTAMP|Keine [b]|Daten [c#]|16 [d]|–|  
  
 [a] die Sekundenbruchteile der Zeit werden abgeschnitten.  
  
 [b] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [c] Datumsfelder der timestampstruktur werden auf das aktuelle Datum festgelegt, und Feld Sekundenbruchteile von Timestamp-Struktur auf 0 (null) festgelegt ist.  
  
 [d] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 Wenn SQL Zeitdaten in Zeichendaten C konvertiert werden, wird die resultierende Zeichenfolge der "*" hh "*:*mm*:*ss*" Format. Dieses Format wird durch die Einstellung der Windows® Land nicht beeinflusst.
