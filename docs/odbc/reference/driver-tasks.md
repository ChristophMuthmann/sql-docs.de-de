---
title: Treiber Aufgaben | Microsoft Docs
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7e351a84272e8ab9bd558e93e0d12bdc8275884
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-tasks"></a>Treiber-Aufgaben
Bestimmte Aufgaben, die vom Treiber ausgeführt:  
  
-   Herstellen einer Verbindung mit und Trennen von der Datenquelle.  
  
-   Es wird überprüft, für die Funktion Fehler vom Treiber-Manager nicht aktiviert.  
  
-   Initiieren Transaktionen; Dies ist für die Anwendung transparent.  
  
-   Senden SQL-Anweisungen an die Datenquelle für die Ausführung an. Der Treiber muss ODBC SQL DBMS-spezifische SQL ändern; Dies ist häufig auf, und Ersetzen Sie dabei folgende Escape-Klauseln, die von ODBC mit DBMS-spezifische SQL definiert.  
  
-   Senden von Daten an und Abrufen von Daten aus der Datenquelle, z. B. Konvertieren von Datentypen entsprechend den Angaben von der Anwendung.  
  
-   Zuordnen von DBMS-spezifische Fehler zu ODBC SQLSTATEs.
