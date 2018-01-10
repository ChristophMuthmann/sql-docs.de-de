---
title: "Übersicht und Verwendungsszenarios | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62c964c5-eae4-4cf1-9024-d5a19adbd652
caps.latest.revision: "5"
author: jodebrui
ms.author: jodebrui
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5c638ad00229f9adaf91cc187ae06e3d751db347
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="overview-and-usage-scenarios"></a>Übersicht und Verwendungsszenarien
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

In-Memory-OLTP ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] die wichtigste verfügbare Technologie für die Optimierung der Transaktionsverarbeitung, das Erfassen und Laden von Daten sowie für vorübergehende Datenszenarios. Dieser Artikel bietet eine Übersicht über die Technologie und beschreibt Verwendungsszenarios für In-Memory-OLTP. Nutzen Sie diese Informationen, um festzustellen, ob In-Memory-OLTP für Ihre Anwendung geeignet ist. Der Artikel endet mit einem Beispiel, das In-Memory-OLTP-Objekte zeigt. Er enthält zudem einen Verweis auf eine leistungsbezogene Demo und Verweise auf Ressourcen, die Sie für die nächsten Schritte nutzen können.

Dieser Artikel behandelt die In-Memory-OLTP-Technologie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Der folgenden Blogbeitrag enthält fundierte Einblicke in die Leistung und die Ressourcenauslastungsvorteile in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: 
- [In-Memory OLTP in Azure SQL-Datenbank](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

## <a name="in-memory-oltp-overview"></a>In-Memory-OLTP: Übersicht

In-Memory-OLTP kann bei den entsprechenden Workloads für große Leistungszuwächse sorgen. Ein Kunde, bwin, hat es geschafft, mit einem einzelnen Computer mit ausgeführtem [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und durch die Nutzung von In-Memory-OLTP [1,2 Millionen Anforderungen pro Sekunde zu erreichen](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/). Ein anderer Kunde, Quorum, konnte durch die Nutzung von In-Memory-OLTP in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] seine Workload verdoppeln und zugleich [die Ressourcenauslastung um 70 % verringern](https://customers.microsoft.com/en-US/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database). Während andere Kunden in einigen Fällen eine Leistungszunahme um das 30-fache verzeichnen konnten, hängt Ihr Zuwachs vornehmlich von der Workload ab.

Woher rührt nun diese Leistungszunahme? Im Wesentlichen verbessert In-Memory-OLTP die Leistung der Transaktionsverarbeitung dank mehr Effizienz bei Datenzugriff und Transaktionsausführung sowie durch Beseitigen von Sperr- und Latchkonflikten zwischen gleichzeitig ausgeführten Transaktionen. Das Tempo beruht nicht auf der Ausführung im Arbeitsspeicher, sondern auf der Optimierung der sich im Arbeitsspeicher befindenden Daten. Datenspeicherung, Zugriff und Verarbeitungsalgorithmen wurden von Grund auf neu gestaltet, um in den Genuss der neuesten Weiterentwicklungen bei der Datenverarbeitung im Arbeitsspeicher und hoher Parallelität zu kommen.

Nur weil sich die Daten im Arbeitsspeicher befinden, heißt dies nicht, dass Sie sie bei einem Ausfall verlieren. Standardmäßig sind alle Transaktionen vollständig dauerhaft. Das bedeutet, dass Sie dieselbe Garantie für Dauerhaftigkeit wie für andere Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erhalten. Als Teil des Transaktionscommits werden alle Änderungen in das Transaktionsprotokoll auf dem Datenträger geschrieben. Wenn es zu einem beliebigen Zeitpunkt nach dem Commit der Transaktion zu einem Fehler kommt, sind Ihre Daten vorhanden, nachdem die Datenbank wieder online geschaltet wurde. Darüber hinaus arbeitet In-Memory-OLTP mit allen Hochverfügbarkeits- und Notfallwiederherstellungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], wie z.B. Always On, Sicherung, Wiederherstellung usw.

Zum Nutzen von In-Memory-OLTP in Ihrer Datenbank verwenden Sie eine oder mehrere der folgenden Typen von Objekten:

- *Speicheroptimierte Tabellen* dienen zum Speichern von Benutzerdaten. Sie deklarieren eine Tabelle bei ihrer Erstellung als speicheroptimiert.
- *Nicht dauerhafte Tabellen* dienen für kurzlebige Daten, entweder zum Zwischenspeichern oder für ein temporäres Resultset (als Ersatz für herkömmliche temporäre Tabellen). Eine nicht dauerhafte Tabelle ist eine speicheroptimierte Tabelle, die mit DURABILITY=SCHEMA_ONLY deklariert ist, was bedeutet, dass bei Änderungen an diesen Tabellen keine Ein-/Ausgaben (E/A) erfolgen. Dadurch wird die Nutzung von E/A-Protokollressourcen in Fällen vermieden, in denen Dauerhaftigkeit nicht unbedingt erforderlich ist.
- *Speicheroptimierte Tabellentypen* werden für Tabellenwertparameter (TVPs) sowie für temporäre Resultsets in gespeicherten Prozeduren verwendet. Diese können anstelle herkömmlicher Tabellentypen verwendet werden. Tabellenvariablen und TVPs, die mit einem speicheroptimierten Tabellentyp deklariert werden, übernehmen die Vorteile nicht dauerhafter speicheroptimierter Tabellen: effizienter Datenzugriff und keine E/A.
- *Nativ kompilierte T-SQL-Module* dienen zum weiteren Verringern des Zeitaufwands einzelner Transaktionen durch Reduzieren der CPU-Zyklen, die für das Verarbeiten von Vorgängen erforderlich sind. Sie deklarieren bei seiner Erstellung, dass ein Transact-SQL-Modul nativ kompiliert werden soll. Derzeit können die folgenden T-SQL-Module nativ kompiliert werden: gespeicherte Prozeduren, Trigger und benutzerdefinierte Skalarfunktionen.

In-Memory-OLTP ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] integriert. Da sich diese Objekte ähnlich wie ihre herkömmlichen Gegenstücke verhalten, können Sie die Leistung oft erhöhen, obwohl nur minimale Änderungen an der Datenbank und Anwendung vorgenommen werden. Darüber hinaus können Sie über speicheroptimierte und herkömmliche datenträgerbasierte Tabellen in derselben Datenbank verfügen und Abfragen auf beide anwenden. Weiter unten in diesem Artikel finden Sie ein Transact-SQL-Skript mit einem Beispiel für diese Objekttypen.

