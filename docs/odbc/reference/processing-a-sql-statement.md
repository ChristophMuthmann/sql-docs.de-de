---
title: Verarbeiten einer SQL-Anweisung | Microsoft Docs
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
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3da40899e3c2289ef53908723642bd5be8e11db8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="processing-a-sql-statement"></a>Verarbeiten einer SQL-Anweisung
Erläutert die Verfahren für die Verwendung von SQL programmgesteuert, ist es erforderlich, die erläutern, wie eine SQL-Anweisung verarbeitet wird. Die Schritte beziehen sich alle drei Methoden, obwohl der einzelnen Techniken zu unterschiedlichen Zeiten ausgeführt. Die folgende Abbildung zeigt die Schritte zur bei der Verarbeitung einer SQL-Anweisung, die im weiteren Verlauf dieses Abschnitts erläutert werden.  
  
 ![Schritte zum Verarbeiten einer SQL-Anweisung](../../odbc/reference/media/pr01.gif "pr01")  
  
 Um eine SQL-Anweisung verarbeiten zu können, führt ein DBMS die folgenden fünf Schritte:  
  
1.  Das DBMS analysiert zunächst die SQL-Anweisung. Es umbricht die Anweisung, in einzelne Wörter, die als Token bezeichnet, stellt sicher, dass die Anweisung ein gültiges Verb und gültige Klauseln usw. aufweist. In diesem Schritt können Syntaxfehler und orthographische erkannt werden.  
  
2.  Das DBMS überprüft die Anweisung. Er überprüft, ob die Anweisung anhand der Systemkatalog. Führen Sie die Tabellen, die mit dem Namen in der Anweisung in der Datenbank vorhanden? Führen Sie alle Spalten vorhanden sind, und sind die Spaltennamen eindeutig? Verfügt der Benutzer die erforderlichen Berechtigungen zum Ausführen der Anweisung? In diesem Schritt können bestimmte semantische Fehler erkannt werden.  
  
3.  Das DBMS generiert ein Plans für die Anweisung. Die Zugriffsplan ist eine binäre Darstellung der Schritte, die erforderlich sind, um die Anweisung auszuführen. Es ist die DBMS-Entsprechung von ausführbarem Code.  
  
4.  Das DBMS optimiert den Plan zugreifen. Es wird erklärt, verschiedene Arten der Zugriffsplan durchzuführen. Kann ein Index zum Beschleunigen der Suche werden verwendet? Sollte das DBMS weisen Sie zunächst eine Suchbedingung zu Tabelle A und dann mit Tabelle B zu verknüpfen, oder sollte er mit den Join beginnen und verwenden Sie anschließend die Suchbedingung? Kann eine sequenzielle Suche über eine Tabelle vermieden oder auf eine Teilmenge der Tabelle reduziert? Nach der Untersuchung der alternativen, wählt das DBMS eine davon.  
  
5.  Das DBMS führt die Anweisung durch die Zugriffsplan ausführen.  
  
 Die Schritte, die zum Verarbeiten von einer SQL-Anweisung verwendet variieren hinsichtlich der Menge des von Ihnen geforderten Datenbankzugriff und die Zeitspanne, die sie verwenden. Analysieren Sie eine SQL-Anweisung erfordert keinen Zugriff auf die Datenbank und kann sehr schnell erfolgen. Optimierung, andererseits, ist ein sehr CPU-intensiv verarbeiten und erfordert Zugriff auf den Systemkatalog. Für eine komplexe und mehreren Tabellen basierende Abfrage kann der Optimierer Tausende von verschiedenen Methoden zum Ausführen derselben Abfrage durchsuchen. Die Kosten der Ausführung der Abfrage ineffizient ist jedoch so hoch, dass die Zeitdauer, die in der Optimierung mehr als in höhere Geschwindigkeit der abfrageausführung wiederhergestellt wird. Dies ist sogar noch stärker wichtig, wenn die gleichen optimierte Zugriffsplan immer wieder zum Ausführen von Abfragen verwendet werden kann.
