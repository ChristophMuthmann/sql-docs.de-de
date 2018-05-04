---
title: ODBC-Treiberarchitektur | Microsoft Docs
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
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c620cbaefa987a722f86ed11bca4e88382ec0ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-driver-architecture"></a>ODBC-Treiberarchitektur
Treiber Writer müssen bewusst sein, dass die Architektur der sprachmonitortreiber auswirken kann, ob eine Anwendung die DBMS-spezifische SQL verwenden kann.  
  
 ![Zeigt die Architektur der ODBC-Treiber](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Dateibasierten Treibern](../../../odbc/reference/file-based-drivers.md)  
  
 Wenn der Treiber die physikalischen Daten direkt zugreift, fungiert der Treiber wie Treiber und die Datenquelle. Der Treiber muss ODBC-Aufrufe und SQL-Anweisungen verarbeiten. Entwickler von dateibasierten Treibern müssen ihre eigenen Datenbankmodule schreiben.  
  
 [DBMS-basierte Treiber](../../../odbc/reference/dbms-based-drivers.md)  
  
 Wenn ein separates Datenbankmodul Zugriff auf physische Daten verwendet wird, verarbeitet der Treiber ODBC-aufrufen. Übergibt SQL-Anweisungen für das Datenbankmodul für die Verarbeitung.  
  
 [Netzwerkarchitektur](../../../odbc/reference/network-example.md)  
  
 Datei- und DBMS-ODBC-Konfigurationen können in einem einzigen Netzwerk vorhanden sein.  
  
 [Andere Treiberarchitekturen](../../../odbc/reference/other-driver-architectures.md)  
  
 Wenn ein Treiber erforderlich ist, um mit einer Vielzahl von Datenquellen zu arbeiten, können sie als Middleware verwendet werden. Heterogene Join-modularchitektur vererbungsoptionen den Treiber, die als ein Treiber-Manager angezeigt werden. Treiber können auch auf Servern installiert werden, in dem sie durch eine Reihe von Clients freigegeben werden kann.  
  
 Weitere Informationen zur Architektur der sprachmonitortreiber finden Sie unter [Treibermanager](../../../odbc/reference/the-driver-manager.md) und [Treiberarchitektur](../../../odbc/reference/driver-architecture.md) im Abschnitt [ODBC-Architektur](../../../odbc/reference/odbc-architecture.md).  
  
 Weitere Informationen zu Treiberproblemen finden Sie in die Speicherorte, die in der folgenden Tabelle beschrieben.  
  
|Problem|Thema|Speicherort|  
|-----------|-----------|--------------|  
|Kompatibilitätsprobleme mit Anwendungen und-Treiber|[Application-Treiber-Kompatibilität](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Überlegungen zur Programmierung](../../../odbc/reference/develop-app/programming-considerations.md), in der ODBC Programmer's Reference|  
|Schreiben von ODBC-Treiber|[Schreiben von ODBC-3.x-Treibern](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Überlegungen zur Programmierung](../../../odbc/reference/develop-app/programming-considerations.md), in der ODBC Programmer's Reference|  
|Treiber-Richtlinien für die Abwärtskompatibilität|[Treiber-Richtlinien für die Abwärtskompatibilität](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Anhang G: Treiber Richtlinien für die Abwärtskompatibilität](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), in der ODBC Programmer's Reference|  
|Herstellen einer Verbindung mit einem Treiber|[Auswählen einer Datenquelle oder eines Treibers](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Herstellen einer Verbindung mit einer Quelle oder Treiber](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), in der ODBC Programmer's Reference|  
|Identifizieren von Treibern|[Anzeigen von Treibern](../../../odbc/admin/viewing-drivers.md)|[Anzeigen von Treibern](../../../odbc/admin/viewing-drivers.md), in der Onlinehilfe von Microsoft ODBC-Datenquellen-Administrator|  
|Aktivieren von Verbindungspooling|[ODBC-Verbindungspooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Herstellen einer Verbindung mit einer Quelle oder Treiber](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), in der ODBC Programmer's Reference|  
|Unicode/ANSI-Treiber und Verbindungsprobleme|[Unicode-Treiber](../../../odbc/reference/develop-app/unicode-drivers.md)|[Überlegungen zur Programmierung](../../../odbc/reference/develop-app/programming-considerations.md), in der ODBC Programmer's Reference|  
  
## <a name="see-also"></a>Siehe auch  
 [Developing an ODBC Driver (Entwickeln eines ODBC-Treibers)](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
