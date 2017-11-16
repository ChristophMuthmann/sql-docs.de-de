---
title: Columnstore-Indizes - Neuigkeiten | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe5ea05-5b19-45a4-9b7a-8ae5ca367897
caps.latest.revision: 28
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 47b0c3fc8aba635dcfd573536b770f13a40956fa
ms.openlocfilehash: 0a63e3e5641ce513e0d3c30705ac8a7523cbc053
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="columnstore-indexes---what39s-new"></a>Columnstore-Indizes - Neuigkeiten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Zusammenfassung der für die einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen und für die neueste Version der Azure SQL-Datenbank Premium Edition, Azure SQL Data Warehouse und Parallel Data Warehouse verfügbaren Columnstore-Funktionen.  

 >[!NOTE]
 > Für Azure SQL-Datenbank sind Columnstore-Indizes nur in der Premium Edition verfügbar.
 
## <a name="feature-summary-for-product-releases"></a>Zusammenfassung der Funktionen für Produktversionen  
 In dieser Tabelle sind die wichtigsten Funktionen für Columnstore-Indizes sowie die Produkte zusammengefasst, in denen sie verfügbar sind.  

  
|Columnstore-Index-Funktion|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|---|  
|Batchausführung für Multithread-Abfragen|Ja|Ja|Ja|Ja|Ja|Ja| 
|Batchausführung für Singlethread-Abfragen|||Ja|Ja|Ja|Ja|  
|Archivierungskomprimierungsoption||Ja|Ja|Ja|Ja|Ja|  
|Momentaufnahmeisolation und Read Commited-Momentaufnahmeisolation|||Ja|Ja|Ja|Ja| 
|Geben Sie den Columnstore-Index bei der Erstellung einer Tabelle an.|||Ja|Ja|Ja|Ja|  
|AlwaysOn unterstützt Columnstore-Indizes.|Ja|Ja|Ja|Ja|Ja|Ja| 
|Lesbare sekundäre AlwaysOn-Datenbanken unterstützt schreibgeschützten nicht gruppierten Columnstore-Index.|Ja|Ja|Ja|Ja|Ja|Ja|  
|Lesbare sekundäre AlwaysOn-Datenbanken unterstützt aktualisierbare Columnstore-Indizes.|||Ja|Ja|||  
|Schreibgeschützter nicht gruppierter Columnstore-Index auf Heap- oder B-Struktur|Ja|Ja|Ja*|Ja*|Ja*|Ja*|  
|Aktualisierbarer nicht gruppierter Columnstore-Index auf Heap- oder B-Struktur|||Ja|Ja|Ja|Ja|  
|Zusätzliche B-Struktur-Indizes für eine Heap- oder B-Struktur mit einem nicht gruppierten Columnstore-Index zulässig|Ja|Ja|Ja|Ja|Ja|Ja|  
|Aktualisierbarer gruppierter Columnstore-Index||Ja|Ja|Ja|Ja|Ja|  
|B-Struktur-Index in einem gruppierten Columnstore-Index|||Ja|Ja|Ja|Ja|  
|Columnstore-Index für eine speicheroptimierte Tabelle|||Ja|Ja|Ja|Ja|  
|Definition von nicht gruppiertem Columnstore-Index unterstützt eine gefilterte Bedingung|||Ja|Ja|Ja|Ja|  
|Komprimierungsverzögerungsoption für Columnstore-Indizes in CREATE TABLE und ALTER TABLE.|||Ja|Ja|Ja|Ja|
|Der Columnstore-Index kann über eine nicht permanent berechnete Spalte verfügen.||||Ja|||   
  
 *Um einen lesbaren nicht gruppierten Columnstore-Index zu erstellen, speichern Sie den Index in einer schreibgeschützten Dateigruppe.  

## [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 
 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] fügt diese neuen Funktionen hinzu.

### <a name="functional"></a>Funktionell
- [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] unterstützt nicht permanent berechnete Spalten in gruppierten Columnstore-Indexen. Persistent berechnete Spalten werden in gruppierten Indexen nicht unterstützt. Sie können einen nicht gruppierten Index auf einem Columnstore-Index erstellen, der über berechnete Spalten verfügt. 

## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] fügt wichtige Verbesserungen hinzu, um die Leistung und Flexibilität von Columnstore-Indizes zu erhöhen. Dies verbessert die Data Warehouse-Szenarios und ermöglicht operative Echtzeitanalysen.  
  
### <a name="functional"></a>Funktionell  
  
-   Eine Rowstore-Tabelle kann über einen aktualisierbaren nicht gruppierten Columnstore-Index verfügen. Bisher war der nicht gruppierte Columnstore-Index schreibgeschützt.  
  
