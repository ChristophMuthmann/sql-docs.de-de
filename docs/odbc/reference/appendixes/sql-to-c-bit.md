---
title: SQL in "c:" Bit | Microsoft Docs
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
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 818a182b44acd2eb135443e95a02bcca935d0210
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-bit"></a>SQL in c-Bit
Der Bezeichner für den ODBC-SQL-Datentyp Bit ist:  
  
 SQL_BIT  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in den Bit-SQL-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*Pufferlänge* 1 ><br /><br /> *Pufferlänge* < = 1|data<br /><br /> Nicht definiert|1<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Keine [a]|data|Größe der C-Datentyp|–|  
|SQL_C_BIT|Keine [a]|data|1 [b]|–|  
|SQL_C_BINARY|*Pufferlänge* > = 1<br /><br /> *Pufferlänge* < 1|data<br /><br /> Nicht definiert|1<br /><br /> Nicht definiert|–<br /><br /> 22003|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 Wenn in Zeichendaten C Bit-SQL-Daten konvertiert werden, sind die möglichen Werte "0" und "1".
