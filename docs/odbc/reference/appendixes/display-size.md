---
title: "Anzeigegröße | Microsoft Docs"
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
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3faac66828cdc408f9bd153377a3aefe74b882b0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="display-size"></a>Die Anzeigegröße
Die Größe einer Spalte ist die maximale Anzahl von Zeichen, die zum Anzeigen von Daten in Form von Zeichen erforderlich. In der folgenden Tabelle definiert die Anzeigegröße für jede ODBC-SQL-Datentyp.  
  
|SQL-Typ-ID|Die Anzeigegröße|  
|-------------------------|------------------|  
|Alle Typen mit Zeichen [a]|(Für eine feste Typen) definiert oder (für Variablentypen) maximale Anzahl von Zeichen, die zum Anzeigen der Daten in Form von Zeichen erforderlich sind.|  
|SQL_DECIMAL SQL_NUMERIC|Die Genauigkeit der Spalte plus 2 (eine Anmeldung, *Genauigkeit* Ziffern und einem Dezimaltrennzeichen). Beispielsweise ist die Größe einer Spalte, die als NUMERIC(10,3) definiert 12.|  
|SQL_BIT|1 (1 Ziffer).|  
|SQL_TINYINT|4, wenn (eine Anmeldung und 3 Ziffern) signiert oder 3, wenn (3 Ziffern) ohne Vorzeichen.|  
|SQL_SMALLINT|6 Wenn (eine Anmeldung und 5 Ziffern) signiert oder 5 Wenn (5 Ziffern) ohne Vorzeichen.|  
|SQL_INTEGER|11 Wenn (eine Anmeldung und 10 Ziffern) signiert oder 10 Wenn (10 Ziffern) ohne Vorzeichen.|  
|SQL_BIGINT|20 (eine Anmeldung und 19 Ziffern Wenn signiert oder 20 Ziffern, wenn nicht signierte).|  
|SQL_REAL|14 (eine Anmeldung, 7 Dezimalstellen, ein Dezimaltrennzeichen, den Buchstaben *E*, eine Anmeldung und 2 Ziffern).|  
|SQL_FLOAT SQL_DOUBLE|24 (eine Anmeldung, 15 Dezimalstellen, ein Dezimaltrennzeichen, den Buchstaben *E*, eine Anmeldung und 3 Ziffern).|  
|Alle Binärtypen [a]|Definiert oder (für Variablentypen), maximale Länge der Spalte x 2. (Jedes binäre Byte wird durch eine hexadezimale Zahl mit 2 Stellen dargestellt.)|  
|SQL_TYPE_DATE|10 (ein Datum im Format *jjjj-mm-tt*).|  
|SQL_TYPE_TIME|8 (eine Uhrzeit im Format *hh: mm:*)<br /><br /> - oder -<br /><br /> 9 + *s* (eine Uhrzeit im Format *hh: mm:*[... ss.fff], wobei *s* ist die Genauigkeit der Sekundenbruchteile).|  
|SQL_TYPE_TIMESTAMP|19 (für ein Zeitstempel in der *jjjj-mm-tt hh: mm:* Format)<br /><br /> - oder -<br /><br /> 20 + *s* (für ein Zeitstempel in der *jjjj-mm-tt hh: mm:*[ss.fff...]-Format, in dem *s* ist die Genauigkeit der Sekundenbruchteile).|  
|Alle Interval-Datentypen|Finden Sie unter [Länge des Datentyps Interval](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (die Anzahl der Zeichen in der *Aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* Format|  
  
 [a] Wenn der Treiber die Spalten- oder Parameternamen Länge des Variablentypen ermitteln kann, gibt Sie SQL_NO_TOTAL zurück.
