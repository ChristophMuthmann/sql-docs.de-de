---
title: "Neuigkeiten für SQLServer 2017 unter Linux | Microsoft Docs"
description: "In diesem Thema werden die Neuigkeiten für die aktuelle Version von SQL Server-2017 unter Linux hervorgehoben."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: f76985a8721e154269b36b0bdcb40a83f6136cb3
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Neuigkeiten für SQL Server-2017 unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieses Thema beschreibt die Neuigkeiten für SQL Server-2017 auf Linux ausgeführt wird.

## <a name="ga"></a>GA

Die allgemeinen Availaiblity (GA) Version enthält die folgenden Verbesserungen und Fehlerbehebungen auf:

- Datenbankdateien können jetzt auf NFS gehostet werden. Dies behebt Probleme mit freigegebenen NFS-Datenträger-Szenarien, Einbinden von Remotespeicher für Container-Plattformen und Bereitstellen von Ordnern für Docker für Windows.
- Andere verschiedene Fehlerbehebungen und Verbesserungen.

## <a name="rc2"></a>RC2

Die RC2-Version enthält verschiedene Fehlerbehebungen und Verbesserungen.

## <a name="rc1"></a>RC1

Die RC1-Version enthält die folgenden Verbesserungen und Fehlerbehebungen auf:

- Transparente Layer Security (TLS) für verschlüsselte Verbindungen aktiviert. Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server on Linux](sql-server-linux-encrypted-connections.md).
- Aktiviert [Active Directory-Authentifizierung](sql-server-linux-active-directory-authentication.md).
- Aktiviert [DB Mail](../relational-databases/database-mail/database-mail.md).
- IPV6-Unterstützung hinzugefügt.
- Hinzugefügte Umgebungsvariablen für die ursprüngliche SQL Server-Setup. Weitere Informationen finden Sie unter [konfigurieren Sie SQL Server-Einstellungen mit Umgebungsvariablen unter Linux](sql-server-linux-configure-environment-variables.md).
- Entfernt **Sqlpackage** von Binärdateien installiert haben. SqlPackage kann immer noch für Linux Remote von Windows ausgeführt werden.
- Freigegebene Datenträger Cluster Agent Ressourcensätze, die Namen der Ressource, wie er auf einer Microsoft SQL Server-Failoverclusterinstanz ausführt. `@@ServerName`Gibt die SQL Server freigegebenen Datenträger clusterressourcenname; vor RC1 zurückgegeben es den Namen des Clusterknotens, der die Ressource besitzen.

## <a name="ctp-21"></a>CTP-VERSION 2.1

Die CTP-Version 2.1-Version enthält die folgenden Verbesserungen und Fehlerbehebungen:

