---
title: "SQL in \"c:\" Binärdaten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ccb6114eab57030d6555931f0bfcdbe469326442
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-binary"></a>SQL in das Binärformat "c:"
Der Bezeichner für die binäre ODBC SQL-Datentypen sind:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in die Binärdaten SQL konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Bytelänge der Daten) \* 2 < *Pufferlänge*<br /><br /> (Bytelänge der Daten) \* 2 > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes|–<br /><br /> 01004|  
|SQL_C_WCHAR|(Länge der Daten) \* 2 < *Pufferlänge*<br /><br /> (Länge der Daten) \* 2 > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen|–<br /><br /> 01004|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes|–<br /><br /> 01004|  
  
 Wenn SQL-Binärdaten in C-Zeichendaten konvertiert werden, wird jedes Byte (8 Bit) der Quelldaten als zwei ASCII-Zeichen dargestellt. Diese Zeichen befinden sich die ASCII-Zeichen-Darstellung der Zahl in hexadezimaler Form. Z. B. eine binäre 00000001 "01" konvertiert, und eine binäre 11111111 "FF" konvertiert.  
  
 Der Treiber immer einzelne Bytes auf Paare von hexadezimalen Zeichen konvertiert und beendet die Zeichenfolge mit null Byte. Aus diesem Grund Wenn *Pufferlänge* gerade und ist kleiner als die Länge der konvertierten Daten, das letzte Byte der **TargetValuePtr* Puffer wird nicht verwendet. (Die konvertierten Daten erfordern eine gerade Anzahl von Bytes, die Byte vorletztes ist ein Nullbyte und das letzte Byte kann nicht verwendet werden.)  
  
> [!NOTE]  
>  Anwendungsentwickler sind aus binären SQL Binden von Daten in einem C-Zeichendatentyp abgeraten. Diese Konvertierung ist in der Regel ineffizient und zeitaufwändig.
