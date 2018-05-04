---
title: ODBC-Programmierer&#39;s-Referenz | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b4ac57816359fe1b69fb46d5d60967804cde5d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-programmer39s-reference"></a>ODBC-Programmierer&#39;s-Referenz
Die *ODBC Programmer's Reference* enthält folgende Abschnitte.  
  
-   [Neuigkeiten in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) Listet die neuen ODBC-Funktionen, die im SDK für Windows 8 hinzugefügt wurden.  
  
-   [Beispiel-ODBC-Anwendung](../../odbc/reference/sample-odbc-program.md) ein ODBC-Beispielprogramm zeigt.  
  
-   [Einführung in ODBC](../../odbc/reference/introduction-to-odbc.md) stellt einen kurzen Verlauf von Structured Query Language, ODBC und grundlegende Informationen über die ODBC-Schnittstelle.  
  
-   [Entwickeln von Anwendungen](../../odbc/reference/develop-app/developing-applications.md) enthält Informationen zum Entwickeln von Anwendungen, die die ODBC-Schnittstelle und Treiber, die ihn implementieren.  
  
-   [Installieren und Konfigurieren von ODBC-Software](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) enthält Informationen zu Installation und Setup Funktionsverweis DLL.  
  
-   [Entwickeln einen ODBC-Treiber](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) enthält Informationen über das Schreiben von einem Treiber.  
  
-   [API-Referenz](../../odbc/reference/syntax/odbc-reference.md) Syntax und die semantischen Informationen für alle ODBC-Funktionen enthält.  
  
-   [ODBC-Anhänge](../../odbc/reference/appendixes/odbc-appendixes.md) enthalten technische Details und Verweistabellen für ODBC-Fehlercodes, Datentypen und SQL-Grammatik.  
  
## <a name="working-with-the-odbc-documentation"></a>Arbeiten mit der ODBC-Dokumentation  
 Die ODBC-Schnittstelle für die Verwendung mit der Programmiersprache C konzipiert. Verwenden der ODBC-Schnittstelle umfasst drei Bereiche: SQL-Anweisungen, ODBC-Funktion aufrufen und C-Programmierung. In dieser Dokumentation wird Folgendes vorausgesetzt:  
  
-   Kenntnisse der Programmiersprache C.  
  
-   Allgemeine DBMS-Kenntnisse und Vertrautheit mit SQL.  
  
 Die folgenden typografischen Konventionen dienen.  
  
|Format|Syntaxelemente|  
|------------|--------------|  
|WÄHLEN SIE * AUS|Großbuchstaben Geben Sie an SQL-Anweisungen, Makronamen und Begriffe, die auf der Ebene Betriebssystembefehl verwendet.|  
|`RETCODE SQLFetch(hdbc)`|Die Festbreitenschriftart dient für Beispielbefehlszeilen und Programmcode.|  
|*argument*|Kursiv geschriebene Wörter Geben Sie den programmatischen Argumente, Information, dass der Benutzer oder die Anwendung muss bereitstellen oder word Betonung.|  
|**SQLEndTran**|Fett formatierte gibt an, dass die Syntax genau wie dargestellt, einschließlich Funktionsnamen, eingegeben werden muss.|  
|&#124;|Ein senkrechter Strich trennt zwei sich gegenseitig ausschließende Optionen in einer Syntaxzeile.|  
|...|Ellipsen gibt an, dass Argumente mehrmals wiederholt werden können.|  
|aus. aus. aus.|Eine Spalte mit den drei Punkten gibt die Fortsetzung des vorherigen Codezeilen an.|  
  
