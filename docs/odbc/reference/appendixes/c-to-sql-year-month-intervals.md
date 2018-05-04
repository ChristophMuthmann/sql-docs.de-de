---
title: 'C, um SQL: Jahr-Monat-Intervallen | Microsoft Docs'
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
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26645ddb4e27335a33aec88f002764d20da3d936
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-year-month-intervals"></a>C, um SQL: Jahr-Monat-Intervallen
Der Bezeichner für die Jahr-Monat-Intervall ODBC C-Datentypen sind:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen in die Jahr-Monat-C-Intervalldaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|Byte-Spaltenlänge > = Byte Zeichenlänge<br /><br /> Spalte Bytelänge < Zeichenlänge Byte [a]<br /><br /> Datenwert ist es sich nicht um ein gültiges Zeichenfolgenliteral Intervall|–<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|Zeichenlänge Spalte > = Zeichenlänge von Daten<br /><br /> Zeichenlänge der Spalte < Zeichenlänge von Daten [a]<br /><br /> Datenwert ist es sich nicht um ein gültiges Zeichenfolgenliteral Intervall|–<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|Die Konvertierung eines Intervalls Einzelfeld führten nicht Abschneiden von ganzen Zahlen<br /><br /> Konvertierung Verzeichnisdiensts Abschneiden von ganzen Zahlen|–<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Datenwert wurde ohne Abschneiden jedes konvertiert.<br /><br /> Ein oder mehrere Felder Datenwerts wurden während der Konvertierung abgeschnitten.|–<br /><br /> 22015|  
  
 [a] alle C-Intervall-Datentypen können in einen Zeichendatentyp konvertiert werden.  
  
 [b] ist das Typfeld in der Struktur Intervall, für die das Intervall ein einzelnes Feld (SQL_YEAR oder SQL_MONTH) entspricht, kann der Intervalltyp C in genauen numerischen (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL oder SQL_NUMERIC) konvertiert werden.  
  
 Die Standard-Konvertierung eines Intervalls C-Typ ist für das entsprechende Jahr-Monat-Intervall SQL-Typ.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus dem Intervall C-Datentyp zu konvertieren und setzt voraus, dass die Größe des Datenpuffers die Größe des Intervalls C-Datentyp ist. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.