- Hinzugefügt [Umgebungsvariablen so konfigurieren Sie die SQL Server-Dienst](sql-server-linux-configure-environment-variables.md).
- [MSSQL-Conf](sql-server-linux-configure-mssql-conf.md) erfordert nun mit dem zweiteiligen Benennungskonvention für Einstellungen.
- Die [Mssql Skripter](https://github.com/Microsoft/sql-xplat-cli) Tool. Dieses Hilfsprogramm ermöglicht es, Entwickler, Datenbankadministratoren und Systemadministratoren generieren `CREATE` und `INSERT` Transact-SQL-Skripts von Datenbankobjekten in SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse-Datenbanken über die Befehlszeile.
- Die [DBFS Tool](https://github.com/Microsoft/dbfs). Dies ist ein Open-Source-Tool, DBAs und Systemadministratoren, SQL Server einfacher zu überwachen, indem Livedaten aus SQL Server dynamische Verwaltungssichten (DMVs) verfügbar gemacht werden als virtuelle Dateien in ein virtuelles Verzeichnis auf Linux-Betriebssystemen ermöglicht.
- SQL Server Integration Services (SSIS) wird nun unter Linux ausgeführt werden. Es ist außerdem ein neues Paket, in dem Sie die SSIS-Pakete auf Linux aus der Befehlszeile ausgeführt werden kann. Weitere Informationen finden Sie unter der [Blog Post Ankündigung SSIS-Unterstützung für Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Mit SSIS auf Linux CTP-Version 2.1 aktualisiert können SSIS-Pakete auf Linux ODBC-Verbindungen. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

## <a name="ctp-20"></a>CTP 2.0

Die Version CTP 2.0, enthält die folgenden Verbesserungen und Fehlerbehebungen:

- Hinzugefügt **des Protokollversands** Funktionalität für SQL Server-Agent.
- Der Mssql-conf lokalisierte Meldungen
- Formatieren von Linux Pfad sind nun in der gesamten SQL Server-Datenbankmoduls kompatibel. Allerdings unterstützen für "" c: "\\" mit Präfix Pfade werden fortgesetzt.
- Aktiviert die DMV **sys.dm_os_file_exists**.
- Aktiviert die DMV **Sys. fn_trace_gettable**.
- Hinzugefügt [Sicherheit der CLR-Strict-Modus](/sql/database-engine/configure-windows/clr-strict-security).
- SQL-Diagramm.
- Von Online geschalteten fortgesetzt werden können.
- Adaptive Abfrageverarbeitung.
- Hinzugefügte UTF-8-Codierung für die Systemdateien, einschließlich Protokolldateien.
- Korrektur von Datenbanken im Arbeitsspeicher Speicherort Einschränkung. 
- Hinzufügen von neuen Clustertyp `CLUSTER_TYPE = EXTERNAL` zum Konfigurieren einer verfügbarkeitsgruppe für hohe Verfügbarkeit.
- Korrigieren eines Verfügbarkeitsgruppenlisteners für schreibgeschütztes routing.
- Unterstützung für die Produktion für Kunden, die frühe Adoption Program (EAP). Registrieren Sie sich [hier](http://aka.ms/eapsignup).

## <a name="ctp-14"></a>CTP 1.4

Die CTP-Version 1.4-Version enthält die folgenden Verbesserungen und Fehlerbehebungen:

- Aktiviert die [SQL Server-Agent](sql-server-linux-setup-sql-agent.md).
  - Aktiviert die Funktionen des T-SQL-Aufträge.
- Feste Timezone-Fehler:
  - TimeZone-Unterstützung für Asien/Kolkata.
  - Fixed-Funktion GETDATE().
- Netzwerk-Async ich / 0 Verbesserungen:
  - Erhebliche Verbesserungen auf die Arbeitsleistung zu In-Memory OLTP.
- Docker-Image enthält jetzt SQL Server-Befehlszeilenprogrammen. (Sqlcmd/Bcp).
- Aktiviert Virtual Device Interface (VDI)-Unterstützung von Sicherungskopien.
- Speicherort von TempDB kann jetzt geändert werden, nachdem die Installation mit `ALTER DATABASE`.

## <a name="ctp-13"></a>CTP-VERSION 1.3

Die CTP-Version 1.3-Version enthält die folgenden Verbesserungen und Fehlerbehebungen auf:

- Aktiviert [Volltextsuche](sql-server-linux-setup-full-text-search.md) Funktion.
- Always On aktiviert [verfügbarkeitsgruppenfunktion](sql-server-linux-availability-group-overview.md) für hohe Verfügbarkeit.
- Zusätzliche Funktionen in **Mssql-Conf**:
  - Erste Einrichtung mit **Mssql-Conf**. Finden Sie die Verwendung der Mssql-Conf in der [Installationshandbüchern](sql-server-linux-setup.md#platforms).
  - Aktivieren von Verfügbarkeitsgruppen. Finden Sie unter der [Verfügbarkeitsgruppen Thema](sql-server-linux-availability-group-overview.md).
- Fester native Linux Pfad Unterstützung für In-Memory OLTP-Dateigruppen.
- Aktiviert die Dm_os_host_info DMV-Funktionalität.

## <a name="ctp-12"></a>CTP-VERSION 1.2

Die CTP-Version 1.2-Version enthält die folgenden Verbesserungen und Fehlerbehebungen auf:

- Unterstützung für [SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md).
- Fehlerbehebungen für Core-Modul und Stabilität Verbesserungen.
- Docker-Image: 
  - Feste [ausstellen #1](https://github.com/Microsoft/mssql-docker/issues/1) durch Hinzufügen von Python zum Bild.
  - Entfernt `/opt/mssql/data` als Standard-Volume.
- Auf .NET 4.6.2 aktualisiert.

## <a name="ctp-11"></a>CTP-VERSION 1.1

Die CTP-Version 1.1-Release enthält die folgenden Verbesserungen und Fehlerbehebungen auf:

- Unterstützung für Red Hat Enterprise Linux Version 7.3.
- Unterstützung für Ubuntu 16.10.
- Aktualisierte Docker-OS-Ebene, Ubuntu 16.04.
- Telemetrie-Probleme in Docker-Images wurden behoben.
- Festen SQL Server-Setup-Skript im Zusammenhang mit Fehlern.
- Verbesserte Leistung für nativ kompilierte T-SQL-Module, einschließlich:
  - **OPENJSON**, **FOR JSON**, **JSON** Option.
  - Berechnete Spalten (nur Indizes für persistente berechnete Spalten, jedoch nicht auf nicht persistente berechnete Spalten für in-Memory-Tabellen zulässig).
  - **CROSS APPLY** Vorgänge.
- Neue Sprachfeatures:
  - Zeichenfolgenfunktionen: **TRIM**, **CONCAT_WS**, **übersetzen** und **STRING_AGG** mit Unterstützung für **WITHIN GROUP (ORDER BY)**.
  - **MASSENIMPORT** unterstützt jetzt die CSV-Format und Azure-Blob-Speicher als Quelle für die Datei.

Unter dem Kompatibilitätsmodus 140:

- Verbessert die Leistung von Updates, die nicht gruppierten columnstore-Indizes in der Fall, wenn die Zeile im deltastore ist. Geändert Delete und insert-Vorgänge zu aktualisieren. Die planform von breit verwendet werden, um einzugrenzen auch geändert werden.
- Abfragen im Batch-Modus unterstützen jetzt "arbeitsspeicherzuweisungen Feedback Schleifen". Dies verbessert sich Parallelität und Durchsatz auf Systemen mit wiederholten Abfragen, die im Batchmodus zu verwenden. Dadurch können mehrere Abfragen für Systeme, die andernfalls für den Arbeitsspeicher blockiert werden, vor dem Starten von Abfragen.
- Verbesserte Leistung im Batch-Modus Parallelität ignorieren triviale Plan für Batchmodus plant für parallele Pläne für Columnstores stattdessen entnommen werden können. 

[Verbesserungen von Service Pack 1](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/) in dieser Version CTP1.1:
- Für CLR, Filestream/Filetable, Objekte im Arbeitsspeicher und der Abfragespeicher das Klonen von Datenbanken.
  - **Aktualisieren von 10/18/2017**: beim Weitere Testzwecke Filestream wird derzeit nicht unterstützt in der GA-Version von SQL Server-2017 unter Linux  
- **Erstellen Sie** oder **ALTER** Operatoren für programmierbarkeitsobjekte.
- Neue **verwenden Hinweis** -Abfrageoption verwenden, um Hinweise für die der Abfrageprozessor zu übermitteln. Erfahren Sie hier: [Abfragehinweise](../t-sql/queries/hints-transact-sql-query.md).
- SQL-Dienstkonto kann nun programmgesteuert aktivieren Sperren von Seiten im Speicher und die sofortige Dateiinitialisierung Berechtigungen identifizieren.
- Unterstützung für die TempDB-Dateianzahl, Dateigröße und Wachstum dateieinstellungen.
- Erweiterte Diagnose in Showplan XML.
- Einfache pro-Operator Abfrage Ausführung profilerstellung.
- Neue dynamische Verwaltungsfunktion **sys.dm_exec_query_statistics_xml**.
- Neue dynamische Verwaltungsfunktion für inkrementelle Statistiken.
- Entfernte verrauschten In-Memory bezogenen Protokollieren von Nachrichten aus Errorlog.
- Verbesserte AlwaysOn-Latenz Diagnose.
- Bereinigt die manuelle Änderungsnachverfolgung.
- **DROP TABLE** für die Replikation unterstützt.
- **BULK INSERT** in Heaps mit **automatisch TABLOCK** unter TF 715.
- Parallele **INSERT... Wählen Sie** Änderungen für lokale temporäre Tabellen.

Weitere Informationen zu diesen Updates in der [Service Pack 1-Version Beschreibung](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/).

Zahlreiche Verbesserungen der Datenbank-Engine gelten für Windows und Linux. Die einzige Ausnahme wäre für Datenbankmodul-Funktionen, die unter Linux derzeit nicht unterstützt werden. Weitere Informationen finden Sie unter [Neuigkeiten in SQL Server-2017 (Datenbankmodul)](https://msdn.microsoft.com/library/mt775028).

## <a name="see-also"></a>Siehe auch

Installationsanforderungen, nicht unterstütztes Feature-Bereiche und bekannte Probleme finden Sie unter [Versionshinweise für SQL Server-2017 unter Linux](sql-server-linux-release-notes.md).

