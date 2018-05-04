---
title: Sys. dm_db_index_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_index_operational_stats
- sys.dm_db_index_operational_stats_TSQL
- sys.dm_db_index_operational_stats
- dm_db_index_operational_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_operational_stats dynamic management function
ms.assetid: 13adf2e5-2150-40a6-b346-e74a33ce29c6
caps.latest.revision: 61
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e8c15d69316eeabb366dbab9759fec66253efe25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbindexoperationalstats-transact-sql"></a>sys.dm_db_index_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Gibt aktuelle E/A-Aktivitäten auf niedriger Ebene sowie Aktivitäten im Zusammenhang mit Sperren, Latches und Zugriffsmethoden für alle Partitionen einer Tabelle oder eines Indexes in der Datenbank zurück.    
    
 Speicheroptimierte Indizes werden in dieser DMV nicht angezeigt.    
    
> [!NOTE]    
>  **Sys. dm_db_index_operational_stats** gibt keine Informationen zu speicheroptimierten Indizes zurück. Informationen zur Verwendung von speicheroptimierten Indizes finden Sie unter [dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).    
        
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
sys.dm_db_index_operational_stats (    
    { database_id | NULL | 0 | DEFAULT }    
  , { object_id | NULL | 0 | DEFAULT }    
  , { index_id | 0 | NULL | -1 | DEFAULT }    
  , { partition_number | NULL | 0 | DEFAULT }    
)    
```    
    
## <a name="arguments"></a>Argumente    
 *Database_id* | NULL | 0 | STANDARDWERT    
 Die ID der Datenbank. *Database_id* ist **"smallint"**. Gültige Eingaben sind die ID einer Datenbank, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig.    
    
 Geben Sie NULL an, wenn Informationen zu allen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgegeben werden sollen. Bei Angabe von NULL für *Database_id*, müssen Sie auch angeben, NULL für *Object_id*, *Index_id*, und *Partition_number*.    
    
 Die integrierte Funktion [DB_ID](../../t-sql/functions/db-id-transact-sql.md) kann angegeben werden.    
    
 *Object_id* | NULL | 0 | STANDARDWERT    
 Die Objekt-ID der Tabelle oder Sicht mit dem Index. *object_id* ist **int**.    
    
 Gültige Eingaben sind die ID einer Tabelle und Sicht, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig.    
    
 Geben Sie NULL an, wenn zwischengespeicherte Informationen zu allen Tabellen und Sichten in der angegebenen Datenbank zurückgegeben werden sollen. Bei Angabe von NULL für *Object_id*, müssen Sie auch angeben, NULL für *Index_id* und *Partition_number*.    
    
 *Index_id* | 0 | NULL | -1 | STANDARDWERT    
 Die ID des Index. *Index_id* ist **Int**. Gültige Eingaben sind die ID-Nummer eines Indexes, 0, wenn *Object_id* ist ein Heap ist, NULL,-1 oder DEFAULT. Der Standardwert ist -1. NULL, -1 und DEFAULT sind in diesem Kontext gleichwertig.    
    
 Geben Sie NULL an, wenn zwischengespeicherte Informationen zu allen Indizes für eine Basistabelle oder Sicht zurückgegeben werden sollen. Bei Angabe von NULL für *Index_id*, müssen Sie auch angeben, NULL für *Partition_number*.    
    
 *Partitionsnummer* | NULL | 0 | STANDARDWERT    
 Partitionsnummer im Objekt. *Partitionsnummer* ist **Int**. Gültige Eingaben sind die *Partion_number* eines Indexes oder Heaps, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig.    
    
 Geben Sie NULL an, um zwischengespeicherte Informationen für alle Partitionen des Indexes oder Heaps zurückzugeben.    
    
 *Partitionsnummer* ist 1-basiert. Ein nicht partitionierter Index oder Heap ist *Partition_number* auf 1 festgelegt.    
    
## <a name="table-returned"></a>Zurückgegebene Tabelle    
    
|Spaltenname|Datentyp|Description|    
|-----------------|---------------|-----------------|    
|**database_id**|**smallint**|Datenbank-ID|    
|**object_id**|**int**|ID der Tabelle oder Sicht.|    
|**index_id**|**int**|ID des Indexes oder Heaps.<br /><br /> 0 = Heap|    
|**hobt_id**|**bigint**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Die ID des datenheaps oder der B-Struktur-Rowset, das die internen Daten für einen columnstore-Index nachverfolgt.<br /><br /> NULL: Dies ist kein interner columnstore-Rowset.<br /><br /> Weitere Informationen finden Sie unter [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|    
|**partition_number**|**int**|Auf 1 basierende Partitionsnummer im Index oder Heap.|    
|**leaf_insert_count**|**bigint**|Gesamtzahl der Einfügevorgänge auf Blattebene.|    
|**leaf_delete_count**|**bigint**|Gesamtzahl der Löschvorgänge auf Blattebene. Leaf_delete_count wird nur für gelöschte Datensätze erhöht, die nicht als inaktive zuerst markiert sind. Für gelöschte Datensätze, die zuerst blasse Darstellung werden **Leaf_ghost_count** wird stattdessen erhöht.|    
|**leaf_update_count**|**bigint**|Gesamtzahl der Updates auf Blattebene.|    
|**leaf_ghost_count**|**bigint**|Gesamtzahl der Zeilen auf Blattebene, die als gelöscht markiert sind, jedoch noch nicht entfernt wurden. Diese Anzahl schließt keine Datensätze ein, die sofort gelöscht werden, ohne dass Sie als inaktive markiert. Diese Zeilen werden durch einen Cleanupthread in bestimmten Intervallen entfernt. In diesem Wert sind keine Zeilen enthalten, die aufgrund einer ausstehenden Momentaufnahmeisolationstransaktion beibehalten werden.|    
|**nonleaf_insert_count**|**bigint**|Gesamtzahl der Einfügevorgänge über der Blattebene.<br /><br /> 0 = Heap oder columnstore|    
|**nonleaf_delete_count**|**bigint**|Gesamtzahl der Löschvorgänge über der Blattebene.<br /><br /> 0 = Heap oder columnstore|    
|**nonleaf_update_count**|**bigint**|Gesamtzahl der Updates über der Blattebene.<br /><br /> 0 = Heap oder columnstore|    
|**leaf_allocation_count**|**bigint**|Gesamtzahl der Seitenzuordnungen auf Blattebene im Index oder Heap.<br /><br /> Bei einem Index entspricht eine Seitenzuordnung einer Seitenteilung.|    
|**nonleaf_allocation_count**|**bigint**|Gesamtzahl der durch Seitenteilungen über der Blattebene verursachten Seitenzuordnungen.<br /><br /> 0 = Heap oder columnstore|    
|**leaf_page_merge_count**|**bigint**|Gesamtzahl der Seitenzusammenführungen auf der Blattebene. Immer 0 für den columnstore-Index.|    
|**nonleaf_page_merge_count**|**bigint**|Gesamtzahl der Seitenzusammenführungen über der Blattebene.<br /><br /> 0 = Heap oder columnstore|    
|**range_scan_count**|**bigint**|Gesamtzahl der im Index oder Heap gestarteten Bereichs- und Tabellenscans.|    
|**singleton_lookup_count**|**bigint**|Gesamtzahl der Abrufvorgänge einzelner Zeilen aus dem Index oder Heap.|    
|**forwarded_fetch_count**|**bigint**|Anzahl der über einen weitergeleiteten Datensatz abgerufenen Zeilen.<br /><br /> 0 = Indizes|    
|**lob_fetch_in_pages**|**bigint**|Gesamtzahl der aus der LOB_DATA-Zuordnungseinheit abgerufenen LOB-Seiten (Large Object). Diese Seiten enthalten Daten, die in Spalten vom Datentyp gespeichert sind **Text**, **Ntext**, **Image**, **varchar(max)**, **Nvarchar () max)**, **varbinary(max)**, und **Xml**. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|    
|**lob_fetch_in_bytes**|**bigint**|Gesamtzahl der abgerufenen LOB-Datenbytes.|    
|**lob_orphan_create_count**|**bigint**|Gesamtzahl verwaister LOB-Werte, die für Massenvorgänge erstellt werden.<br /><br /> 0 = Nicht gruppierter Index|    
|**lob_orphan_insert_count**|**bigint**|Gesamtzahl verwaister LOB-Werte, die während Massenvorgängen eingefügt werden.<br /><br /> 0 = Nicht gruppierter Index|    
|**row_overflow_fetch_in_pages**|**bigint**|Gesamtwert der Zeilenüberlauf-Datenseiten, die aus der ROW_OVERFLOW_DATA-Zuordnungseinheit abgerufen werden.<br /><br /> Diese Seiten enthalten Daten in Spalten vom Typ **varchar**, **nvarchar (n)**, **varbinary**, und **Sql_variant** , das seit aus der Zeile verschoben.|    
|**row_overflow_fetch_in_bytes**|**bigint**|Gesamtzahl der abgerufenen Zeilenüberlauf-Datenbytes.|    
|**column_value_push_off_row_count**|**bigint**|Gesamtzahl der Spaltenwerte für LOB-Daten und Zeilenüberlaufdaten, die durch Ausführen eines Pushs außerhalb von Zeilen verschoben wurden, damit eine eingefügte oder aktualisierte Zeile auf eine Seite passt.|    
|**column_value_pull_in_row_count**|**bigint**|Gesamtwert der Spaltenwerte für LOB-Daten und Zeilenüberlaufdaten, die durch Ausführen eines Pulls innerhalb eine Zeile verschoben werden. Dieser Vorgang findet statt, wenn Speicherplatz in einem Datensatz durch einen Updatevorgang frei gemacht wird und die Möglichkeit besteht, durch Ausführen eines Pulls einen oder mehrere Werte außerhalb von Zeilen aus den Zuordnungseinheiten LOB_DATA oder ROW_OVERFLOW_DATA zur IN_ROW_DATA-Zuordnungseinheit zu verschieben.|    
|**row_lock_count**|**bigint**|Gesamtzahl der angeforderten Zeilensperren.|    
|**row_lock_wait_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf eine Zeilensperre gewartet hat.|    
|**row_lock_wait_in_ms**|**bigint**|Gesamtzahl der Millisekunden, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf eine Zeilensperre gewartet hat.|    
|**page_lock_count**|**bigint**|Gesamtzahl der angeforderten Seitensperren.|    
|**page_lock_wait_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf eine Seitensperre gewartet hat.|    
|**page_lock_wait_in_ms**|**bigint**|Gesamtzahl der Millisekunden, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf eine Seitensperre gewartet hat.|    
|**index_lock_promotion_attempt_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht hat, Sperren auszuweiten.|    
|**index_lock_promotion_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] Sperren ausgeweitet hat.|    
|**page_latch_wait_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] aufgrund eines Latchkonflikts gewartet hat.|    
|**page_latch_wait_in_ms**|**bigint**|Gesamtzahl der Millisekunden, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] aufgrund eines Latchkonflikts gewartet hat.|    
|**page_io_latch_wait_count**|**bigint**|Gesamthäufigkeit, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf einen E/A-Seitenlatch gewartet hat.|    
|**page_io_latch_wait_in_ms**|**bigint**|Gesamtzahl der Millisekunden, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf einen E/A-Seitenlatch gewartet hat.|    
|**tree_page_latch_wait_count**|**bigint**|Teilmenge von **Page_latch_wait_count** , die nur die B-Struktur Seiten der oberen Ebene umfasst. Immer 0 für einen Heap oder einen columnstore-Index.|    
|**tree_page_latch_wait_in_ms**|**bigint**|Teilmenge von **Page_latch_wait_in_ms** , die nur die B-Struktur Seiten der oberen Ebene umfasst. Immer 0 für einen Heap oder einen columnstore-Index.|    
|**tree_page_io_latch_wait_count**|**bigint**|Teilmenge von **Page_io_latch_wait_count** , die nur die B-Struktur Seiten der oberen Ebene umfasst. Immer 0 für einen Heap oder einen columnstore-Index.|    
|**tree_page_io_latch_wait_in_ms**|**bigint**|Teilmenge von **Page_io_latch_wait_in_ms** , die nur die B-Struktur Seiten der oberen Ebene umfasst. Immer 0 für einen Heap oder einen columnstore-Index.|    
|**page_compression_attempt_count**|**bigint**|Die Anzahl der Seiten, die für Komprimierung auf PAGE-Ebene für bestimmte Partitionen einer Tabelle, eines Index oder einer indizierten Sicht bewertet wurden. Dies schließt Seiten ein, die nicht komprimiert wurden, da beträchtliche Einsparungen nicht erreicht werden konnten. Immer 0 für den columnstore-Index.|    
|**page_compression_success_count**|**bigint**|Die Anzahl der Datenseiten, die mithilfe von PAGE-Komprimierung für bestimmte Partitionen einer Tabelle, eines Index oder einer indizierten Sicht komprimiert wurden. Immer 0 für den columnstore-Index.|    
    
## <a name="remarks"></a>Hinweise    
 Dieses dynamische Verwaltungsobjekt akzeptiert keine abhängigen Parameter von CROSS APPLY und OUTER APPLY.    
    
 Sie können **Sys. dm_db_index_operational_stats** um die Länge der Zeit zu verfolgen, die Benutzer warten müssen, lesen oder Schreiben in eine Tabelle, Index oder Partition und die Tabellen oder Indizes, die hohen e/a-Aktivitäten sind auftreten oder während des Betriebs zu identifizieren Teilnehmern.    
    
 Mithilfe der folgenden Spalten können Sie Konfliktbereiche erkennen.    
    
 **Eine gebräuchliche Zugriffsmuster für die Tabellen- oder Indexpartition zu analysieren**, verwenden Sie diese Spalten:    
    
-   **leaf_insert_count**    
    
-   **leaf_delete_count**    
    
-   **leaf_update_count**    
    
-   **leaf_ghost_count**    
    
-   **range_scan_count**    
    
-   **singleton_lookup_count**    
    
 Verwenden Sie die folgenden Spalten, um Latch- und Sperrkonflikte zu identifizieren:    
    
-   **Page_latch_wait_count** und **Page_latch_wait_in_ms**    
    
     Diese Spalten geben an, ob ein Latchkonflikt im Index oder Heap vorliegt, und zeigen die Bedeutung des Konflikts an.    
    
-   **Row_lock_count** und **Page_lock_count**    
    
     Diese Spalten geben die Häufigkeit an, mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht hat, Zeilen- und Seitensperren abzurufen.    
    
-   **Row_lock_wait_in_ms** und **Page_lock_wait_in_ms**    
    
     Diese Spalten geben an, ob ein Sperrkonflikt im Index oder Heap vorliegt, und zeigen die Bedeutung des Konflikts an.    
    
 **So analysieren Sie Statistiken der physischen e/as in einem Index oder heappartition**    
    
-   **Page_io_latch_wait_count** und **Page_io_latch_wait_in_ms**    
    
     Diese Spalten geben an, ob physische E/A-Vorgänge zum Verschieben der Index- oder Heapseiten in den Arbeitsspeicher ausgestellt wurden, und zeigen die Anzahl der ausgestellten E/A-Vorgänge an.    
    
## <a name="column-remarks"></a>Hinweise zu Spalten    
 Die Werte in **Lob_orphan_create_count** und **Lob_orphan_insert_count** sollten immer gleich sein.    
    
 Der Wert in den Spalten **Lob_fetch_in_pages** und **Lob_fetch_in_bytes** kann größer sein als 0 (null) bei nicht gruppierten Indizes, die mindestens eine LOB-Spalte als eingeschlossene Spalten enthalten. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md). Entsprechend den Werten in den Spalten **Row_overflow_fetch_in_pages** und **Row_overflow_fetch_in_bytes** kann bei nicht gruppierten Indizes größer als 0 sein, wenn der Index Spalten enthält, die verschoben werden können außerhalb von Zeilen.    
    
## <a name="how-the-counters-in-the-metadata-cache-are-reset"></a>Zurücksetzen der Leistungsindikatoren im Metadatencache    
 Die zurückgegebene Daten **Sys. dm_db_index_operational_stats** existiert nur, solange das Metadaten-Cacheobjekt, das den Heap oder Index darstellt verfügbar ist. Diese Daten sind weder persistent noch im Hinblick auf Transaktionen konsistent. Sie können somit diese Leistungsindikatoren nicht verwenden, um zu ermitteln, ob und wann ein Index zuletzt verwendet wurde. Weitere Informationen hierzu finden Sie unter [Sys. dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md).    
    
 Die Daten für die einzelnen Spalten werden auf 0 gesetzt, wenn die Metadaten für den Heap oder Index in den Metadatencache verschoben und Statistiken gesammelt werden, bis das Cacheobjekt aus dem Metadatencache entfernt wird. Deshalb befinden sich die Metadaten eines aktiven Heaps oder Indexes wahrscheinlich immer im Cache; die Gesamtzahlen können die Aktivität seit dem letzten Starten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz widerspiegeln. Die Metadaten für einen weniger aktiven Heap oder Index werden, abhängig von der Verwendung, in und aus dem Cache verschoben. Folglich ist es möglich, dass Werte zur Verfügung stehen oder auch nicht. Durch das Löschen eines Indexes werden die entsprechenden Statistiken aus dem Arbeitsspeicher entfernt und nicht mehr von der Funktion gemeldet. Sonstige indexbezogene DDL-Vorgänge können dazu führen, dass der Wert der Statistiken auf 0 zurückgesetzt wird.    
    
## <a name="using-system-functions-to-specify-parameter-values"></a>Verwenden von Systemfunktionen zum Angeben von Parameterwerten    
 Können Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen [DB_ID](../../t-sql/functions/db-id-transact-sql.md) und [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) , geben Sie einen Wert für die *Database_id* und *Object_id* Parameter. Das Übergeben von Werten, die für diese Funktionen nicht gültig sind, kann jedoch zu unerwarteten Ergebnissen führen. Stellen Sie stets sicher, dass bei der Verwendung von DB_ID oder OBJECT_ID eine gültige ID zurückgegeben wird. Weitere Informationen finden Sie im Abschnitt "Hinweise" in [Sys. dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).    
    
## <a name="permissions"></a>Berechtigungen    
 Folgende Berechtigungen sind erforderlich:    
    
-   CONTROL-Berechtigung für das angegebene Objekt innerhalb der Datenbank    
    
-   VIEW DATABASE STATE-Berechtigung zum Zurückgeben von Informationen zu allen Objekten innerhalb der angegebenen Datenbank mithilfe des Objekt-Platzhalters @*Object_id* = NULL    
    
-   VIEW SERVER STATE-Berechtigung zum Zurückgeben von Informationen zu allen Datenbanken mithilfe des Datenbank-Platzhalters @*Database_id* = NULL    
    
 Wenn die VIEW DATABASE STATE-Berechtigung erteilt wurde, ist die Rückgabe für alle Objekte in der Datenbank zulässig, unabhängig davon, ob CONTROL-Berechtigungen für bestimmte Objekte verweigert wurden.    
    
 Nach dem Verweigern der VIEW DATABASE STATE-Berechtigung können keine Objekte in der Datenbank zurückgegeben werden, unabhängig von möglicherweise erteilten CONTROL-Berechtigungen für bestimmte Objekte. Auch wenn dem Datenbank-Platzhalter @*Database_id*= NULL angegeben wird, wird die Datenbank ausgelassen.    
    
 Weitere Informationen finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).    
    
## <a name="examples"></a>Beispiele    
    
### <a name="a-returning-information-for-a-specified-table"></a>A. Zurückgeben von Informationen für eine angegebene Tabelle    
 Im folgenden Beispiel werden Informationen für alle Indizes und Partitionen der `Person.Address`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Für die Ausführung dieser Abfrage ist zumindest die CONTROL-Berechtigung in der `Person.Address`-Tabelle erforderlich.    
    
> [!IMPORTANT]    
>  Wenn Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen DB_ID und OBJECT_ID zur Rückgabe eines Parameterwerts verwenden, sollten Sie sicherstellen, dass eine gültige ID zurückgegeben wird. Wenn der Datenbank- oder Objektname nicht gefunden werden kann, wenn sie z. B. nicht vorhanden oder fehlerhaft geschrieben sind, geben beide Funktionen NULL zurück. Die **sys.dm_db_index_operational_stats**-Funktion interpretiert NULL als Platzhalterwert, der alle Datenbanken oder alle Objekte angibt. Da dies ein versehentlicher Vorgang sein kann, veranschaulichen die Beispiele in diesem Abschnitt, wie Sie auf sichere Weise Datenbank- und Objekt-IDs bestimmen.    
    
```    
DECLARE @db_id int;    
DECLARE @object_id int;    
SET @db_id = DB_ID(N'AdventureWorks2012');    
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');    
IF @db_id IS NULL     
  BEGIN;    
    PRINT N'Invalid database';    
  END;    
ELSE IF @object_id IS NULL    
  BEGIN;    
    PRINT N'Invalid object';    
  END;    
ELSE    
  BEGIN;    
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);    
  END;    
GO    
    
```    
    
### <a name="b-returning-information-for-all-tables-and-indexes"></a>B. Zurückgeben von Informationen für alle Tabellen und Indizes    
 Im folgenden Beispiel werden Informationen für alle Tabellen und Indizes in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zurückgegeben. Zum Ausführen dieser Abfrage erfordert die VIEW SERVER STATE-Berechtigung.    
    
```    
SELECT * FROM sys.dm_db_index_operational_stats( NULL, NULL, NULL, NULL);    
GO    
    
```    
    
## <a name="see-also"></a>Siehe auch    
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
 [Index Related Dynamic Management Views and Functions (Transact-SQL) (Indexbezogene dynamische Verwaltungssichten und -funktionen (Transact-SQL))](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)     
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)     
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)     
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)     
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)     
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)    
    
  

