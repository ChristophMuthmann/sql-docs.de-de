---
title: 'C, um SQL: GUID | Microsoft Docs'
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
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a393aefa101bef2738e15ed12b0f1679e4a6c9c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-guid"></a>C, um SQL: GUID
Der Bezeichner für die GUID ODBC C-Datentyp ist:  
  
 SQL_C_GUID  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in die GUID C-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Byte-Spaltenlänge > = 36|–|  
|SQL_VARCHAR|Spalte Byte Länge < 36|22001|  
|SQL_LONGVARCHAR|Datenwert ist keine gültige GUID|22018|  
|SQL_WCHAR|Zeichenlänge Spalte > = 36|–|  
|SQL_WVARCHAR|Spalte Zeichen Länge < 36|22001|  
|SQL_WLONGVARCHAR|Datenwert ist keine gültige GUID|22018|  
|SQL_GUID|Keine [a]|–|  
  
 [a] alle Hexadezimalwerte sind gültig, als GUID.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus der GUID-C-Datentyp zu konvertieren und setzt voraus, dass die Größe des Datenpuffers die Größe der der GUID-C-Datentyp ist. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.
