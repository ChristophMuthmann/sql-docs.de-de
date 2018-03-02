---
title: "Neuheiten bei SSMA für die MySQL (MySQLToSql) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 03/01/2018
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 503e6c5a6c2d06a5c6a98ae1e9f45faebc40ae34
ms.sourcegitcommit: 6a5b80cac78fe5c2d2567a391daa335f9b4b3637
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2018
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Was ist neu in SSMA für die MySQL (MySQLToSql)
In diesem Thema werden die SSMA für MySQL-Änderungen in jeder Version aufgelistet. 

## <a name="ssma-v77"></a>SSMA v7.7
Die v7.7-Version von SSMA für MySQL enthält die folgenden Änderungen:
- SSMA für die MySQL wurde mit den entsprechenden Updates verbessert, die Qualität und Konvertierung Metriken zu verbessern.
- Basierend auf der großen Nachfrage ist die 32-Bit-Version von SSMA für die MySQL zurück. Im Vergleich zu die vorherige Implementierung (vor v7.4), es gibt zwei Installationspakete, aber sie können nicht nebeneinander installiert werden. Daher müssen Sie die am besten geeignete Version basierend auf die Konnektivitätskomponenten verwaltungsstufe auswählen. Es ist immer vorzuziehen, nach Möglichkeit die 64-Bit-Version zu verwenden.
- SSMA für die MySQL verfügt jetzt über ODBC-Verbindungszeichenfolge Verbindungsmodus, dem Sie keine ODBC-Treiber von Drittanbietern, die kompatibel mit MySQL verwenden kann.

> [!IMPORTANT]
> SSMA v7.4 und höheren Versionen ist .net 4.5.2 eine Installation Voraussetzung.

## <a name="ssma-v76"></a>SSMA v7.6
Die v7.6-Version von SSMA für MySQL wurde verbessert, mit der targeted Korrekturen, die Qualität und Konvertierung Metriken zu verbessern und Unterstützung für SQL Server-2017 (öffentliche Vorschau). Unterstützung für SQL Server-2017 auf Windows- und Linux ist als öffentliche Vorschau verfügbar und sollte nicht für die Produktionsmigrationen verwendet werden.

> [!IMPORTANT]
> SSMA v7.4 und höhere Versionen .net 4.5.2 ist eine Voraussetzung für Installation, und die 32-Bit-Version des Tools wurde eingestellt.

## <a name="ssma-v75"></a>SSMA v7.5
Die Version 7.5 von SSMA für MySQL wurde verbessert, mit zahlreiche Verbesserungen, um größere Barrierefreiheit für Personen mit behinderungen sicherzustellen.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA 7.5. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v74"></a>SSMA v7.4
Die v7.4-Version von SSMA für MySQL enthält die folgenden Änderungen:
- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.
![Option Timeout für Remoteabfragen](../media/query-timeout_red.png)
- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird. 

## <a name="ssma-v73"></a>SSMA v7.3
Die V7. 3-Version von SSMA für MySQL enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- SSMA Extensibility Framework verfügbar gemacht werden, über die folgenden Elemente:
  - Exportieren Sie zu einem SQL Server Data Tools (SSDT)-Projekt bereit.
    -   Sie können jetzt Schemaskripts von SSMA in ein SSDT-Projekt exportieren. Die Schemaskripts können Sie zusätzliche Schemas ändern und Bereitstellen der Datenbank.
