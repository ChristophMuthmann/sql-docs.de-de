---
title: Architektur der sprachmonitortreiber | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa23b4a900e0415268746b84b94d68ea8492bbca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="driver-architecture"></a>Architektur der sprachmonitortreiber
Architektur der sprachmonitortreiber fällt in zwei Kategorien unterteilt, je nachdem welche Software Prozesse SQL-Anweisungen:  
  
-   **Dateibasierten Treibern** der Treiber greift direkt auf die physischen Daten. In diesem Fall fungiert der Treiber wie Treiber und Datenquelle; d. h., verarbeitet sie ODBC-Aufrufe und SQL-Anweisungen. DBASE-Treiber sind z. B. dateibasierten Treibern, da dBASE keine bietet, dass ein eigenständiges Datenbankmodul den Treiber verwenden kann. Es ist wichtig zu beachten, dass Entwickler von dateibasierten Treibern eigene Datenbankmodule schreiben müssen.  
  
-   **DBMS-basierten Treibern** der Treiber greift auf die physischen Daten über eine separate Datenbank-Engine. In diesem Fall verarbeitet der Treiber ODBC-aufrufen; übergibt SQL-Anweisungen für das Datenbankmodul für die Verarbeitung. Oracle-Treiber sind z. B. DBMS-basierten Treibern, da Oracle eine eigenständige Datenbank-Engine hat, die der Treiber verwendet. Das Datenbankmodul, in dem sich befindet, ist irrelevant. Es kann sich auf demselben Computer wie der Treiber oder einem anderen Computer im Netzwerk befinden; Es kann auch über ein Gateway zugegriffen werden.  
  
 Architektur der sprachmonitortreiber ist im Allgemeinen nur für Treiber Writer interessante; Treiberarchitektur macht, also in der Regel kein Unterschied zur Anwendung. Die Architektur kann jedoch beeinflussen, ob eine Anwendung die DBMS-spezifische SQL verwenden kann. Microsoft Access enthält beispielsweise eine eigenständige Datenbank-Engine. Wenn ein Microsoft Access-Treiber DBMS-basiert ist – greift auf die Daten über dieses Modul – die Anwendung kann Microsoft Access – SQL-Anweisungen an das Modul zur Verarbeitung übergeben.  
  
 Jedoch, wenn der Treiber einen dateibasierten ist – d. h., er enthält ein proprietäres Modul, das der Microsoft® Access-MDB-Datei greift direkt auf – alle Versuche, Microsoft Access-spezifische SQL-Anweisungen an das Modul übergeben werden voraussichtlich zu einem Syntaxfehler führt. Der Grund ist, dass proprietäre Modul wahrscheinlich nur ODBC SQL implementiert ist.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Dateibasierte Treiber](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS-basierte Treiber](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Netzwerkbeispiel](../../odbc/reference/network-example.md)  
  
-   [Andere Treiberarchitekturen](../../odbc/reference/other-driver-architectures.md)
