---
title: Aufrufe von Skalarfunktionen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba961f17cf244cd013f7c62b6cec411a0f642882
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="scalar-function-calls"></a>Aufrufe von Skalarfunktionen
Skalarfunktionen geben einen Wert für jede Zeile zurück. Beispielsweise die Skalarfunktion absoluten Wert eine numerische Spalte als Argument akzeptiert und gibt den absoluten Wert der einzelnen Werte in der Spalte zurück. Ist die-Escapesequenz zum Aufrufen einer Skalarfunktion  
  
 **{fn***Skalarfunktion* **}**  
  
 wobei *Skalarfunktion* ist eine der Funktionen in [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Weitere Informationen über die Skalarfunktion Escapesequenz finden Sie unter [skalare Funktionsescapesequenz](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) in Anhang C: SQL-Grammatik.  
  
 Z. B. erstellen die folgenden SQL-Anweisungen des gleichen Ergebnissatzes Großbuchstaben Kunden Namen. Die erste Anweisung verwendet die Syntax der Escapesequenz. Die zweite Anweisung verwendet die systemeigene Syntax für Ingres für OS/2 und ist nicht interoperabel.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Eine Anwendung kann mischen, Aufrufe von Skalarfunktionen, die systemeigene Syntax verwenden und Aufrufe von Skalarfunktionen, die ODBC-Syntax verwenden. Nehmen wir beispielsweise an, dass Namen in der Employee-Tabelle als einen Nachnamen, ein Komma und ein Vorname gespeichert werden. Die folgende SQL-Anweisung erstellt ein Resultset der Nachnamen der Mitarbeiter in der Employee-Tabelle. Die Anweisung verwendet die ODBC-Skalarfunktion **TEILZEICHENFOLGE** und der SQL Server-Skalarfunktion **CHARINDEX** und werden nur in SQL Server ordnungsgemäß ausgeführt.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 Für eine optimale Interoperabilität sollten Anwendungen verwenden die **konvertieren** Skalarfunktion, um sicherzustellen, dass die Ausgabe eine skalare Funktion der erforderliche Typ ist. Die **konvertieren** Funktion konvertiert die Daten von einem SQL-Datentyp in den angegebenen SQL-Datentyp. Die Syntax der **konvertieren** Funktion ist  
  
 **KONVERTIEREN (** *Value_exp* **,** *Data_type ***)**  
  
 auf dem *Value_exp* ist ein Spaltenname ist das Ergebnis des anderen Skalarfunktion oder einen literalen Wert und *Data_type* ist ein Schlüsselwort, das entspricht der **#define** Namens wird durch eine SQL-Datentyp Bezeichner gemäß [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md). Beispielsweise die folgende SQL-Anweisung verwendet die **konvertieren** Funktion, um sicherzustellen, dass die Ausgabe der **CURDATE** Funktion ist ein Datum ist, statt einen Zeitstempel oder Zeichen-Daten:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Um zu bestimmen, welche Skalarfunktionen von einer Datenquelle unterstützt werden, eine Anwendung ruft **SQLGetInfo** SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS und SQL_TIMEDATE_ Optionen für Funktionen. Um zu bestimmen, welche Konvertierungsvorgänge von unterstützt werden die **konvertieren** -Funktion, eine Anwendung ruft **SQLGetInfo** mit den Optionen, die mit SQL_CONVERT beginnen.
