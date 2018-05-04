---
title: Transaktionsisolationsstufen | Microsoft-Dokumentation
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
- dirty reads [ODBC]
- isolation levels [ODBC]
- nonrepeatable reads [ODBC]
- read uncommitted [ODBC]
- read committed [ODBC]
- serializable reads [ODBC]
- phantoms [ODBC]
- transaction isolation [ODBC]
- repeatable reads [ODBC]
- transactions [ODBC], isolation
ms.assetid: 0d638d55-ffd0-48fb-834b-406f466214d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ae915d748f59b48bf4a4a8a4a6e8b9cc168ae57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-isolation-levels"></a>Transaktionsisolationsstufen
*Isolationsstufen von Transaktionen* sind ein Maß für den Umfang an, in dem Isolation erfolgreich ausgeführt wird. Insbesondere werden Isolationsstufen von Transaktionen durch das Vorhandensein oder fehlen der folgenden Phänomene definiert:  
  
-   **Dirty Reads** ein *"unsauberen" Lesevorgang* tritt auf, wenn eine Transaktion Daten liest, die noch kein Commit ausgeführt wurde. Nehmen wir beispielsweise an Transaktion 1 Updates einer Zeile. Transaktion 2 liest die aktualisierte Zeile vor dem Commit der Transaktion 1-Update. Wenn Transaktion 1 die Änderung ein Rollback, werden Transaktion 2 Daten gelesen haben, das als betrachtet wird nie vorhanden waren.  
  
-   **Nicht wiederholbaren Lesevorgängen** ein *nicht wiederholbarer Lesevorgang* tritt auf, wenn eine Transaktion die gleiche Zeile zweimal liest, sondern verschiedene Daten jedes Mal ruft. Nehmen wir beispielsweise an Transaktion 1 liest eine Zeile. Transaktion 2 aktualisiert oder löscht diese Zeile und führt einen Commit für die Update- oder Delete. Wenn Transaktion 1 Zeile filtereinstellungen, andere Zeilenwerte abgerufen oder erkennt, dass die Zeile gelöscht wurde.  
  
-   **Phantome** ein *phantom* eine Zeile, die mit den Suchkriterien übereinstimmt, aber nicht anfänglich sichtbar ist. Angenommen Sie beispielsweise, bis Transaktion 1 einen Satz von Zeilen liest, die einige Suchkriterien erfüllen. Transaktion 2 generiert eine neue Zeile (über ein Update oder Insert), die die Suchkriterien für die Transaktion 1 entspricht. Wenn die Transaktion 1 die Anweisung reexecutes, die die Zeilen liest, ruft er einen anderen Satz von Zeilen ab.  
  
 Die vier Transaktionsisolationsstufen (gemäß SQL-92) sind im Hinblick auf diese Phänomene definiert. In der folgenden Tabelle kennzeichnet ein "X" jedes Phänomen, die auftreten können.  
  
|Transaktionsisolationsstufe|Dirty reads|Nicht wiederholbaren Lesevorgängen|Phantome|  
|---------------------------------|-----------------|-------------------------|--------------|  
|Read Uncommitted|X|X|X|  
|Read Committed|--|X|X|  
|Repeatable Read|--|--|X|  
|Serializable|--|--|--|  
  
 Die folgende Tabelle beschreibt die auf einfache Weise, dass möglicherweise ein DBMS Isolationsstufen von Transaktionen implementieren.  
  
> [!IMPORTANT]  
>  Die meisten DBMS verwenden komplexe Schemas als diese, um die Parallelität zu erhöhen. Diese Beispiele dienen nur zu Illustrationszwecken. Insbesondere ODBC nicht wie bestimmte DBMS vorschreiben Transaktionen voneinander isoliert.  
  
