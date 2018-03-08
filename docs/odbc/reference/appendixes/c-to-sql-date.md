---
title: 'C, um SQL: Datum | Microsoft Docs'
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
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba2869a8fb8272251f6a23df0808b12e68ec5a59
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-date"></a>C, um SQL: Datum
Der Bezeichner für die Date ODBC C-Datentyp ist:  
  
 SQL_C_TYPE_DATE  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in denen Datum C-Daten konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Byte-Spaltenlänge > = 10<br /><br /> Spalte Byte Länge < 10<br /><br /> Datenwert ist kein gültiges Datum|–<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Zeichenlänge Spalte > = 10<br /><br /> Spalte Zeichen Länge < 10<br /><br /> Datenwert ist kein gültiges Datum|–<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Datenwert ist ein gültiges Datum<br /><br /> Datenwert ist kein gültiges Datum|–<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Datenwert ist ein gültiges Datum [a]<br /><br /> Datenwert ist kein gültiges Datum|–<br /><br /> 22007|  
  
 [a] den Uhrzeitteil des Zeitstempels auf 0 (null) festgelegt ist.  
  
 Informationen, welche Werte in einer Struktur SQL_C_TYPE_DATE gültig sind, finden Sie unter [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md)weiter oben in diesem Anhang.  
  
 Wenn Datumsdaten C in SQL-Zeichendaten konvertiert werden, werden die resultierende Zeichendaten der "*Yyyy*-*mm*-*Dd*" Format.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus den Date-C-Datentyp zu konvertieren, und es wird davon ausgegangen, dass die Größe des Datenpuffers die Größe des Datentyps Date C. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.
