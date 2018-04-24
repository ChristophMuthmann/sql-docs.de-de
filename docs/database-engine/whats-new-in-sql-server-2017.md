---
title: Neues im Datenbankmodul – SQL Server 2017 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Active
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 00a99af38eb93eda65928a033dc025329e944b21
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="whats-new-in-database-engine---sql-server-2017"></a>Neues im Datenbankmodul – SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

In diesem Thema werden die Verbesserungen an [!INCLUDE[ssdenoversion-md](../includes/ssdenoversion-md.md)] für [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] beschrieben. Klicken Sie auf die Links, um weitere Informationen zu jedem Element zu erhalten:

> [!NOTE]  
> SQL Server 2017 beinhaltet auch die in den SQL Server 2016 Service Packs hinzugefügten Features. Informationen zu diesen Elementen finden Sie unter [Neuigkeiten im Datenbankmodul](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).

**Erweiterungen**  

- CLR verwendet die Codezugriffssicherheit (Code Access Security, CAS) im .NET Framework, die nicht länger als Sicherheitsbegrenzung unterstützt wird. Eine CLR-Assembly, die mit `PERMISSION_SET = SAFE` erstellt wurde, kann womöglich auf externe Systemressourcen zugreifen, nicht verwalteten Code aufrufen und sysadmin-Privilegien erwerben. Ab [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] wird eine `sp_configure`-Option mit der Bezeichnung `clr strict security` eingeführt, um die Sicherheit von CLR-Assemblys zu erhöhen. `clr strict security` ist standardmäßig aktiviert und behandelt `SAFE`- und `EXTERNAL_ACCESS`-Assemblys so, als wären Sie als `UNSAFE` gekennzeichnet. Die Option `clr strict security` kann für die Abwärtskompatibilität deaktiviert werden, es wird jedoch nicht empfohlen. Microsoft empfiehlt, dass alle Assemblys durch ein Zertifikat oder einen asymmetrischen Schlüssel mit einem entsprechenden Anmeldenamen signiert werden, dem `UNSAFE ASSEMBLY`-Berechtigung für die Masterdatenbank gewährt wurde. CLR-Assemblys können als Problemumgehung für das `clr strict security`-Feature einer Positivliste hinzugefügt werden. [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) und [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) wurden hinzugefügt, um die Positivliste von vertrauenswürdigen Assemblys zu unterstützen. Weitere Informationen finden Sie unter [CLR Strict Security](configure-windows/clr-strict-security.md).  
- Eine neue DMF, [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), wird eingeführt, um zusammenfassende Ebenenattribute und Informationen zu den Transaktionsprotokolldateien verfügbar zu machen. Dies ist hilfreich für die Überwachung der Integrität des Transaktionsprotokolls.  
- Fortsetzbare Neuerstellungen von online geschalteten Indizes Mit fortsetzbaren Online-Indexneuerstellung können Sie den Vorgang einer Online-Indexneuerstellung dort fortsetzen, wo es nach einem Fehler aufgehört hat (z.B. einem Failover in einem Replikat oder nicht genügend Speicherplatz). Sie können es aus pausieren und den Vorgang der Online-Indexneuerstellung später fortsetzen. Es kann z.B. notwendig sein, dass Sie vorübergehend Systemressourcen verfügbar machen, um einen Task mit hoher Priorität auszuführen oder Indexneuerstellung in einem anderen Wartungsfenster abzuschließen, wenn das verfügbare Wartungsfenster zu klein für eine große Tabelle ist. Zudem erfordern fortsetzbare Online-Indexneuerstellungen keinen erheblichen Speicherplatz, wodurch Sie eine Protokollkürzung durchführen können, während der Vorgang der fortsetzbaren Erstellung ausgeführt wird. Finden Sie unter [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) und [Richtlinien für Onlineindexvorgänge](../relational-databases/indexes/guidelines-for-online-index-operations.md).
- **IDENTITY_CACHE-Option für ALTER DATABASE SCOPED CONFIGURATION** Die Option IDENTITY_CACHE wurde neue in `ALTER DATABASE SCOPED CONFIGURATION` T-SQL-Anweisungen hinzugefügt. Wenn diese Option auf `OFF` festgelegt ist, kann das Datenbankmodul Lücken in den Werten von Identitätsspalten vermeiden, wenn ein Server unerwartet neu startet oder ein Failover auf einen sekundären Server ausführt. Finden Sie unter [ALTER ausgelegte DATENBANKKONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).   
-  [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] bietet jetzt Graphdatenbank-Funktionen, mit denen aussagekräftigere beziehungsorientierte Daten modelliert werden können. Dazu zählt [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md)-Syntax zum Erstellen von Knoten- und Rahmentabellen und das Schlüsselwort [MATCH](../t-sql/queries/match-sql-graph.md) für Abfragen. Weitere Informationen finden Sie unter [Graph Processing with SQL Server 2017 (Graph-Verarbeitung mit SQL Server-2017)](../relational-databases/graphs/sql-graph-overview.md).   
- Eine neue Generation von Verbesserungen bei der Abfrageverarbeitung wendet Optimierungsstrategien auf die Laufzeitbedingungen Ihrer Anwendungsarbeitsauslastung an. In dieser ersten Version der Featurefamilie für die **adaptive Abfrageverarbeitung** gibt es drei neue Verbesserungen: **Adaptive Joins im Batchmodus**, **Feedback zur Speicherzuweisung im Batchmodus** und **überlappende Ausführung** für Tabellenwertfunktionen mit mehreren Anweisungen.  Weitere Informationen finden Sie unter [Adaptive Abfrageverarbeitung in SQL-Datenbanken](../relational-databases/performance/adaptive-query-processing.md).
- Die automatische Datenbankoptimierung bietet einen Einblick in die potentiellen Abfrageleistungsprobleme, empfiehlt Lösungen und kann identifizierte Probleme automatisch beheben. Die automatische Optimierung in [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] benachrichtigt Sie, wenn ein mögliches Leistungsproblem erkannt wird. Sie können mit Ihr Korrekturmaßnahme ergreifen. Zudem kann [!INCLUDE[ssde-md](../includes/ssde-md.md)] die Leistungsprobleme automatisch beheben. Weitere Informationen finden Sie unter [Automatic tuning (Automatische Optimierung)](../relational-databases/automatic-tuning/automatic-tuning.md).
- PERFORMANCE ENHANCEMENT FOR NON CLUSTERED INDEX BUILD ON MEMORY-OPTIMIZED TABLES. Die Leistung von bwtree-Indexneuerstellung (kein Cluster) für MEMORY_OPTIMIZED-Tabellen während der Datenbankwiederherstellung wurde deutliche optimiert. Diese Verbesserung reduziert die Zeit der Datenbankwiederherstellung deutlich, wenn Nicht-Cluster-Indizes verwendet werden.  
- [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) hat drei neue Spalten: socket_count, cores_per_socket, numa_node_count. Dies ist nützlich, wenn Sie Ihren Server in einer VM ausführen, weil ein übermäßiger NUMA zu einer Überbelegung von Hosts und so letztlich zu Leistungsproblemen führen kann.
- Die neue Spalte column modified_extent_page_count\, wird in [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) eingeführt, um differenzielle Änderungen in jeder Datenbankdatei der Datenbank nachzuverfolgen. Mit der neuen Spalte „modified_extent_page_count“ können Sie intelligente Sicherungslösungen erstellen, die differenzielle Sicherungen durchführen, wenn die Prozentzahl der geänderten Seiten einen Schwellenwert (z.B. 70-80 %) nicht erreichen. Andernfalls wird eine vollständige Datenbanksicherung durchgeführt.
- SELECT INTO … ON FileGroup: [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) unterstützt jetzt das Laden einer Tabelle in eine Dateigruppe, die nicht die Standarddateigruppe des Benutzers ist. Dies ist durch die in die SELECT INTO TSQL-Syntax hinzugefügte Unterstützung des Schlüsselworts **ON** möglich.
- Tempdb-Setupverbesserungen: Setup erlaubt das Festlegen der anfänglichen tempdb-Dateigröße auf bis zu **256 GB (262.144 MB)** pro Datei mit einer Meldung an den Kunden, wenn die Dateigröße auf einen Wert größer als 1 GB festgelegt und IFI nicht aktiviert ist. Es ist wichtig, dass Sie verstehen, was es bedeutet, wenn Sie die schnelle Dateiinitialisierung (IFI) nicht aktivieren: Die Setupzeit kann exponentiell steigen je nach festgelegter anfänglicher Größe der tempdb-Datendatei. IFI kann nicht auf die Größe von Transaktionsprotokollen angewendet werden. Wenn Sie also den Wert der Transaktionsprotokolle erhöhen, kann dies die Setupzeit beim Starten von tempdb während des Setups erhöhen, unabhängig von der IFI-Einstellung für das SQL Sever-Dienstkonto.
- Eine neue DMV [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) wird eingeführt, um die Versionspeichernutzung pro Datenbank nachzuverfolgen. Diese neue DMV ist beim Überwachen von tempdb für die Versionspeichernutzung nützlich, sodass Sie tempdb-Größen proaktiv planen können, basierend auf den Anforderungen der Versionspeichernutzung pro Datenbank, ohne dass Sie bei der Leistung einbüßen müssen und ohne den Aufwand der Ausführung auf Produktionsservern.
- Eine neue DMF [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) wird eingeführt, mit der Sie VLF-Informationen ähnlich wie DBCC LOGINFO verfügbar machen können, um potentielle Transaktionsprotokollprobleme zu überwachen, davor zu warnen und diese zu vermeiden.
- Verbesserte Leistung bei der Sicherung kleinerer Datenbanken auf hochwertigen Servern: Beim Ausführen einer Sicherung einer Datenbank in SQL Server, erfordert der Sicherungsprozess mehrere Iterationen des Pufferpools, um fortlaufende E/A auszugleichen. Dadurch ist die Sicherungszeit nicht nur eine Funktion der Datenbankgröße sondern auch eine Funktion der Größe des aktiven Pufferpools. In SQL Server 2017 wurde die Sicherung optimiert, um mehrere Iterationen des Pufferpools zu vermeiden. Dies führt zu einer deutlichen Leistungssteigerung für kleine bis mittelgroße Datenbanken. Die Leistungssteigerung sinkt mit steigender Datenbankgröße, da die zu sichernden Seiten und die Sicherungs-E/A im Vergleich zur Iteration des Pufferpools mehr Zeit in Anspruch nehmen.  
- Der Abfragedatenspeicher erfasst jetzt Zusammenfassungsinformationen zu Wartestatistiken. Das Erfassen von Wartestatistikkategorien pro Abfrage im Abfragedatenspeicher ermöglicht die nächste Stufe der Problembehebung bei der Leistung, da dadurch noch mehr Einblicke in die Workloadleistung und deren Engpässe gegeben werden, während gleichzeitg die Hauptvorteile des Abfragedatenspeichers bestehen bleiben.  
- Temporale Tabelle mit Versionsverwaltung durch das System unterstützen jetzt CASCADE DELTE und CASCADE UPDATE.  
- Indirekte Prüfpunkte für die Leistungsverbesserung
- Verfügbarkeitsgruppen mit weniger Clusterunterstützung wurden hinzugefügt.
- Die Einstellungen des Minimum Replikat-Commits der Verfügbarkeitsgruppen wurden hinzugefügt.
- Verfügbarkeitsgruppen funktionieren jetzt auch über Windows-Linux, um OS-übergreifende Migrationen und Tests zu ermöglichen.
- Temporale Tabellen für den Support der Beibehaltungsrichtlinien wurden hinzugefügt.
- Neue DMV SYS.DM_DB_STATS_HISTOGRAM
- Onlinesupport für die Erstellung und Neuerstellung des nicht geclusterten Columnstore-Index wurde hinzugefügt.
- [Sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) wird zum Untersuchen von Statistiken hinzugefügt.
- Der Datenbankoptimierungsratgebers (DTA), der mit SQL Server Management Studio Version 16.4 freigegeben wurde, verfügt über zusätzliche Optionen, wenn SQL Server 2016 analysiert wird.    
   - Verbesserte Leistung. Weitere Informationen finden Sie unter [Performance Improvements using Database Engine Tuning Advisor (DTA) recommendations (Leistungsverbesserungen mithilfe von Empfehlungen des Datenbankoptimierungsratgebers (DTA))](../relational-databases/performance/performance-improvements-using-dta-recommendations.md).
   - Die `-fc` -Option, die Empfehlungen für Columnstore-Indizes zulässt. Weitere Informationen finden Sie unter [dta (Hilfsprogramm)](../tools/dta/dta-utility.md) und [Columnstore index recommendations in Database Engine Tuning Advisor (DTA) (Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA))](../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).  
   - Die `-iq` -Option, die dem DTA erlaubt, eine Arbeitsauslastung aus dem Abfragespeicher zu überprüfen. Weitere Informationen finden Sie unter [Tuning Database Using Workload from Query Store (Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher)](../relational-databases/performance/tuning-database-using-workload-from-query-store.md).  
