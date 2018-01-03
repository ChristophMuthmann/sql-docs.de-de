---
title: Unicode-Anwendungen | Microsoft Docs
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
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bc4228f693f2d5753c3b04cf6e2cd48e18a591b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="unicode-applications"></a>Unicode-Anwendungen
Sie können eine Anwendung als Unicode-Anwendung in einer von zwei Methoden kompilieren:  
  
-   Die Unicode enthalten **#define** in die Headerdatei Sqlucode.h in der Anwendung enthalten sind.  
  
-   Kompilieren Sie die Anwendung mit Unicode-Compileroption. (Diese Option wird für zwischen den verschiedenen Compilern unterschiedlich sein.)  
  
 Um eine ANSI-Anwendung in einer Unicode-Anwendung zu konvertieren, Schreiben Sie die Anwendung zum Speichern und übergeben von Unicode-Daten. Aufrufen von Funktionen, die Argumente SQLPOINTER unterstützen müssen darüber hinaus konvertiert werden, um die Anzahl von Bytes zu verwenden.  
  
 Nachdem eine Anwendung eine Unicode-Anwendung, kompiliert wird, wenn die Anwendung eine ODBC-API-Funktion (ohne Suffix) aufruft, erkennt die Anwendung als Unicode-Anwendung und Aufruf der Funktion in eine Unicode-Funktion (mit der konvertiertderTreiber-Manager *W* Suffix), wenn der zugrunde liegende Treiber Unicode unterstützt. Wenn eine ANSI-Anwendung einen Funktionsaufruf ohne Suffix herstellt, konvertiert der Treiber-Manager es in ANSI, wenn der zugrunde liegenden Treiber ANSI unterstützt. Wenn die Anwendung und der Treiber die gleichen zeichencodierung unterstützt, übergibt der Treiber-Manager die Aufrufe über den Treiber (mit Ausnahmen für ANSI-Anwendungen).  
  
 Eine Anwendung kann sowohl Unicode-Funktionen aufrufen (mit der *W* Suffix) und ANSI-Funktionen (mit oder ohne die *ein* Suffix). Unicode und ANSI-Funktionsaufrufe können gemischt werden. Wenn die Cursorbibliothek verwendet werden, können nicht jedoch Unicode und ANSI-Funktionsaufrufe gemischt werden. Die Cursorbibliothek ist entweder Unicode oder ANSI, keine Mischung.  
  
 Eine Anwendung kann geschrieben werden, sodass er als eine Unicode-Anwendung oder eine ANSI-Anwendung kompiliert werden kann. In diesem Fall können die Unicodezeichen-Datentypen als SQL_C_TCHAR deklariert werden. Dies ist ein Makro, das SQL_C_WCHAR eingefügt, wenn die Anwendung, als Unicode-Anwendung kompiliert wird oder SQL_C_CHAR eingefügt, wenn es als eine ANSI-Anwendung kompiliert wird. Der Anwendungsprogrammierer achten von Funktionen, die als Argument, SQLPOINTER akzeptieren, da die Größe der Length-Argument (für Zeichenfolgen-Datentypen) ändern, wird je nachdem, ob die Anwendung ANSI oder Unicode.  
  
 Eine Funktion kann in einer von drei Methoden aufgerufen werden: als nur-Unicode-Funktionsaufruf (mit der *W* Suffix), wie ein nur-ANSI-Funktionsaufruf (mit der *ein* Suffix), oder als der ODBC-Funktionsaufruf ohne Suffix. Die Argumente für eine Funktion in der drei Formen sind identisch. Nur die Funktionen mit SQLCHAR \* Argumente oder SQLPOINTER-Argumente, die auf Zeichenfolgen verweisen erfordern Unicode und ANSI-Formulare. Für Funktionen, die Argumente, die als einen Zeichentyp handelt, z. B. deklariert werden können, haben **SQLBindCol** oder **SQLGetData** (die verfügen nicht über Unicode und ANSI-Formulare), das Argument kann als der Unicode-Datentyp deklariert werden die ANSI eingeben, oder geben Sie im Falle eines C-Argument, das SQL_C_TCHAR-Makro. Weitere Informationen finden Sie unter [Unicode-Daten](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Eine Anwendung kann als Unicode-Anwendung geschrieben werden, auch wenn keine Unicode-Treiber für ihn zur Bearbeitung verfügbar sind. Der Treiber-Manager werden Unicode-Funktionen und Datentypen in ANSI zugeordnet. Es gibt einige Einschränkungen in den Unicode, ANSI-Zuordnungen, die ausgeführt werden können. Das Vorhandensein eines Unicode-Treibers für die Unicode-Anwendung mit einer verbesserten Leistung führt und die Einschränkungen, die inhärente in Unicode zu ANSI-Zuordnungen entfernen.
