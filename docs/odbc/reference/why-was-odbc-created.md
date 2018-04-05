---
title: Warum wurde ODBC erstellt? | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33cc5f63c34618f51196e173e58adbac58377f29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="why-was-odbc-created"></a>Warum wurde ODBC erstellt?
In der Vergangenheit verwendet Unternehmen eine einzelne DBMS. Jeglicher Datenbankzugriff erfolgte durch Front-End des entsprechenden Systems oder Anwendungen, die ausschließlich mit diesem System funktioniert geschrieben. Allerdings gestartet Computer vergrößert wurde, und weitere Computerhardware und-Software verfügbar war, Unternehmen, unterschiedliche DBMS abzurufen. Die Gründe wurden viele: Personen gekauft kostengünstigsten, war war schnellsten, was sie bereits wussten, was auf dem Markt, was am besten für eine einzelne Anwendung funktioniert neueste wurde. Aus anderen Gründen wurden zusammenfallen und Fusionen verwendet, bei denen aufwies Abteilungen, die zuvor von einer einzelnen DBMS jetzt mehrere.  
  
 Das Problem wurde durch die Einführung von PCs auch komplexere. Diese Computer in eine Vielzahl von Tools für Abfragen, analysieren und Anzeigen von Daten, zusammen mit einer Reihe von kostengünstigen, einfach zu bedienenden Datenbanken gebracht wird. Von nun an werden musste ein einzelnes Corporation häufig Daten unzählige Desktops, Server und Minicomputern verteilt, in einer Vielzahl von inkompatiblen Datenbanken gespeichert und auf eine große Anzahl von verschiedenen Tools, die wenig von denen auf alle Daten abgerufen werden konnte.  
  
 Die letzte Abfrage wurden durch die Einführung von Client/Server-Umgebung, die effizienteste Nutzung von Computerressourcen sucht. Kostengünstigen PCs (Clients) auf dem Desktop befinden, und geben Sie sowohl ein grafisches Front-End auf Daten und eine Anzahl von kostengünstigen Tools, z. B. Tabellen, Diagramme, Programmen und beim Erstellen von Berichten. Kleincomputer und Mainframecomputer (Server) hosten die DBMS-Systeme, in dem sie ihre rechenleistung und einen zentralen Speicherort verwenden können, um schnelle und koordinierte Datenzugriff bereitzustellen. Klicken Sie dann wie wurde die Front-End-Software mit den Back-End-Datenbanken verbunden werden?  
  
 Ein ähnliches Problem Datenwachstums unabhängige Softwarehersteller (ISVs). Anbieter schreiben Datenbanksoftware für Kleincomputer und Mainframes wurden in der Regel gezwungen, eine Version einer Anwendung für jedes DBMS geschrieben, oder Schreiben von DBMS-spezifischen Code für jede DBMS, die sie zugreifen wollten. Schreiben von Software für Personalcomputer Lieferanten musste Data Access-Routinen für jeden unterschiedlichen DBMS zu schreiben, mit denen sie arbeiten möchten. Dies bedeutet häufig, riesige Menge an Ressourcen wurden aufgewendet, schreiben und Verwalten von Datenzugriff Routinen anstelle von Anwendungen und Anwendungen häufig nicht auf ihre Qualität aber auf, ob sie Daten in einem bestimmten DBMS zugreifen konnte verkauft wurden.  
  
 Beide Gruppen von Entwicklern benötigt wurde eine Möglichkeit, den Zugriff auf Daten in anderen DBMS. Die Gruppe Großrechner und Minicomputer benötigt eine Möglichkeit zum Zusammenführen von Daten aus anderen DBMS in einer einzigen Anwendung während die PC-Gruppe erforderlich, diese Möglichkeit als auch eine Möglichkeit, eine einzelne Anwendung schreiben, die unabhängig von der alle einem DBMS war. Beide Gruppen erforderlich kurz gesagt, interoperable Weise auf Daten zugreifen. Sie benötigt Datenbankkonnektivität öffnen.
