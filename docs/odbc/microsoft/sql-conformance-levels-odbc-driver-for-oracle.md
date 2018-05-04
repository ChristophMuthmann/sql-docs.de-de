---
title: SQL-Übereinstimmungsebenen (ODBC-Treiber für Oracle) | Microsoft Docs
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 247009b387cf7538a841477bab5f7be72fa20fd5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL-Übereinstimmungsebenen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Der ODBC-Treiber für Oracle unterstützt die minimale SQL-Grammatik und -SQL-kerngrammatik und unterstützt außerdem die folgenden ODBC-Erweiterungen für SQL:  
  
-   Date, Time und Timestamp-Daten  
  
-   Linke und Rechte äußere joins  
  
-   Numerische Funktionen:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Höchstwert|LOG10|second|truncate|  
    |Cos|Mod|Anmelden||  
    |Exponential|PI|Sin||  
    |Floor|Power|sqrt||  
  
-   Datumsfunktionen:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|"MonthName"|second|  
    |Curtime|Dayofyear|minute|week|  
    |DAYNAME|Hour|jetzt|Jahr|  
    |DayOfMonth|Month|Quartal||  
  
-   Zeichenfolgenfunktionen:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Left|Richting|UCase|  
    |Char|Länge|RTrim||  
    |Concat|Ltrim|SOUNDEX||  
    |Lcase|Ersetzen|substring||  
  
-   Typkonvertierungs-Funktion:  
  
    ||  
    |-|  
    |Konvertieren|  
  
-   Systemfunktionen:  
  
    ||  
    |-|  
    |IFNULL|  
    |Benutzer|
