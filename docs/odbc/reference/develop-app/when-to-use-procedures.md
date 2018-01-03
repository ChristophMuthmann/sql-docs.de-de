---
title: Verwendung von Prozeduren | Microsoft Docs
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
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f62c820f57fba7af608a870e00e0b2ddf0ad13b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="when-to-use-procedures"></a>Verwendung von Prozeduren
Es gibt diverse Vorteile gegenüber der Verwendung von Prozeduren, alle basiert sowohl auf der Tatsache, dass Prozeduren verschiebt SQL-Anweisungen von der Anwendung an die Datenquelle. Nun muss nur noch in der Anwendung ist eine interoperable Prozeduraufruf. Diese bietet folgende Vorteile:  
  
-   **Leistung** Prozeduren sind in der Regel die schnellste Möglichkeit zum Ausführen von SQL-Anweisungen. Wie vorbereiteten Ausführung ist die Anweisung kompiliert und in zwei separate Schritte ausgeführt. Im Gegensatz zu vorbereitete Ausführung werden Prozeduren nur zur Laufzeit ausgeführt. Sie werden zu einem anderen Zeitpunkt kompiliert.  
  
-   **Geschäftsregeln** ein *Geschäftsregel* ist eine Regel über die Möglichkeit, in dem ein Unternehmen Business verfügt. Beispielsweise kann nur eine Person mit dem Titel Vertriebsmitarbeiter zulässig neue Bestellungen hinzufügen. Platzieren diese Regeln in Prozeduren kann einzelne Unternehmen vertikale Anwendungen anpassen, indem Sie Umschreiben der Prozeduren, die von der Anwendung aufgerufen werden, ohne den Anwendungscode ändern zu müssen. Z. B. eine Anwendung möglicherweise rufen Sie die Prozedur **InsertOrder** mit einer festen Anzahl von Parametern; genau wie **InsertOrder** wird implementiert von Unternehmen zu Unternehmen kann variieren.  
  
-   **Replaceability** eng mit überführen Geschäftsregeln in den Prozeduren wird die Tatsache, dass Prozeduren ersetzt werden können, ohne die Anwendung neu zu kompilieren. Wenn eine Geschäftsregel ändert, nachdem ein Unternehmen gekauft haben und eine Anwendung installiert wurde, kann das Unternehmen die Prozedur, die mit dieser Regel ändern. Vom Standpunkt der Anwendung hat nichts geändert. Er ruft immer noch eine bestimmte Prozedur um eine bestimmte Aufgabe auszuführen.  
  
-   **DBMS-spezifische SQL** Prozeduren bieten eine Möglichkeit, Anwendungen für DBMS-spezifische SQL ausnutzen und weiterhin interoperabel. Z. B. möglicherweise eine Prozedur auf einem DBMS, die Control-of-Flow-Anweisungen in SQL unterstützt abfangen und Wiederherstellen nach Fehlern, während eine Prozedur auf einem DBMS, die Control-of-Flow-Anweisungen nicht unterstützt einfach einen Fehler zurückgeben kann.  
  
-   **Prozeduren überleben Transaktionen** für einige Datenquellen werden die Zugriffspläne für alle vorbereiteten Anweisungen für eine Verbindung gelöscht, wenn eine Transaktion ein Commit oder Rollback ist. Durch Platzieren von SQL-Anweisungen in Prozeduren, die dauerhaft in der Datenquelle gespeichert sind, überstehen die Anweisungen für die Transaktion. Angibt, ob die Prozeduren überleben, in eine vorbereitete, teilweise vorbereitet wurde, oder der Vorbereitung Zustand ist DBMS-spezifische.  
  
-   **Trennen Sie die Entwicklung** Prozeduren können getrennt vom Rest der Anwendung entwickelt werden. In großen Unternehmen kann dies eine Möglichkeit, die weitere Ausführung die Fähigkeiten sehr spezielle Programmierer ausnutzen bereitstellen. Das heißt, Anwendungsprogrammierer, Benutzeroberflächen-Code zu schreiben und Datenbankprogrammierer können Prozeduren schreiben.  
  
 Prozeduren sind im Allgemeinen von vertikalen und benutzerdefinierten Anwendungen verwendet. Diese Anwendungen festen Aufgaben tendenziell, und es ist möglich, hartcodieren Prozeduraufrufe darin. Eine Anwendung kann z. B. die Prozeduren aufrufen **InsertOrder**, **DeleteOrder**, **UpdateOrder**, und **GetOrders** .  
  
 Es ist ratsam, die vom generischen Clientanwendungen Prozeduren aufrufen. Prozeduren in der Regel zum Ausführen einer Aufgabe im Kontext einer bestimmten Anwendung geschrieben werden, und daher keine keine Use an generischer Anwendungen. Beispielsweise verfügt ein Arbeitsblatt keinen Grund, rufen Sie die **InsertOrder** aufgeführten Verfahren. Darüber hinaus sollten allgemeine Anwendungen Prozeduren nicht zur Laufzeit Wert bereitstellen schneller anweisungsausführung erstellen; ist nicht nur diesem wahrscheinlich langsamer als eine vorbereitete oder direkte Ausführung werden darüber hinaus müssen DBMS-spezifische SQL-Anweisungen.  
  
 Eine Ausnahme ist die Anwendungsentwicklung-Umgebungen, die bieten häufig eine Möglichkeit für Programmierer, die SQL-Anweisungen erstellen, die Prozeduren ausführen und möglicherweise bieten eine Möglichkeit für Programmierer, die zum Testen von Prozeduren. Umgebungen Aufruf **SQLProcedures** auf die Liste verfügbarer Prozeduren und **SQLProcedureColumns** um Eingabe-, Eingabe/Ausgabe- und Ausgabeparameter aufzulisten, die Prozedur zurückgeben, Wert und Spalten keine Resultsets, die von einer Prozedur erstellt wird. Auf diese Weise müssen jedoch im Voraus auf jede Datenquelle entwickelt werden; Dazu müssen Sie dies DBMS-spezifische SQL-Anweisungen.  
  
 Es gibt drei gravierenden Nachteile Prozeduren verwenden. Das erste ist, dass Prozeduren geschrieben und für jede DBMS, mit dem die Anwendung ausgeführt wird, kompiliert werden müssen. Während dies kein Problem für benutzerdefinierte Anwendungen darstellt, kann er Entwicklung und Wartung für vertikale Anwendungen, die mit einer Anzahl von DBMS ausgeführt erheblich erhöhen.  
  
 Der zweite Nachteil ist, dass viele Datenbankmanagementsysteme Prozeduren nicht unterstützt werden. In diesem Fall ist dies wahrscheinlich ein Problem für vertikale Anwendungen, die mit einer Anzahl von DBMS-Systeme ausgeführt werden. Um zu bestimmen, ob Prozeduren unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_PROCEDURES.  
  
 Der dritte Nachteil, der insbesondere für entwicklungsumgebungen Anwendung gilt, ist, dass die ODBC-Grammatik eine standard zum Erstellen von Prozeduren nicht definiert ist. D. h. auch wenn Clientanwendungen Prozeduren interoperably aufrufen können, können nicht sie diese interoperably erstellen.
