---
title: Call-Level Schnittstellen | Microsoft Docs
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
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e22537b5ce7b2b1ecfdf579e78859812895671c2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="call-level-interfaces"></a>Call-Level-Schnittstellen
Das letzte Verfahren für das Senden von SQL-Anweisungen an das DBMS erfolgt über eine Call-Level-Interface (CLI). Ein Call-Level-Interface enthält eine Bibliothek von DBMS-Funktionen, die von der Anwendung aufgerufen werden kann. Folglich ähnelt statt SQL mit einer anderen Programmiersprache ausgeblendet, ein Call-Level-Interface routinemäßigen Bibliotheken an, die meisten Programmierer daran gewöhnt sind, zu verwenden, z. B. die Zeichenfolge, die e/a- oder die mathematische Bibliotheken in c-Hinweis Dieser DBMS-Systeme, die eingebettetes SQL unterstützen verfügen Sie bereits eine Call-Level-Interface, die Aufrufe an die von der vorkompilierten generiert werden. Allerdings sind diese Aufrufe nicht dokumentiert und können ohne vorherige Ankündigung geändert werden.  
  
 Call-Level-Schnittstellen werden häufig in Client/Server-Architekturen verwendet, in der die Anwendung (Client) auf einem Computer befindet, und das DBMS (Server) auf einem anderen Computer befindet. Die Anwendung ruft die CLI-Funktionen auf dem lokalen System und diese Aufrufe werden an das DBMS für die Verarbeitung über das Netzwerk gesendet.  
  
 Ein Call-Level-Interface ähnelt dynamische SQL-, SQL-Anweisungen an das DBMS für die Verarbeitung zur Laufzeit übergeben werden, aber es unterscheidet sich von embedded SQL als Ganzes, keine eingebetteten SQL-Anweisungen vorhanden sind und keine vorkompilierten erforderlich ist.  
  
 Verwenden in der Regel eine Call-Level-Interface umfasst die folgenden Schritte aus:  
  
1.  Die Anwendung ruft eine CLI-Funktion zur Verbindung mit dem DBMS.  
  
2.  Die Anwendung eine SQL-Anweisung erstellt und platziert sie in einen Puffer. Er ruft dann eine oder mehrere CLI-Funktionen, um die Anweisung an das DBMS zur Vorbereitung und Ausführung zu senden.  
  
3.  Wenn die Anweisung eine SELECT-Anweisung ist, ruft die Anwendung eine CLI-Funktion zum Zurückgeben der Ergebnisse in Anwendungspuffer an. Diese Funktion gibt eine Zeile oder eine Spalte mit Daten in der Regel zu einem Zeitpunkt.  
  
4.  Die Anwendung ruft eine CLI-Funktion zum Trennen der Verbindung das DBMS an.
