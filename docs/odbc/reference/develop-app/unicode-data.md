---
title: Unicode-Daten | Microsoft Docs
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
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee404891b20f721cec0ea9e56b9eab1e78ad6f8f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-data"></a>Unicode-Daten
SQL-Unicode-Datentypen werden bereitgestellt, um Daten zu beschreiben, die im Unicode-Format, systemintern für das DBMS befindet. Ein C#-Unicode-Datentyp wird bereitgestellt, damit eine Anwendung zum Binden von Daten in einen Unicode-Puffer kann. Der Treiber-Manager können Daten aus einem Unicode-C-Typ (SQL_C_WCHAR) zu erleichtern konvertieren-Funktion mit einer ANSI-Treiber.  
  
 Ein ODBC 3.0 oder 2. *x* Anwendung immer eine Bindung an die ANSI-Datentypen. Für eine optimale Leistung sollten eine ODBC 3.5 (oder höhere)-Anwendung in der ANSI-C-Datentyp binden, wenn der SQL-Spaltentyp ANSI ist und in den Unicode C-Datentyp binden sollten, wenn der SQL-Spaltentyp aus Unicode besteht.  
  
 Die SQL-Unicode-typindikatoren sind SQL_WCHAR, SQL_WVARCHAR oder SQL_WLONGVARCHAR. SQL_WCHAR-Daten hat eine Zeichenfolge fester Länge, während SQL_WVARCHAR verfügt über eine Variable Länge mit einer maximalen deklarierte und SQL_WLONGVARCHAR hat einen Variablen Länge mit einer maximalen, die von der Datenquelle abhängig.  
  
 Die C#-Unicode-Typindikator ist SQL_C_WCHAR an. Dies ist die Standardeinstellung für jede der SQL-Unicode-typindikatoren. Alle SQL-Typen konvertiert werden können SQL_C_WCHAR, und für alle SQL-Datentypen SQL_C_WCHAR konvertiert werden kann. Eine Anwendung kann Daten in einer von drei Methoden abrufen:  
  
-   Abrufen von Daten als SQL_C_CHAR.  
  
-   Rufen Sie die Daten als SQL_C_WCHAR an.  
  
-   Deklarieren Sie die Daten als SQL_C_TCHAR. Dies ist ein Makro, das SQL_C_WCHAR eingefügt, wenn die Anwendung, als Unicode-Anwendung kompiliert wird oder SQL_C_CHAR eingefügt, wenn es als eine ANSI-Anwendung kompiliert wird.  
  
 SQL_C_TCHAR wird in einer Funktion wie folgt deklariert:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Wenn die Anwendung, als Unicode-Anwendung kompiliert wird, die *ValueType* Argument würde von SQL_C_TCHAR in SQL_C_WCHAR geändert werden. Wenn die Anwendung, wie eine ANSI-Anwendung sowie kompiliert wird die *ValueType* Argument in SQL_C_CHAR geändert.  
  
 Unicode-Treiber müssen dennoch ANSI-Datentypen, einschließlich SQL_CHAR unterstützen. Wenn eine Anwendung, die mit einem Unicode-Treiber arbeiten SQL_CHAR gebunden, wird der Treiber-Manager die SQL_CHAR-Daten nicht SQL_WCHAR zuordnen. Der Unicode-Treiber muss die SQL_CHAR-Daten akzeptieren.  
  
 Der Treiber-Manager speichert Treiber und DSN-Namen im Unicode-Format und ordnet sie ANSI nach Bedarf. Wenn ein Unicode-Zeichen in eine ANSI-Zeichen (wie auftreten können, wenn Zeichen aus einer Codepage, die nicht den systemeigenen Code auf dem Computer ist im DSN-Namen und Treiber verwendet werden) zugeordnet werden kann, werden die Zeichen, die nicht konvertiert werden konnten von einer Standard-Sup Zeichen dargestellt. vom System plied.
