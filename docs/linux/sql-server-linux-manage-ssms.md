---
title: Verwenden von SSMS zum Verwalten von SQLServer on Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 7a09e44b80cdf80b3ce5e033210d0f55276a42b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Verwenden von SQL Server Management Studio unter Windows zum Verwalten von SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel führt [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) und führt Sie durch ein paar häufige Aufgaben. SSMS ist eine Windows-Anwendung, daher SSMS verwenden, wenn Sie einen Windows-Computer verfügen, der mit einer SQL Server-Remoteinstanz unter Linux eine Verbindung herstellen können.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) ist Teil einer Suite von SQL-Tools, die Microsoft-Angebote kostenlos für Entwicklung und Verwaltung Anforderungen freizugeben. SSMS ist eine integrierte Umgebung zugreifen, konfigurieren, verwalten, verwalten und entwickeln aller Komponenten von SQL Server lokal oder in der Cloud unter Linux, Windows oder Docker unter MacOS und Azure SQL-Datenbank und Azure SQL Data Warehouse. SSMS kombiniert eine umfassende Gruppe grafischer Tools mit einer Reihe umfassender Skript-Editoren, um Entwicklern und Administratoren mit verschiedenem Kenntnisstand den Zugriff auf SQL Server zu ermöglichen.

SSMS bietet eine Breite Palette von Funktionen zur Entwicklung und Verwaltung für SQL Server, Tools, einschließlich:

- Konfigurieren Sie, überwachen Sie und verwalten Sie einzelne oder mehrere Instanzen von SQL Server
- bereitstellen, überwachen und aktualisieren Sie die Datenebenen-Komponenten wie z. B. Datenbanken und Data Warehouses
- Sichern und Wiederherstellen von Datenbanken
- Erstellen und T-SQL-Abfragen und Skripts ausführen und die Ergebnisse anzuzeigen
- Generieren von T-SQL-Skripts für Datenbankobjekte
- Anzeigen und Bearbeiten von Daten in Datenbanken
- visuell zu entwerfen, T-SQL-Abfragen und Datenbankobjekte, z. B. Sichten, Tabellen und gespeicherten Prozeduren

Finden Sie unter [verwenden Sie SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx) für Weitere Informationen.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Installieren Sie die neueste Version von SQL Server Management Studio (SSMS)

Bei der Arbeit mit SQL Server sollten Sie immer die neueste Version von SQL Server Management Studio (SSMS) verwenden. Die neueste Version von SSMS wird laufend aktualisiert und optimiert und arbeitet zurzeit mit SQLServer 2017 on Linux. Zum Herunterladen und installieren Sie die neueste Version, finden Sie unter [Herunterladen von SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Um auf dem neuesten Stand zu bleiben, die neueste Version von SSMS werden Sie aufgefordert, wenn eine neue Version für den download verfügbaren vorhanden ist. 

## <a name="before-you-begin"></a>Vorbereitungen
- Finden Sie unter [Verwenden von SSMS unter Windows zur Verbindung mit SQL Server on Linux](sql-server-linux-develop-use-ssms.md) wie eine Verbindung herstellen und Abfragen mithilfe von SSMS
- Lesen der [bekannte Probleme](sql-server-linux-release-notes.md) für SQLServer 2017 unter Linux

## <a name="create-and-manage-databases"></a>Erstellen und Verwalten von Datenbanken
Während einer Verbindung mit der *master* Datenbank, Sie können Datenbanken auf dem Server erstellen und ändern oder Löschen vorhandener Datenbanken. Die folgenden Schritte beschreiben, wie Sie verschiedene allgemeine Datenbankverwaltungsaufgaben über Management Studio ausführen. Um diese Aufgaben ausführen, stellen Sie sicher, dass Sie verbunden sind, die *master* Datenbank mit der prinzipalanmeldung auf Serverebene, die Sie beim Einrichten einer Verbindung mit SQL Server-2017 unter Linux erstellt haben.

### <a name="create-a-new-database"></a>Erstellen einer neuen Datenbank

1. Starten Sie SSMS aus, und verbinden Sie Ihre Server in SQL Server-2017 unter Linux

2. Objekt-Explorer mit der Maustaste auf die *Datenbanken* Ordner, und klicken Sie dann auf * neue Datenbank... "

3. In der *neue Datenbank* Dialogfeld, geben Sie einen Namen für die neue Datenbank, und klicken Sie dann auf *OK*

Die neue Datenbank wird auf dem Server wurde erfolgreich erstellt. Wenn Sie lieber eine neue Datenbank mit T-SQL zu erstellen, finden Sie unter [CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Löschen einer Datenbank

1. Starten Sie SSMS aus, und verbinden Sie Ihre Server in SQL Server-2017 unter Linux

2. Erweitern Sie im Objekt-Explorer die *Datenbanken* Ordner, um eine Liste aller Datenbanken auf dem Server anzuzeigen.

3. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank, die Sie löschen möchten, und klicken Sie dann auf *löschen*

4. In der *Objekt löschen* Dialogfeld Kontrollkästchen *bestehende Verbindungen schließen* , und klicken Sie dann auf *OK*

Die Datenbank wird vom Server wurde erfolgreich gelöscht. Wenn Sie eine Datenbank mit T-SQL löschen möchten, finden Sie unter [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Mit dem Aktivitätsmonitor Informationen zu SQL Server-Aktivitäten finden Sie unter

Die [Aktivitätsmonitor](../relational-databases/performance-monitor/activity-monitor.md) Tool ist eine integrierte Funktion in SQL Server Management Studio (SSMS) und zeigt Informationen zu SQL Server-Prozesse und Auswirkungen diese Prozesse auf die aktuelle Instanz von SQL Server.

1. Starten Sie SSMS aus, und verbinden Sie Ihre Server in SQL Server-2017 unter Linux

2. Klicken Sie im Objekt-Explorer mit der Maustaste die *Server* Knoten, und klicken Sie dann auf *Aktivitätsmonitor*

Aktivitätsmonitor zeigt erweiterbare und reduzierbare Bereichen mit Informationen zu folgendem:
- Übersicht
- Prozesse
- Ressourcenwartevorgänge
- Datendatei-e/a
- Aktuelle wertvolle Abfragen
- Aktuelle ressourcenintensive Abfragen

Wenn ein Bereich erweitert wird, fragt der Aktivitätsmonitor die Instanz nach Informationen. Wenn ein Bereich reduziert wird, werden sämtliche Abfrageaktivitäten für diesen Bereich angehalten. Sie können einen oder mehrere Bereiche erweitern, zur gleichen Zeit um unterschiedliche Aktivitätstypen für die Instanz anzuzeigen.

## <a name="see-also"></a>Siehe auch
- [Verwenden von SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [Exportieren Sie und importieren Sie eine Datenbank mit SSMS](sql-server-linux-migrate-ssms.md)
- [Lernprogramm: SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [Lernprogramm: Schreiben von Transact-SQL-Anweisungen](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Überwachen der Serverleistung und -aktivität](../relational-databases/performance/server-performance-and-activity-monitoring.md)
