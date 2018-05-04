---
title: C, um Beispiele für die Konvertierung von SQL-Daten | Microsoft Docs
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
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcba6d92970d0e0b5490f4c24506fe8bb2951217
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-data-conversion-examples"></a>C, um Beispiele für die Konvertierung von SQL-Daten
Die folgenden Beispiele veranschaulichen, wie der Treiber C-Daten in SQL-Daten konvertiert:  
  
|C-Typ-ID|C-Datenwert|SQL-Typ<br /><br /> Bezeichner (identifier)|Column<br /><br /> length|SQL data<br /><br /> Wert|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|–|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8 [b]|1234.56|–|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|–|1234.56|–|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|–|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|–|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|–|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|–|1992-12-31 00:00:00.0|–|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|–|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" stellt ein Null-Terminierung Byte dar. Das Null-Terminierung Byte ist erforderlich, nur, wenn die Länge der Daten SQL_NTS ist.  
  
 [b] neben Bytes für Zahlen 1 Byte für eine Anmeldung erforderlich ist und eine andere Byte für das Dezimaltrennzeichen erforderlich ist.  
  
 [c] die Zahlen in dieser Liste werden die Zahlen in den Feldern der SQL_DATE_STRUCT-Struktur gespeichert.  
  
 [d] die Zahlen in dieser Liste werden die Zahlen in die Felder der Struktur SQL_TIMESTAMP_STRUCT gespeichert.