![Speichern Sie als SSDT-Befehl "Projekt"](../media/export-schema-scripts_red.png)
  - Bibliotheken, die zum Ausführen von benutzerdefinierter Konvertierungen von SSMA genutzt werden können.
    - Jetzt können Sie Code erstellen, die benutzerdefinierte Syntax Konvertierungen und Konvertierungen, die zuvor vom SSMA verarbeitet wurden nicht verarbeiten kann.
      - Anweisungen zum Erstellen eines benutzerdefinierten Konverters stehen in diesem Blogbeitrag [Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Beispielprojekt für die Konvertierung herunterladen dies [Blogbeitrag](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
Die V7. 2-Version von SSMA für MySQL enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- Telemetrie-Erweiterungen bieten eine bessere Datenpunkte, um Kundenprobleme zu beheben und zu verbessern SSMAs-Wechselkurse.

## <a name="ssma-v71"></a>SSMA v7.1
Die v7.1-Version von SSMA für Access umfasst die folgenden Änderungen:
- SQL Server-2017 auf Windows- und Linux CTP1 ist jetzt eine unterstützte Zielplattform für die Migration. Dieses Feature ist in der technischen Vorschau und ermöglicht das Verschieben von Schema und Daten an SQL-Zielserver.
- SSMA unterstützt jetzt die automatische Updates, um die neueste Version von SSMA herunterladen, sobald es verfügbar ist.
- Installierbare SSMA-Binärdateien werden jetzt über Windows Installer-Paket-Dateien (.msi) übermittelt.

**Ressourcen**

[Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Bewerten und Migrieren von Daten aus datenplattformen nicht von Microsoft SQL Server *(mit der Oracle-Beispiel)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für MySQL enthält die folgenden Änderungen:.

-  Unterstützung für SQL Server 2016.
-  Verbesserte Parser und den resolvereinstellungen.
-  Überprüfen Sie Installationsprogramm für .net 2.0 wird entfernt.
-  Aktualisierte Erweiterung Pack Abhängigkeit von .net 3.5, .net 4.0.
-  Fester Standardwert "bigint" Typemapping für MySql.
-  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole.
-  Feste "Securepassword"-Befehl für SSMA-Konsole.
-  Korrektur von Objekten für das erstmalige laden zählen.
-  Feste MsSql-Objekte laden.
-  Korrektur von Bug in den globalen Einstellungen.
 
## <a name="march-2016"></a>März 2016  
Die März 2016 Preview-Version von SSMA für MySQL enthält die folgenden Änderungen:  
  
-  Unterstützung für die Migration zu SQL Server 2016. 
  
## <a name="january-2016"></a>Januar 2016  
Die Januar 2016 Wartung-Version von SSMA für MySQL enthält die folgenden Änderungen:  
  
-  Hinzugefügte Ansicht der Protokoll-Menüelement zu SSMA (RFC 5706203).  
-  Hinzugefügte Telemetrie.  
  
## <a name="july-2014"></a>Juli 2014  
Die Version Juli 2014 von SSMA für MySQL enthält die folgenden Änderungen:  
  
-  Verbesserte codekonvertierung für Azure SQL-Datenbank. 
-  Extension-Pack-Funktionen, die zur Unterstützung von Azure SQL-Datenbank in Schema verschoben werden.  
-  Verbesserte Leistung beim getestet Objekte für Datenbanken mit mehr als 10 KB.  
-  Verbesserungen der Benutzeroberfläche für den Umgang mit einer großen Anzahl von Objekten.  
-  Hervorheben von "bekannte" LOB-Schemas (damit sie bei der Konvertierung ignoriert werden können).  
-  Geschwindigkeitsverbesserungen Konvertierung.  
-  Objektanzahl Benutzeroberfläche anzeigen.  
-  Reduzierung der Größe von mehr als 25 % zu melden.  
-  Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die vom Juli 2011-Version von SSMA für MySQL enthält die folgenden Änderungen:  
  
-  Unterstützung von MS SQL Server 2014 hinzugefügt.  
-  Korrigierte Fehler hinsichtlich Konvertierung in Azure  
-  Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für MySQL enthält die folgenden Änderungen:  
  
-   Unterstützung für die Konvertierung von begrenzt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" VERSETZT.  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011 von SSMA für MySQL enthält die folgenden Änderungen:  
  
-   Einzelne installierbar von "SSMA für MySQL", die unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" und SQL Azure.  
-   Die Fähigkeit zum Verbinden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"  
-   Erweiterte clientseitige Migration Datenmodul, parallele Migration von Daten unterstützen.  
-   Verbesserte Daten migrationsleistung mit einfachen und Bulk protokolliert Wiederherstellungsmodelle.  
-   SSMA für die MySQL-Konsolenversion unterstützt Abwärtskompatibilität. Öffnen Sie die Projekte, die von früheren Versionen SSMA V5. 0 erstellt.  
-   SSMA für die MySQL-Version 5.0 Produkt werden kann werden nebeneinander angezeigt werden (SxS) mit älteren Versionen von SSMA-Produkt installiert.  
  
## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für MySQL enthält die folgenden Funktionen:  
  
1.  **Verbesserte Benutzeroberfläche:**  
  
    -   Auf der Registerkarte "SQL-Modi" MySQL-Datenbank-Objekte  
    -   Registerkarte "Einstellungen" für MySQL-Datenbank Objekte  
    -   Registerkarte "Daten" für MySQL-Tabellen  
    -   Aktualisierte Projekteinstellungen in Konvertierung und Migration Seiten  
    -   "Data Migrationseinstellungen" auf Tabellenebene  
  
2.  **Verbesserungen bei einer Verbindung mit MySQL und SQLServer:**  
  
    -   SSL-Verbindung in MySQL  
    -   Verschlüsselte Verbindung in SQLServer  
  
3.  **Verbesserungen für MySQL-Metabase Explorer:**  
  
    -   Laden alle Objekte der MySQL-Datenbank und die entsprechenden Registerkarten.  
  
4.  **Verbesserungen an Objekt Konvertierung:**  
  
    -   Konvertierung von MySQL-Metabase-Objekte – Prozeduren, Funktionen, Sichten, Trigger und Anweisungen.  
    -   Eingeschränkte Unterstützung für räumliche Datentypen in Tabellen.  
    -   Option zum Konvertieren von MySQL-Funktionen in SQL Server gespeicherte Prozeduren  
    -   Option, um SQL-Modi und Charset Zuordnung während der Konvertierung Objekt anzuwenden.  
  
5.  **Verbesserungen für die Datenmigration:**  
  
    -   Unterstützung für die Datenmigration mithilfe von serverseitigen und clientseitigen Daten Migration Module  
    -   Unterstützung für die Migration von räumlichen Daten  
    -   Benutzerdefinierte SQL für die Datenmigration für Tabellen  
  
6.  **SSMA für die MySQL-Konsole:**  
  
    -   Unterstützung Konsolenfunktion SSMA für MySQL  
    -   Unterstützung für Skriptebene Schnittstelle  
  
## <a name="january-2010"></a>Januar 2010  
Die Januar 2010-Version von SSMA für MySQL war die erste Version. Sie enthalten die folgenden Funktionen:  
  
-   Unterstützung für die Migration sowohl einer lokalen SQL Server und SQL Azure.  
  
-   **Feature-Momentaufnahme:** Schema und Daten Migration von Tabellen/Indizes/Einschränkungen MySQL.
