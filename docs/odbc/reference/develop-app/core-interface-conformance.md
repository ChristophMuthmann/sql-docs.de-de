---
title: "Haupt-Schnittstelle Konformität | Microsoft Docs"
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1df0215014eea87559e87aeb2f29e848e1473a66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="core-interface-conformance"></a>Core-Schnittstelle Konformität
Alle ODBC-Treiber müssen mindestens ein Hauptebenen-aufweisen Schnittstelle-Konformität. Da die Funktionen in die Core-Ebene diejenigen, die von interoperablen Anwendungen ausführen können die meisten generischen erforderlich sind, kann der Treiber mit solchen Anwendungen arbeiten. Die Funktionen in der Core-Ebene entsprechen auch auf die Funktionen, die in der ISO-CLI-Spezifikation definiert und auf die nonoptional Funktionen, die in der Open Group-CLI-Spezifikation definiert. Ein Hauptebenen-Benutzeroberfläche – konforme ODBC-Treiber kann die Anwendung die folgenden vornehmen:  
  
-   Reservieren und Freigeben von allen Arten von Handles, durch den Aufruf **SQLAllocHandle** und **SQLFreeHandle**.  
  
-   Jede Form von verwenden die **SQLFreeStmt** Funktion.  
  
-   Binden der Resultsetspalten, durch den Aufruf **SQLBindCol**.  
  
-   Behandeln von dynamischen Parametern, einschließlich Arrays von Parametern, die Eingabe nur in Richtung, durch den Aufruf **SQLBindParameter** und **SQLNumParams**. (Parameter in der Ausgabe Richtung sind 203 in Funktion [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Geben Sie einen Offset binden.  
  
-   Verwenden Sie das Dialogfeld "Data-at-Execution-", im Zusammenhang mit Aufrufe **SQLParamData** und **SQLPutData**.  
  
-   Verwalten von Cursorn und Cursornamen, durch den Aufruf **SQLCloseCursor**, **SQLGetCursorName**, und **SQLSetCursorName**.  
  
-   Erhalten Sie Zugriff auf die Beschreibung (Metadaten) von Resultsets, durch den Aufruf **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, und **SQLRowCount** . (Verwendung dieser Funktionen auf Spaltennummer 0 zum Abrufen von Metadaten Lesezeichen 204 in Features sind [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Abfragen des Datenwörterbuchs durch Aufrufen der Katalogfunktionen **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, und **SQLTables**.  
  
     Der Treiber ist nicht zur Unterstützung von mehrteiliger Namen der Datenbanktabellen und-Sichten erforderlich. (Weitere Informationen finden Sie unter Funktion 101 in [Ebene 1 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-1-interface-conformance.md) und 201 in Funktionen [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) Allerdings sind bestimmte Funktionen der SQL-92-Spezifikation, wie z. B. den Spalte Qualifizierung und die Namen der Indizes, syntaktisch vergleichbar sein, um mehrteilige benennen. Die vorhandene Liste der ODBC-Funktionen dient nicht zum Einfügen von neuer Optionen in dieser Aspekte der SQL-92.  
  
-   Verwalten von Datenquellen und Verbindungen, durch den Aufruf **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, und **SQLDriverConnect**. Abrufen von Informationen auf Treiber, unabhängig davon, welche ODBC level sie, durch den Aufruf unterstützen **SQLDrivers**.  
  
-   Vorbereiten und Ausführen von SQL-Anweisungen durch den Aufruf **SQLExecDirect**, **SQLExecute**, und **SQLPrepare**.  
  
-   Abrufen einer Zeile eines Resultsets oder mehrere Zeilen, nur vorwärts durch Aufrufen von **SQLFetch** oder durch Aufrufen von **SQLFetchScroll** mit der *FetchOrientation* Argument Legen Sie auf SQL_FETCH_NEXT.  
  
-   Abrufen eine ungebundene Spalte in Teilen, durch den Aufruf **SQLGetData**.  
  
-   Abrufen der aktuellen Werte aller Attribute durch Aufrufen **SQLGetConnectAttr**, **SQLGetEnvAttr**, und **SQLGetStmtAttr**, und legen Sie alle Attribute auf ihre Standardwerte fest und bestimmte Attribute nicht standardmäßige Werte festzulegen, durch den Aufruf **SQLSetConnectAttr**, **SQLSetEnvAttr**, und **SQLSetStmtAttr**.  
  
-   Bearbeiten Sie bestimmte Felder beschreibungshierarchie, aus der durch den Aufruf **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, und **SQLSetDescRec**.  
  
-   Abrufen von Diagnoseinformationen, durch den Aufruf **SQLGetDiagField** und **SQLGetDiagRec**.  
  
-   Treiber-Funktionen, die durch den Aufruf erkennen **SQLGetFunctions** und **SQLGetInfo**. Darüber hinaus erkennt das Ergebnis jeder an eine SQL-Anweisung vorgenommen werden, bevor sie mit der Datenquelle, durch Aufrufen von gesendet wird Ersetzungen **SQLNativeSql**.  
  
-   Verwenden Sie die Syntax der **SQLEndTran** Commit eine Transaktion. Ein Hauptebenen-Treiber muss "true" Transaktionen nicht unterstützt. die Anwendung kann nicht aus diesem Grund für das SQL_ATTR_AUTOCOMMIT-Verbindungsattribut SQL_ROLLBACK noch SQL_AUTOCOMMIT_OFF angeben. (Weitere Informationen finden Sie unter Funktion 109 in [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Rufen Sie **SQLCancel** um das Dialogfeld "Data-at-Execution" abzubrechen und im multithread-Umgebungen, eine ODBC-Funktion ausführen in einem anderen Thread abgebrochen. Core-Level-Interface-Konformität Unterstützung für asynchrone Ausführung von Funktionen noch die Verwendung von nicht anordnet **SQLCancel** zum Abbrechen von einer ODBC-Funktion, die asynchron ausgeführt. Weder die Plattform noch der ODBC-Treiber muss für den Treiber für die Durchführung von unabhängigen Aktivitäten gleichzeitig multithread sein. Allerdings muss der ODBC-Treiber im multithread-Umgebungen threadsicher sein. Serialisierung von Anforderungen von der Anwendung lässt konforme sich dieser Spezifikation zu implementieren, obwohl es schwerwiegende Leistungsprobleme erstellen kann.  
  
-   Abrufen der SQL_BEST_ROWID Zeile identifizieren-Spalte mit Tabellen, durch Aufrufen **SQLSpecialColumns**. (Unterstützung für SQL_ROWVER Features sind in 208 [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  ODBC-Treiber müssen die Funktionen in der Konformitätsgrad des Core-Schnittstelle implementieren.
