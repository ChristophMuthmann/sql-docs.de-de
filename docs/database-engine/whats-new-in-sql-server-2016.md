---
title: "Neues im Datenbankmodul – SQL Server 2016 | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: "431"
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0e5018b6b111790d2ff0415180e0608798da44ac
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>Neues im Datenbankmodul – SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

In diesem Thema werden die eingeführten Verbesserungen der [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Version des [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]vorgestellt.  Die neuen Funktionen und Verbesserungen verbessern die Leistungsfähigkeit und Produktivität von Architekten, Entwicklern und Administratoren, die Datenspeichersysteme entwerfen, entwickeln und pflegen.

Die Neuigkeiten der anderen SQL Server-Komponenten finden Sie unter [Was ist neu in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] ist eine 64-Bit-Anwendung. Die 32-Bit-Installation wird eingestellt, obwohl einige Elemente als 32-Bit-Komponenten ausgeführt werden.

#### <a name="try-it-out"></a>Probieren Sie es aus

- Navigieren Sie zum Herunterladen von [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] zu **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**![Herunterladen](../analysis-services/media/download.png "download").

- Sie haben ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** , um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] bereits installiert ist.

> [!NOTE]
> Die aktuellen Anmerkungen zu dieser Version finden Sie unter [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md).
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  `CREATE OR ALTER <object>` -Syntax ist jetzt für [Prozeduren](../t-sql/statements/create-procedure-transact-sql.md), [Ansichten](../t-sql/statements/create-view-transact-sql.md), [Funktionen](../t-sql/statements/create-function-transact-sql.md)und [Trigger](../t-sql/statements/create-trigger-transact-sql.md)verfügbar.
-   Unterstützung für ein allgemeineres Modell für Abfragehinweise wurde hinzugefügt: `OPTION (USE HINT('<hint1>', '<hint2>'))`. Weitere Informationen finden Sie unter [Abfragehinweise (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md).  
- Die [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) -DMV wurden den Listenhinweisen hinzugefügt.  
- Die [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) -DMV wurde hinzugefügt und gibt Übergangsstatistiken zu Showplan-XML zurück.  
- Die [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) -DMV wurde der inkrementellen Statistik für die angegebene Tabelle hinzugefügt.  
- Die `instant_file_initialization_enabled` -Spalte wurde zu [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)hinzugefügt.  
- Die of    `estimated_read_row_count` -Spalte wurde zu [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)hinzugefügt.  
-  Die Spalten `sql_memory_model` und `sql_memory_model_desc` wurden zu [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) hinzugefügt, um Informationen über das Sperrmodell für Speicherseiten zur Verfügung zu stellen.
-  Die Editionen, die eine Reihe von Funktionen unterstützen, wurden erweitert. Dazu gehören Sicherheit auf Zeilenebene, Always Encrypted, Dynamische Datenmaskierung, Datenbanküberwachung, In-Memory-OLTP und viele weitere Funktionen für alle Editionen. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../sql-server/editions-and-supported-features-for-sql-server-2016.md).   
-  [sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) ermöglicht die Always On-Verschlüsselung zum Aktualisieren von Metadaten, wenn verschlüsselte Objekte, die Always On verwenden, neu definiert werden.  


##  <a name="Feature"></a> SQL Server 2016 RTM
Dieser Abschnitt enthält folgende Unterabschnitte:

