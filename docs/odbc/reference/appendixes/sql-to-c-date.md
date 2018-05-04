---
title: SQL bisheriges "c:" | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d99ebd45ffa463ccfd66bd751dd7415b35a8f5d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-date"></a>SQL bisheriges "c:"
Der Bezeichner für das Datum, an die ODBC-SQL-Datentyp ist:  
  
 SQL_TYPE_DATE  
  
 In der folgenden Tabelle zeigt den ODBC C-Datentypen, die in denen Datum SQL-Daten konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Pufferlänge* > Byte Zeichenlänge<br /><br /> 11 < = *Pufferlänge* < = Byte Zeichenlänge<br /><br /> *Pufferlänge* < 11|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|10<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Pufferlänge* > Zeichenlänge<br /><br /> 11 < = *Pufferlänge* < = Zeichenlänge<br /><br /> *Pufferlänge* < 11|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|10<br /><br /> Länge der Daten in Zeichen<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Keine [a]|data|6 [c]|–|  
|SQL_C_TYPE_TIMESTAMP|Keine [a]|Daten [b]|16 [c]|–|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b der timestampstruktur] Zeitfelder werden auf 0 (null) festgelegt.  
  
 [c] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 Wenn in Zeichendaten C Datum SQL-Daten konvertiert wird, wird die resultierende Zeichenfolge der "*Yyyy*-*mm*-*Dd*" Format. Dieses Format wird durch die Einstellung der Windows® Land nicht beeinflusst.
