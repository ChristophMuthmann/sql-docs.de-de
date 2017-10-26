---
title: Treiber Aufgaben | Microsoft Docs
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 331e3aee3a4a60cbfa1a1308b71da80bf9772f23
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="driver-tasks"></a>Treiber-Aufgaben
Bestimmte Aufgaben, die vom Treiber ausgeführt:  
  
-   Herstellen einer Verbindung mit und Trennen von der Datenquelle.  
  
-   Es wird überprüft, für die Funktion Fehler vom Treiber-Manager nicht aktiviert.  
  
-   Initiieren Transaktionen; Dies ist für die Anwendung transparent.  
  
-   Senden SQL-Anweisungen an die Datenquelle für die Ausführung an. Der Treiber muss ODBC SQL DBMS-spezifische SQL ändern; Dies ist häufig auf, und Ersetzen Sie dabei folgende Escape-Klauseln, die von ODBC mit DBMS-spezifische SQL definiert.  
  
-   Senden von Daten an und Abrufen von Daten aus der Datenquelle, z. B. Konvertieren von Datentypen entsprechend den Angaben von der Anwendung.  
  
-   Zuordnen von DBMS-spezifische Fehler zu ODBC SQLSTATEs.

