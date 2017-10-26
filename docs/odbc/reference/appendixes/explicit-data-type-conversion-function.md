---
title: Explizite Datentypen Konvertierungsfunktion | Microsoft Docs
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
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e0bba777a69607447428d83115c545edfeccec5d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="explicit-data-type-conversion-function"></a>Explizite Daten Typkonvertierungsfunktion
Explizite datentypkonvertierung wird im Hinblick auf die SQL-Datentypdefinitionen angegeben.  
  
 Die ODBC-Syntax für die explizite Daten Typkonvertierungsfunktion schränkt Konvertierungen nicht. Die Gültigkeit des bestimmte Konvertierungen von einem Datentyp in einen anderen Datentyp wird von jeder Treiber-spezifische Implementierung bestimmt. Der Treiber, wie er in die systemeigene Syntax die ODBC-Syntax übersetzt diese Konvertierungen abgelehnt, die zwar in der ODBC-Syntax zulässig, von der Datenquelle nicht unterstützt werden. Der ODBC-Funktion **SQLGetInfo**, bei der Konvertierung-Optionen (z. B. SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY SQL_CONVERT_INTERVAL_YEAR_MONTH und So weiter), bietet eine Möglichkeit, erkundigen Sie sich von der Datenquelle unterstützten Konvertierungen .  
  
 Das Format der **konvertieren** Funktion ist:  
  
 **KONVERTIEREN (** *Value_exp*, *Data_type***)**  
  
 Die Funktion gibt den Wert von angegebenen *Value_exp* konvertiert in den angegebenen *Data_type*, wobei *Data_type* ist eines der folgenden Schlüsselwörter:  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 Die ODBC-Syntax für die explizite Daten Typkonvertierungsfunktion unterstützt Spezifikation des Formats der Konvertierung nicht. Wenn die Spezifikation der expliziten Formate, die von der zugrunde liegenden Datenquelle unterstützt wird, muss ein Treiber einen Standardwert angeben oder Formatspezifikation implementieren.  
  
 Das Argument *Value_exp* können einen Spaltennamen an, das Ergebnis von einem anderen Skalarfunktion oder einen numerischen oder die Zeichenfolge literal sein. Beispiel:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 Konvertiert die Ausgabe der CURDATE skalare Funktion in eine Zeichenfolge.  
  
 Da ODBC nicht über einen Datentyp für die Rückgabewerte von vorschreibt Skalarfunktionen (da die Funktionen, die häufig Daten datenquellenspezifischen sind), Anwendungen sollten die CONVERT-Skalarfunktion nach Möglichkeit zwingen datentypkonvertierung verwenden.  
  
 Die beiden folgenden Beispiele veranschaulichen die Verwendung des der **konvertieren** Funktion. Diese Beispielen wird angenommen, das Vorhandensein einer Tabelle, die Mitarbeiter mit einer EMPNO-Spalte vom Typ SQL_SMALLINT und eine EMPNAME-Spalte vom Typ SQL_CHAR aufgerufen wird.  
  
 Wenn eine Anwendung die folgenden SQL-Anweisung angibt:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Ein Treiber für ORACLE übersetzt der SQL-Anweisung:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Ein Treiber für SQL Server übersetzt die SQL-Anweisung:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Wenn eine Anwendung die folgenden SQL-Anweisung angibt:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Ein Treiber für ORACLE übersetzt der SQL-Anweisung:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Ein Treiber für SQL Server übersetzt die SQL-Anweisung:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ein Treiber für Ingres übersetzt der SQL-Anweisung:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```

