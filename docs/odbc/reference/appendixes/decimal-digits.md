---
title: Dezimalstellen | Microsoft Docs
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
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4593b1faacfc235ce0ee5c54bc9ca70416444f5e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="decimal-digits"></a>Dezimalstellen
Die *Dezimalstellen* decimal und numeric-Daten Typen als die maximale Anzahl der Ziffern rechts vom Dezimaltrennzeichen oder die Skalierung der Daten definiert ist. Für ungefähren Gleitkommazahlen Zahlenspalten oder die Typparameter sind keine Dezimalstellen definiert, da die Anzahl der Ziffern rechts neben dem Dezimalzeichen nicht festgelegt ist. Für "DateTime" oder ein Zeitintervall Daten, die eine Komponente für Sekunden enthält, wird als die Anzahl der Ziffern rechts vom Dezimaltrennzeichen in die Sekundenkomponente der Daten die Dezimalstellen definiert.  
  
 Für die Datentypen SQL_DECIMAL und SQL_NUMERIC ist die maximale Dezimalstellen in der Regel identisch mit der maximalen Genauigkeit. Einige Datenquellen verursachen jedoch einen eigenen Grenzwert für die maximalen Dezimalstellen. Um zu bestimmen, die minimalen und maximalen Skalierungen, die für einen Datentyp zulässig, eine Anwendung ruft **SQLGetTypeInfo**.  
  
 Die Dezimalstellen definiert, die für jeden präzise SQL-Datentyp wird in der folgenden Tabelle gezeigt.  
  
|SQL-Typ|Dezimalstellen|  
|--------------|--------------------|  
|Alle Zeichen- und Binärtypen [a]|–|  
|SQL_DECIMAL<br />SQL_NUMERIC|Die festgelegte Anzahl von Ziffern rechts vom Dezimaltrennzeichen an. Die Dezimalstellen einer Spalte, die als "NUMERIC(10,3)" definiert ist z. B. 3. Dies kann eine negative Zahl, um Speicher von sehr großen Zahlen zu unterstützen, ohne Sie mit der Exponentialschreibweise sein; Beispielsweise könnte "12000" als "12" mit einer Skala-3 gespeichert werden.|  
|Exakte numerische Typen als SQL_DECIMAL und SQL_NUMERIC [a]|0|  
|Alle ungefähre Datentypen [a]|–|  
|SQL_TYPE_DATE und alle Interval mit keine Sekundenkomponente [a]|–|  
|Alle Typen von "DateTime" mit Ausnahme von SQL_TYPE_DATE und alle Intervalltypen mit einer Sekundenkomponente in|Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen in der zweite Teil des Werts (Sekundenbruchteile). Diese Zahl darf nicht negativ sein.|  
|SQL_GUID|–|  
  
 [a] der *DecimalDigits* Argument **SQLBindParameter** wird für diesen Datentyp ignoriert.  
  
 Die zurückgegebenen Werte für die Dezimalstellen müssen nicht auf die Werte in jedem Deskriptorfeld für einen entsprechen. Die Werte können entweder die SQL_DESC_SCALE oder Feld SQL_DESC_PRECISION je nach Datentyp, stammen, wie in der folgenden Tabelle gezeigt.  
  
|SQL-Typ|Deskriptorfeld entspricht<br /><br /> Dezimalstellen|  
|--------------|----------------------------------------------------------|  
|Alle Zeichen- und Binärtypen|–|  
|Alle exakte numerische Typen|SCALE|  
|SQL_BIT|–|  
|Alle ungefähren numerischen Typen|–|  
|Alle Typen von "DateTime"|PRECISION|  
|Alle Intervalltypen mit einer Sekundenkomponente in|PRECISION|  
|Alle Intervalltypen mit keine Sekundenkomponente in|–|
