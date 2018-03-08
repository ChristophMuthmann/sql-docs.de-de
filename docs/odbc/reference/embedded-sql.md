---
title: Embedded SQL | Microsoft Docs
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
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db7c9b02f885c09df1eccbdc27ef2fd895168848
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="embedded-sql"></a>Embedded SQL
Das erste Verfahren für das Senden von SQL-Anweisungen an das DBMS eingebettet ist SQL. Da SQL keine Variablen und die Control-of-Flow-Anweisungen verwendet werden, wird dies häufig als eine Datenbanksprache verwendet, die in einer konventionellen Programmiersprache, z. B. C# oder COBOL geschriebenes Programm hinzugefügt werden können. Dies ist eine zentrale Vorstellung von embedded SQL: Platzieren von SQL-Anweisungen in einem Programm auf einem Host Programmiersprache geschrieben. Nur kurz, werden die folgenden Techniken zum Einbetten von SQL-Anweisungen in einer Hostsprache verwendet:  
  
-   Embedded SQL-Anweisungen werden durch eine spezielle SQL-vorkompilierten verarbeitet. Alle SQL-Anweisungen mit einer Introducer beginnen und enden mit Abschlusszeichen, beide über die SQL-Anweisung für den vorkompilierten kennzeichnen. Die Introducer und Abschlusszeichen hängt von der Hostsprache. Beispielsweise ist die Introducer "EXEC SQL" in C# und "& SQL (" in MUMPS, und das Abschlusszeichen wird ein Semikolon (;) in C und einer schließenden Klammer im MUMPS.  
  
-   Variablen aus der Anwendung aufgerufen, Hostvariablen können in eingebetteten SQL-Anweisungen verwendet werden, wo Konstanten zulässig sind. Diese können bei der Eingabe verwendet werden, um eine SQL-Anweisung zu einer bestimmten Situation und bei der Ausgabe die Ergebnisse einer Abfrage erhält individuell anzupassen.  
  
-   Abfragen, die eine einzelne Zeile mit Daten zurückgeben, werden mit einer Singleton-SELECT-Anweisung behandelt; Diese Anweisung gibt die Abfrage und die Hostvariablen in den Daten zurückgegeben.  
  
-   Abfragen, die mehrere Datenzeilen zurückgeben werden mit Cursorn behandelt. Ein Cursor behält den Überblick über der aktuellen Zeile in einem Resultset. DECLARE CURSOR-Anweisung definiert die Abfrage, die OPEN-Anweisung beginnt die abfrageverarbeitung, die FETCH-Anweisung ruft aufeinander folgenden Zeilen mit Daten und die CLOSE-Anweisung beendet die Verarbeitung von Abfragen.  
  
-   Während ein Cursor geöffnet ist, können positionierte Update- und positionierte Delete-Anweisungen verwendet werden, aktualisieren oder löschen Sie die Zeile, die aktuell durch den Cursor ausgewählt ist.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Embedded SQL – Beispiel](../../odbc/reference/embedded-sql-example.md)  
  
-   [Kompilieren eines eingebetteten SQL-Programms](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [Statische SQL-Anweisungen](../../odbc/reference/static-sql.md)  
  
-   [Dynamisches SQL](../../odbc/reference/dynamic-sql.md)
