---
title: Zeichenfolgenfunktionen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf8654f4851f2d0ed93437be884057112c26a968
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="string-functions"></a>Zeichenfolgenfunktionen
Die folgende Tabelle enthält die Funktionen zur Zeichenfolgenmanipulation. Eine Anwendung kann bestimmen, welche Funktionen für Zeichenfolgen durch Aufrufen von einem Treiber unterstützt werden **SQLGetInfo** mit einem *Informationstyp* von SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Hinweise  
 Als Argumente bezeichnet *String_exp* kann der Name einer Spalte, eine *Zeichen Zeichenfolgenliteral*, oder das Ergebnis von einem anderen Skalarfunktion, in denen die zugrunde liegenden Datentyp als SQL_CHAR SQL_ dargestellt werden kann VARCHAR oder SQL_LONGVARCHAR.  
  
 Als Argumente bezeichnet *Character_exp* eine Zeichenfolge variabler Länge sind.  
  
 Als Argumente bezeichnet *starten*, *Länge*, oder *Anzahl* kann eine *numerische Literal* oder das Ergebnis von einem anderen Skalarfunktion, in denen die zugrunde liegende Datentyp kann als SQL_TINYINT, SQL_SMALLINT oder SQL_INTEGER dargestellt werden.  
  
 Die String-Funktionen, die hier aufgeführten sind 1-basiert. das erste Zeichen in der Zeichenfolge ist, also Zeichen 1.  
  
 Die Zeichenfolge-Skalarfunktionen BIT_LENGTH, CHAR_LENGTH CHARACTER_LENGTH, OCTET_LENGTH und POSITION wurden in ODBC 3.0 SQL-92 veröffentlichungshäufigkeit hinzugefügt.  
  
