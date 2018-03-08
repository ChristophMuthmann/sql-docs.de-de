---
title: Numerische Funktionen | Microsoft Docs
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
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8a4b3c0cca843e576fd200b6803db8f1bac5adcb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="numeric-functions"></a>Numerische Funktionen
Die folgende Tabelle beschreibt die numerische Funktionen, die in der ODBC-Skalarfunktion Menge enthalten sind. Durch Aufrufen von **SQLGetInfo** mit einem *Informationstyp* von SQL_NUMERIC_FUNCTIONS, kann eine Anwendung ermitteln, welche numerischen Funktionen von einem-Treiber unterstützt werden.  
  
 Alle numerische Funktionen Rückgabewerte vom Datentyp SQL_FLOAT mit Ausnahme von ABS, ROUND, TRUNCATE, Anmeldung, FLOOR und CEILING, die Werte der gleichen Daten zurückgeben als Eingabeparameter geben.  
  
 Als Argumente bezeichnet *Numeric_exp* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *numerische Litera*l, in denen die zugrunde liegenden Datentyp als SQL_NUMERIC SQL_ dargestellt werden konnte DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL oder SQL_DOUBLE.  
  
 Als Argumente bezeichnet *Float_exp* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *numerische Literal*, wobei die zugrunde liegenden Datentyp als SQL_FLOAT dargestellt werden kann.  
  
 Als Argumente bezeichnet *Integer_exp* kann der Name einer Spalte, die das Ergebnis von einem anderen Skalarfunktion sein oder ein *numerische Literal*, wobei die zugrunde liegenden Datentyp als SQL_TINYINT SQL_ dargestellt werden können "Smallint", SQL_INTEGER oder SQL_BIGINT.  
  
 Die CURRENT_DATE aktuelle_zeit und CURRENT_TIMESTAMP skalaren Funktionen wurden in ODBC 3.0 SQL-92 veröffentlichungshäufigkeit hinzugefügt.  
  
|Funktion|Description|  
|--------------|-----------------|  
|**ABS (** *Numeric_exp* **)** (ODBC 1.0)|Gibt den absoluten Wert des *Numeric_exp*.|  
|**ACOS (** *Float_exp* **)** (ODBC 1.0)|Gibt den Arkuskosinus von *Float_exp* ein Winkel im Bogenmaß ausgedrückten.|  
|**ASIN (** *Float_exp* **)** (ODBC 1.0)|Gibt den Arkussinus des *Float_exp* ein Winkel im Bogenmaß ausgedrückten.|  
|**ATAN (** *Float_exp* **)** (ODBC 1.0)|Gibt den Arkustangens von *Float_exp* ein Winkel im Bogenmaß ausgedrückten.|  
|**ATAN2 (** *float_exp1*, *float_exp2***)** (ODBC 2.0)|Gibt den Arkustangens von der *x* und *y* angegebenen Koordinaten *float_exp1* und *float_exp2*bzw. einen Winkel ausgedrückt als Bogenmaß (Radiant).|  
|**CEILING (** *Numeric_exp* **)** (ODBC 1.0)|Gibt die kleinste ganze Zahl größer als oder gleich *Numeric_exp*. Der Rückgabewert ist von den gleichen Datentyp wie der input-Parameter.|  
|**COS (** *Float_exp* **)** (ODBC 1.0)|Gibt den Kosinus des *Float_exp*, wobei *Float_exp* einen Winkel im Bogenmaß ausgedrückt wird.|  
|**COT (** *Float_exp* **)** (ODBC 1.0)|Gibt den Kotangens eines *Float_exp*, wobei *Float_exp* einen Winkel im Bogenmaß ausgedrückt wird.|  
|**Grad (** *Numeric_exp* **)** (ODBC 2.0)|Gibt die Anzahl der aus konvertiert Grad *Numeric_exp* Bogenmaß (Radiant).|  
|**EXP (** *Float_exp* **)** (ODBC 1.0)|Gibt den Exponentialwert des *Float_exp*.|  
|**FLOOR (** *Numeric_exp* **)** (ODBC 1.0)|Gibt der größten ganze Zahl kleiner als oder gleich *Numeric_exp*. Der Rückgabewert ist von den gleichen Datentyp wie der input-Parameter.|  
|**LOG (** *Float_exp* **)** (ODBC 1.0)|Gibt den natürlichen Logarithmus von *Float_exp*.|  
|**LOG10 (** *Float_exp* **)** (ODBC 2.0)|Gibt die Basis-10-Logarithmus des *Float_exp*.|  
|**MOD (** *integer_exp1*, *integer_exp2***)** (ODBC 1.0)|Gibt den Rest (Modulo) von *integer_exp1* geteilt durch *integer_exp2*.|  
|**PI ()** (ODBC 1.0)|Gibt den konstanten Wert von Pi als Gleitkommawert an.|  
|**POWER (** *Numeric_exp*, *Integer_exp***)** (ODBC 2.0)|Gibt den Wert der *Numeric_exp* zur Potenz einer *Integer_exp*.|  
|**BOGENMAß (** *Numeric_exp* **)** (ODBC 2.0)|Gibt die Anzahl der Bogenmaß konvertiert aus *Numeric_exp* Grad.|  
|**RAND (**[*Integer_exp*]**)** (ODBC 1.0)|Gibt einen zufälligen Gleitkommawert mit *Integer_exp* als optionale Startwert.|  
|**ROUND (** *Numeric_exp*, *Integer_exp***)** (ODBC 2.0)|Gibt *Numeric_exp* auf gerundet *Integer_exp* wird rechts vom Dezimaltrennzeichen an. Wenn *Integer_exp* negativ ist, *Numeric_exp* wird gerundet, um &#124; *Integer_exp*&#124; Stellen links vom Dezimaltrennzeichen an.|  
|**Signieren (** *Numeric_exp* **)** (ODBC 1.0)|Gibt einen Indikator, der das Vorzeichen des *Numeric_exp*. Wenn *Numeric_exp* ist kleiner als 0 (null),-1 zurückgegeben. Wenn *Numeric_exp* gleich 0 (null) ist, wird 0 zurückgegeben. Wenn *Numeric_exp* ist größer als 0 (null), wird 1 zurückgegeben.|  
|**SIN (** *Float_exp* **)** (ODBC 1.0)|Gibt den Sinus des *Float_exp*, wobei *Float_exp* einen Winkel im Bogenmaß ausgedrückt wird.|  
|**SQRT (** *Float_exp* **)** (ODBC 1.0)|Gibt die Quadratwurzel von *Float_exp*.|  
|**TAN (** *Float_exp* **)** (ODBC 1.0)|Gibt den Tangens des *Float_exp*, wobei *Float_exp* einen Winkel im Bogenmaß ausgedrückt wird.|  
|**TRUNCATE (** *Numeric_exp*, *Integer_exp***)** (ODBC 2.0)|Gibt *Numeric_exp* auf gekürzt *Integer_exp* wird rechts vom Dezimaltrennzeichen an. Wenn *Integer_exp* negativ ist, *Numeric_exp* auf abgeschnitten &#124; *Integer_exp*&#124; Stellen links vom Dezimaltrennzeichen an.|