- Für InMemory-Funktionen sind zusätzliche Erweiterungen zu speicheroptimierten Tabellen und nativ kompilierten Funktionen verfügbar. Codebeispiele, die diese Verbesserungen veranschaulichen, finden Sie unter [Optimieren der JSON-Verarbeitung mit In-Memory-OLTP](../relational-databases/json/optimize-json-processing-with-in-memory-oltp.md).
    - Unterstützung für berechnete Spalten in speicheroptimierten Tabellen und Indizes auf berechneten Spalten.
    - Vollständige Unterstützung für JSON-Funktionen in nativ kompilierten Modulen und CHECK-Einschränkungen.  
    - `CROSS APPLY` -Operator in nativ kompilierten Modulen.   
- Die neuen Zeichenfolgenfunktionen [CONCAT_WS](../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../t-sql/functions/translate-transact-sql.md)und [TRIM](../t-sql/functions/trim-transact-sql.md) wurden hinzugefügt.   
- Die `WITHIN GROUP` -Klausel wird nun für die [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) -Funktion unterstützt.
- Es wurden zwei neue japanische Sortierungsfamilien (Japanese_Bushu_Kakusu_140 und Japanese_XJIS_140) hinzugefügt, und die Sortierungsoption „Unterscheidung nach Variierungsauswahlzeichen“ (_VSS) wurde für die Verwendung in diesen neuen japanischen Sortierungen hinzugefügt. Darüber hinaus unterstützen alle neuen Sortierungen automatisch ergänzende Zeichen, ohne dass die Angabe der _SC-Option notwendig ist. Einzelheiten dazu finden Sie unter [Sortierung und Unicode-Unterstützung](../relational-databases/collations/collation-and-unicode-support.md).   
- Neue Bulk-Access-Optionen ([BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET(BULK...)](../t-sql/functions/openrowset-transact-sql.md)) ermöglichen den Zugriff auf Daten direkt aus einer Datei, die als CSV-Format angegeben ist, und über die neue `BLOB_STORAGE` -Option von [EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)aus Dateien in Azure Blob Storage.
- Der Datenbank- **KOMPATIBILITÄTSGRAD** 140 wurde hinzugefügt.   Kunden, die diesen Kompatibilitätsgrad ausführen, können die neuesten Sprachfeatures und Verhaltensweisen des Abfrageoptimierers nutzen. Dies schließt Änderungen in den einzelnen von Microsoft veröffentlichten Vorabversionen ein.
- Verbesserte Berechnung der Aktualisierungsschwellenwerte für inkrementelle Statistiken (Kompatibilitätsgrad 140 erforderlich).
- [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) wurde hinzugefügt.
- Es wurden mehrere Verbesserungen der Leistung und Sprache an speicheroptimierten Objekten vorgenommen:
    - `sp_spaceused` wird jetzt für speicheroptimierte Tabellen unterstützt.
    - `sp_rename` wird jetzt für speicheroptimierte Tabelle und nativ kompilierte T-SQL-Module unterstützt.
    - `CASE`-Anweisungen werden jetzt für nativ kompilierte T-SQL-Module unterstützt.
    - Die Beschränkung auf 8 Indizes für speicheroptimierte Tabellen wurde aufgehoben.
    - `TOP (N) WITH TIES` wird jetzt in nativ kompilierten T-SQL-Modulen unterstützt.
    - `ALTER TABLE` mit speicheroptimierten Tabellen ist jetzt für gewöhnlich deutlich schneller.
    - Das Wiederholen des Transaktionsprotokolls von speicheroptimierten Tabellen wird nun parallel ausgeführt. Dies verbessert die Wiederherstellungszeit und erhöht den erhaltenen Durchsatz von Always On-Verfügbarkeitsgruppenkonfigurationen deutlich.
    - Speicheroptimierte Dateigruppendateien können jetzt in Azure Storage gespeichert werden. Sichern/Wiederherstellen von speicheroptimierten Dateien ist jetzt in Azure Storage verfügbar.
- Gruppierte Columnstore-Indizes unterstützen jetzt LOB-Spalten (nvarchar(max), varchar(max), varbinary(max)).
- Die Aggregatfunktion [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) wurde hinzugefügt.  
- Neue Berechtigungen: `DATABASE SCOPED CREDENTIAL` ist jetzt eine Klasse von sicherungfsähigen, unterstützenden `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP`und `VIEW DEFINITION` -Berechtigungen. `ADMINISTER DATABASE BULK OPERATIONS`, das auf SQL-Datenbanken beschränkt ist, ist jetzt in `sys.fn_builtin_permissions` sichtbar.   
- Die DMV [sys.dm_os_host_info](../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) wurde hinzugefügt und stellt Systeminformationen sowohl für Windows als auch für Linux bereit.   
- Die Datenbankrollen werden mit R Services für das Verwalten von Berechtigungen erstellt, die Paketen zugeordnet sind. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).