## <a name="usage-scenarios-for-in-memory-oltp"></a>Verwendungsszenarien für In-Memory-OLTP

In-Memory-OLTP ist kein magischer Schnellschalter und auch nicht für alle Workloads geeignet. Speicheroptimierte Tabellen verringern Ihre CPU-Auslastung nicht, wenn bei den meisten Abfragen eine Aggregation über große Datenbereiche erfolgt. In diesem Szenario empfehlen sich Columnstore-Indizes.

Es folgt eine Liste von Szenarien und Anwendungsmustern, bei denen Kunden mit In-Memory OLTP-erfolgreich waren.

### <a name="high-throughput-and-low-latency-transaction-processing"></a>Transaktionsverarbeitung mit hohem Durchsatz und niedriger Latenz

Dies ist das wichtigste Szenario, für das wir In-Memory-OLTP entwickelt haben: die Unterstützung großer Mengen von Transaktionen mit konsistent niedriger Latenz für einzelne Transaktionen.

Gängige Workloadszenarien sind u.a. Wertpapierhandel, Sportwetten, Spiele auf Mobilgeräten und Übermittlung von Werbeanzeigen. Ein weiteres häufiges Muster ist ein „Katalog“, der häufig gelesen und/oder aktualisiert wird. Beispiel: Sie verfügen über große Dateien, die jeweils auf verschiedene Clusterknoten verteilt sind, und katalogisieren den Speicherort jedes Shards jeder Datei in einer speicheroptimierten Tabelle.

#### <a name="implementation-considerations"></a>Überlegungen zur Implementierung

Verwenden Sie speicheroptimierte Tabellen für Ihre wichtigsten Transaktionstabellen, d.h. die Tabelle mit den meisten leistungskritischen Transaktionen. Verwenden Sie nativ kompilierte gespeicherte Prozeduren zum Optimieren der Ausführung der Logik, die den Geschäftstransaktion zugeordnet ist. Je mehr Logik Sie an gespeicherte Prozeduren in der Datenbank weitergeben können, desto mehr können Sie von In-Memory-OLTP profitieren.

So fangen Sie bei einer vorhandenen Anwendung an
1. Verwenden Sie den [Bericht mit der Transaktionsleistungsanalyse](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) , um die Objekte zu bestimmen, die Sie migrieren möchten. 
2. Verwenden Sie die Ratgeber für [Speicheroptimierung](memory-optimization-advisor.md) und [native Kompilierung](native-compilation-advisor.md) , die Sie bei der Migration unterstützen.