-   Die Definition des nicht gruppierten Columnstore-Index unterstützt gefilterte Bedingungen. Um die Auswirkung auf die Leistung beim Hinzufügen eines Columnstore-Indexes in eine OLTP-Tabelle zu verringern, verwenden Sie eine gefilterte Bedingung, um einen nicht gruppierten Columnstore-Index anhand der kalten Daten Ihrer Betriebsworkload zu erstellen. 
  
-   Eine In-Memory-Tabelle kann nur über einen Columnstore-Index verfügen. Sie können ihn bei Erstellung der Tabelle generieren oder später mit [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) hinzufügen. Früher konnte nur eine datenträgerbasierte Tabelle über einen Columnstore-Index verfügen.  
  
-   Ein gruppierter Columnstore-Index kann über eine oder mehrere nicht gruppierte Rowstore-Indizes verfügen. Früher hat der Columnstore-Index keine nicht gruppierten Indizes unterstützt. SQL Server verwaltet die nicht gruppierten Indizes für DML-Vorgänge automatisch.  
  
-   Unterstützung für Primär- und Fremdschlüssel unter Verwendung eines B-Struktur-Index zum Erzwingen dieser Einschränkungen für einen gruppierten Columnstore-Index.  
  
-   Columnstore-Indizes können über eine Komprimierungsverzögerungsoption verfügen, die die Auswirkungen minimiert, die die Transaktionsarbeitsauslastung auf betriebliche Echtzeitanalysen hat.  Mit dieser Option können häufig geänderte Zeilen vor der Komprimierung in den Columnstore stabilisiert werden. Weitere Informationen finden Sie unter [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) und [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>Leistung für Datenbankkompatibilitätsgrad 120 oder 130  
  
-   Columnstore-Indizes unterstützen die RCSI-Stufe (Read Committed Snapshot Isolation) sowie die Momentaufnahmeisolation (Snapshot Isolation, SI). Dies ermöglicht transaktionale konsistente Analyseabfragen ohne Sperren.  
  
-   Columnstore unterstützt Indexdefragmentierung durch Entfernen von gelöschten Zeilen, ohne dass der Index explizit neu erstellt werden muss. Mit der Anweisung ALTER INDEX … Mit der REORGANIZE-Anweisung werden gelöschte Zeilen basierend auf einer intern definierten Richtlinie in Form eines Onlinevorgangs aus dem Columnstore entfernt.  
  
-   Columnstore-Indizes können Zugriff auf ein lesbares sekundäres AlwaysOn-Replikat haben. Sie können die Leistung von Betriebsanalysen verbessern, indem Sie die Analyseabfragen in ein sekundäres AlwaysOn-Replikat auslagern.  
  
-   Zur Verbesserung der Leistung berechnet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Aggregatfunktionen MIN, MAX, SUM, COUNT, AVG bei Tabellenscans, wenn der Datentyp nicht mehr als 8 Datenbytes enthält und keine Zeichenfolgen ist. Die Aggregatweitergabe mit oder ohne Group By-Klausel wird für gruppierte und nicht gruppierte Columnstore-Indizes unterstützt.  
  
-   Die Prädikatweitergabe beschleunigt Abfragen, die Zeichenfolgen vom Typ „[v]char“ oder „n[v]char“ vergleichen. Dies gilt für die allgemeinen Vergleichsoperatoren und schließt Operatoren wie LIKE ein, die Bitmapfilter verwenden. Dies funktioniert bei allen Sortierungen, die von SQL Server unterstützt werden.  
  
### <a name="performance-for-database-compatibility-level-130"></a>Leistung für Datenbankkompatibilitätsgrad 130  
  
-   Unterstützung der neuen Batchmodusausführung für Abfragen, die diese Vorgänge verwenden:  
  
    -   SORT  
  
    -   Aggregate mit mehrere verschiedenen Funktionen. Einige Beispiele: COUNT/COUNT, AVG/SUM, CHECKSUM_AGG, STDEV/STDEVP.  
  
    -   Fensteraggregatfunktionen: COUNT, COUNT_BIG, SUM, AVG, MIN, MAX und CLR.  
  
    -   Benutzerdefinierte Fensteraggregatfunktionen: CHECKSUM_AGG, STDEV, STDEVP, VAR, VARP und GROUPING.  
  
    -   Fensteraggregat-Analysefunktionen: LAG< LEAD, FIRST_VALUE, LAST_VALUE, PERCENTILE_CONT, PERCENTILE_DISC, CUME_DIST und PERCENT_RANK.  
  
-   Singlethread-Abfragen unter MAXDOP 1 oder mit der seriellen Abfrageplanausführung im Batchmodus. Früher konnten nur Multithread-Abfragen im Batchmodus ausgeführt werden.  
  
-   Speicheroptimierte Tabellenabfragen können sowohl beim Zugriff auf Daten im Rowstore- als auch beim Zugriff auf Daten im Columnstore-Index parallele Pläne im SQL InterOp-Modus verwenden.  
  
### <a name="supportability"></a>Unterstützbarkeit  
 Diese Systemsichten sind für Columnstore neu:  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
 In-Memory-OLTP-basierte DMVs enthalten Updates für den Columnstore:  
  
-   [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)  
  
-   [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)  
  
-   [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)  
  
### <a name="limitations"></a>Einschränkungen  
  
-   MERGE wird deaktiviert, wenn ein B-Struktur-Index für einen gruppierten Columnstore-Index definiert wird.  
  
-   Für In-Memory-Tabellen muss ein Columnstore-Index alle Spalten enthalten. Der Columnstore-Index kann keine gefilterte Bedingung haben.  
  
-   Für In-Memory-Tabellen können Abfragen für Columnstore-Indizes nur im InterOP-Modus und nicht im einheitlichen In-Memory-Modus ausgeführt werden. Parallele Ausführung wird unterstützt.  
  
## <a name="sql-server-2014"></a>SQL Server 2014  
 In SQL Server 2014 wurde der gruppierten Columnstore-Index als primäres Speicherformat eingeführt. Dieser ermöglichte reguläre Ladevorgänge sowie Aktualisierungs-, Lösch- und Einfügevorgänge.  
  
-   Die Tabelle kann einen gruppierten Columnstore-Index als primären Tabellenspeicher verwenden. Für die Tabelle sind keine anderen Indizes zulässig, aber der gruppierte Columnstore-Index ist aktualisierbar, sodass Sie reguläre Ladevorgänge ausführen und Änderungen an einzelnen Zeilen vornehmen können.  
  
-   Der nicht gruppierte Columnstore-Index weist weiterhin die gleiche Funktionalität wie in SQL Server 2012 auf, ermöglicht jedoch jetzt die Ausführung zusätzlicher Operatoren im Batchmodus. Er ist weiterhin nur durch erneutes Erstellen und mithilfe eines Partitionswechsels aktualisierbar. Der nicht gruppierte Columnstore-Index wird nur in datenträgerbasierten Tabellen und nicht in In-Memory-Tabellen unterstützt.  
  
-   Sowohl der gruppierte als auch der nicht gruppierte Columnstore-Index verfügt über eine Archivierungskomprimierungsoption, die die Daten weiter komprimiert. Die Archivierungsoption eignet sich zur Verringerung der Datengröße sowohl im Arbeitsspeicher als auch auf dem Datenträger, verlangsamt jedoch die Leistung der Abfrage. Dies funktioniert gut für Daten, auf die nur selten zugegriffen wird.  
  
-   Der gruppierte und der nicht gruppierte Columnstore-Index funktionieren auf sehr ähnliche Weise. Sie verwenden das gleiche Format für spaltenweise Speicherung, dasselbe Abfrageverarbeitungsmodul und den gleichen Satz von dynamischen Verwaltungssichten. Der Unterschied besteht in den primären bzw. sekundären Indextypen, und darin, dass der nicht gruppierte Columnstore-Index schreibgeschützt ist.  
  
-   Diese Operatoren werden für Multithread-Abfragen im Batchmodus ausgeführt: SCAN, FILTER, PROJECT, JOIN, GROUP BY und UNION ALL.  
  
## <a name="sql-server-2012"></a>SQL Server 2012  
 In SQL Server 2012 wurden der nicht gruppierte Columnstore-Index als weiterer Indextyp für Rowstore-Tabellen sowie die Batchverarbeitung für Abfragen für Columnstore-Daten eingeführt.  
  
-   Eine Rowstore-Tabelle kann über einen nicht gruppierten Columnstore-Index verfügen.  
  
-   Der Columnstore-Index ist schreibgeschützt. Nachdem Sie den Columnstore-Index erstellt haben, können Sie die Tabelle nicht mehr mit Einfüge-, Lösch- und Aktualisierungsvorgängen aktualisieren. Um diese Vorgänge auszuführen, müssen Sie den Index löschen,die Tabelle aktualisieren und den Columnstore-Index neu erstellen. Sie können zusätzliche Daten mithilfe von Partitionswechseln in die Tabelle laden. Der Vorteil der Partitionswechsel besteht darin, dass Sie Daten laden können, ohne den Columnstore-Index löschen und neu erstellen zu müssen.  
  
-   Der Columnstore-Index erfordert stets zusätzlichen Speicherplatz (in der Regel zusätzliche 10 % gegenüber Rowstore), da eine Kopie der Daten gespeichert wird.  
  
-   Die Batchverarbeitung bietet eine mindestens doppelt so gute Leistung, ist aber nur für die parallele Abfrageausführung verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 Beschreibung von Columnstore-Indizes   
 Laden von Daten für Columnstore-Indizes   
 [Abfrageleistung für Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 Columnstore-Indizes für Data Warehousing   
 [Columnstore-Index-Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  

