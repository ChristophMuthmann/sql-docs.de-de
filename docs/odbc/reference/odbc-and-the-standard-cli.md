---
title: ODBC und die Standard-CLI | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3dd0120602e6f6fe82022aff75bb7d8157dd5bd8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-and-the-standard-cli"></a>ODBC und die Standard-CLI
ODBC richtet die folgenden Spezifikationen und Standards, die mit der Call-Level Interface (CLI) zu verarbeiten. (Die ODBC-Funktionen sind eine Obermenge aller dieser Standards.)  
  
-   Die Open Group CAE-Spezifikation "Datenverwaltung: SQL-Call-Level-Interface (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) Call-Level-Interface (SQL/CLI)  
  
 Als Ergebnis dieser Ausrichtung gilt Folgendes:  
  
-   Eine Anwendung, die in die Open Group und ISO-CLI-Spezifikationen geschrieben funktioniert mit einer ODBC-3. *x* oder eine Standards kompatible Treiber bei der Kompilierung mit der ODBC-3. *X* Header-Dateien und verknüpft Sie mit ODBC 3.. *X* Bibliotheken, und wenn sie Zugriff auf die vom Treiber über die ODBC 3. erlangt. *X* -Treiber-Manager.  
  
-   Ein Treiber, die den Spezifikationen Open Group und ISO-CLI geschrieben funktioniert mit einer ODBC 3.*.x* oder eine standardisierte Anwendung bei der Kompilierung mit der ODBC 3.*.x* Header-Dateien und verknüpft mit ODBC 3.*.x* Bibliotheken, und wenn die Anwendung erhält Zugriff auf die vom Treiber über die ODBC 3.*.x* -Treiber-Manager. (Weitere Informationen finden Sie unter [Standards kompatiblen Anwendungen und-Treiber](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 Der Konformitätsgrad des Core-Schnittstelle umfasst alle Funktionen in der ISO-CLI und die nonoptional Funktionen in der Open Group CLI. Optionale Features der Open Group CLI werden in höheren Schnittstelle Übereinstimmungsebenen angezeigt. Da alle ODBC-3. *x* Treiber sind erforderlich, um die Funktionen in der Konformitätsgrad des Core-Schnittstelle unterstützen, die Folgendes zutrifft:  
  
-   Eine ODBC-3. *x* Treiber unterstützt alle Funktionen, die von einer mit Standards kompatible Anwendung verwendet.  
  
-   Eine ODBC-3. *x* Anwendung, die nur die in ISO-CLI und nonoptional Funktionen der Open Group CLI funktioniert mit jeder Standards kompatible Treiber.  
  
 Zusätzlich zu den Call-Level-Interface-Spezifikationen, die in den ISO/IEC und Open Group-CLI-Standards enthalten sind implementiert ODBC die folgenden Funktionen. (Einige dieser Funktionen Waren in Versionen von ODBC vor ODBC 3.. *x*.)  
  
-   Mehrzeilige Abrufvorgänge durch einen einzigen Funktionsaufruf  
  
-   Binden an ein Array von Parametern  
  
-   Lesezeichenunterstützung einschließlich Abrufen von Lesezeichen, variabler Länge Lesezeichen und Bulk aktualisieren und Löschen von Lesezeichen-Vorgänge auf nicht zusammenhängende Zeilen  
  
-   Zeilenbezogene Bindungen  
  
-   Binden von offsets  
  
-   Unterstützung für Batches von SQL-Anweisungen in einer gespeicherten Prozedur oder als eine Abfolge von SQL-Anweisungen, die über ausgeführt wurden, **SQLExecute** oder **SQLExecDirect**  
  
-   Cursor für genaue oder Ungefähre Zeilenanzahl  
  
-   Update und Delete-Vorgänge und als Batch erstellten Updates und Löschvorgänge durch Funktionsaufruf positioniert (**SQLSetPos**)  
  
-   Katalogfunktionen, die Informationen aus dem Informationsschema ohne die Notwendigkeit zur Unterstützung von Informationsschemasichten extrahiert werden.  
  
-   Escapesequenzen für äußere Joins, Skalarfunktionen, Datetime-Literale, Intervall Literale und gespeicherten Prozeduren  
  
-   Codepage Übersetzung Bibliotheken  
  
-   Eines Treibers ANSI-Konformität Ebene und Unterstützung für SQL Reporting  
  
-   Bedarfsgesteuerte automatische Auffüllung der IPD-  
  
-   Verbesserte Diagnose und Zeilen- und Parameter-Status-arrays  
  
-   "DateTime", Intervall, numerische/Dezimalzahl und 64-Bit-Ganzzahl-Puffer Anwendungstypen  
  
-   Asynchrone Ausführung  
  
-   Unterstützung für gespeicherte Prozeduren,-Escapesequenzen, einschließlich Parameterbindungsmechanismen ausgeben und Katalogfunktionen  
  
-   Verbindungs-Erweiterungen, einschließlich der Unterstützung für-Verbindungsattributen und das Attribut durchsuchen
