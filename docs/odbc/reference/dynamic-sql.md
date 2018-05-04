---
title: Dynamisches SQL | Microsoft Docs
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
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9804e42182f691702e379e48cc2e445daa24351d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-sql"></a>Dynamische SQL-Anweisungen
Obwohl statisches SQL auch in vielen Fällen funktioniert, besteht eine Klasse von Anwendungen, in denen der Datenzugriff im Voraus nicht bestimmt werden kann. Nehmen Sie z. B. an, dass eine Kalkulationstabelle kann der Benutzer eine Abfrage eingeben, die das Arbeitsblatt, das DBMS dann zum Abrufen von Daten sendet. Der Inhalt dieser Abfrage können nicht für den Programmierer offensichtlich bekannt sein, wenn die Tabellenkalkulationsprogramm geschrieben wird.  
  
 Um dieses Problem zu beheben, verwendet das Arbeitsblatt eine Form von embedded SQL, dynamische SQL-Anweisungen aufgerufen. Im Gegensatz zur statischen SQL-Anweisungen, die in der Anwendung hartcodiert sind, können dynamische SQL-Anweisungen zur Laufzeit erstellt und in eine Zeichenfolgenvariable für den Host platziert werden. Sie werden dann zur Verarbeitung an das DBMS gesendet. Da das DBMS ein Plans für die Laufzeit für dynamische SQL-Anweisungen generieren muss, ist dynamisches SQL i. a. langsamer als statische SQL. Beim Kompilieren eines Programms, dynamische SQL-Anweisungen enthält, werden die dynamischen SQL-Anweisungen nicht aus der Anwendung, wie statische SQL entfernt. Stattdessen werden sie durch einen Funktionsaufruf ersetzt, die die Anweisung an das DBMS übergibt; statische SQL-Anweisungen im selben Programm werden normalerweise behandelt.  
  
 Die einfachste Möglichkeit, eine dynamische SQL-Anweisung auszuführen, ist mit einer EXECUTE IMMEDIATE-Anweisung. Diese Anweisung übergibt die SQL-Anweisung an das DBMS für die Kompilierung und Ausführung an.  
  
 Ein Nachteil der EXECUTE IMMEDIATE-Anweisung ist, dass das DBMS durchlaufen müssen fünf Schritte der Verarbeitung einer SQL-Anweisung jedes Mal, wenn die Anweisung ausgeführt wird. Der Aufwand, die bei diesem Vorgang kann sehr erheblich sein, wenn mehrere-Anweisungen dynamisch ausgeführt werden und unnötig, ist Wenn diese Anweisungen ähneln. Um dieses Problem zu beheben, bietet dynamische SQL optimierten Form der Ausführung aufgerufen vorbereiteten Ausführung wird dem verwendet die folgenden Schritte aus:  
  
1.  Das Programm erstellt eine SQL-Anweisung in einem Puffer, ebenso wie bei der EXECUTE IMMEDIATE-Anweisung dar. Anstelle von Hostvariablen kann ein Fragezeichen (?) ersetzt werden, für die eine Konstante an eine beliebige Stelle im Text Anweisung, um anzugeben, dass ein Wert für die Konstante werden später bereitgestellt werden. Das Fragezeichen wird als eine parametermarkierung aufgerufen.  
  
2.  Die Anwendung übergibt die SQL-Anweisung an das DBMS mit eine PREPARE-Anweisung, welche Anforderungen an, dass das DBMS analysieren, zu überprüfen, und optimieren die Anweisung und generieren eine Ausführung planen. Das Programm verwendet dann eine EXECUTE-Anweisung (nicht EXECUTE IMMEDIATE-Anweisung), um die PREPARE-Anweisung zu einem späteren Zeitpunkt auszuführen. Parameterwerte für die Anweisung über eine besondere Datenstruktur, die als SQL-Datenbereich oder SQLDA übergibt.  
  
3.  Das Programm können die EXECUTE-Anweisung wiederholt wird, unterschiedliche Parameterwerte jedem angeben die dynamische-Anweisung ausgeführt wird.  
  
 Die vorbereitete Ausführung ist noch nicht mit statischen SQL identisch. In statischen SQL erfolgen die ersten vier Schritte der Verarbeitung einer SQL-Anweisung zum Zeitpunkt der Kompilierung. Bei der vorbereiteten Ausführung dieser Schritte weiterhin stattfinden zur Laufzeit, aber sie nur einmal ausgeführt werden; Ausführung des Plans findet statt nur EXECUTE aufgerufen wird. Dadurch werden in der Architektur von dynamischem SQL inhärenten Leistung Nachteile zu vermeiden. Die nächste Abbildung zeigt die Unterschiede zwischen statischen SQL, dynamische SQL mit unmittelbare Ausführung und dynamischem SQL mit vorbereitete Ausführung.