-   [Columnstore-Indizes](#columnstore)
-   [Datenbankweit gültige Konfigurationen](#scopedconfiguration)
-   [In-Memory-OLTP](#InMemory)
-   [Abfrageoptimierer](#QueryOptimizer)
-   [Live-Abfragestatistik](#LiveStats)
-   [Abfragespeicher](#QueryStore)
-   [Temporale Tabellen](#TT)
-   [Stripesetsicherungen in Microsoft Azure-Blobspeicher](#StripedBackupToAzure)
-   [Dateimomentaufnahmesicherungen in Microsoft Azure-Blobspeicher](#FileSnapshotBackup)
-   [Verwaltete Sicherung](#ManagedBackup)
-   [tempdb-Datenbank](#multipleTempDB)
-   [Integrierte JSON-Unterstützung](#ForJson)
-   [PolyBase](#bkPolyBase)
-   [Stretch-Datenbank](#stretch)
-   [Unterstützung für UTF-8](#UTF8)
-   [Neue Standarddatenbankgröße und Werte für die automatische Vergrößerung](#DefaultDB)
-   [Transact-SQL-Erweiterungen](#TSQL)
-   [Systemsichterweiterungen](#SystemTable)
-   [Sicherheitserweiterungen](#Security)
-   [Verbesserungen im Hinblick auf hohe Verfügbarkeit](#HighAvailability)
-   [Verbesserte Replikation](#Repl)
-   [Toolverbesserungen](#Tools)

####  <a name="columnstore"></a> Columnstore-Indizes

Diese Version bietet Verbesserungen für Columnstore-Indizes, einschließlich aktualisierbare nicht gruppierte Columnstore-Indizes, Columnstore-Indizes für Tabellen im Arbeitsspeicher und viele weitere neue Funktionen für die operative Analyse.

- Ein schreibgeschützter nicht gruppierter Columnstore-Index ist nach dem Upgrade aktualisierbar.  Die Neuerstellung des Indexes ist nicht erforderlich, um ihn aktualisierbar zu machen.

- Es gibt Leistungsverbesserungen für Analyseabfragen von Columnstore-Indizes, vor allem für Aggregate und Zeichenfolgenprädikate.

- DMVs und XEvents weisen Verbesserungen hinsichtlich der Unterstützbarkeit auf.

Weitere Informationen finden Sie in den folgenden Themen im Abschnitt [Beschreibung von Columnstore-Indizes](../relational-databases/indexes/columnstore-indexes-overview.md) der Onlinedokumentation:

- [Columnstore-Indizes, Zusammenfassung der Funktionen nach Version](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) – einschließlich der Neuigkeiten.

- [Laden von Daten für Columnstore-Indizes](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [Abfrageleistung für Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [Columnstore-Indizes für Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [Columnstore-Index-Defragmentierung](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


####  <a name="scopedconfiguration"></a> Datenbankweit gültige Konfigurationen


Mithilfe der neuen [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)-Anweisung können Sie bestimmte Konfigurationen für Ihre Datenbank steuern. Die Konfigurationseinstellungen wirken sich auf das Verhalten der Anwendung aus.

Die neue Anweisung ist sowohl in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] als auch in [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)]verfügbar.



####  <a name="InMemory"></a> In-Memory-OLTP


##### <a name="storage-format-change"></a>Speicherformatänderung

Das Speicherformat für speicheroptimierte Tabellen wechselt von SQL Server 2014 zu SQL Server 2016. Für Upgrades und zum Anfügen/Wiederherstellen von SQL Server 2014 wird das neue Speicherformat serialisiert und die Datenbank während der Wiederherstellung der Datenbank einmal neu gestartet.

- [Aktualisieren auf SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


##### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE ist für Protokolle optimiert und wird parallel ausgeführt.

Wenn Sie jetzt eine ALTER TABLE-Anweisung für eine speicheroptimierte Tabelle ausführen, werden nur die Metadatenänderungen in das Protokoll geschrieben. Dadurch werden die Ein- und Ausgaben für Protokolle deutlich verringert. Zudem können die meisten Szenarien für ALTER TABLE jetzt gleichzeitig ausgeführt werden, wodurch sich die Dauer der Anweisung erheblich verkürzt.

- Informationen zu nicht parallelen Ausnahmen, einschließlich LOBs, finden Sie unter [Ändern von speicheroptimierten Tabellen](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).



##### <a name="statistics"></a>Statistik

Die[Statistiken für speicheroptimierte](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) Tabellen werden jetzt automatisch aktualisiert. Darüber hinaus ist das Sampling jetzt eine unterstützte Methode zum Erfassen von Statistiken, wodurch Sie die aufwendigere Methode mit vollständigem Scanvorgang vermeiden können.


##### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>Paralleler und Heapscanvorgang für speicheroptimierte Tabellen

Speicheroptimierte Tabellen und Indizes für speicheroptimierte Tabellen unterstützen jetzt parallele Scanvorgänge. Dies verbessert die Leistung von Analyseabfragen.

Darüber hinaus wird der Heapscanvorgang unterstützt, der parallel ausgeführt werden kann. Für eine speicheroptimierte Tabelle bezeichnet ein Heapscanvorgang das Scannen aller Zeilen in einer Tabelle mithilfe der In-Memory-Heapdatenstruktur, die zum Speichern der Zeilen verwendet wird. Für einen vollständigen Tabellenscan ist der Heapscanvorgang effizienter als die Verwendung eines Indexes.

##### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>Transact-SQL-Verbesserungen für speicheroptimierte Tabellen

Es gibt mehrere Transact-SQL-Elemente, die in SQL Server 2014 für speicheroptimierte Tabellen nicht unterstützt wurden, die jetzt in SQL Server 2016 unterstützt werden:


- UNIQUE-Einschränkungen und Indizes werden unterstützt.


- FOREIGN KEY-Verweise zwischen speicheroptimierten Tabellen werden unterstützt.
  - Diese Fremdschlüssel können nur auf einen Primärschlüssel und nicht auf einen eindeutigen Schlüssel verweisen.


- CHECK-Einschränkungen werden unterstützt.

- Ein nicht eindeutiger Index kann in seinem Schlüssel NULL-Werte zulassen.

- TRIGGER werden für speicheroptimierte Tabellen unterstützt.
  - Nur AFTER-Trigger werden unterstützt. INSTEADOF-Trigger werden nicht unterstützt.
  - Jeder Trigger für speicheroptimierte Tabellen muss WITH NATIVE_COMPILATION verwenden.

- Vollständige Unterstützung für alle SQL Server-Codepages und -Sortierungen mit Indizes und anderen Artefakten in speicheroptimierten Tabellen und systemintern kompilierten T-SQL-Modulen.


- Unterstützung für das [Ändern speicheroptimierter Tabellen](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md):
  - ADD- und DROP-Indizes. Ändern Sie „bucket_count“ von Hashindizes.
  - Schemaänderungen: Spalten hinzufügen/löschen/ändern. Einschränkung hinzufügen/löschen.

- Eine speicheroptimierte Tabelle kann jetzt über mehrere Spalten verfügen, deren kombinierte Länge größer als die Länge der Seite mit 8060 Byte ist. Ein Beispiel ist eine Tabelle mit drei Spalten vom Typ `nvarchar(4000)`. In solchen Beispielen werden einige Spalten nun außerhalb der Zeile gespeichert. Ihren Abfragen ist nicht bekannt, ob sich eine Spalte innerhalb oder außerhalb einer Zeile befindet.

- [LOB-Typen (Large Object)](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)`und `varchar(max)` werden jetzt in speicheroptimierten Tabellen unterstützt.


Allgemeine Informationen finden Sie unter:

- [Von In-Memory OLTP nicht unterstützte Transact-SQL-Konstrukte](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [Nicht unterstützte SQL Server-Funktionen für In-Memory OLTP](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


##### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>Transact-SQL-Verbesserungen für systemintern kompilierte Module

Es gibt einige Transact-SQL-Elemente, die in SQL Server 2014 für systemintern kompilierte Module nicht unterstützt wurden, die jetzt in SQL Server 2016 unterstützt werden:


- Abfragekonstrukte:
  - UNION und UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - Unterabfragen in SELECT


- INSERT-, UPDATE- und DELETE-Anweisungen können jetzt die [OUTPUT-Klausel](../t-sql/queries/output-clause-transact-sql.md)einbeziehen.

- LOBs können jetzt auf folgende Weise in einer systeminternen Prozedur verwendet werden:
  - Deklaration von Variablen
  - Empfangene Eingabeparameter
  - In Zeichenfolgenfunktionen übergebene Parameter, z. B. in „LTrim“ oder „Substring“, in einer systeminternen Prozedur


- Inline-Tabellenwertfunktionen (d. h. mit einzelner Anweisung) können jetzt systemintern kompiliert werden.

- Skalare benutzerdefinierte Funktionen (UDFs) können jetzt systemintern kompiliert werden.

- Verbesserte Unterstützung für eine aufzurufende systeminterne Prozedur:
  - Integrierte [Systemsicherheitsfunktionen](../t-sql/functions/security-functions-transact-sql.md)
  - Integrierte [mathematische Funktionen](../t-sql/functions/mathematical-functions-transact-sql.md)
  - Integrierte Funktion `@@SPID`.


- EXECUTE AS CALLER wird jetzt unterstützt und somit ist die EXECUTE AS-Klausel beim Erstellen eines systemintern kompilierten T-SQL-Moduls nicht mehr erforderlich.


Allgemeine Informationen finden Sie unter:

- [Unterstützte Funktionen für nativ kompilierte T-SQL-Module](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [Ändern von systemintern kompilierten T-SQL-Modulen](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)


##### <a name="performance-and-scaling-improvements"></a>Verbesserungen hinsichtlich der Leistung und Skalierung

- Es besteht keine Einschränkung mehr hinsichtlich der Datengröße. Weitere Informationen finden Sie unter [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).

- Es sind jetzt mehrere gleichzeitig ausgeführte Threads dafür verantwortlich, [Änderungen an speicheroptimierten Tabellen dauerhaft auf dem Datenträger zu speichern](../relational-databases/in-memory-oltp/scalability.md).

- Unterstützung von parallelen Plänen für das [Zugreifen auf speicheroptimierte Tabellen mit interpretiertem Transact-SQL](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md).


##### <a name="enhancements-in-sql-server-management-studio"></a>Verbesserungen in SQL Server Management Studio

- Für die Option [Bestimmen, ob eine Tabelle oder eine gespeicherte Prozedur zu In-Memory OLTP portiert werden soll](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) ist die Konfiguration von Datensammlern oder einem Verwaltungs-Data Warehouse nicht mehr erforderlich. Der Bericht kann jetzt direkt in einer Produktionsdatenbank ausgeführt werden.

- [PowerShell-Cmdlet für die Migrationsauswertung](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) für die Auswertung der Migrationseignung von mehreren Objekten in einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbank.

- Generieren von Migrationsprüflisten durch Klicken mit der rechten Maustaste auf eine Datenbank und Auswählen von „Aufgaben“ > „Prüflisten für die Migration zum In-Memory-OLTP erstellen“.

##### <a name="cross-feature-support"></a>Funktionsübergreifende Unterstützung

- Unterstützung für die Verwendung der temporalen Systemversionsverwaltung mit In-Memory-OLTP. Weitere Informationen finden Sie unter [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).

- Abfragespeicherunterstützung für nativ kompilierten Code von In-Memory-OLTP-Workloads. Weitere Informationen finden Sie unter [Verwenden des Abfragespeichers mit In-Memory-OLTP](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md).

- [Sicherheit auf Zeilenebene in speicheroptimierten Tabellen](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- Durch das [Verwenden von Multiple Active Result Sets &#40;MARS&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) können Verbindungen jetzt auf speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren zugreifen.

- Unterstützung der [transparenten Datenverschlüsselung (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md). Wenn eine Datenbank für die Verschlüsselung konfiguriert ist, werden Dateien in der [speicheroptimierten Dateigruppe](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md) jetzt ebenfalls verschlüsselt.

Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).


####  <a name="QueryOptimizer"></a> Abfrageoptimierer
##### <a name="compatibility-level-guarantees"></a>Garantien zum Kompatibilitätsgrad
Wenn Sie für Ihre Datenbank ein Upgrade auf SQL Server 2016 durchführen, sind keine Planänderungen ersichtlich, wenn Sie bei den älteren Kompatibilitätsgraden verbleiben, die Sie verwendet haben (z. B. 120 oder 110). Neue Features und Verbesserungen in Bezug auf den Abfrageoptimierer werden nur unter dem aktuellen Kompatibilitätsgrad verfügbar sein. 
##### <a name="trace-flag-4199"></a>Ablaufverfolgungsflag 4199
Im Allgemeinen müssen Sie das Ablaufverfolgungsflag 4199 nicht in SQL Server 2016 verwenden, da der Großteil der Abfrageoptimiererverhalten, die durch dieses Ablaufverfolgungsflag gesteuert werden, bedingungslos unter dem aktuellen Kompatibilitätsgrad (130) in SQL Server 2016 aktiviert sind.
##### <a name="new-referential-integrity-operator"></a>Neuer Operator für die referentielle Integrität
Eine Tabelle kann auf maximal 253 andere Tabellen und Spalten als Fremdschlüssel (ausgehende Referenzen) verweisen. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] erhöht den Grenzwert für die Anzahl der anderen Tabellen und Spalten, die auf Spalten in einer einzelnen Tabelle (eingehende Referenzen) verweisen können, von 253 auf 10.000. Einschränkungen finden Sie unter [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md). Es wird ein neuer Operator für die referenzielle Integrität eingeführt (unter dem Kompatibilitätsgrad 130), der die vorhandenen referenziellen Integritätsprüfungen durchführt. Dies verbessert die Gesamtleistung für UPDATE- und DELETE-Vorgänge für Tabellen, die eine große Anzahl von eingehenden Verweisen aufweisen, wodurch es möglich ist, eine große Anzahl von eingehenden Verweisen zu verarbeiten. Weitere Informationen finden Sie unter [Ergänzungen für den Abfrageoptimierer in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)
##### <a name="parallel-update-of-sampled-statistics"></a>Parallele Aktualisierung aus Stichproben gewonnener Statistiken
Datenstichproben zum Erstellen von Statistiken werden jetzt parallel gewonnen (unter dem Kompatibilitätsgrad 130), um die Leistung von Statistiken zu verbessern. Weitere Informationen finden Sie unter [Aktualisieren von Statistiken](../t-sql/statements/update-statistics-transact-sql.md).
#### <a name="sublinear-threshold-for-update-of-statistics"></a>Unterlinearer Schwellenwert zum Aktualisieren von Statistiken
Die automatische Aktualisierung der Statistik erfolgt jetzt aggressiver für große Tabellen (unter dem Kompatibilitätsgrad 130). Der Schwellenwert zum Auslösen der automatische Aktualisierung der Statistik beträgt 20 %. Ab SQL Server 2016 wird dieser Schwellenwert für größere Tabellen sinken (weiterhin ein Prozentsatz), da die Anzahl der Zeilen in der Tabelle zunimmt. Sie müssen das Ablaufverfolgungsflag 2371 nicht mehr festlegen, um den Schwellenwert zu verringern. 
##### <a name="other-enhancements"></a>Weitere Verbesserungen
Die INSERT-Anweisung in einer INSERT-SELECT-Anweisung erhält mehrere Threads oder kann einen parallelen Plan aufweisen (unter dem Kompatibilitätsgrad 130). Um einen parallelen Plan zu erhalten, muss die INSERT... SELECT-Anweisung den TABLOCK-Hinweis verwenden. Weitere Informationen finden Sie unter [Paralleles Verwenden von INSERT-SELECT](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)

####  <a name="LiveStats"></a> Live-Abfragestatistik
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] bietet die Möglichkeit, den Live-Ausführungsplan einer aktiven Abfrage anzuzeigen. Dieser Live-Abfrageplan bietet Einblicke in Echtzeit in den Abfrageausführungsprozess, während die Steuerelemente von einem Abfrageplanoperator zu einem anderen übertragen werden. Weitere Informationen finden Sie unter [Live Query Statistics](../relational-databases/performance/live-query-statistics.md).

####  <a name="QueryStore"></a> Abfragespeicher
Der Abfragespeicher ist eine neue Funktion, die über DBAs Einblick in die Auswahl und die Leistung des Abfrageplans bietet. Er vereinfacht das Beheben von Leistungsproblemen, indem er das schnelle Auffinden von Leistungsabweichungen durch Änderungen an Abfrageplänen ermöglicht. Das Feature erfasst automatisch einen Verlauf der Abfrage-, Plan- und Laufzeitstatistiken und bewahrt diese zur Überprüfung auf. Es unterteilt die Daten nach Zeitfenstern und ermöglicht es Ihnen so, Verwendungsmuster für Datenbanken zu erkennen und zu verstehen, wann Abfrageplanänderungen auf dem Server aufgetreten sind. Der Abfragespeicher zeigt die Informationen in einem [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] -Dialogfeld an. Zudem können Sie die Abfrage von einem der ausgewählten Abfragepläne erzwingen. Weitere Informationen finden Sie unter [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).


####  <a name="TT"></a> Temporale Tabellen
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] unterstützt jetzt temporale Tabellen mit Versionsverwaltung durch das System. Eine temporale Tabelle ist ein neuer Tabellentyp, der jederzeit die richtigen Informationen zu gespeicherten Fakten bereitstellt. Jede temporale Tabelle besteht tatsächlich aus zwei Tabellen, einer für die aktuellen Daten und einer für die Verlaufsdaten. Das System stellt sicher, dass bei einer Änderungen der Daten in der Tabelle mit den aktuellen Daten die vorherigen Werte in der Verlaufstabelle gespeichert werden. Um diese Komplexität vor dem Benutzer zu verbergen, werden Abfragekonstrukte bereitgestellt. Weitere Informationen finden Sie unter [Temporal Tables](../relational-databases/tables/temporal-tables.md).

####  <a name="StripedBackupToAzure"></a> Stripesetsicherungen in Microsoft Azure-Blobspeicher
In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]unterstützt die SQL Server-Sicherung über URLs mithilfe des Microsoft Azure-Blobspeicherdiensts jetzt Stripesetsicherungen mit Blockblobs zur Unterstützung einer maximale Sicherungsgröße von 12,8 TB. Beispiele finden Sie unter [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples).

####  <a name="FileSnapshotBackup"></a> Dateimomentaufnahmesicherungen in Microsoft Azure-Blobspeicher
 In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]unterstützt die SQL Server-Sicherung über URLs nun die Verwendung von Azure-Momentaufnahmen zum Sichern von Datenbanken, in denen alle Datenbankdateien mit dem Microsoft Azure-Blobspeicherdienst gespeichert werden. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).

####  <a name="ManagedBackup"></a> Verwaltete Sicherung
In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] verwendet SQL Server Managed Backup für Microsoft Azure den neuen Blockblobspeicher für die Sicherungsdateien. Es gibt auch mehrere Änderungen und Erweiterungen für die verwaltete Sicherung.

-   Unterstützung für automatisierte und benutzerdefinierte Planung von Sicherungen

-   Unterstützung von Sicherungen für Systemdatenbanken

-   Unterstützung für Datenbanken, die das einfache Wiederherstellungsmodell verwenden

 Weitere Informationen finden Sie unter [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).

> [!NOTE]
>  Diese neuen verwalteten Sicherungsfunktion für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]verfügen noch nicht über die entsprechende Benutzeroberflächenunterstützung in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

####  <a name="multipleTempDB"></a> tempdb-Datenbank
 Es gibt mehrere Erweiterungen für TempDB:

-   Ablaufverfolgungsflags 1117 und 1118 sind nicht mehr für tempdb erforderlich. Wenn mehrere tempdb-Datenbankdateien vorhanden sind, werden alle Dateien gleichzeitig je nach Wachstumseinstellungen vergrößert. Darüber hinaus verwenden alle Zuordnungen in tempdb gleichartige Blöcke.

-   Standardmäßig fügt das Setup genau so viele tempdb-Dateien hinzu wie die CPU-Anzahl oder 8, je nachdem, welcher Wert niedriger ist.

-   Während des Setups können Sie die Anzahl der tempdb-Datenbankdateien, die Anfangsgröße, die automatische Vergrößerung und die Verzeichnisplatzierung über das neue UI-Eingabesteuerelement im Abschnitt „Datenbankmodulkonfiguration - TempDB“ des SQL Server-Installationsassistenten konfigurieren.

-   Die anfängliche Standardgröße liegt bei 8 MB und der Standardwert für die automatische Vergrößerung beträgt 64 MB.

-   Sie können mehrere Volumes für tempdb-Datenbankdateien angeben. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.

####  <a name="ForJson"></a> Integrierte JSON-Unterstützung
SQL Server 2016 fügt die integrierte Unterstützung für das Importieren und Exportieren von JSON und das Arbeiten mit JSON-Zeichenfolgen hinzu. Diese integrierte Unterstützung umfasst die folgenden Anweisungen und Funktionen.

-   Formatieren oder exportieren Sie die Abfrageergebnisse als JSON, indem Sie einer **SELECT** -Anweisung die **FOR JSON** -Klausel hinzufügen. Verwenden Sie die **FOR JSON**-Klausel, um z. B. die Formatierung der JSON-Ausgabe von Ihren Clientanwendungen an [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu delegieren. Weitere Informationen finden Sie unter [Formatieren von Abfrageergebnissen als JSON mit FOR JSON &#40;SQL Server&#41;](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

-   Konvertieren Sie die JSON-Daten in Zeilen und Spalten, oder importieren Sie JSON, indem Sie die **OPENJSON**-Rowset-Anbieterfunktion aufrufen. Verwenden Sie **OPENJSON** , um die JSON-Daten in SQL Server zu importieren, oder konvertieren Sie die JSON-Daten in Zeilen und Spalten für eine Anwendung oder einen Dienst, die bzw. der derzeit JSON nicht direkt nutzen kann. Weitere Informationen finden Sie unter [Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON &#40;SQL Server&#41;](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).

-   Die **ISJSON**-Funktion testet, ob eine Zeichenfolge gültiges JSON enthält. Weitere Informationen finden Sie unter [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md).

-   Die **JSON_VALUE**-Funktion extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge. Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md).

-   Die **JSON_QUERY**-Funktion extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge. Weitere Informationen finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md).

-   Die **JSON_MODIFY**-Funktion aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge, und gibt die aktualisierte JSON-Zeichenfolge zurück. Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md).

####  <a name="bkPolyBase"></a> PolyBase
 PolyBase ermöglicht es Ihnen, T-SQL-Anweisungen für den Zugriff auf Daten zu verwenden, die in Hadoop oder Azure-Blobspeicher gespeichert wurden, und sie ad-hoc abzufragen. Außerdem können Sie die teilweise strukturierten Daten abfragen und die Ergebnisse mit relationalen Datasets zu verbinden, die in SQL Server gespeichert sind. PolyBase ist für Data Warehouse-Workloads optimiert und wurde für Analyseabfrageszenarien konzipiert.

 Weitere Informationen finden Sie im [PolyBase-Handbuch](../relational-databases/polybase/polybase-guide.md).

####  <a name="stretch"></a> Stretch-Datenbank
 Die Stretch-Datenbank ist ein neues Feature in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , mit dem Ihre Verlaufsdaten transparent und sicher in die Microsoft Azure-Cloud migriert werden. Sie können problemlos auf Ihre SQL Server-Daten zugreifen, unabhängig davon, ob sie lokal oder in der Cloud gespeichert sind. Sie legen die Richtlinie fest, die bestimmt, wo Daten gespeichert werden, und SQL Server übernimmt die Verschiebung der Daten im Hintergrund. Die gesamte Tabelle ist ständig online und kann jederzeit abgefragt werden. Und für die Stretch-Datenbank sind keine Änderungen an vorhandenen Abfragen oder Anwendungen erforderlich – der Speicherort der Daten ist für die Anwendung vollständig transparent. Weitere Informationen finden Sie unter [Stretch Database](../sql-server/stretch-database/stretch-database.md).
 
####  <a name="UTF8"></a> Unterstützung für UTF-8
Das Hilfsprogramm [bcp](../tools/bcp-utility.md), [BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) unterstützen jetzt die UTF-8-Codepage. Weitere Informationen finden Sie in diesen Themen und unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).

####  <a name="DefaultDB"></a> Neue Standarddatenbankgröße und Werte für die automatische Vergrößerung
Neue Werte für die Modelldatenbank und die Standardwerte für neue Datenbanken (die auf dem Modell basieren). Die Anfangsgröße der Daten-und Protokolldateien beträgt jetzt 8 MB. Die standardmäßige automatische Vergrößerung der Daten-und Protokolldateien beträgt jetzt 64 MB.


###  <a name="TSQL"></a> Transact-SQL-Erweiterungen
Zahlreiche Verbesserungen unterstützen die Features, die in anderen Abschnitten dieses Themas beschrieben wurden. Die folgenden zusätzlichen Verbesserungen sind verfügbar.
- Die TRUNCATE TABLE-Anweisung ermöglicht jetzt das Abschneiden der angegebenen Partitionen. Weitere Informationen finden Sie unter [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md).
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) ermöglicht jetzt die Ausführungen von vielen Aktionen zum Ändern einer Spalte, während die Tabelle verfügbar bleibt.
- Die Volltextindex-DMV [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) gibt die Positionen der Schlüsselwörter in Dokumenten zurück. Diese DMV wurde auch in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 und [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1 hinzugefügt.
- Ein neuer Abfragehinweis **NO_PERFORMANCE_SPOOL** kann verhindern, dass ein Spooloperator den Abfrageplänen hinzugefügt wird. Dies kann die Leistung verbessern, wenn viele gleichzeitige Abfragen mit Spoolvorgängen ausgeführt werden. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- Die [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md)-Anweisung wurde verbessert, um ein msg_string-Argument zu akzeptieren.
- Die maximal zulässige Indexschlüsselgröße für NONCLUSTERED-Indizes wurde auf 1700 Bytes angehoben.
- Neue DROP IF-Syntax wurde für Drop-Anweisungen hinzugefügt, die im Zusammenhang mit AGGREGATE, ASSEMBLY, COLUMN, CONSTRAINT, DATABASE, DEFAULT, FUNCTION, INDEX, PROCEDURE, ROLE, RULE, SCHEMA, SECURITY POLICY, SEQUENCE, SYNONYM, TABLE, TRIGGER, TYPE, USER und VIEW stehen. Informationen zur Syntax finden Sie unter den einzelnen Syntaxthemen.
- Eine MAXDOP-Option wurde zu [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md), [DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) und [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) hinzugefügt, um den Grad an Parallelität anzugeben.
- SESSION_CONTEXT kann jetzt festgelegt werden. Enthält die Funktionen [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md), [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) und die Prozedur [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).
- Advanced Analytics-Erweiterungen ermöglichen es Benutzern, Skripts in einer unterstützten Sprache wie R auszuführen. [!INCLUDE[tsql](../includes/tsql-md.md)] unterstützt R durch die Einführung der gespeicherten Prozedur [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) und der für [externe Skripts aktivierten Serverkonfigurationsoption](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md). Weitere Informationen finden Sie unter [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md).
- Die Fähigkeit, einen externen Ressourcenpool zu erstellen, dient ebenfalls zur Unterstützung von R. Weitere Informationen finden Sie unter [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md).  Neue Katalogsichten und DMVs ([sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) und [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)). Zusätzliche Argumente stehen für [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) und [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md) zur Verfügung. Einigen der vorhandenen Katalogsichten der Ressourcenkontrolle und DMVs werden zusätzliche Spalten hinzugefügt.
- Die [CREATE USER](../t-sql/statements/create-user-transact-sql.md) -Syntax wurde mit der ALLOW_ENCRYPTED_VALUE_MODIFICATIONS-Option verbessert, um Unterstützung für das Always Encrypted-Feature zu bieten. Weitere Informationen finden Sie unter [Migrieren von durch Always Encrypted geschützten sensiblen Daten](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
- Die Funktionen [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) und [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) konvertieren Werte in den sowie aus dem GZIP-Algorithmus.
- Die Funktionen [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) und [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) sowie die Sicht [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) werden hinzugefügt, um Interaktionen für Datumsangaben und Uhrzeiten zu unterstützen.
- Anmeldeinformationen können jetzt auf der Datenbankebene erstellt werden (zusätzlich zu den Anmeldeinformationen auf Serverebene, die zuvor verfügbar waren). Weitere Informationen finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).
- [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md) wurden acht neue Eigenschaften hinzugefügt: InstanceDefaultDataPath, InstanceDefaultLogPath, ProductBuild, ProductBuildType, ProductMajorVersion, ProductMinorVersion, ProductUpdateLevel und ProductUpdateReference.
- Der Eingabelängengrenzwert von 8.000 Bytes wurde für die [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md)-Funktion entfernt.
- Die neuen Zeichenfolgenfunktionen [STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) und [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md) wurden hinzugefügt.
- Optionen für die automatische Vergrößerung: Ablaufverfolgungsflag 1117 wird durch die Option AUTOGROW_SINGLE_FILE und AUTOGROW_ALL_FILES von ALTER DATABASE ersetzt, und Ablaufverfolgungsflag 1117 hat keine Auswirkungen. Weitere Informationen finden Sie unter [ALTER DATABASE-Optionen für Dateien und Dateigruppen &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) und unter der neuen „is_autogrow_all_files“-Spalte von [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).
- Zuordnung von gemischten Blöcken: Bei Benutzerdatenbanken wird die Standardzuordnung für die ersten acht Seiten eines Objekts geändert, von gemischten Seitenblöcken hin zu gleichartigen Blöcken. Ablaufverfolgungsflag 1118 wird durch die Option SET MIXED_PAGE_ALLOCATION von ALTER DATABASE ersetzt, und Ablaufverfolgungsflag 1118 hat keine Auswirkung. Weitere Informationen finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) und unter der neuen `is_mixed_page_allocation_on`-Spalte von [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md).


###  <a name="SystemTable"></a> Systemsichterweiterungen
- Zwei neue Ansichten unterstützen Sicherheit auf Zeilenebene. Weitere Informationen finden Sie unter [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) und [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md).
- Sieben neue Ansichten unterstützen die Abfragespeicherfunktion. Weitere Informationen finden Sie unter [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md).
- 24 neue Spalten werden zu [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) hinzugefügt, um Informationen zu Speicherzuweisungen bereitzustellen.
- Zwei neue Abfragehinweise (MIN_GRANT_PERCENT und MAX_GRANT_PERCENT) werden hinzugefügt, um Arbeitsspeicherzuweisungen festzulegen. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) bietet einen Bericht pro Sitzung, ähnlich dem serverweiten [dm_os_wait_stats &#40; Transact-SQL &#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) stellt Statistiken zur Ausführung in Bezug auf Skalarwertfunktionen zur Verfügung.
- Ab [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] werden Einträge in [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) wie vor [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] beibehalten.
- Informationen zu Anweisungen, die an eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] übergeben werden, können durch die neue dynamische Verwaltungsfunktion [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) zurückgegeben werden.
- Zwei neue Ansichten unterstützen [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md): [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) und [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 


###  <a name="Security"></a> Sicherheitserweiterungen

####  <a name="RLS"></a> Sicherheit auf Zeilenebene
Sicherheit auf Zeilenebene führt eine prädikatbasierte Zugriffssteuerung ein. Sie bietet eine flexible, zentrale und prädikatbasierte Bewertung, die Metadaten (wie Beschriftungen) oder andere Kriterien berücksichtigt, die der Administrator nach Bedarf bestimmt. Das Prädikat wird als Kriterium verwendet, um zu bestimmen, ob der Benutzer den entsprechenden Zugriff auf die Daten anhand von Benutzerattributen verfügt. Die beschriftungsbasierte Zugriffssteuerung kann mithilfe der prädikatbasierten Zugriffssteuerung implementiert werden. Weitere Informationen finden Sie unter [Sicherheit auf Zeilenebene](../relational-databases/security/row-level-security.md).


####  <a name="TCE"></a> Always Encrypted
Mit Always Encrypted kann [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Vorgänge für verschlüsselte Daten durchführen. Das Beste daran ist, der Verschlüsselungsschlüssel befindet sich bei der Anwendung innerhalb der vertrauenswürdigen Umgebung des Kunden und nicht auf dem Server. Always Encrypted sichert die Kundendaten, sodass DBAs keinen Zugriff auf Nur-Text-Daten haben. Die Verschlüsselung und Entschlüsselung von Daten erfolgt transparent auf Treiberebene, wodurch Änderungen minimiert werden, die an vorhandenen Anwendungen vorgenommen werden müssen. Weitere Informationen finden Sie unter [Always Encrypted &#40;Datenbankmodul&#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md).


####  <a name="Masking"></a> Dynamische Datenmaskierung
Die dynamische Datenmaskierung beschränkt die Offenlegung vertraulicher Daten, indem sie für nicht berechtigte Benutzer maskiert werden. Mit der dynamischen Datenmaskierung können Sie unbefugten Zugriff auf sensible Daten verhindern, indem Kunden festlegen können, wie viele sensible Daten mit minimaler Auswirkung auf die Anwendungsschicht offengelegt werden. Es handelt sich um eine richtlinienbasierte Sicherheitsfunktion, die die sensiblen Daten im Resultset einer Abfrage in festgelegten Datenbankfeldern ausblendet, während die Daten in der Datenbank nicht geändert werden. Weitere Informationen finden Sie unter [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md).


####  <a name="Perms"></a> Neue Berechtigungen
- Die **ALTER ANY SECURITY POLICY** -Berechtigung ist als Teil der Implementierung der Sicherheit auf Zeilenebene verfügbar.
- Die Berechtigungen **ALTER ANY MASK** und **UNMASK** stehen als Teil der Implementierung der dynamischen Datenmaskierung zur Verfügung.
- Die Berechtigungen **ALTER ANY COLUMN ENCRYPTION KEY**, **VIEW ANY COLUMN ENCRYPTION KEY**, **ALTER ANY COLUMN MASTER KEY DEFINITION**und **VIEW ANY COLUMN MASTER KEY DEFINITION** stehen als Teil der Implementierung der Always Encrypted-Funktion zur Verfügung.
- Die Berechtigungen **ALTER ANY EXTERNAL DATA SOURCE** und **ALTER ANY EXTERNAL FILE FORMAT** sind in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] sichtbar, gelten aber nur für das [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)]).
- Die **EXECUTE ANY EXTERNAL SCRIPT**-Berechtigungen stehen als Teil der Unterstützung für R-Skripte zur Verfügung.
 - Die **ALTER ANY DATABASE SCOPED CONFIGURATION**-Berechtigungen sind zur Autorisierung der Verwendung der [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)-Anweisung verfügbar.

####  <a name="TDE"></a> Transparente Datenverschlüsselung
- Transparent Data Encryption wurde durch die Unterstützung für Intel AES-NI-Hardwarebeschleunigung der Verschlüsselung verbessert. Dies reduziert die CPU-Auslastung beim Aktivieren der Transparent Data Encryption.

###  <a name="AES"></a> AES-Verschlüsselung für Endpunkte
- Die Standardverschlüsselung für Endpunkte wurde von RC4 in AES geändert.

####  <a name="newcredentialtype"></a> Neuer Anmeldeinformationstyp
- Anmeldeinformationen können jetzt auf der Datenbankebene erstellt werden (zusätzlich zu den Anmeldeinformationen auf Serverebene, die zuvor verfügbar waren). Weitere Informationen finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).


###  <a name="HighAvailability"></a> Verbesserungen im Hinblick auf hohe Verfügbarkeit
SQL Server 2016 Standard Edition unterstützt jetzt die grundlegenden AlwaysOn-Verfügbarkeitsgruppen. Grundlegende Verfügbarkeitsgruppen bieten Unterstützung für ein primäres und sekundäres Replikat. Diese Funktion ersetzt die veraltete Datenbankspiegelungstechnologie für hohe Verfügbarkeit. Weitere Informationen zu den Unterschieden zwischen grundlegenden und erweiterten Verfügbarkeitsgruppen finden Sie unter [Basis-Verfügbarkeitsgruppen &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).

Der Lastenausgleich von Verbindungsanforderungen für beabsichtigte Lesevorgänge wird jetzt über einen Satz von schreibgeschützten Replikaten unterstützt. Das vorherige Verhalten leitete die Verbindungen immer an das erste verfügbare schreibgeschützte Replikat in der Verteilerliste. Weitere Informationen finden Sie unter [Konfigurieren von Lastenausgleich über schreibgeschützte Replikate hinweg](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).

 Die Anzahl der Replikate, die ein automatisches Failover unterstützen wurde von zwei auf drei erhöht.

 Gruppenverwaltete Dienstkonten werden jetzt für AlwaysOn-Failovercluster unterstützt. Weitere Informationen finden Sie unter [Gruppenverwaltete Dienstkonten: Übersicht](https://technet.microsoft.com/library/hh831782.aspx). Für Windows Server 2012 R2 ist ein Update erforderlich, um nach einer Kennwortänderung eine vorübergehende Downtime zu vermeiden. Das Update erhalten Sie unter [gMSA-basierte Dienste können sich nach dem Ändern eines Kennworts nicht in einer Domäne Windows Server 2012 R2 anmelden](https://support.microsoft.com/kb/2998082/).

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] unterstützt verteilte Transaktionen und das DTC auf Windows Server 2016. Weitere Informationen finden Sie unter [Unterstützung für verteilte Transaktionen](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport).

 Sie können [!INCLUDE[ssHADR](../includes/sshadr-md.md)] jetzt konfigurieren, um ein Failover durchzuführen, sobald eine Datenbank offline geschaltet wird. Für diese Änderung müssen Sie die **DB_FAILOVER**-Option in der [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md)- oder [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md)-Anweisung auf **ON** festlegen.

AlwaysOn unterstützt jetzt verschlüsselte Datenbanken. Der Verfügbarkeitsgruppenassistent fordert Sie nun zur Eingabe eines Kennworts für eine beliebige Datenbank auf, die einen Datenbankhauptschlüssel enthält, wenn Sie eine neue Verfügbarkeitsgruppe erstellen oder Datenbanken oder Replikate zu einer vorhandenen Verfügbarkeitsgruppe hinzufügen.

Zwei Verfügbarkeitsgruppen in zwei separaten Windows Server Failover Clustern (WSFC) können jetzt zu einer verteilten Verfügbarkeitsgruppe kombiniert werden. Weitere Informationen finden Sie unter [Verteilte Verfügbarkeitsgruppen &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).

Durch direktes Seeding kann das Seeding eines sekundären Replikats automatisch über das Netzwerk ausgeführt werden (anstatt das Seeding manuell auszuführen, wofür eine physische Sicherung der Zieldatenbank erforderlich ist, die auf dem sekundären wiederhergestellt werden soll). Das direkte Seeding wird durch Festlegen von **SEEDING_MODE=AUTOMATIC** in der [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md)- oder [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md)-Anweisung angegeben. Sie müssen auch auf jedem sekundären Replikat, das mit direktem Seeding verwendet wird, **GRANT CREATE ANY DATABASE** mit [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) angeben.

**Leistungsverbesserungen**: Der Synchronisierungsdurchsatz von Verfügbarkeitsgruppen wurde durch die parallele und schnellere Komprimierung von Protokollblöcken auf dem primären Replikat, durch ein optimiertes Synchronisierungsprotokoll und die parallele Dekomprimierung und Wiederherstellung von Protokolldatensätzen auf dem sekundären Replikat um etwa das Zehnfache erhöht. Dies erhöht die Aktualität der lesbare sekundären Replikate und verringert die Wiederherstellungszeit von Datenbanken im Falle eines Failovers. Beachten Sie, dass die Wiederherstellung für speicheroptimierte Tabellen in SQL Server 2016 noch nicht parallel erfolgt.

###  <a name="Repl"></a> Verbesserte Replikation
- Die Replikation von speicheroptimierten Tabellen wird jetzt unterstützt. Weitere Informationen finden Sie unter [Replikation mit Abonnenten von speicheroptimierten Tabellen](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).
- Replikation auf [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]wird jetzt unterstützt. Weitere Informationen finden Sie unter [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md).

###  <a name="Tools"></a> Toolverbesserungen

####  <a name="SSMS"></a> Management Studio
Laden Sie das neueste [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)herunter

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] unterstützt die Active Directory Authentication Library (ADAL), die für die Verbindung mit Microsoft Azure entwickelt wird. Dies ersetzt die zertifikatbasierte Authentifizierung von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].
- Die[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] -Installation erfordert die Installation von .NET 4.6 als erforderliche Komponente. .NET 4.6 wird automatisch vom Setupprogramm installiert, wenn [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] installiert wird.
- Eine neue Abfrageergebnis-Rasteroption unterstützt die Beibehaltung von Wagenrücklauf-/Zeilenvorschubzeichen (neue Zeilenumbruchzeichen) beim Kopieren oder Speichern von Text aus dem Ergebnisraster. Legen Sie dies im Menü „Extras/Optionen“ fest.
- Die SQL Server-Verwaltungstools werden nicht mehr aus der Hauptfunktionsstruktur installiert. Weitere Informationen finden Sie unter [Installieren von SQL Server-Verwaltungstools mit SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381).
- Die[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] -Installation erfordert die Installation von .NET 4.6.1 als erforderliche Komponente. .NET 4.6.1 wird automatisch vom Setupprogramm installiert, wenn [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] installiert wird.

####  <a name="UA"></a> Upgrade Advisor
SQL Server 2016 Upgrade Advisor Preview ist ein eigenständiges Tool, mit dem Benutzer von früheren Versionen eine Reihe von Upgraderegeln für ihre SQL Server-Datenbank ausführen können, um Unterbrechungen und Verhaltensänderungen sowie veraltete Features zu ermitteln. Zudem bieten sie Hilfe bei der Übernahme von neuen Features wie die Stretch-Datenbank.

 Sie können Upgrade Advisor Preview [hier](https://www.microsoft.com/en-us/download/details.aspx?id=48119) herunterladen, oder Sie können es mit dem Webplattform-Installer installieren.

## <a name="see-also"></a>Weitere Informationen finden Sie unter
[Neues in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
 
[Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md) 
 
[Installieren von SQL Server-Verwaltungstools mit SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)








