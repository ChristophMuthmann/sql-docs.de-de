---
title: Anwendungen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ba4e9a05f3dba74a973bf2b8b8a83a52ef78811
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="applications"></a>Anwendungen
Ein *Anwendung* ist ein Programm, das die ODBC-API für den Datenzugriff aufruft. Obwohl viele Arten von Anwendungen möglich sind, fallen in drei Kategorien unterteilt, die als Beispiele in diesem Handbuch verwendet werden.  
  
-   **Allgemeiner Anwendungen** diese werden auch als eingeschweißt Anwendungen oder Standardanwendungen bezeichnet. Allgemeine Anwendungen dienen zum Arbeiten mit einer Vielzahl von verschiedenen DBMS sind. Beispiele: ein Arbeitsblatt oder Statistiken-Pakete, die ODBC zum Importieren von Daten zur weiteren Analyse verwenden und ein Textverarbeitungsprogramm, die ODBC verwendet wird, um eine Mailingliste aus einer Datenbank abzurufen.  
  
     Eine wichtige Unterkategorie allgemeiner Anwendungen ist die Anwendung entwicklungsumgebungen wie z. B. PowerBuilder oder Microsoft® Visual Basic®. Auch wenn die Anwendungen, die mit diesen Umgebungen konstruiert wahrscheinlich nur mit einer einzelnen DBMS funktioniert, muss die Umgebung selbst mit mehreren DBMS zu arbeiten.  
  
     Was alle allgemeine Anwendungen gemeinsam haben werden, dass sie sehr interoperabel zwischen DBMS und sie zur Verwendung von ODBC in relativ generischer Form müssen. Weitere Informationen zur Interoperabilität finden Sie unter [Auswählen einer Ebene Interoperabilität](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Vertikale Anwendungen** vertikale Anwendungen nur ein Task, z. B. Auftragseingabe oder Produktion-Nachverfolgungsdaten, Ausführen von und Arbeiten mit eines Datenbankschemas, der vom Entwickler der Anwendung gesteuert wird. Für einen bestimmten Kunden funktioniert die Anwendung mit einer einzelnen DBMS. Ein kleines Unternehmen verwenden z. B. die Anwendung bei dBase, während ein großes Unternehmen mit Oracle verwenden kann.  
  
     Die Anwendung verwendet ODBC in einer Weise, dass die Anwendung nicht an alle ein DBMS gebunden ist, obwohl er auf eine begrenzte Anzahl von DBMS gebunden werden kann, die ähnliche Funktionalität bereitstellen. Der Anwendungsentwickler kann daher die Anwendung unabhängig von den DBMS verkaufen. Vertikale Anwendungen sind interoperabel, wenn sie entwickelt werden, aber manchmal angepasst, sodass noninteroperable Code enthalten, sobald der Kunde ein DBMS ausgewählt wurde.  
  
-   **Benutzerdefinierte Anwendungen** Custom Applications verwendet, um eine bestimmte Aufgabe in einem einzelnen Unternehmen auszuführen. Beispielsweise kann eine Anwendung in einem großen Unternehmen Sammeln von Umsatzdaten aus verschiedenen Abteilungen (von denen jeder einen unterschiedlichen DBMS verwendet) und einen einzigen Bericht erstellen. ODBC wird verwendet, da es eine gemeinsame Schnittstelle und Programmierer erspart von mehreren Schnittstellen zu erfahren. Solche Anwendungen sind im Allgemeinen nicht interoperabel und spezifische DBMS und Treiber geschrieben werden.  
  
 Eine Reihe von Tasks beziehen sich auf alle Anwendungen, unabhängig davon, wie sie ODBC verwenden. Zusammen definieren sie zum größten Teil des Ablaufs der alle ODBC-Anwendung. Die Aufgaben definiert sind:  
  
-   Auswählen einer Datenquelle, und sie eine Verbindung herstellen.  
  
-   Senden eine SQL-Anweisung für die Ausführung an.  
  
-   Abrufen von Ergebnissen (sofern vorhanden).  
  
-   Verarbeitungsfehler.  
  
-   Commit oder Rollback der Transaktion, die die SQL-Anweisung einschließen.  
  
-   Trennen die Datenquelle aus.  
  
 Da die meisten Datenzugriffe mit SQL ausgeführt wird, werden die primäre Aufgabe, die für die Anwendung ODBC verwenden SQL-Anweisungen zu senden und Abrufen der Ergebnisse (sofern vorhanden), das durch diese Anweisungen generiert werden. Andere Aufgaben, die für die Anwendung ODBC verwenden sind bestimmen und Treiber Funktionen anpassen und den Datenbankkatalog durchsuchen.

