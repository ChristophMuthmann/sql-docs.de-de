---
title: Kompilieren eines eingebetteten SQL-Programms | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b4914a0f7c426f8409c53835e84ff26cecca94ba
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="compiling-an-embedded-sql-program"></a>Kompilieren eines eingebetteten SQL-Programms
Da eine embedded SQL-Programm eine Mischung aus SQL- und Host-sprachanweisungen enthält, kann es direkt an einen Compiler der Hostsprache übermittelt werden. Stattdessen wird er durch den Upgradevorgang kompiliert. Obwohl dabei aus einem Produkt zu einem anderen Produkt im Detail variiert, die Schritte sind ungefähr gleich für alle Produkte.  
  
 Diese Abbildung zeigt die Schritte zum Kompilieren eines eingebetteten SQL-Programms erforderlich.  
  
 ![Schritte zum Kompilieren eines eingebetteten SQL-Programms](../../odbc/reference/media/pr02.gif "pr02")  
  
 Die folgenden fünf Schritte sind beim Kompilieren eines eingebetteten SQL-Programms beteiligt:  
  
1.  Embedded SQL-Programm wird an die SQL-vorkompilierten eine Programmiertool übermittelt. Die vorkompilierten scannt das Programm, findet die embedded SQL-Anweisungen und verarbeitet sie. Eine andere vorkompilierten ist erforderlich, damit jeder Programmiersprache, die vom DBMS unterstützt. DBMS-Produkte in der Regel bieten Precompilers für eine oder mehrere Sprachen, z. B. C, Pascal, COBOL, Fortran, Ada, PL / I und verschiedene Sprachen der Assembly.  
  
2.  Die vorkompilierten erstellt zwei Ausgabedateien. Die erste Datei wird die Quelldatei, die embedded SQL-Anweisungen entfernt. An ihrer Stelle ersetzt die vorkompilierten Aufrufe von proprietären DBMS-Routinen, die zur Laufzeit Links zwischen der Anwendung und das DBMS bereitstellen. In der Regel werden die Namen und die aufrufenden Sequenzen dieser Routinen nur für den vorkompilierten und das DBMS bezeichnet; Sie eignen sich nicht um eine öffentliche Schnittstelle für das DBMS. Die zweite Datei ist eine Kopie aller embedded SQL-Anweisungen in der Anwendung verwendet. Diese Datei ist ein Datenbank-Request-Modul oder DBRM bezeichnet.  
  
3.  Die Ausgabe der Quelle-Datei aus der vorkompilierten wird für die Host-Programmiersprache (z. B. eine C- oder COBOL-Compiler) für den standard-Compiler gesendet. Der Compiler den Quellcode verarbeitet und Objektcode als Ausgabe erzeugt. Beachten Sie, dass dieser Schritt hat nichts mit dem DBMS oder mit SQL.  
  
4.  Der Linker akzeptiert die Objektmodule, die vom Compiler generierte, verknüpft diese mit verschiedenen Bibliotheksroutinen und erzeugt ein ausführbares Programm. Die Bibliotheksroutinen mit verknüpft, das ausführbare Programm enthalten die proprietären DBMS-Routinen, die in Schritt 2 beschrieben.  
  
5.  Das Datenbank-Anforderung-Modul generiert, die für den vorkompilierten wird mit einem Hilfsprogramm der speziellen Bindung gesendet werden. Dieses Dienstprogramm überprüft die SQL-Anweisungen, analysiert, überprüft hat, und optimiert werden und anschließend ein Plans für die for each-Anweisung erzeugt. Das Ergebnis ist eine kombinierte Zugriffsplan für das gesamte Programm, das eine ausführbare Version der eingebetteten SQL-Anweisungen darstellt. Das Hilfsprogramm Bindung speichert den Plan in der Datenbank, in der Regel der Name des Anwendungsprogramms, die sie verwenden zuweisen. Gibt an, ob dieser Schritt zur Kompilierzeit oder zur Laufzeit stattfindet, hängt das DBMS ab.  
  
 Beachten Sie, die die Schritten zum Kompilieren eines eingebetteten SQL-Programms lehnt sich eng mit den zuvor beschriebenen Schritten korrelieren [eine SQL-Anweisung verarbeiten](../../odbc/reference/processing-a-sql-statement.md). Insbesondere Beachten Sie, dass der vorkompilierten die SQL-Anweisungen aus den Sprachcode der Host trennt, und die Bindung Hilfsprogramm analysiert und überprüft die SQL-Anweisungen und erstellt die Zugriffspläne. Im DBMS-Systeme, in denen Schritt 5 zum Zeitpunkt der Kompilierung stattfindet, werden die ersten vier Schritte eine SQL-Anweisung zu verarbeiten zum Zeitpunkt der Kompilierung während der letzte Schritt (Ausführung) zur Laufzeit stattfindet. Dies hat die Auswirkungen bei der Ausführung von Abfragen in solchen DBMS sehr schnell.