#### <a name="customer-case-studies"></a>Fallstudien von Kunden

- CMC Markets nutzt In-Memory-OLTP in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], um eine konsistent niedrige Latenz zu erreichen: [Da eine Sekunde Wartezeit zu lang ist, aktualisiert dieser Finanzdienstleister gerade seine Handelssoftware.](https://customers.microsoft.com/en-us/story/because-a-second-is-too-long-to-wait-this-financial-services-firm-is-updating-its-trading-software)
- Derivco nutzt In-Memory-OLTP in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], um einen erhöhten Durchsatz zu unterstützen und Workloadspitzen zu bewältigen: [Wenn ein Anbieter von Onlinespielen seine Zukunft nicht riskieren will, setzt er auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].](https://customers.microsoft.com/en-us/story/when-an-online-gaming-company-doesnt-want-to-risk-its-future-it-bets-on-sql-server-2016)


### <a name="data-ingestion-including-iot-internet-of-things"></a>Datenerfassung, einschließlich IoT (Internet der Dinge)

In-Memory-OLTP ist für die gleichzeitige Erfassung großer Datenmengen aus vielen verschiedenen Quellen geeignet. Häufig ist es vorteilhaft, Daten im Vergleich mit anderen Zielen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zu erfassen, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Anwenden von Abfragen auf die Daten stark beschleunigt und Ihnen dadurch Einblicke in Echtzeit ermöglicht.

Folgende Anwendungsmuster werden häufig verwendet: 
-  Erfassen von Sensormesswerten und -ereignissen sowie das Zulassen von Benachrichtigungen und Verlaufsanalysen. 
-  Verwalten von Batchaktualisierungen, auch aus mehreren Quellen, bei gleichzeitiger Minimierung der Auswirkungen auf die gleichzeitige Leseworkload.

#### <a name="implementation-considerations"></a>Überlegungen zur Implementierung

Verwenden Sie für die Datenerfassung eine speicheroptimierte Tabelle. Wenn die Erfassung hauptsächlich aus Einfügungen (anstelle von Aktualisierungen) besteht und der In-Memory-OLTP-Speicherbedarf von Belang ist, haben Sie diese Optionen:

- Verwenden Sie einen Auftrag, der [verwendet, um Daten regelmäßig per Batchvorgang in einer datenträgerbasierten Tabelle mit einem](../indexes/columnstore-indexes-overview.md)gruppierten Columnstore-Index `INSERT INTO <disk-based table> SELECT FROM <memory-optimized table>`abzuladen, oder
- Arbeiten Sie mit einer [temporalen speicheroptimierten Tabelle](../tables/system-versioned-temporal-tables-with-memory-optimized-tables.md) zum Verwalten von Verlaufsdaten. In diesem Modus befinden sich die Verlaufsdaten auf dem Datenträger, und die Datenverschiebung wird vom System verwaltet.

Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Beispielrepository enthält eine Smart Grid-Anwendung, die eine temporale speicheroptimierte Tabelle, einen speicheroptimierten Tabellentyp und eine nativ kompilierte gespeicherte Prozedur verwendet, um die Datenerfassung zu beschleunigen, während der In-Memory-OLTP-Speicherbedarf der Sensordaten verwaltet wird: 

 - [smart-grid-release](https://github.com/Microsoft/sql-server-samples/releases/tag/iot-smart-grid-v1.0) 
 - [smart-grid-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/iot-smart-grid)
 
#### <a name="customer-case-studies"></a>Fallstudien von Kunden

- [Quorum verdoppelt die Workload seiner wichtigen Datenbank und senkt die Auslastung um 70 % mithilfe von In-Memory-OLTP in Azure SQL-Datenbank](http://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)
- EdgeNet hat mit In-Memory-OLTP in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] die Leistung von Batch-Datenladevorgängen verbessert und die Notwendigkeit eines Mid-Tier-Caches beseitigt: [Anbieter von Datendiensten verschafft sich Echtzeitzugriff auf Produktdaten mit In-Memory-Technologie](https://customers.microsoft.com/en-us/story/data-services-firm-gains-real-time-access-to-product-d)
- Das Beth Israel Deaconess Medical Center konnte mithilfe von In-Memory-OLTP in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] die Datenerfassungsrate von Domänencontrollern drastisch steigern: [https://customers.microsoft.com/en-us/story/strengthening-data-security-and-creating-more-time-for]

### <a name="caching-and-session-state"></a>Zwischenspeicherung und Sitzungszustand

Die In-Memory-OLTP-Technologie macht SQL Server für die Verwaltung des Sitzungszustands (z. B. für ASP.NET-Anwendungen) und die Zwischenspeicherung sehr attraktiv.

Der ASP.NET-Sitzungszustand ist ein sehr erfolgreicher Anwendungsfall für In-Memory-OLTP. Mithilfe von[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konnte ein Kunde 1,2 Millionen Anforderungen pro Sekunde erreichen. Mittlerweile hat das Unternehmen begonnen, In-Memory-OLTP für die Cacheanforderungen aller Mid-Tier-Anwendungen zu nutzen. Details: [Wie bwin In-Memory-OLTP in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] zum Erreichen einer beispiellosen Leistung und Skalierung nutzt](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

#### <a name="implementation-considerations"></a>Überlegungen zur Implementierung

Sie können nicht dauerhafte speicheroptimierte Tabellen als einfachen Schlüssel-Wert-Speicher nutzen, indem Sie ein Blob in Spalten des Typs „varbinary(max)“ speichern. Alternativ können Sie einen teilweise strukturierten Cache mit [JSON-Unterstützung](https://azure.microsoft.com/blog/json-support-is-generally-available-in-azure-sql-database/) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] implementieren. Schließlich können Sie einen vollständig relationalen Cache mithilfe nicht dauerhafter Tabellen mit einem vollständig relationalen Schema einschließlich verschiedener Datentypen und Einschränkungen erstellen.

Machen Sie die ersten Schritte mit einem speicheroptimierten ASP.NET-Sitzungsstatus, indem Sie die auf GitHub veröffentlichten Skripts nutzen, um die vom integrierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sitzungsstatusanbieter erstellten Objekte zu ersetzen:

- [aspnet-session-state](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/aspnet-session-state)

#### <a name="customer-case-studies"></a>Fallstudien von Kunden

- bwin konnte mit In-Memory-OLTP in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] den Durchsatz drastisch steigern und den Hardwarebedarf für den ASP.NET-Sitzungsstatus verringern: [Website für Onlinespiele kann eine Skalierung von 250.000 Anforderungen pro Sekunde erreichen und das Spielerlebnis verbessern](https://customers.microsoft.com/en-us/story/gaming-site-can-scale-to-250000-requests-per-second-an)
- bwin hat mit In-Memory-OLTP in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] den Durchsatz mithilfe des ASP.NET-Sitzungsstatus noch weiter erhöht und unternehmensweit ein Mid-Tier-Cachesystem implementiert: [Wie bwin In-Memory-OLTP in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nutzt, um eine beispiellose Leistung und Skalierung zu erreichen](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

### <a name="tempdb-object-replacement"></a>Ersetzen des Objekts „tempdb“

Nutzen Sie nicht dauerhafte Tabellen und speicheroptimierte Tabellentypen, um Ihre herkömmlichen auf tempdb basierenden Strukturen wie temporäre Tabellen, Tabellenvariablen und Tabellenwertparameter (TVPs) zu ersetzen.

Speicheroptimierte Tabellenvariablen und nicht dauerhafte Tabellen sorgen im Vergleich mit herkömmlichen Tabellenvariablen und der Tabelle „#temp“ meist für eine Senkung der CPU-Last und die vollständige Beseitigung von Ein- und Ausgaben für Protokolle.

#### <a name="implementation-considerations"></a>Überlegungen zur Implementierung

Lesen Sie zum Einstieg: [Verbesserern der temporären Tabelle und Tabellenvariablenleistung mithilfe der Speicheroptimierung](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)

#### <a name="customer-case-studies"></a>Fallstudien von Kunden

- Ein Kunde konnte die Leistung um 40 % verbessern, indem herkömmliche Tabellenwertparameter einfach durch speicheroptimierte Gegenstücke ersetzt wurden: [Sehr schnelle Erfassung von IoT-Daten mithilfe von In-Memory-OLTP in Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/04/07/a-technical-case-study-high-speed-iot-data-ingestion-using-in-memory-oltp-in-azure/)

### <a name="etl-extract-transform-load"></a>ETL (Extrahieren, Transformieren, Laden)

ETL-Workflows sehen häufig das Laden von Daten in eine Stagingtabelle, Transformationen der Daten und das Laden in die endgültigen Tabellen vor.

#### <a name="implementation-considerations"></a>Überlegungen zur Implementierung

Verwenden Sie für das Staging von Daten nicht dauerhafte speicheroptimierte Tabellen. Bei diesen Tabellen fallen keine E/A-Vorgänge an, wodurch der Datenzugriff effizienter wird.

Wenn Sie im Rahmen des Workflows Transformationen auf die Stagingtabelle anwenden, können Sie zum Beschleunigen dieser Transformationen nativ kompilierte gespeicherte Prozeduren verwenden. Wenn diese Transformationen parallel erfolgen können, verschaffen Sie sich durch die Speicheroptimierung weitere Skalierungsvorteile.

## <a name="sample-script"></a>Beispielskript

Bevor Sie In-Memory-OLTP verwenden können, müssen Sie die Dateigruppe MEMORY_OPTIMIZED_DATA erstellen. Außerdem empfehlen wir den Datenbank-Kompatibilitätsgrad 130 (oder höher) und das Festlegen der Datenbankoption MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT auf ON.

Sie können mithilfe des Skripts am folgenden Speicherort die Dateigruppe im standardmäßigen Datenordner erstellen und die empfohlenen Einstellungen konfigurieren:

- [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)

Das folgende Skript veranschaulicht In-Memory-OLTP-Objekte, die Sie in der Datenbank erstellen können:

```sql
-- configure recommended DB option
ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
GO
-- memory-optimized table
CREATE TABLE dbo.table1
( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
  c2 NVARCHAR(MAX))
WITH (MEMORY_OPTIMIZED=ON)
GO
-- non-durable table
CREATE TABLE dbo.temp_table1
( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
  c2 NVARCHAR(MAX))
WITH (MEMORY_OPTIMIZED=ON,
      DURABILITY=SCHEMA_ONLY)
GO
-- memory-optimized table type
CREATE TYPE dbo.tt_table1 AS TABLE
( c1 INT IDENTITY,
  c2 NVARCHAR(MAX),
  is_transient BIT NOT NULL DEFAULT (0),
  INDEX ix_c1 HASH (c1) WITH (BUCKET_COUNT=1024))
WITH (MEMORY_OPTIMIZED=ON)
GO
-- natively compiled stored procedure
CREATE PROCEDURE dbo.usp_ingest_table1
  @table1 dbo.tt_table1 READONLY
WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC
    WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT,
          LANGUAGE=N'us_english')

  DECLARE @i INT = 1

  WHILE @i > 0
  BEGIN
    INSERT dbo.table1
    SELECT c2
    FROM @table1
    WHERE c1 = @i AND is_transient=0

    IF @@ROWCOUNT > 0
      SET @i += 1
    ELSE
    BEGIN
      INSERT dbo.temp_table1
      SELECT c2
      FROM @table1
      WHERE c1 = @i AND is_transient=1

      IF @@ROWCOUNT > 0
        SET @i += 1
      ELSE
        SET @i = 0
    END
  END

END
GO
-- sample execution of the proc
DECLARE @table1 dbo.tt_table1
INSERT @table1 (c2, is_transient) VALUES (N'sample durable', 0)
INSERT @table1 (c2, is_transient) VALUES (N'sample non-durable', 1)
EXECUTE dbo.usp_ingest_table1 @table1=@table1
SELECT c1, c2 from dbo.table1
SELECT c1, c2 from dbo.temp_table1
GO
```   

## <a name="resources-to-learn-more"></a>Weiterführende Ressourcen:

[In-Memory-OLTP-Technologien für höhere T-SQL-Leistung](http://msdn.microsoft.com/library/mt694156.aspx)   
Eine Demo der Leistung bei der Verwendung von In-Memory-OLTP finden Sie unter: [in-memory-oltp-perf-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)   
[17-minütiges Video mit einer Erläuterung von In-Memory-OLTP und Präsentation der Demo](https://www.youtube.com/watch?v=l5l5eophmK4) (Demo bei 8:25)   
[Skript zum Aktivieren von In-Memory-OLTP und zum Festlegen empfohlener Optionen](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)   
[Hauptdokumentation zu In-Memory-OLTP](in-memory-oltp-in-memory-optimization.md)   
[Vorteile bei der Nutzung von Leistung und Ressourcen des In-Memory OLTP in der Azure SQL-Datenbank](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)  
[Verbesserern der temporären Tabelle und Tabellenvariablenleistung mithilfe der Speicheroptimierung](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)   
[Optimieren der Leistung mithilfe von In-Memory-Technologien in SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)  
[Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
[In-Memory-OLTP – Allgemeine Arbeitsauslastungsmuster und Überlegungen zur Migration](http://msdn.microsoft.com/library/dn673538.aspx) 
