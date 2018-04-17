---
title: 'C, um SQL: Zeit | Microsoft Docs'
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
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7079b266442b3ca766a9bb5aa38cb45d07fa41c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-time"></a>C, um SQL: Uhrzeit
Der Bezeichner für die Zeit ODBC C-Datentyp ist:  
  
 SQL_C_TYPE_TIME  
  
 In der folgenden Tabelle wird gezeigt, auf die ODBC-SQL-Datentypen in die C-Zeitdaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Byte-Spaltenlänge > = 8<br /><br /> Spalte Byte Länge < 8<br /><br /> Datenwert ist nicht gültig|–<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Zeichenlänge Spalte > = 8<br /><br /> Spalte Zeichen Länge < 8<br /><br /> Datenwert ist nicht gültig|–<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Datenwert ist gültig<br /><br /> Datenwert ist nicht gültig|–<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Datenwert ist gültig [a]<br /><br /> Datenwert ist nicht gültig|–<br /><br /> 22007|  
  
 [a] das Datum, die Teil des Zeitstempels festgelegt ist, um das aktuelle Datum und die Sekundenbruchteile, die Teil der Zeitstempel auf 0 (null) festgelegt ist.  
  
 Informationen, welche Werte in einer Struktur SQL_C_TYPE_TIME gültig sind, finden Sie unter [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md)weiter oben in diesem Anhang.  
  
 Wenn Zeitdaten C in SQL-Zeichendaten konvertiert werden, werden die resultierende Zeichendaten der "*" hh "*:*mm*:*ss*" Format.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, beim Konvertieren von Daten von der Zeit, C-Datentyp, und setzt voraus, dass die Größe des Datenpuffers die Größe des Datentyps Zeit C ist. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.
