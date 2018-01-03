---
title: "Neuheiten bei SSMA für DB2 (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 09/30/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ce602bd9726c8762793d9289daf5c52b2176494
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Neuheiten bei SSMA für DB2 (DB2ToSQL)
In diesem Thema werden die SSMA für DB2-Änderungen in jeder Version aufgelistet.  

## <a name="ssma-v76"></a>SSMA v7.6
Die v7.6-Version von SSMA für DB2 wurde verbessert, mit der targeted Korrekturen, die Qualität und Konvertierung Metriken zu verbessern und Unterstützung für SQL Server-2017 (öffentliche Vorschau). Unterstützung für SQL Server-2017 auf Windows- und Linux ist als öffentliche Vorschau verfügbar und sollte nicht für die Produktionsmigrationen verwendet werden.

> [!IMPORTANT]
> SSMA v7.4 und höhere Versionen .net 4.5.2 ist eine Voraussetzung für Installation, und die 32-Bit-Version des Tools wurde eingestellt.

## <a name="ssma-v75"></a>SSMA 7.5
Die Version 7.5 von SSMA für DB2 wurde verbessert, mit zahlreiche Verbesserungen, um größere Barrierefreiheit für Personen mit behinderungen sicherzustellen.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA 7.5. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v74"></a>SSMA v7.4
Die v7.4-Version von SSMA für DB2 enthält die folgenden Änderungen:
- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.
![Option Timeout für Remoteabfragen](../media/query-timeout_red.png)

- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v73"></a>SSMA V7. 3
Die V7. 3-Version von SSMA für DB2 enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- SSMA Extensibility Framework verfügbar gemacht werden, über die folgenden Elemente:
  - Exportieren Sie zu einem SQL Server Data Tools (SSDT)-Projekt bereit.
    -   Sie können jetzt Schemaskripts von SSMA in ein SSDT-Projekt exportieren. Die Schemaskripts können Sie zusätzliche Schemas ändern und Bereitstellen der Datenbank.
![Speichern Sie als SSDT-Befehl "Projekt"](../media/export-schema-scripts_red.png)
  - Bibliotheken, die zum Ausführen von benutzerdefinierter Konvertierungen von SSMA genutzt werden können.
    - Jetzt können Sie Code erstellen, die benutzerdefinierte Syntax Konvertierungen und Konvertierungen, die zuvor vom SSMA verarbeitet wurden nicht verarbeiten kann.
      - Anweisungen zum Erstellen eines benutzerdefinierten Konverters stehen in diesem Blogbeitrag [Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Beispielprojekt für die Konvertierung herunterladen dies [Blogbeitrag](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA V7. 2
Die V7. 2-Version von SSMA für DB2 enthält die folgenden Änderungen:
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
Die Mai 2016-Version von SSMA für DB2 enthält die folgenden Änderungen:  

-  Unterstützung für SQL Server 2016.
-  Hinzugefügte Konvertierung DB2 im Arbeitsspeicher und reguläre Tabellen in SQL Server-Funktionen für in-Memory und Hekaton.
-  Hinzugefügte Konvertierung von DB2 Zugriff auf Steuerelemente in SQL Server-Richtlinienobjekten (Sicherheit auf Zeilenebene für DB2).
-  Hinzugefügte Konvertierung systemversionsangabe DB2-Tabellen in temporalen Tabellen mit SQL Server.
-  Verbesserter DB2-Parser und Konfliktlöser.
-  Überprüfen Sie Installationsprogramm für .net 2.0 wird entfernt.
-  Unnötige *.dll entfernt aus Db2-Installer.
-  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole.
-  Feste "Securepassword"-Befehl für SSMA-Konsole.
-  Korrektur von Objekten für das erstmalige laden zählen.
-  Korrektur von Bug in den globalen Einstellungen.
  
## <a name="march-2016"></a>März 2016  
Die März 2016 Preview-Version von SSMA für DB2 enthält die folgenden Änderungen:  
  
-  Unterstützung für die Migration zu SQL Server 2016.  
  
## <a name="january-2016"></a>Januar 2016  
Die Januar 2016 Wartung-Version von SSMA für DB2 enthält die folgenden Änderungen:  
  
-  Unterstützung für eine Reihe von standardmäßigen Funktionen hinzugefügt.  
-  Feste DB2-Parserfehler.  
-  Feste DB2 v9 zOS erörtert Support (RFC 5690920).  
-  Feste DB2 unresolved Bezeichner Fehler während der Konvertierung.  
-  Hinzugefügte Ansicht der Protokoll-Menüelement zu SSMA (RFC 5706203).  
-  Hinzugefügte Telemetrie.
  
## <a name="november-2014"></a>November 2014  
Die Version vom November 2014 von SSMA für DB2 war die erste Version.