|Funktion|Description|  
|--------------|-----------------|  
|**ASCII (** *String_exp* **)** (ODBC 1.0)|Gibt den ASCII-Codewert des äußeren linken Zeichens *String_exp* als ganze Zahl.|  
|**BIT_LENGTH (** *String_exp* **)** (ODBC 3.0)|Gibt die Länge des Zeichenfolgenausdrucks in Bits zurück.<br /><br /> Nur für Zeichenfolgen-Datentypen nicht verwendet werden, wird daher nicht implizit konvertiert *String_exp* , sondern stattdessen Zeichenfolge beliebigen Datentyp aufweisen, wird ihm, die (interne) Größe zurück.|  
|**CHAR (** *Code* **)** (ODBC 1.0)|Gibt das Zeichen, das der ASCII-Codewert gemäß *Code*. Der Wert der *Code* muss zwischen 0 und 255 sein; andernfalls ist des Rückgabewerts datenquellenabhängig.|  
|**CHAR_LENGTH (** *String_exp* **)** (ODBC 3.0)|Gibt die Länge in Zeichen im Zeichenfolgenausdruck zurück, wenn der Zeichenfolgenausdruck für einen Zeichendatentyp ist; andernfalls gibt die Länge in Bytes des Zeichenfolgenausdrucks (die kleinste ganze Zahl nicht kleiner als die Anzahl der Bits dividiert durch 8) zurück. (Diese Funktion ist identisch mit der CHARACTER_LENGTH-Funktion.)|  
|**CHARACTER_LENGTH (** *String_exp* **)** (ODBC 3.0)|Gibt die Länge in Zeichen im Zeichenfolgenausdruck zurück, wenn der Zeichenfolgenausdruck für einen Zeichendatentyp ist; andernfalls gibt die Länge in Bytes des Zeichenfolgenausdrucks (die kleinste ganze Zahl nicht kleiner als die Anzahl der Bits dividiert durch 8) zurück. (Diese Funktion ist die CHAR_LENGTH identisch.)|  
|**CONCAT (** *string_exp1*,*string_exp2 und ***)** (ODBC 1.0)|Gibt eine Zeichenfolge, die das Ergebnis der Verkettung wird *string_exp2 und* auf *string_exp1*. Die Ergebniszeichenfolge hängt vom DBMS ab. Angenommen, wenn die Spalte über dargestellt *string_exp1* enthalten einen NULL-Wert, DB2 würde return NULL aber SQL Server würden die ungleich NULL-Zeichenfolge zurückzugeben.|  
|**Unterschied (** *string_exp1*,*string_exp2 und ***)** (ODBC 2.0)|Gibt einen ganzzahligen Wert, der den Unterschied zwischen den Werten, die von der SOUNDEX-Funktion für zurückgegebene angibt *string_exp1* und *string_exp2 und*.|  
|**Einfügen (** *string_exp1*, *starten*, *Länge*, *string_exp2 und ***)** (ODBC 1.0)|Gibt ein Zeichen, Zeichenfolge Where *Länge* Zeichen aus gelöscht wurden *string_exp1*, beginnend bei *starten*, und wo *string_exp2 und* in eingefügt wurde *String_exp,* beginnend *starten*.|  
|**LCASE (** *String_exp* **)** (ODBC 1.0)|Gibt eine Zeichenfolge in gleich *String_exp*, mit der alle Großbuchstaben in Kleinbuchstaben konvertiert.|  
|**LEFT (** *String_exp*, *Anzahl ***)** (ODBC 1.0)|Gibt die am weitesten links stehende *Anzahl* Zeichen des *String_exp*.|  
|**Länge (** *String_exp* **)** (ODBC 1.0)|Gibt die Anzahl der Zeichen in *String_exp,* jedoch ohne nachfolgende Leerzeichen.<br /><br /> **Länge** akzeptiert nur Zeichenfolgen. Aus diesem Grund wird implizite Konvertierung *String_exp* auf eine Zeichenfolge, und der Rückgabewert der Länge dieser Zeichenfolge (und nicht die interne Größe des Datentyps).|  
|**Suchen (** *string_exp1*, *string_exp2 und*[, *starten*]**)** (ODBC 1.0)|Gibt die Anfangsposition des ersten Vorkommens des *string_exp1* in *string_exp2 und*. Die Suche nach dem ersten Vorkommen des *string_exp1* beginnt mit der ersten Zeichenposition im *string_exp2 und* , wenn das optionale Argument *starten*, angegeben ist. Wenn *starten* angegeben ist, wird die Suche beginnt mit der durch den Wert der angegebenen Zeichenposition *starten*. Positionieren Sie das erste Zeichen *string_exp2 und* wird durch den Wert 1 angegeben. Wenn *string_exp1* befindet sich nicht innerhalb von *string_exp2 und*, wird der Wert 0 zurückgegeben.<br /><br /> Wenn eine Anwendung die suchen-Skalarfunktion mit aufrufen kann die *string_exp1*, *string_exp2 und*, und *starten* Argumente, gibt der Treiber SQL_FN_STR_LOCATE beim  **SQLGetInfo** aufgerufen wird und ein *Option* von SQL_STRING_FUNCTIONS. Wenn die Anwendung die suchen-Skalarfunktion mit nur aufrufen, kann die *string_exp1* und *string_exp2 und* Argumente, gibt der Treiber SQL_FN_STR_LOCATE_2 beim **SQLGetInfo**aufgerufen wird und ein *Option* von SQL_STRING_FUNCTIONS. Treiber, dass die Suchen-Funktion mit zwei oder drei Argumenten aufrufen Unterstützung SQL_FN_STR_LOCATE und SQL_FN_STR_LOCATE_2 zurückgeben.|  
|**LTRIM (** *String_exp* **)** (ODBC 1.0)|Gibt die Zeichen des *String_exp*, mit führenden Leerzeichen entfernt.|  
|**OCTET_LENGTH (** *String_exp* **)** (ODBC 3.0)|Gibt die Länge des Zeichenfolgenausdrucks in Bytes zurück. Das Ergebnis ist die kleinste ganze Zahl, die nicht kleiner ist als die Anzahl der Bits dividiert durch 8.<br /><br /> Nur für Zeichenfolgen-Datentypen nicht verwendet werden, wird daher nicht implizit konvertiert *String_exp* , sondern stattdessen Zeichenfolge beliebigen Datentyp aufweisen, wird ihm, die (interne) Größe zurück.|  
|**POSITION (** *Character_exp* **IN** *Character_exp ***)** (ODBC 3.0)|Gibt die Position des ersten Zeichens Ausdrucks in der zweiten Zeichenausdruck zurück. Das Ergebnis ist ein genauen numerischen Wert mit einer Implementierung definierten Genauigkeit und Dezimalstellen 0.|  
|**Wiederholen (** *String_exp,* *Anzahl ***)** (ODBC 1.0)|Gibt eine Zeichenfolge besteht *String_exp* wiederholt *Anzahl* Zeiten.|  
|**Ersetzen (** *string_exp1*, *string_exp2 und*, *string_exp3 ***)** (ODBC 1.0)|Suche *string_exp1* Foroccurrences von *string_exp2 und*, und Ersetzen Sie durch *string_exp3*.|  
|**RECHTS (** *String_exp*, *Anzahl ***)** (ODBC 1.0)|Gibt die äußersten rechten *Anzahl* Zeichen des *String_exp*.|  
|**RTRIM (** *String_exp* **)** (ODBC 1.0)|Gibt die Zeichen des *String_exp* mit nachfolgenden Leerzeichen entfernt.|  
|**SOUNDEX (** *String_exp* **)** (ODBC 2.0)|Gibt eine Datenzeichenfolge-Quelle vom Änderungsmanagement angeforderten Zeichen, die die Wörter in den Sound darstellt *String_exp*. SQL Server gibt beispielsweise einen 4 Ziffern SOUNDEX-Code zurück; Oracle gibt eine Phonetische Darstellung eines einzelnen Worts zurück.|  
|**Speicherplatz (** *Anzahl* **)** (ODBC 2.0)|Gibt eine Zeichenfolge bestehend aus *Anzahl* Leerzeichen.|  
|**SUBSTRING (** *String_exp*, *starten*, Länge**)** (ODBC 1.0)|Gibt eine Zeichenfolge, die abgeleitet ist *String_exp*, beginnend an der Position des Zeichens, angegeben durch *starten* für *Länge* Zeichen.|  
|**UCASE (** *String_exp* **)** (ODBC 1.0)|Gibt eine Zeichenfolge in gleich *String_exp*, mit der alle Kleinbuchstaben in Großbuchstaben konvertiert.|