|Transaktionsisolation|Mögliche Implementierung|  
|---------------------------|-----------------------------|  
|Read Uncommitted|Transaktionen sind nicht voneinander isoliert. Wenn das DBMS anderen Isolationsstufen von Transaktionen unterstützt, wird es geeignete Mechanismus verwendet, um diese Grade implementiert ignoriert. Damit sie andere Transaktionen nicht nachteilig auswirken, sind Transaktionen auf Read Uncommitted-Ebene ausgeführt wird, in der Regel schreibgeschützt.|  
|Read Committed|Die Transaktion wird wartet, bis für den Schreibzugriff gesperrt durch andere Transaktionen Zeilen entsperrt werden; Dies verhindert "unsaubere" Daten lesen.<br /><br /> Die Transaktion enthält, die eine Lesesperre (Wenn sie nur die Zeile liest) oder Schreibzugriff sperren (falls er aktualisiert oder löscht die Zeile) auf der aktuellen Zeile, um zu verhindern, dass andere Transaktionen aktualisieren oder löschen. Die Transaktion frei Lesesperren, wenn es aus der aktuellen Zeile bewegt wird. Sie enthält Schreibsperren, bis ein Commit oder Rollback.|  
|Repeatable Read|Die Transaktion wird wartet, bis für den Schreibzugriff gesperrt durch andere Transaktionen Zeilen entsperrt werden; Dies verhindert "unsaubere" Daten lesen.<br /><br /> Die Transaktion enthält Lesesperren in allen Zeilen, die er an die Anwendung und Write-Sperren für alle Zeilen zurückgibt, sie Einfüge-, Update- oder löscht. Wenn die Transaktion, die SQL-Anweisung enthält beispielsweise **wählen Sie \* FROM Orders**, Lesesperren Transaktion Zeilen, die sie für die Anwendung ruft ab. Wenn die Transaktion, die SQL-Anweisung umfasst **Löschen von Aufträgen, in dem Status "Geschlossen" =**, Schreibsperren Transaktion Zeilen, die sie gelöscht.<br /><br /> Da andere Transaktionen nicht aktualisieren oder löschen diese Zeilen, wird die aktuelle Transaktion nicht wiederholbaren Lesevorgängen vermieden. Die Transaktion hebt seine sperren, wenn ein Commit oder Rollback.|  
|Serializable|Die Transaktion wird wartet, bis für den Schreibzugriff gesperrt durch andere Transaktionen Zeilen entsperrt werden; Dies verhindert "unsaubere" Daten lesen.<br /><br /> Die Transaktion eine Sperre read (wenn es nur Zeilen gelesen werden) oder Schreibsperre (falls er kann aktualisieren oder Löschen von Zeilen) in den Bereich der Zeilen auswirkt. Z. B., wenn die Transaktion, die SQL-Anweisung enthält **wählen \* FROM Orders**, der Bereich ist die gesamte Tabelle "Orders"; die lesen-Transaktionssperren der Tabelle, jedoch nicht zu, dass alle neuen Zeilen in diese eingefügt werden soll. Wenn die Transaktion, die SQL-Anweisung enthält **Löschen von Aufträgen, in dem Status "Geschlossen" =**, der Bereich liegt, alle Zeilen mit dem Status "Geschlossen"; die Transaktionssperren-Schreibvorgänge aller Zeilen in der Orders Tabelle mit dem Status "Geschlossen", jedoch nicht erlauben Sie keine Zeilen eingefügt oder aktualisiert, sodass die daraus resultierende Zeile den Status "Geschlossen" aufweist.<br /><br /> Da andere Transaktionen nicht aktualisieren oder Löschen von Zeilen in den Bereich, wird die aktuelle Transaktion nicht wiederholbaren Lesevorgängen vermieden. Da andere Transaktionen Zeilen im Bereich einfügen können, wird die aktuelle Transaktion Phantome vermieden. Die Transaktion gibt die Sperre frei, wenn ein Commit oder Rollback.|  
  
 Es ist wichtig zu beachten, dass die Transaktionsisolationsstufe einer Transaktion Möglichkeit zum Anzeigen von eigenen Änderungen nicht beeinträchtigt; Transaktionen können immer alle Änderungen erkennen, die sie vornehmen. Angenommen, eine Transaktion möglicherweise bestehen aus zwei **UPDATE** Anweisungen, die das erste löst die Zahlung aller Mitarbeiter aus, um 10 Prozent und dem zweiten legt das Bezahlen von Mitarbeitern über einige Höchstmenge dieser Menge. Ist der Vorgang erfolgreich als einzelne Transaktion, da die zweite **UPDATE** Anweisung kann die Ergebnisse der ersten angezeigt.
