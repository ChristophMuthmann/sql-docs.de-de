---
title: "SQL-Übereinstimmungsebenen (ODBC-Treiber für Oracle) | Microsoft Docs"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d57a126459d250a13a2ddd5ef1bb90732d1b4a45
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL-Übereinstimmungsebenen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
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
