---
title: 'C, um SQL: Bit | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e7232773b97a66fc0b1b047e3fb8cc4212754f0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-bit"></a>C, um SQL: Bit
Der Bezeichner für die Bit ODBC C-Datentyp ist:  
  
 SQL_C_BIT  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in den Bit-C-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Keine|–|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL SQL_FLOAT<br /><br /> SQL_DOUBLE|Keine|–|  
|SQL_BIT|Keine|–|  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn vom C-Bit-Datentyp konvertiert, und es wird davon ausgegangen, dass die Größe des Datenpuffers die Größe des C-Bit-Datentyps. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.

