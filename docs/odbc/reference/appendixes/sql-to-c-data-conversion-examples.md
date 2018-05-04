---
title: SQL, um Beispiele für die Konvertierung von C-Daten | Microsoft Docs
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
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a2fa699cb8d57e9ec44ec133ec766b70414e00b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-data-conversion-examples"></a>SQL, um Beispiele für die Konvertierung von C-Daten
Die in der folgenden Tabelle dargestellten Beispiele veranschaulichen, wie der Treiber SQL-Daten in C-Daten konvertiert:  
  
|SQL-Typ<br /><br /> Bezeichner (identifier)|SQL data<br /><br /> Wert|C-Typ<br /><br /> Bezeichner (identifier)|Puffer<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|–|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56\0 [a]|–|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|wird ignoriert.|1234.56|–|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|wird ignoriert.|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|wird ignoriert.|----|22003|  
SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|wird ignoriert.|1.2345678|–|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|wird ignoriert.|1.234567|–|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|wird ignoriert.|1|–|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|–|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|wird ignoriert.|1992,12,31, 0,0,0,0 [b]|–|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12\0 [a]|–|  
SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1\0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\0" stellt ein Null-Terminierung Byte dar. Der Treiber beendet Null immer SQL_C_CHAR-Daten.  
  
 [b] die Zahlen in dieser Liste werden die Zahlen in den Feldern der TIMESTAMP_STRUCT Struktur gespeichert.