## <a name="about-the-code-examples"></a>Informationen zu den Codebeispielen  
 Die Codebeispiele in diesem Handbuch dienen nur zur Veranschaulichung. Da sie in erster Linie in ODBC-Prinzipien veranschaulichen geschrieben werden, wurde Effizienz reserviert manchmal Klarheit festgelegt. Darüber hinaus wurden ganze Bereiche des Codes in einigen Fällen aus Gründen der Übersichtlichkeit ausgelassen. Dazu gehören die Definitionen von nicht-ODBC-Funktionen (diese Funktionen nicht, deren Namen mit "SQL starten") und die meisten Fehlerbehandlung.  
  
 Alle Codebeispiele verwenden, ANSI-Zeichenfolgen und das gleiche Datenbankschema, die zu Beginn der dargestellt wird [Katalogfunktionen](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Empfohlene Lektüre  
 Weitere Informationen zu SQL stehen die folgenden Standards:  
  
-   Datenbanksprache – "SQL" mit der Datenintegrität zu optimieren, ANSI, 1989 ANSI x 3.135-1989.  
  
-   Datenbanksprache – SQL: X3H2 ANSI und ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Open Group, Datenverwaltung: Structured Query Language (SQL), Version 2 (The Open Group, 1996).  
  
 Zusätzlich zu den Standards und anbieterspezifische SQL-Handbücher, beschreiben viele Bücher SQL, einschließlich:  
  
-   Datum, C. J., mit Darwen Hugh: *eine Orientierungshilfe für die SQL-Standard* (Addison Wesley, 1993).  
  
-   Emerson, Stefan L. Darnovsky, Marcy und Bowman Dorena S.: *praktische SQL-Handbuch* (Addison Wesley, 1989).  
  
-   Groff, James r und Weinberg, Paul N.: *verwenden SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Grundlegendes zum SQL* (Sybex, 1990).  
  
-   Hursch, Stecker L. und Carolyn J.: *SQL, die strukturierte Abfragesprache* (Registerkarte Bücher, 1988).  
  
-   Melton, Jim und Simon "," Alan r: *Grundlegendes zu den neuen SQL: eine vollständige Anleitung* (Morgan Kaufmann Herausgebern, 1993).  
  
-   Pascal-Schreibweise, Fabian: *SQL- und relationale Grundlagen* (M & T Bücher, 1990).  
  
-   Trimble, J. Harvey, Jr. und Chappell, David: *eine Visual Einführung in SQL* (Wiley, 1989).  
  
-   Der van Lans, Rick F.: *Einführung in SQL* (Addison Wesley, 1988).  
  
-   Vang, Soren: *SQL und relationale Datenbanken* (Microtrend Buchexemplar, 1990).  
  
-   Viescas, John: *Kurzreferenz zu SQL* (Microsoft Corp., 1989).  
  
 Weitere Informationen zu transaktionsverarbeitung finden Sie unter:  
  
-   Grau, N. J. und Reuter, Andreas: *Transaktionsverarbeitung: Konzepte und Techniken* (Morgan Kaufmann Herausgebern, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise-Datenbankkonnektivität* (Wiley & Sons, 1993).  
  
 Weitere Informationen zur Call-Level-Schnittstellen sind die folgenden Standards verfügbar:  
  
-   Open Group *Datenverwaltung: SQL Call Level Interface (CLI), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995 Call-Level-Interface (SQL/CLI).  
  
 Weitere Informationen zu ODBC sind eine Anzahl von Büchern zur Verfügung, darunter:  
  
-   Geiger, Kyle: *in ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon "," Robert "," Charpentier "," Luc "," Oelschlager "," Jon "," Familiengeschichte aus?, Andrew Cross, Jim, "und" Lilley, Albert W.: *mithilfe von ODBC 2* (Que, 1994).  
  
-   Johnston, Tom und Osborne, kennzeichnen: *ODBC Developers Guide* (Howard W. Sams & Unternehmen, 1994).  
  
-   Nordamerika, Ken: *Windows Multi-DBMS-Programmierung: Verwenden von C++, Visual Basic, ODBC, OLE 2 und Tools für DBMS-Projekte* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, Michael O. Signore, Robert und Creamer, John: *der ODBC-Lösung, die Open Database Connectivity in verteilten Umgebungen* (McGraw Hill, 1995).  
  
-   Welch, Keith: *mithilfe von ODBC 2* (Que, 1994).  
  
-   Wittling, Bill: *bringen Sie sich selbst ODBC in 21 Tage* (Howard W. Sams & Unternehmen, 1994).
