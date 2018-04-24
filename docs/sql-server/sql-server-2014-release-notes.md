---
title: SQL Server 2014 Release Notes | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2018
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 727798fd3cc320f90586f476e4ee43f0a1867f3f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
In diesem Artikel werden bekannte Probleme mit Releases von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] erläutert, einschließlich der zugehörigen Service Packs.

## <a name="sql-server-2014-service-pack-2-sp2"></a>SQL Server 2014 Service Pack 2 (SP2)

SQL Server 2014 SP2 enthält Rollups von veröffentlichten Hotfixes für SQL Server 2014 SP1 CU7. Es umfasst Verbesserungen im Bereich der Leistung, Skalierbarkeit und Diagnose, die auf dem Feedback von Kunden und der SQL-Community basieren.

### <a name="performance-and-scalability-improvements-in-sp2"></a>Verbesserte Leistung und Skalierbarkeit in SP2

|Funktion|Description|Weitere Informationen finden Sie unter|
|---|---|---|
|Automatische Soft-NUMA-Partitionierung|Sie können Soft-NUMA automatisch auf Systemen konfigurieren, die über mindestens 8 CPUs pro NUMA-Knoten verfügen.|[Soft-NUMA (SQL Server)](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)|
|Pufferpoolerweiterung|Ermöglicht eine Skalierung des SQL Server-Pufferpools über 8 TB hinaus.|[Pufferpoolerweiterung](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension)|
|Skalierung dynamischer Arbeitsspeicherobjekte| Dynamische Partitionierung von Arbeitsspeicherobjekten basierend auf der Anzahl von Knoten und Kernen. Durch diese Erweiterung wird das Ablaufverfolgungsflag 8048 nach SQL 2014 SP2 nicht mehr benötigt.|[Dynamic Memory Object Scaling](https://blogs.msdn.microsoft.com/sql_server_team/dynamic-memory-object-scaling/) (Skalierung dynamischer Arbeitsspeicherobjekte)|
|MAXDOP-Hinweis für DBCC CHECK*-Befehle|Diese Verbesserung ist für die Ausführung von DBCC CHECKDB mit einer anderen MAXDOP-Einstellung als dem Wert „sp_configure“ hilfreich.|[Hinweise (Transact-SQL) – Abfrage](https://docs.microsoft.com/sql/t-sql/queries/hints-transact-sql-query)|
|Verbesserung des SOS_RWLock-Spinlocks|Dadurch ist der SOS_RWLock-Spinlock nicht mehr erforderlich. Stattdessen können Techniken ohne Sperren verwendet werden, die mit In-Memory OLTP vergleichbar sind. |[Änderung von SOS_RWLock](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)|
|Räumliche native Implementierung|Erhebliche Verbesserung der Leistung bei Abfragen nach räumlichen Daten.|[Spatial performance improvements in SQL Server 2012 and 2014 (Leistungsverbesserungen für räumliche Funktionen in SQL Server 2012 und 2014)](https://support.microsoft.com/help/3107399/spatial-performance-improvements-in-sql-server-2012-and-2014)

### <a name="supportability-and-diagnostics-improvements-in-sp2"></a>Verbesserte Unterstützung und Diagnose in SP2

|Funktion|Description|Weitere Informationen finden Sie unter|
|---|---|---|
|Protokollierung des Always On-Zeitlimits|Für Leasezeitlimit-Nachrichten wurde eine neue Protokollierungsfunktion hinzugefügt, mit der die aktuelle Zeit und die Zeiten für die erwartete Erneuerung protokolliert werden. |[Improved Always On Availability Group Lease Timeout Diagnostics (Verbesserte Leasezeitlimit-Diagnose bei Always On-Verfügbarkeitsgruppe)](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)
|Always On-XEvents und -Leistungsindikatoren|Neue Always On-XEvents und -Leistungsindikatoren zur Verbesserung der Diagnose von Problemen mit Always On in Bezug auf die Wartezeit bei der Problembehandlung. |[KB 3107172](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve) und [KB 3107400](https://support.microsoft.com/help/3107400/improved-tempdb-spill-diagnostics-in-showplan-xml-schema-in-sql-server)
|Bereinigen der Änderungsnachverfolgung|Eine neue gespeicherte Prozedur, sp_flush_CT_internal_table_on_demand, bereinigt bedarfsgesteuert interne Tabellen der Änderungsnachverfolgung.|[KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)
|Klonen von Datenbanken|Verwenden Sie den neuen DBCC-Befehl, um durch Klonen von Schema, Metadaten und Statistiken, jedoch ohne die Daten, eine Fehlerbehebung bei vorhandenen Produktionsdatenbanken durchzuführen. Geklonte Datenbanken sind nicht für die Verwendung in Produktionsumgebungen bestimmt.|[KB 3177838](https://support.microsoft.com/help/3177838/how-to-use-dbcc-clonedatabase-to-generate-a-schema-and-statistics-only)
|DMF-Ergänzungen|Neue sys.dm_db_incremental_stats_properties der DMF machen Informationen pro Partition zu inkrementellen Statistiken verfügbar.|[KB 3170114](https://support.microsoft.com/help/3170114/update-to-add-dmf-sys-dm-db-incremental-stats-properties-in-sql-server)
|DMF zum Abrufen von Eingabepuffer in SQL Server|Eine neue DMF zum Abrufen des Eingabepuffers für eine Sitzung/Anforderung (sys.dm_exec_input_buffer) ist jetzt verfügbar. Diese ist funktionell äquivalent zu DBCC INPUTBUFFER.|[sys.dm_exec_input_buffer](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql)
|DROP DDL-Unterstützung für die Replikation|Ermöglicht das Löschen einer Tabelle aus der Datenbank und der Veröffentlichung, die als Artikel in der Veröffentlichung einer Transaktionsreplikation enthalten ist.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)
|IFI-Berechtigung für SQL-Dienstkonto|Bestimmt, ob die schnelle Dateiinitialisierung (Instant File Initialization, IFI) beim Starten des SQL Server-Dienstes aktiviert ist.|[Datenbankdatei-Initialisierung](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)
|Arbeitsspeicherzuweisungen – Behandlung von Problemen|Sie können während der Ausführung von Abfragen Diagnosehinweise nutzen, indem Sie zur Vermeidung eines Speicherkonflikts die zugehörigen Speicherzuweisungen beschränken.|[KB 3107401](https://support.microsoft.com/help/3107401/new-query-memory-grant-options-are-available-min-grant-percent-and-max)
|Lightweight-Profilerstellung für die Abfrageausführung pro Operator |Optimiert die Erfassung von Statistiken zur Abfrageausführung pro Operator, wie z.B. die tatsächliche Anzahl von Zeilen.|[Developers Choice: Query progress - anytime, anywhere (Wahl der Entwickler: Abfragestatus – jederzeit und überall)](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)
|Abfrageausführungsdiagnose|Tatsächlich gelesene Zeilen werden jetzt zur Verbesserung der Behebung von Abfrageleistungsproblemen in Abfrageausführungsplänen gemeldet.|[KB 3107397](https://support.microsoft.com/help/3107397/improved-diagnostics-for-query-execution-plans-that-involve-residual-p)
|Abfrageausführungsdiagnose bei tempdb spill|Hash Warning und Sort Warnings verfügen jetzt über zusätzliche Spalten zum Nachverfolgen von physischen E/A-Statistiken, verwendetem Speicher und betroffenen Zeilen. |[Verbesserte Diagnose von temptdb spill](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve)
|Tempdb-Unterstützbarkeit |Verwenden Sie beim Serverstart eine neue Errorlog-Nachricht für die Anzahl der tempdb-Dateien und tempdb-Datendateiänderungen.|[KB 2963384](https://support.microsoft.com/help/2963384/fix-sql-server-crashes-when-the-log-file-of-tempdb-database-is-full-in)


Zudem sollten Sie folgende Problembehandlungen beachten:
- Die Xevent-Aufrufliste enthält jetzt Modulnamen und Offsets anstelle von absoluten Adressen.
- Verbesserte Korrelation zwischen XE- und DMV-Diagnosen: Query_hash und query_plan_hash werden verwendet, um Abfragen eindeutig zu identifizieren. Sie werden von der DMV als varbinary(8) und von XEvent als UINT64 definiert. Da der SQL Server nicht über „unsignierten bigint“ verfügt, können Umwandlungen nicht immer erfolgreich vorgenommen werden. Mit dieser Verbesserung werden neue Aktions- bzw. Filterspalten für XEvent eingeführt, die query_hash und query_plan_hash weitestgehend entsprechen, es sei denn, sie werden als INT64 definiert. Mithilfe dieser Fehlerbehebung können Abfragen zwischen XE und DMV korreliert werden.
- Unterstützung für UTF-8 in BULK INSERT und BCP: Die Unterstützung für den Export und Import von Daten mit Codierung im UTF-8-Zeichensatz ist jetzt in BULK INSERT und BCP aktiviert.

### <a name="download-pages-and-more-information-for-sp2"></a>Downloadseiten und weitere Informationen zu SP2

- [Service Pack 2 für Microsoft SQL Server 2014 herunterladen](https://www.microsoft.com/download/details.aspx?id=53168)
- [SQL Server 2014 Service Pack 2 (SP1) ist jetzt verfügbar](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2012 SP2 Express](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164)
- [Berichts-Generator in SQL Server 2014 SP2](https://www.microsoft.com/download/details.aspx?id=53163)
- [SQL Server 2014 SP2 Reporting Services-Add-In für Microsoft Sharepoint](https://www.microsoft.com/download/details.aspx?id=53162)
- [SQL Server 2014 SP2 Semantic Language Statistics](https://www.microsoft.com/download/details.aspx?id=53165)
- [Releaseinformationen zu SQL Server 2014 Service Pack 2](https://support.microsoft.com/help/3171021/sql-server-2014-service-pack-2-release-information)

## <a name="sql-server-2014-service-pack-1-sp1"></a>SQL Server 2014 Service Pack 1 (SP1)

SQL Server 2014 SP1 enthält in SQL Server 2014 CU 1 bis einschließlich CU 5 bereitgestellte Fehlerbehebungen sowie ein Rollup mit Fehlerbehebungen, die in SQL Server 2012 SP2 bereits veröffentlicht wurden.

> [!NOTE]
> Wenn der SSISDB-Katalog auf Ihrer SQL Server-Instanz aktiviert ist und beim Durchführen eines Upgrades auf SP1 ein Fehler auftritt, sollten Sie die unter [Fehler 912 oder 3417 bei der Installation von SQL Server 2014 SP1](https://support.microsoft.com/help/3018269/error-912-or-3417-when-you-install-sql-server-2014-sp1-build-12-0-4050/) zu diesem Fehler beschriebenen Anweisungen befolgen.

### <a name="download-pages-and-more-information-for-sp1"></a>Downloadseiten und weitere Informationen zu SP1

- [Service Pack 1 für Microsoft SQL Server 2014 herunterladen](https://www.microsoft.com/download/details.aspx?id=46694)
- [SQL Server 2014 Service Pack 1 wurde freigegeben – aktualisiert](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2014-service-pack-1-has-released-updated/)
- [Microsoft SQL Server 2014 SP1 Express](https://www.microsoft.com/download/details.aspx?id=46697)
- [Microsoft SQL Server 2014 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=46696)


## <a name="before-you-install-sql-server-2014-rtm"></a>Vor der Installation von SQL Server 2014 RTM

### <a name="limitations-and-restrictions-in-sql-server-2014-rtm"></a>Einschränkungen in SQL Server 2014 RTM

1.  Upgrades von SQL Server 2014 CTP 1 auf SQL Server 2014 RTM werden NICHT unterstützt.  
2.  Die parallele Installation von SQL Server 2014 CTP 1 und SQL Server 2014 RTM wird NICHT unterstützt.  
3.  Das Anfügen einer SQL Server 2014 CTP 1-Datenbank an SQL Server 2014 RTM bzw. das Wiederherstellen einer solchen Datenbank in SQL Server 2014 RTM wird NICHT unterstützt.  

**Problemumgehung:** Keine

#### <a name="upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm"></a>Durchführen eines Upgrades von SQL Server 2014 CTP 2 auf SQL Server RTM
Das Upgrade wird vollständig unterstützt. Sie haben insbesondere folgende Möglichkeiten:

1.  Anfügen einer SQL Server 2014-CTP 2-Datenbank an eine Instanz von SQL Server 2014 RTM.    
2.  Wiederherstellen einer Datenbanksicherung, die unter SQL Server 2014 CTP 2 erstellt wurde, auf einer Instanz von SQL Server 2014 RTM.    
3.  Direktes Upgrade auf SQL Server 2014 RTM.
4.  Paralleles Upgrade auf SQL Server 2014 RTM. Bevor Sie das parallele Upgrade initiieren, müssen Sie in den manuellen Failovermodus wechseln. Ausführliche Informationen finden Sie unter [Upgraden und Update von Verfügbarkeitsgruppenservern bei minimaler Downtime und minimalem Datenverlust](http://msdn.microsoft.com/library/dn178483.aspx).    
5.  Daten, die durch die in SQL Server 2014 CTP 2 installierten Transaktionsleistungs-Sammlungssätze gesammelt werden, können von SQL Server Management Studio in SQL Server 2014 RTM nicht angezeigt werden und umgekehrt.
  
#### <a name="downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>Durchführen eines Downgrades von SQL Server 2014 RTM auf SQL Server 2014 CTP 2  
Diese Aktion wird nicht unterstützt.  
  
**Problemumgehung:** Es gibt keine Problemumgehung für das Downgrade. Es wird empfohlen, die Datenbank vor einem Upgrade auf SQL Server 2014 RTM zu sichern.  
  
#### <a name="incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>Falsche Version von StreamInsight Client bei SQL Server 2014-Medien/ISO/CAB  
Die falsche Version von StreamInsight.msi und StreamInsightClient.msi befindet sich unter folgendem Pfad auf SQL Server-Media/ISO/CAB (StreamInsight\\\<Architecture\>\\\<Language ID\>).  
  
**Problemumgehung:** Laden Sie die richtige Version von der [SQL Server 2014 Feature Pack-Downloadseite](http://go.microsoft.com/fwlink/?LinkID=306709)herunter, und installieren Sie sie.  
  
### <a name="ProdDoc"></a>Produktdokumentation (RTM)
  
Inhalte zum Berichts-Generator und PowerPivit sind nicht in allen Sprachen verfügbar. 

**Problem**: In den folgenden Sprachen sind keine Inhalte zum Berichts-Generator verfügbar:  
  
-   Griechisch (el-GR)  
-   Norwegisch (Bokmal) (nb-NO)  
-   Finnisch (fi-FI)  
-   Dänisch (da-DK)  
  
In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]waren die Inhalte in Form einer mit dem Produkt gelieferten CHM-Datei auch in diesen Sprachen verfügbar. Da die CHM-Dateien nicht mehr im Produktlieferumfang enthalten sind, stehen Inhalte zum Berichts-Generator nur auf MSDN zur Verfügung. Diese Sprachen werden von MSDN nicht unterstützt. Der Berichts-Generator wurde auch aus TechNet entfernt und ist in diesen unterstützten Sprachen nicht mehr verfügbar.  
  
**Problemumgehung:** Keine  
  
**Problem**: In den folgenden Sprachen sind keine Informationen zu Power Pivot verfügbar:
  
-   Griechisch (el-GR)  
-   Norwegisch (Bokmal) (nb-NO)  
-   Finnisch (fi-FI)  
-   Dänisch (da-DK)  
-   Tschechisch (cs-CZ)  
-   Ungarisch (hu-HU)  
-   Niederländisch (Niederlande) (nl-NL)  
-   Polnisch (pl-PL)  
-   Schwedisch (sv-SE)  
-   Türkisch (tr-TR)  
-   Portugiesisch (Portugal) (pt-PT)  
  
In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]waren diese Inhalte in TechNet in diesen Sprachen verfügbar. Die Inhalte wurden aus TechNet entfernt und sind in diesen unterstützten Sprachen nicht mehr verfügbar.  
  
**Problemumgehung:** Keine  
  
### <a name="DBEngine"></a>Datenbank-Engine (RTM)
  
#### <a name="changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>An der Standard Edition in SQL Server 2014 RTM vorgenommene Änderungen  
SQL Server 2014 Standard weist die folgenden Änderungen auf:  
  
-   Die Pufferpoolerweiterungsfunktion unterstützt die Verwendung einer maximalen Größe, die bis zu viermal so groß wie der konfigurierte Arbeitsspeicher sein kann.    
-   Der maximale Arbeitsspeicher wurde von 64 GB auf 128 GB erweitert.  
 
#### <a name="memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>Der Ratgeber für die Speicheroptimierung kennzeichnet Standardeinschränkungen als inkompatibel  
**Problem:** Der Ratgeber für die Speicheroptimierung in SQL Server Management Studio kennzeichnet alle Standardeinschränkungen als inkompatibel. In einer speicheroptimierten Tabelle werden nicht alle Standardeinschränkungen unterstützt. Der Ratgeber unterscheidet nicht zwischen unterstützten und nicht unterstützten Typen von Standardeinschränkungen. Zu den unterstützten Standardeinschränkungen gehören alle Konstanten, Ausdrücke und integrierten Funktionen, die innerhalb nativer kompilierter gespeicherter Prozeduren unterstützt werden. Die Liste der in systemintern kompilierten gespeicherten Prozeduren unterstützten Funktionen finden Sie unter [Unterstützte Konstrukte in systemintern kompilierten gespeicherten Prozeduren](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx).  
  
**Problemumgehung:** Wenn Sie den Ratgeber zum Identifizieren von Blockierungen verwenden möchten, sollten Sie die kompatiblen Standardeinschränkungen ignorieren. Um den Ratgeber für die Speicheroptimierung zum Migrieren von Tabellen zu verwenden, die über kompatible Standardeinschränkungen, aber keine anderen Blockierungen verfügen, führen Sie folgende Schritte aus:  
  
1.  Entfernen Sie die Standardeinschränkungen aus der Tabellendefinition.    
2.  Lassen Sie vom Ratgeber ein Migrationsskript für die Tabelle generieren.    
3.  Fügen Sie die Standardeinschränkungen wieder in das Migrationsskript ein.    
4.  Führen Sie das Migrationsskript aus.  
  
#### <a name="informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>Die Informationsmeldung „file access denied“ (Kein Zugriff auf Datei) wird im Fehlerprotokoll von SQL Server 2014 fälschlicherweise als Fehler gemeldet  
**Problem:** Beim Neustart eines Servers, der Datenbanken mit speicheroptimierten Tabellen enthält, kann im Fehlerprotokoll von SQL Server 2014 folgende Art von Fehlermeldungen angezeigt werden:  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
Diese Meldung dient tatsächlich nur zu Informationszwecken und erfordert keine Benutzeraktion.  
  
**Problemumgehung:** Keine Diese Meldung dient zu Informationszwecken.  
  
#### <a name="missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>In den Details zu fehlenden Indizes sind fälschlicherweise eingeschlossene Spalten für eine speicheroptimierte Tabelle angegeben.  
**Problem:** Wenn in SQL Server 2014 ein fehlender Index für eine Abfrage einer speicheroptimierten Tabelle erkannt wird, wird in SHOWPLAN_XML sowie in den DMVs zu fehlenden Indizes, z. B. sys.dm_db_missing_index_details, ein fehlender Index gemeldet. In einigen Fällen enthalten die Details zu fehlenden Indizes eingeschlossene Spalten. Da alle Spalten mit allen Indizes für speicheroptimierte Tabellen implizit eingeschlossen werden, ist es nicht zulässig, eingeschlossene Spalten mit speicheroptimierten Indizes explizit anzugeben.  
  
**Problemumgehung:** Geben Sie bei Indizes für speicheroptimierte Tabellen keine INCLUDE-Klausel an.  
  
#### <a name="missing-index-details-omit-missing-indexes-when-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>In den Details zu fehlenden Indizes werden fehlende Indizes ausgelassen, wenn ein Hashindex vorhanden ist, der für die Abfrage aber nicht geeignet ist.  
**Problem:** Wenn für Spalten einer speicheroptimierten Tabelle ein HASH-Index vorhanden ist, auf den in einer Abfrage verwiesen wird, der für die Abfrage jedoch nicht verwendet werden kann, wird von SQL Server 2014 in SHOWPLAN_XML und in der sys.dm_db_missing_index_details-DMV nicht immer ein fehlender Index gemeldet.  
  
Insbesondere, wenn eine Abfrage Gleichheitsprädikate enthält, die eine Teilmenge der Indexschlüsselspalten umfassen, oder wenn die Abfrage Ungleichheitsprädikate enthält, die die Indexschlüsselspalten umfassen, kann der HASH-Index in seiner ursprünglichen Form nicht verwendet werden. Um die Abfrage effizient auszuführen, wäre ein anderer Index erforderlich.  
  
**Problemumgehung:** Sofern Sie Hashindizes verwenden, sollten Sie die Abfragen und Abfragepläne daraufhin überprüfen, ob die Abfragen von Index Seek-Vorgängen für eine Teilmenge des Indexschlüssels oder für Ungleichheitsprädikate profitieren könnten. Wenn Sie eine Suche für eine Teilmenge des Indexschlüssels ausführen müssen, verwenden Sie einen NONCLUSTERED-Index. Alternativ verwenden Sie einen HASH-Index für exakt die Spalten, in denen gesucht werden soll. Wenn eine Suche für ein Ungleichheitsprädikat ausgeführt werden muss, verwenden Sie einen NONCLUSTERED-Index anstelle eines HASH-Indexes.  
  
#### <a name="failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>Bei Verwendung einer speicheroptimierten Tabelle und einer speicheroptimierten Tabellenvariablen in derselben Abfrage tritt ein Fehler auf, wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt ist.  
**Problem:** Wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt ist und Sie sowohl auf eine speicheroptimierte Tabelle als auch auf eine speicheroptimierte Tabellenvariable in derselben Anweisung außerhalb des Kontexts einer Benutzertransaktion zugreifen, kann folgende Fehlermeldung ausgegeben werden:  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**Problemumgehung:** Verwenden Sie entweder den WITH (SNAPSHOT)-Tabellenhinweis mit der Tabellenvariablen, oder legen Sie die Datenbankoption MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT auf ON fest. Verwenden Sie dazu folgende Anweisung:  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>In den Prozedur- und Abfrageausführungsstatistiken für nativ kompilierte gespeicherte Prozeduren wird die Workerzeit in Vielfachen von 1.000 aufgezeichnet.  
**Problem:** Nachdem Sie die Sammlung von Prozedur- oder Abfrageausführungsstatistiken für systemintern kompilierte gespeicherte Prozeduren unter Verwendung von sp_xtp_control_proc_exec_stats oder sp_xtp_control_query_exec_stats aktiviert haben, stellen Sie fest, dass *_worker_time in den DMVs sys.dm_exec_procedure_stats und sys.dm_exec_query_stats in Vielfachen von 1000 angegeben wird. Für Abfrageausführungen, die unter 500 Mikrosekunden liegen, wird unter worker_time der Wert 0 angegeben.  
  
**Problemumgehung:** Keine Bei Abfragen in systemintern kompilierten gespeicherten Prozeduren, die über eine kurze Ausführungsdauer verfügen, sollten Sie sich nicht auf den in den DMVs zu Ausführungsstatistiken angegebenen worker_time-Wert verlassen.  
  
#### <a name="error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>SHOWPLAN_XML-Fehler bei nativ kompilierten gespeicherten Prozeduren mit langen Ausdrücken  
**Problem:** Wenn eine systemintern kompilierte gespeicherte Prozedur einen langen Ausdruck enthält und Sie die SHOWPLAN_XML für die Prozedur entweder mit der T-SQL-Option SET SHOWPLAN_XML ON oder mit der Option „Geschätzten Ausführungsplan anzeigen“ in Management Studio abrufen, kann folgender Fehler auftreten:  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**Problemumgehung:** Es werden zwei Problemumgehungen empfohlen:  
  
1.  Fügen Sie dem Ausdruck Klammern hinzu, wie im folgenden Beispiel veranschaulicht:  
  
    Verwenden Sie anstelle von  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    beispielsweise  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  Erstellen Sie eine zweite Prozedur mit einem leicht vereinfachten Ausdruck. Für den Showplan sollte die allgemeine Form des Plans identisch sein. Verwenden Sie anstelle von  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    beispielsweise  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>Die Verwendung eines Zeichenfolgenparameters oder einer Variablen mit DATEPART und zugehörigen Funktionen in einer nativ kompilierten gespeicherten Prozedur führt zu einem Fehler.  
**Problem:** Wenn Sie eine nativ kompilierte gespeicherte Prozedur verwenden, die einen Zeichenfolgenparameter oder eine -variable mit den integrierten Funktionen DATEPART, DAY, MONTH und YEAR verwendet, wird eine Fehlermeldung mit dem Hinweis angezeigt, dass der Datentyp „datetimeoffset“ bei nativ kompilierten gespeicherten Prozeduren nicht unterstützt wird.  
  
**Problemumgehung:** Weisen Sie den Zeichenfolgenparameter oder die Variable einer neuen Variablen des datetime2-Typs zu, und verwenden Sie diese Variable in der Funktion DATEPART, DAY, MONTH oder YEAR. Zum Beispiel:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>DELETE FROM-Klauseln werden vom Ratgeber für native Kompilierung falsch gekennzeichnet.  
**Problem:** DELETE FROM-Klauseln innerhalb einer gespeicherten Prozedur werden vom Ratgeber für systeminterne Kompilierung fälschlicherweise als inkompatibel gekennzeichnet.  
  
**Problemumgehung:** Keine  
  
#### <a name="register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>Bei der Registrierung über SSMS werden DAC-Metadaten mit nicht übereinstimmenden Instanz-IDs hinzugefügt.  
**Problem:** Beim Registrieren oder Löschen eines Datenschichtanwendungspakets (DACPAC) über SQL Server Management Studio werden die sysdac*-Tabellen nicht ordnungsgemäß aktualisiert, um einem Benutzer das Abfragen des DACPAC-Verlaufs für die Datenbank zu ermöglichen.  Die „instance_id“ für „sysdac_history_internal“ und „sysdac_instances_internal“ stimmen nicht überein und ermöglichen keinen JOIN-Vorgang.  
  
**Problemumgehung:** Dieses Problem wird mit der Feature Pack-Umverteilung des [Data-Tier Application Framework](https://www.microsoft.com/download/details.aspx?id=42295)behoben.  Nach dem Anwenden des Updates verwenden alle neuen Verlaufseinträge den in der Tabelle „sysdac_instances_internal“ für „instance_id“ aufgelisteten Wert.  
  
Wenn das Problem mit nicht übereinstimmenden instance_id-Werten bei Ihnen bereits besteht, ist die einzige Möglichkeit zum Korrigieren der nicht übereinstimmenden Werte, als Benutzer mit Schreibberechtigungen eine Verbindung zur MSDB-Datenbank herzustellen und die instance_id-Werte so zu aktualisieren, dass sie übereinstimmen.  Wenn mehrere Registrierungs- und Deregistrierungsereignisse der gleichen Datenbank aufgetreten sind, müssen Sie möglicherweise die Uhrzeit bzw. das Datum überprüfen, um festzustellen, welche Datensätze mit dem aktuellen instance_id-Wert übereinstimmen.  
  
1.  Stellen Sie in SQL Server Management Studio unter Verwendung einer Anmeldung, die über Updateberechtigungen für MSDB verfügt, eine Verbindung mit dem Server her.    
2.  Öffnen Sie eine neue Abfrage unter Verwendung der MSDB-Datenbank.    
3.  Führen Sie diese Abfrage aus, um alle Ihre aktiven DAC-Instanzen anzuzeigen.  Suchen Sie die zu berichtigende Instanz, und notieren Sie die „instance_id“:  
  
    `select * from` sysdac_instances_internal  
  
4.  Führen Sie die folgende Abfrage aus, um alle Verlaufseinträge anzuzeigen:  
  
    `select * from` sysdac_history_internal  
  
5.  Identifizieren Sie die Zeilen, die der korrigierten Instanz entsprechen sollten. 
6.  Aktualisieren Sie den sysdac_history_internal.instance_id-Wert auf den in Schritt 3 notierten Wert (aus der sysdac_instances_internal-Tabelle):  
  
    `update` sysdac_history_internal `set` instance_id = '\<Wert aus Schritt 3\>' `where` \<Ausdruck, der den zu aktualisierenden Zeilen entspricht\>  
  
### <a name="SSRS"></a>Reporting Services (RTM)
  
#### <a name="the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>Der SQL Server 2012 Reporting Services-Berichtsserver im einheitlichen Modus kann nicht parallel mit SharePoint-Komponenten von SQL Server 2014 Reporting Services ausgeführt werden  
**Problem:** Der Windows-Dienst [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im einheitlichen Modus „SQL Server Reporting Services“ (ReportingServicesService.exe) kann nicht gestartet werden, wenn auf demselben Server SharePoint-Komponenten von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] installiert sind.  
  
**Problemumgehung:** Deinstallieren Sie SharePoint-Komponenten von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , und starten Sie den Windows-Dienst "Microsoft SQL Server 2012 Reporting Services" neu.  
  
**Weitere Informationen**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Der einheitliche Modus kann unter einer der folgenden Bedingungen nicht parallel ausgeführt werden:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte    
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Gemeinsamer SharePoint-Dienst  
  
Die parallele Installation verhindert, dass der Windows-Dienst [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (einheitlicher Modus) gestartet wird. Im Windows-Ereignisprotokoll werden Fehlermeldungen wie die Folgenden angezeigt:  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
Weitere Informationen finden Sie unter [Tipps &amp; Tricks und Problembehandlung für SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
#### <a name="required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>Für das Upgrade einer SharePoint-Farm mit mehreren Knoten auf SQL Server 2014 Reporting Services ist eine bestimmte Reihenfolge erforderlich.  
**Problem:** Das Rendern von Berichten in einer Farm mit mehreren Knoten schlägt fehl, wenn Instanzen des gemeinsamen SharePoint-Diensts für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] vor allen Instanzen des [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-Ins für SharePoint-Produkte aktualisiert werden.  
  
**Problemumgehung:** In einer SharePoint-Farm mit mehreren Knoten:  
  
1.  Aktualisieren Sie zuerst alle Instanzen des [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-Ins für SharePoint-Produkte.    
2.  Aktualisieren Sie dann alle Instanzen des gemeinsamen SharePoint-Diensts für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
Weitere Informationen finden Sie unter [Tipps, Tricks und Problembehandlung für SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
### <a name="AzureVM"></a>SQL Server 2014 RTM auf Microsoft Azure Virtual Machines  
  
#### <a name="the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>Der Assistent zum Hinzufügen von Azure-Replikaten gibt beim Konfigurieren eines Verfügbarkeitsgruppenlisteners in Windows Azure einen Fehler zurück.  
**Problem:** Wenn eine Verfügbarkeitsgruppe über einen Listener verfügt, gibt der Assistent zum Hinzufügen von Azure-Replikaten beim Versuch, den Listener in Windows Azure zu konfigurieren, einen Fehler zurück.  
  
Grund für dieses Problem ist, dass Verfügbarkeitsgruppenlistenern in jedem Subnetz, das Verfügbarkeitsgruppenreplikate hostet, eine IP-Adresse zugewiesen werden muss. Dies gilt auch für das Azure-Subnetz.  
  
**Problemumgehung:**  
  
1.  Weisen Sie dem Verfügbarkeitsgruppenlistener auf der Seite Listener eine freie statische IP-Adresse im Azure-Subnetz zu, das das Verfügbarkeitsgruppenreplikat hostet.  
  
    Durch diese Problemumgehung kann der Assistent das Replikat in Windows Azure endgültig hinzufügen.  
  
2.  Nachdem der Assistent beendet ist, müssen Sie die Konfiguration des Listeners in Windows Azure, wie in [Listener-Konfiguration für AlwaysOn-Verfügbarkeitsgruppen in Windows Azure](http://msdn.microsoft.com/library/dn376546.aspx)beschrieben, abschließen.  
  
### <a name="SSAS"></a>Analysis Services (RTM)
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>Für eine neue SharePoint 2010-Farm, die mit SQL Server 2014 konfiguriert ist, muss MSOLAP.5 heruntergeladen, installiert und registriert werden.  
**Problem:**  
  
-   Bei einer SharePoint 2010-Farm, bei der MSOLAP.5 für eine neue SharePoint 2013-Farm heruntergeladen, installiert und registriert werden muss, die mit einer mit der SQL Server 2014 RTM-Bereitstellung konfigurierten SQL Server 2014-Farm konfiguriert ist, können PowerPivot-Arbeitsmappen keine Verbindung mit Datenmodellen herstellen, da der Anbieter, auf den in der Verbindungszeichenfolge verwiesen wird, nicht installiert ist.  
  
**Problemumgehung:**  
  
1.  Laden Sie den MSOLAP.5-Anbieter aus dem [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack herunter. Installieren Sie den Anbieter auf den Anwendungsservern, auf denen Excel Services ausgeführt wird. Weitere Informationen finden Sie im Abschnitt "Microsoft Analysis Services OLE DB Provider für Microsoft SQL Server 2012 SP1" im [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registrieren Sie MSOLAP.5 als vertrauenswürdigen Anbieter bei SharePoint Excel Services. Weitere Informationen finden Sie unter [Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Weitere Informationen**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] enthält MSOLAP.6. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] - und [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappen verwenden MSOLAP.&5;. Wenn MSOLAP.5 auf dem Computer, auf dem Excel Services ausgeführt werden, nicht installiert ist, können die Datenmodelle von Excel Services nicht geladen werden.  
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>Für eine neue SharePoint 2013-Farm, die mit SQL Server 2014 konfiguriert ist, muss MSOLAP.5 heruntergeladen, installiert und registriert werden.  
**Problem:**  
  
-   Bei einer SharePoint 2013-Farm, die mit einer [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] -Bereitstellung konfiguriert ist, können Excel-Arbeitsmappen, die auf den MSOLAP.5-Anbieter verweisen, keine Verbindung mit tabellarischen Datenmodellen herstellen, da der Anbieter, auf den in der Verbindungszeichenfolge verwiesen wird, nicht installiert ist.  
  
**Problemumgehung:**  
  
1.  Laden Sie den MSOLAP.5-Anbieter aus dem [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack herunter. Installieren Sie den Anbieter auf den Anwendungsservern, auf denen Excel Services ausgeführt wird. Weitere Informationen finden Sie im Abschnitt "Microsoft Analysis Services OLE DB Provider für Microsoft SQL Server 2012 SP1" im [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registrieren Sie MSOLAP.5 als vertrauenswürdigen Anbieter bei SharePoint Excel Services. Weitere Informationen finden Sie unter [Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Weitere Informationen**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] enthält MSOLAP.6. PowerPivot-Arbeitsmappen aus SQL Server 2014 verwenden jedoch MSOLAP.5. Wenn MSOLAP.5 auf dem Computer, auf dem Excel Services ausgeführt werden, nicht installiert ist, können die Datenmodelle von Excel Services nicht geladen werden.  
  
#### <a name="corrupt-data-refresh-schedules-rtm"></a>Beschädigte Zeitpläne zur Datenaktualisierung (RTM)
**Problem:**  
  
-   Sie aktualisieren einen Aktualisierungszeitplan, und der Zeitplan wird beschädigt und unbrauchbar.  
  
**Problemumgehung:**  
  
1.  Deaktivieren Sie in Microsoft Excel die benutzerdefinierten erweiterten Eigenschaften. Weitere Informationen finden Sie im Abschnitt „Problemumgehung“ des folgenden Knowledge Base-Artikels: [KB 2927748](http://support.microsoft.com/kb/2927748).  
  
**Weitere Informationen**  
  
-    Wenn Sie einen Zeitplan zur Datenaktualisierung für eine Arbeitsmappe aktualisieren und die serialisierte Länge des Aktualisierungszeitplans geringer als der ursprüngliche Zeitplan ist, wird die Puffergröße nicht ordnungsgemäß aktualisiert, und die neuen Zeitplaninformationen werden mit den alten Zeitplaninformationen zusammengeführt, wodurch der Zeitplan beschädigt wird.  
  
### <a name="DQS"></a>Data Quality Services (RTM)
  
#### <a name="no-cross-version-support-for-data-quality-services-in-master-data-services"></a>Data Quality Services werden in Master Data Services nicht versionsübergreifend unterstützt.  
**Problem:** Die folgenden Szenarien werden nicht unterstützt:  
  
-   Master Data Services 2014, gehostet in einer Datenbank des SQL Server-Datenbankmoduls in SQL Server 2012 mit installierten Data Quality Services 2012  
  
-   Master Data Services 2012, gehostet in einer Datenbank des SQL Server-Datenbankmoduls in SQL Server 2014 mit installierten Data Quality Services 2014.  
  
**Problemumgehung:** Master Data Services, die Datenbank des Datenbankmoduls und Data Quality Services müssen dieselbe Version aufweisen.  
  
### <a name="UA"></a>Probleme bei Upgrade Advisor (RTM)
  
#### <a name="sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>SQL Server 2014 Upgrade Advisor meldet irrelevante Upgradeprobleme für SQL Server Reporting Services.  
**Problem:** Der im Lieferumfang von SQL Server 2014 enthaltene SQL Server Upgrade Advisor (SSUA) meldet bei der Analyse eines SQL Server Reporting Services-Servers fälschlicherweise mehrere Fehler.  
  
**Problemumgehung:** Dieses Problem wurde im SQL Server Upgrade Advisor, der im [SQL Server 2014 Feature Pack für SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)verfügbar ist, behoben.  
  
#### <a name="sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>SQL Server 2014 Upgrade Advisor meldet bei der Analyse eines SQL Server Integration Services-Servers einen Fehler.  
**Problem:** Der mit den SQL Server 2014-Medien ausgelieferte SQL Server Upgrade Advisor (SSUA) meldet einen Fehler beim Analysieren eines SQL Server Integration Services-Servers.  Fehler, der dem Benutzer angezeigt wird:  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**Problemumgehung:** Dieses Problem wurde im SQL Server Upgrade Advisor, der im [SQL Server 2014 Feature Pack für SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)verfügbar ist, behoben.  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]