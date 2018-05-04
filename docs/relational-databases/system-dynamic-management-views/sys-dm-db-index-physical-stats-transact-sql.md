---
title: Sys. dm_db_index_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
caps.latest.revision: 95
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f5e548a6ef4a01cd88a33c015ff2567639c91c62
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbindexphysicalstats-transact-sql"></a>sys.dm_db_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Größen- und Fragmentierungsinformationen für die Daten und Indizes der angegebenen Tabelle oder Sicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück. Bei einem Index wird eine Zeile für jede B-Strukturebene in den einzelnen Partitionen zurückgegeben. Bei einem Heap wird eine Zeile für die IN_ROW_DATA-Zuordnungseinheit jeder Partition zurückgegeben. Bei LOB-Daten (Large Object) wird eine Zeile für die LOB_DATA-Zuordnungseinheit jeder Partition zurückgegeben. Falls Zeilenüberlaufdaten in der Tabelle vorhanden sind, wird eine Zeile für die ROW_OVERFLOW_DATA-Zuordnungseinheit in jeder Partition zurückgegeben. Gibt keine Informationen zu speicheroptimierten xVelocity-ColumnStore-Indizes zurück.  
  
> [!IMPORTANT]
> Wenn Sie Abfragen **Sys. dm_db_index_physical_stats** auf einer Serverinstanz, die Always On hostet [lesbares sekundäres Replikat](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), ein REDO-Blockierungsproblem auftreten. Dies kommt daher, dass diese dynamische Verwaltungssicht eine beabsichtigte gemeinsame Sperre für die angegebene Benutzertabelle oder Sicht erhält, die Anforderungen von einem REDO-Thread für eine X-Sperre dieser Benutzertabelle oder Sicht blockieren kann.  
  
 **Sys. dm_db_index_physical_stats** gibt keine Informationen zu speicheroptimierten Indizes zurück. Informationen zur Verwendung von speicheroptimierten Indizes finden Sie unter [dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md).  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argumente  
 *Database_id* | NULL | 0 | STANDARDWERT  
 Ist die ID der Datenbank. *Database_id* ist **"smallint"**. Gültige Eingaben sind die ID einer Datenbank, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig.  
  
 Geben Sie NULL an, wenn Informationen zu allen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgegeben werden sollen. Bei Angabe von NULL für *Database_id*, müssen Sie auch angeben, NULL für *Object_id*, *Index_id*, und *Partition_number*.  
  
 Die integrierte Funktion [DB_ID](../../t-sql/functions/db-id-transact-sql.md) kann angegeben werden. Wenn DB_ID verwendet wird, ohne dass ein Datenbankname angegeben wird, muss der Kompatibilitätsgrad der aktuellen Datenbank 90 oder höher sein.  
  
 *Object_id* | NULL | 0 | STANDARDWERT  
 Die Objekt-ID der Tabelle oder Sicht mit dem Index. *object_id* ist **int**.  
  
 Gültige Eingaben sind die ID einer Tabelle und Sicht, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig. Als der [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], gültige Eingaben auch der Name der Service Broker-Warteschlange oder der Name der Warteschlange interne Tabelle enthalten. Wenn der Standardparameter angewendet werden (d. h. alle Objekte, alle Indizes usw.), Fragmentierungsinformationen für alle Warteschlangen im Resultset enthalten sind.  
  
 Geben Sie NULL an, wenn Informationen zu allen Tabellen und Sichten in der angegebenen Datenbank zurückgegeben werden sollen. Bei Angabe von NULL für *Object_id*, müssen Sie auch angeben, NULL für *Index_id* und *Partition_number*.  
  
 *Index_id* | 0 | NULL | -1 | STANDARDWERT  
 Die ID des Indexes. *Index_id* ist **Int**. Gültige Eingaben sind die ID-Nummer eines Indexes, 0, wenn *Object_id* ist ein Heap ist, NULL,-1 oder DEFAULT. Der Standardwert ist-1. NULL,-1 und DEFAULT sind in diesem Kontext gleichwertig.  
  
 Geben Sie NULL an, um Informationen zu allen Indizes für eine Basistabelle oder Sicht zurückgegeben. Bei Angabe von NULL für *Index_id*, müssen Sie auch angeben, NULL für *Partition_number*.  
  
 *Partitionsnummer* | NULL | 0 | STANDARDWERT  
 Die Partitionsnummer im Objekt. *Partitionsnummer* ist **Int**. Gültige Eingaben sind die *Partion_number* eines Indexes oder Heaps, NULL, 0 oder DEFAULT. Die Standardeinstellung ist 0. NULL, 0 und DEFAULT sind in diesem Kontext gleichwertig.  
  
 Geben Sie NULL an, um Informationen für alle Partitionen des besitzenden Objekts zurückgegeben.  
  
 *Partitionsnummer* ist 1-basiert. Ein nicht partitionierter Index oder Heap ist *Partition_number* auf 1 festgelegt.  
  
 *Modus* | NULL | STANDARDWERT  
 Der Name des Modus. *Modus* gibt die Scanebene an, die verwendet wird, um Statistiken zu erhalten. *Modus* ist **Sysname**. Gültige Eingaben sind DEFAULT, NULL, LIMITED, SAMPLED oder DETAILED. Der Standardwert (NULL) ist LIMITED.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Datenbank-ID der Tabelle oder Sicht.|  
|object_id|**int**|Objekt-ID der Tabelle oder Sicht mit dem Index.|  
|index_id|**int**|Index-ID eines Indexes.<br /><br /> 0 = Heap.|  
|partition_number|**int**|1-basierte Partitionsnummer im besitzenden Objekt; eine Tabelle, eine Sicht oder ein Index.<br /><br /> 1 = Nicht partitionierter Index oder Heap.|  
|index_type_desc|**nvarchar(60)**|Beschreibung des Indextyps:<br /><br /> HEAP<br /><br /> CLUSTERED INDEX<br /><br /> NONCLUSTERED INDEX<br /><br /> PRIMARY XML INDEX<br /><br /> SPATIAL INDEX<br /><br /> XML INDEX<br /><br /> Columnstore-ZUORDNUNG INDEX (intern)<br /><br /> Columnstore-DELETEBUFFER INDEX (intern)<br /><br /> Columnstore-DELETEBITMAP INDEX (intern)|  
|hobt_id|**bigint**|Heap- oder B-Struktur-ID des Indexes oder der Partition.<br /><br /> Neben der Rückgabe die Hobt_id benutzerdefinierte Indizes, gibt auch die Hobt_id der internen columnstore-Indizes zurück.|  
|alloc_unit_type_desc|**nvarchar(60)**|Beschreibung des Typs der Zuordnungseinheit:<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> Die LOB_DATA-Zuordnungseinheit enthält die Daten, die in Spalten vom Datentyp gespeichert sind **Text**, **Ntext**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und **Xml**. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).<br /><br /> Die ROW_OVERFLOW_DATA-Zuordnungseinheit enthält die Daten, die in Spalten vom Datentyp gespeichert sind **varchar**, **nvarchar (n)**, **varbinary**, und **Sql_ Variante** , die ein Push ausgeführt wurde außerhalb von Zeilen.|  
|index_depth|**tinyint**|Anzahl von Indexebenen.<br /><br /> 1 = Heap oder LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheit.|  
|index_level|**tinyint**|Aktuelle Ebene des Indexes.<br /><br /> 0 für Indexblattebene, Heaps und LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten.<br /><br /> Werte größer 0 für Nicht-Indexblattebenen. *Index_level* werden auf der Stammebene eines Indexes den höchsten Wert.<br /><br /> Die nichtblattebenen von Indizes werden nur verarbeitet, wenn *Modus* = DETAILED.|  
|avg_fragmentation_in_percent|**float**|Die logische Fragmentierung für Indizes oder die Blockfragmentierung für Heaps in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Der Wert wird als Prozentsatz gemessen und berücksichtigt mehrere Dateien. Definitionen für die logische Fragmentierung und die Blockfragmentierung finden Sie unter den Hinweisen.<br /><br /> 0 für LOB_DATA- und ROW_OVERFLOW_DATA-Zuordnungseinheiten.<br /><br /> NULL für heaps, wenn *Modus* = SAMPLED.|  
|fragment_count|**bigint**|Anzahl von Fragmenten auf der Blattebene einer IN_ROW_DATA-Zuordnungseinheit. Weitere Informationen zu Fragmenten finden Sie unter den Hinweisen.<br /><br /> NULL für Nichtblattebenen eines Indexes und LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten.<br /><br /> NULL für heaps, wenn *Modus* = SAMPLED.|  
|avg_fragment_size_in_pages|**float**|Durchschnittliche Anzahl von Seiten in einem Fragment auf der Blattebene einer IN_ROW_DATA-Zuordnungseinheit.<br /><br /> NULL für Nichtblattebenen eines Indexes und LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten.<br /><br /> NULL für heaps, wenn *Modus* = SAMPLED.|  
|page_count|**bigint**|Gesamtanzahl von Index- oder Datenseiten.<br /><br /> Bei einem Index die Gesamtanzahl von Indexseiten auf der aktuellen B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf die Gesamtanzahl von Datenseiten in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf die Gesamtanzahl von Seiten in der Zuordnungseinheit.|  
|avg_page_space_used_in_percent|**float**|Durchschnittlicher Prozentsatz des auf allen Seiten verwendeten verfügbaren Datenspeicherplatzes.<br /><br /> Bei einem Index bezieht sich der Durchschnittswert auf die aktuelle B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf den Durchschnittswert aller Datenseiten in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf den Durchschnittswert aller Seiten in der Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|record_count|**bigint**|Gesamtanzahl von Datensätzen.<br /><br /> Bei einem Index bezieht sich die Gesamtanzahl von Datensätzen auf die aktuelle B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf die Gesamtanzahl von Datensätzen in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> **Hinweis:** für einen Heap möglicherweise die Anzahl der Datensätze, die von dieser Funktion zurückgegeben werden. die Anzahl der Zeilen, die zurückgegeben werden, durch Ausführen von Wählen Sie die Anzahl nicht überein (\*) für den Heap. Das liegt daran, dass eine Zeile möglicherweise mehrere Datensätze enthält. So kann in bestimmten Updatesituationen eine einzelne Heapzeile möglicherweise über einen Weiterleitungsdatensatz und einen weitergeleiteten Datensatz als Ergebnis des Updates verfügen. Außerdem werden die meisten großen LOB-Zeilen im LOB_DATA-Speicher in mehrere Datensätze geteilt.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf die Gesamtanzahl von Datensätzen in der gesamten Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|ghost_record_count|**bigint**|Anzahl von inaktiven Datensätzen, die durch den Cleanuptask für inaktive Datensätze in der Zuordnungseinheit entfernt werden können.<br /><br /> 0 für Nichtblattebenen eines Indexes in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|version_ghost_record_count|**bigint**|Anzahl inaktiver Datensätze, die von einer ausstehenden Momentaufnahme-Isolationstransaktion in einer Zuordnungseinheit beibehalten werden.<br /><br /> 0 für Nichtblattebenen eines Indexes in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|min_record_size_in_bytes|**int**|Minimale Datensatzgröße in Bytes.<br /><br /> Bei einem Index bezieht sich die minimale Datensatzgröße auf die aktuelle B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf die minimale Datensatzgröße in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf die minimale Datensatzgröße in der gesamten Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|max_record_size_in_bytes|**int**|Maximale Datensatzgröße in Bytes.<br /><br /> Bei einem Index bezieht sich die maximale Datensatzgröße auf die aktuelle B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf die maximale Datensatzgröße in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf die maximale Datensatzgröße in der gesamten Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|avg_record_size_in_bytes|**float**|Durchschnittliche Datensatzgröße in Bytes.<br /><br /> Bei einem Index bezieht sich die durchschnittliche Datensatzgröße auf die aktuelle B-Strukturebene in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei einem Heap auf die durchschnittliche Datensatzgröße in der IN_ROW_DATA-Zuordnungseinheit.<br /><br /> Bei LOB_DATA- oder ROW_OVERFLOW_DATA-Zuordnungseinheiten auf die durchschnittliche Datensatzgröße in der gesamten Zuordnungseinheit.<br /><br /> NULL zurück, wenn *Modus* = LIMITED.|  
|forwarded_record_count|**bigint**|Anzahl der Datensätze in einem Heap, die weiterleitungszeiger auf einen anderen Datenspeicherort besitzen. (Dieser Status tritt während eines Updates auf, wenn nicht genügend Speicherplatz vorhanden ist, um die neue Zeile am ursprünglichen Speicherort zu speichern.)<br /><br /> NULL für eine beliebige Zuordnungseinheit außer IN_ROW_DATA-Zuordnungseinheiten für einen Heap.<br /><br /> NULL für heaps, wenn *Modus* = LIMITED.|  
|compressed_page_count|**bigint**|Die Anzahl der komprimierten Seiten.<br /><br /> Bei Heaps sind neu zugeordnete Seiten nicht mit PAGE seitenkomprimiert. Ein Heap wird nur unter zwei besonderen Bedingungen PAGE-komprimiert: wenn Massendaten importiert werden oder wenn ein Heap neu erstellt wird. Typische DML-Vorgänge, die Seitenzuordnungen hervorrufen, werden nicht PAGE-komprimiert. Erstellen Sie einen Heap neu, wenn der compressed_page_count-Wert den gewünschten Schwellenwert überschreitet.<br /><br /> Für Tabellen mit gruppiertem Index gibt der compressed_page_count-Wert die Wirksamkeit der PAGE-Komprimierung an.|  
|hobt_id|bigint|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Für columnstore-Indizes ist dies die ID für ein Rowset, das die internen columnstore-Daten für eine Partition nachverfolgt. Die Rowsets sind, wie Daten heaps gespeicherte oder binäre Strukturen. Sie verfügen über dieselbe Index-ID wie der übergeordnete columnstore-Index. Weitere Informationen finden Sie unter [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md).<br /><br /> NULL, wenn|  
|column_store_delete_buffer_state|tinyint|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = EIN AUSGLEICH DURCHGEFÜHRT<br /><br /> 3 = LEEREN<br /><br /> 4 = ABKOPPELN<br /><br /> 5 = BEREIT|  
|column_store_delete_buff_state_desc||**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> NOT_APPLICABLE – der Index der übergeordneten ist kein columnstore-Index.<br /><br /> Öffnen – Löschvorgänge und Scanner verwenden Sie diese.<br /><br /> BELASTUNG – Löschvorgänge werden ein Ausgleich durchgeführt aber Scanner jedoch verwendet werden.<br /><br /> Das leeren – Puffer wird geschlossen, und Zeilen im Puffer für die Delete-Bitmap geschrieben werden.<br /><br /> ABKOPPELN – von Zeilen in der geschlossenen löschungspuffers geschrieben wurden, für die Delete-Bitmap, aber der Puffer wurde nicht abgeschnitten, da Scanner verwendet werden. Neue Scanner müssen nicht die Abschaltung Puffer verwendet werden, da der geöffnete Puffer ausreichend ist.<br /><br /> Soweit sind – diese löschungspuffers verwendet werden kann.|  
  
## <a name="remarks"></a>Hinweise  
 Die dynamische Verwaltungsfunktion sys.dm_db_index_physical_stats ersetzt die DBCC SHOWCONTIG-Anweisung.  
  
## <a name="scanning-modes"></a>Scanmodi  
 Der Modus, in dem die Funktion ausgeführt wird, bestimmt die Scanebene, die zum Abrufen der statistischen Daten von der Funktion verwendet wird. *Modus* wird als LIMITED, SAMPLED oder DETAILED angegeben. Die Funktion durchsucht die Seitenketten nach den Zuordnungseinheiten, aus denen die angegebenen Partitionen der Tabelle oder des Indexes bestehen. Sys. dm_db_index_physical_stats erfordert nur eine beabsichtigte freigegebene Tabellensperre (IS) Tabellensperre, unabhängig vom Modus in ausgeführt wird.  
  
 Der Modus LIMITED ist am schnellsten und durchsucht am wenigsten Seiten. Bei einem Index werden nur die Seiten der übergeordneten B-Strukturebene (d. h. die Seiten oberhalb der Blattebene) gescannt. Bei einem Heap werden nur die zugehörigen PFS- und IAM-Seiten untersucht; die Datenseiten des Heaps werden im Modus LIMITED gescannt.  
  
 Mit dem Modus LIMITED ist compressed_page_count NULL, da der [!INCLUDE[ssDE](../../includes/ssde-md.md)] nur Nicht- Blattseiten der B-Struktur und die IAM- und PFS-Seiten des Heaps scannt. Verwenden Sie den Modus SAMPLED, um einen geschätzten Wert für Compressed_page_count abzurufen, und verwenden Sie Modus DETAILED, um den tatsächlichen Wert für Compressed_page_count abzurufen. Der Modus SAMPLED gibt Statistiken basierend auf einer Stichprobe von 1 % aller Seiten im Index oder Heap zurück. Ergebnisse im SAMPLED-Modus sollten als ungefähre Werte angesehen werden. Falls der Index oder Heap weniger als 10.000 Seiten aufweist, wird anstelle des Modus SAMPLED der Modus DETAILED verwendet.  
  
 Der Modus DETAILED durchsucht alle Seiten und gibt alle Statistiken zurück.  
  
 Die Geschwindigkeit der Modi nimmt von LIMITED zu DETAILED schrittweise ab, weil im jeweils nächsten Modus mehr Arbeitsschritte ausgeführt werden. Verwenden Sie den Modus LIMITED, wenn Sie die Größe oder die Fragmentierungsebene einer Tabelle oder eines Indexes schnell messen möchten. Dies ist der schnellste Modus und gibt nicht für jede Nichtblattebene in der IN_ROW_DATA-Zuordnungseinheit des Indexes eine Zeile zurück.  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>Verwenden von Systemfunktionen zum Angeben von Parameterwerten  
 Können Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen [DB_ID](../../t-sql/functions/db-id-transact-sql.md) und [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) , geben Sie einen Wert für die *Database_id* und *Object_id* Parameter. Das Übergeben von Werten, die für diese Funktionen nicht gültig sind, kann jedoch zu unerwarteten Ergebnissen führen. Falls z. B. die Datenbank oder der Objektname nicht gefunden wird, weil er nicht vorhanden oder falsch geschrieben ist, geben beide Funktionen NULL zurück. Die sys.dm_db_index_physical_stats-Funktion interpretiert NULL als Platzhalterwert, mit dem alle Datenbanken oder alle Objekte angegeben werden.  
  
 Darüber hinaus die OBJECT_ID-Funktion wird verarbeitet, bevor die Sys. dm_db_index_physical_stats-Funktion aufgerufen wird, und daher im Kontext der aktuellen Datenbank ausgewertet wird, nicht in die Datenbank angegeben, *Database_id*. Dadurch gibt die OBJECT_ID-Funktion unter Umständen einen NULL-Wert zurück, oder es wird eine Fehlermeldung zurückgegeben, falls der Objektname sowohl im aktuellen Datenbankkontext als auch in der angegebenen Datenbank vorhanden ist. In den folgenden Beispielen werden diese nicht beabsichtigten Ergebnisse veranschaulicht.  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>Bewährte Methoden  
 Stellen Sie stets sicher, dass bei der Verwendung von DB_ID oder OBJECT_ID eine gültige ID zurückgegeben wird. Beispielsweise bei Verwendung von OBJECT_ID Geben Sie einen dreiteiligen Namen wie z. B. `OBJECT_ID(N'AdventureWorks2012.Person.Address')`, oder testen Sie den Wert, der von der Funktion zurückgegebenen werden, bevor Sie sie in der Sys. dm_db_index_physical_stats-Funktion verwenden. In den nachstehenden Beispielen A und B wird eine sichere Möglichkeit zur Angabe von Datenbank- und Objekt-IDs aufgezeigt.  
  
## <a name="detecting-fragmentation"></a>Erkennen der Fragmentierung  
 Die Fragmentierung wird durch Datenänderungen (mithilfe der Anweisungen INSERT, UPDATE oder DELETE) in Bezug auf die Tabelle und dadurch an den für diese Tabelle definierten Indizes hervorgerufen. Da diese Änderungen normalerweise nicht gleichmäßig über alle Zeilen der Tabelle und Indizes verteilt vorgenommen werden, kann sich mit der Zeit der Füllgrad jeder Seite ändern. Diese Tabellenfragmentierung kann bei Abfragen, bei denen die Indizes einer Tabelle teilweise oder ganz gescannt werden, zu zusätzlichen Seitenlesevorgängen führen. Dies behindert das parallele Scannen von Daten.  
  
 Die Fragmentierungsebene eines Indexes oder Heaps wird in der avg_fragmentation_in_percent-Spalte angezeigt. Bei Heaps stellt dieser Wert die Blockfragmentierung des Heaps dar. Bei Indizes stellt dieser Wert die logische Fragmentierung des Indexes dar. Im Gegensatz zu DBCC SHOWCONTIG wird bei den Algorithmen zur Fragmentierungsberechnung in beiden Fällen Speicherplatz berücksichtigt, der sich über mehrere Dateien erstreckt; folglich sind diese Algorithmen genauer.  
  
 **Die logische Fragmentierung**  
  
 Dies ist der Prozentsatz der Seiten, die auf den Blattseiten eines Indexes nicht ordnungsgemäß sortiert sind. Eine nicht ordnungsgemäß einsortierte Seite ist eine Seite, für die die nächste physische Seite, die dem Index zugeordnet ist, nicht die Seite ist, auf die der Zeiger für die nächste Seit*e* auf der aktuellen Blattseite zeigt.  
  
 **Blockfragmentierung**  
  
 Dies ist der Prozentsatz der Blöcke, die auf den Blattseiten eines Heaps nicht ordnungsgemäß sortiert sind. Ein nicht ordnungsgemäß sortierter Block ist ein Block, für den der Block, der die aktuelle Seite eines Heaps enthält, physisch nicht der nächste Block nach dem Block ist, der die vorherige Seite enthält.  
  
 Der Wert für avg_fragmentation_in_percent sollte möglichst nahe bei null liegen, um eine optimale Leistung sicherzustellen. Werte zwischen 0 und 10 % sind jedoch akzeptabel. Um diese Werte zu verringern, können alle Methoden zur Reduzierung der Fragmentierung verwendet werden, wie z. B. Neuerstellung oder Neuorganisierung. Weitere Informationen zum Analysieren des Grad der Fragmentierung in einem Index finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="reducing-fragmentation-in-an-index"></a>Reduzieren der Fragmentierung in einem Index  
 Wenn ein Index derart fragmentiert ist, dass die Fragmentierung die Abfrageleistung beeinträchtigt, gibt es drei Möglichkeiten, um die Fragmentierung zu reduzieren:  
  
-   Löschen Sie den gruppierten Index, und erstellen Sie ihn neu.  
  
     Durch das erneute Erstellen eines gruppierten Indexes werden die Daten neu verteilt, was zu vollen Datenseiten führt. Der Füllungsgrad kann über die Option FILLFACTOR in CREATE INDEX konfiguriert werden. Diese Methode hat den Nachteil, dass der Index während des Löschens und Neuerstellens offline und der Vorgang atomar ist. Wenn die Indexerstellung unterbrochen wird, wird der Index nicht neu erstellt. Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
-   Verwenden Sie ALTER INDEX REORGANIZE (der Ersatz für DBCC INDEXDEFRAG), um die Indexseiten auf Blattebene in einer logischen Reihenfolge neu anzuordnen. Da es sich hierbei um einen Onlinevorgang handelt, steht der Index während der Ausführung der Anweisung zur Verfügung. Der Vorgang kann auch ohne Verlust bereits abgeschlossener Arbeitsschritte unterbrochen werden. Diese Methode hat den Nachteil, dass die Daten nicht so gut neu organisiert werden wie bei einem Indexneuerstellungsvorgang, und außerdem werden die Statistiken nicht aktualisiert.  
  
-   Verwenden Sie ALTER INDEX REBUILD (der Ersatz für DBCC DBREINDEX), um den Index im Online- oder Offlinemodus neu zu erstellen. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
 Die Fragmentierung alleine ist kein ausreichender Grund, um einen Index neu zu organisieren oder neu zu erstellen. Durch die Fragmentierung wird in erster Linie der Read-Ahead-Durchsatz von Seiten während Indexscans reduziert. Dies verursacht langsamere Antwortzeiten. Falls die Abfragearbeitsauslastung für eine fragmentierte Tabelle oder einen fragmentierten Index keine Scans enthält, weil es sich bei der Arbeitsauslastung in erster Linie um Singleton-Suchvorgänge handelt, hat das Beseitigen der Fragmentierung möglicherweise keine Auswirkungen. Weitere Informationen finden Sie in diesem [Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=31012).  
  
> [!NOTE]  
>  Ausführen von DBCC SHRINKFILE oder DBCC SHRINKDATABASE kann zur Fragmentierung führen, wenn ein Index während des Verkleinerungsvorgangs teilweise oder vollständig verschoben wird. Wenn ein Verkleinerungsvorgang ausgeführt werden muss, sollten Sie diesen deshalb vor dem Beseitigen der Fragmentierung vornehmen.  
  
## <a name="reducing-fragmentation-in-a-heap"></a>Reduzieren der Fragmentierung in einem Heap  
 Um die Blockfragmentierung eines Heaps zu reduzieren, erstellen Sie einen gruppierten Index für die Tabelle, und löschen Sie dann den Index. Dadurch werden die Daten neu verteilt, während der gruppierte Index erstellt wird. Dabei wird ein möglichst optimaler Zustand in Bezug auf die Verteilung des freien Speicherplatzes in der Datenbank angestrebt. Wenn der gruppierte Index dann gelöscht wird, um den Heap neu zu erstellen, werden die Daten nicht verschoben und verbleiben an ihrer optimalen Position. Informationen zum Ausführen dieser Vorgänge finden Sie unter [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) und [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md).  
  
> [!CAUTION]  
>  Durch das Erstellen oder Verwerfen eines gruppierten Indexes einer Tabelle werden alle nicht gruppierten Indexes der Tabelle doppelt neu erstellt.  
  
## <a name="compacting-large-object-data"></a>Komprimieren von LOB-Daten  
 Standardmäßig komprimiert die ALTER INDEX REORGANIZE-Anweisung Seiten, die LOB-Daten (Large Object) enthalten. Die Zuordnung von LOB-Seiten wird nicht aufgehoben, wenn sie leer sind. Deshalb kann durch das Komprimieren dieser Daten der Speicherplatz optimiert werden, falls viele LOB-Daten gelöscht wurden oder eine LOB-Spalte entfernt wird.  
  
 Durch das Neuorganisieren eines angegebenen gruppierten Indexes werden alle im gruppierten Index enthaltenen LOB-Spalten komprimiert. Durch das Neuorganisieren eines nicht gruppierten Indexes werden alle LOB-Spalten komprimiert, die (eingeschlossene) Nichtschlüsselspalten im Index sind. Wenn ALL in der Anweisung angegeben wird, werden alle Indizes, die der angegebenen Tabelle oder Sicht zugeordnet sind, neu organisiert. Darüber hinaus werden alle LOB-Spalten, die dem gruppierten Index, der zugrunde liegenden Tabelle oder dem nicht gruppierten Index mit eingeschlossenen Spalten zugeordnet sind, komprimiert.  
  
## <a name="evaluating-disk-space-use"></a>Auswerten der Speicherplatzverwendung  
 Die avg_page_space_used_in_percent-Spalte gibt den Seitenfüllgrad an. Für eine optimale Speicherplatzverwendung sollte dieser Wert für einen Index ohne viele zufällige Einfügungen nahe bei 100 % liegen. Ein Index mit zahlreichen zufälligen Einfügungen und sehr vollen Seiten verfügt jedoch über eine höhere Anzahl von Seitenteilungen. Dadurch entsteht mehr Fragmentierung. Deshalb sollte dieser Wert unter 100 % liegen, um Seitenteilungen zu reduzieren. Durch die Neuerstellung eines Indexes mit angegebener Option FILLFACTOR kann der Seitenfüllgrad an das Abfragemuster für den Index angepasst werden. Weitere Informationen zum Füllfaktor finden Sie unter [angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md). Darüber hinaus komprimiert ALTER INDEX REORGANIZE einen Index, indem versucht wird, Seiten bis zum zuletzt angegebenen FILLFACTOR-Wert zu füllen. Dadurch erhöht sich der Wert in avg_space_used_in_percent. Beachten Sie, dass der Seitenfüllgrad mit ALTER INDEX REORGANIZE nicht reduziert werden kann. Stattdessen muss eine Indexneuerstellung ausgeführt werden.  
  
## <a name="evaluating-index-fragments"></a>Auswerten von Indexfragmenten  
 Ein Fragment besteht aus aufeinander folgenden Blattseiten in derselben Datei für eine Zuordnungseinheit. Ein Index weist mindestens ein Fragment auf. Die maximale Anzahl von Fragmenten für einen Index entspricht der Anzahl von Seiten auf der Blattebene des Indexes. Größere Fragmente bedeuten, dass weniger Datenträger-E/A-Vorgänge zum Lesen der gleichen Anzahl von Seiten erforderlich sind. Deshalb gilt, je höher der Wert für avg_fragment_size_in_pages, desto besser ist die Leistung des Bereichsscans. Die Werte avg_fragment_size_in_pages und avg_fragmentation_in_percent verhalten sich umgekehrt proportional zueinander. Deshalb sollte durch das Neuerstellen oder Neuorganisieren eines Indexes die Fragmentierung reduziert und die Fragmentgröße erhöht werden.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Gibt keine Daten für gruppierte columnstore-Indizes zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Folgende Berechtigungen sind erforderlich:  
  
-   CONTROL-Berechtigung für das angegebene Objekt innerhalb der Datenbank.  
  
-   VIEW DATABASE STATE-Berechtigung zum Zurückgeben von Informationen zu allen Objekten innerhalb der angegebenen Datenbank mithilfe des Objekt-Platzhalters @*Object_id*= NULL.  
  
-   VIEW SERVER STATE-Berechtigung zum Zurückgeben von Informationen zu allen Datenbanken mithilfe des Datenbank-Platzhalters @*Database_id* = NULL.  
  
 Wenn die VIEW DATABASE STATE-Berechtigung erteilt wurde, ist die Rückgabe für alle Objekte in der Datenbank zulässig, unabhängig davon, ob CONTROL-Berechtigungen für bestimmte Objekte verweigert wurden.  
  
 Nach dem Verweigern der VIEW DATABASE STATE-Berechtigung können keine Objekte in der Datenbank zurückgegeben werden, unabhängig von möglicherweise erteilten CONTROL-Berechtigungen für bestimmte Objekte. Auch wenn dem Datenbank-Platzhalter @*Database_id*= NULL angegeben wird, wird die Datenbank ausgelassen.  
  
 Weitere Informationen finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. Zurückgeben von Informationen zu einer angegebenen Tabelle  
 Im folgenden Beispiel werden die Größen- und Fragmentierungsstatistiken für alle Indizes und Partitionen der `Person.Address`-Tabelle zurückgegeben. Als Scanmodus ist `'LIMITED'` festgelegt, um eine optimale Leistung sicherzustellen und die zurückgegebenen Statistiken zu begrenzen. Für die Ausführung dieser Abfrage wird zumindest die CONTROL-Berechtigung für die `Person.Address`-Tabelle benötigt.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
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
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. Zurückgeben von Informationen zu einem Heap  
 Im folgenden Beispiel werden alle Statistiken für den `dbo.DatabaseLog`-Heap in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Da die Tabelle LOB-Daten enthält, wird eine Zeile für die `LOB_DATA`-Zuordnungseinheit zurückgegeben. Dies geschieht zusätzlich zu der Zeile, die für `IN_ROW_ALLOCATION_UNIT` zurückgegeben wird und in der die Datenseiten des Heaps gespeichert sind. Für die Ausführung dieser Abfrage wird zumindest die CONTROL-Berechtigung für die `dbo.DatabaseLog`-Tabelle benötigt.  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. Zurückgeben von Informationen zu allen Datenbanken  
 Im folgenden Beispiel werden alle Statistiken für alle Tabellen und Indizes innerhalb der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgegeben, indem der Platzhalter `NULL` für alle Parameter angegeben wird. Zum Ausführen dieser Abfrage erfordert die VIEW SERVER STATE-Berechtigung.  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdmdbindexphysicalstats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. Verwenden von "sys.dm_db_index_physical_stats" in einem Skript, um Indizes neu zu erstellen oder neu zu organisieren  
 Im folgenden Beispiel werden automatisch alle Partitionen in einer Datenbank neu angeordnet oder neu erstellt, die eine durchschnittliche Fragmentierung von über 10 % aufweisen. Zum Ausführen dieser Abfrage ist die VIEW DATABASE STATE-Berechtigung erforderlich. In diesem Beispiel wird `DB_ID` als erster Parameter angegeben, ohne einen Datenbanknamen anzugeben. Ein Fehler wird generiert, wenn die aktuelle Datenbank über einen Kompatibilitätsgrad von 80 oder niedriger verfügt. Zum Beheben des Fehlers ersetzen Sie `DB_ID()` durch einen gültigen Datenbanknamen. Weitere Informationen zu Kompatibilitätsgraden von Datenbanken finden Sie unter [ALTER DATABASE Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdmdbindexphysicalstats-to-show-the-number-of-page-compressed-pages"></a>E. Anzeigen der Anzahl von Seiten mit Seitenkomprimierung mithilfe von "sys.dm_db_index_physical_stats"  
 Im folgenden Beispiel wird gezeigt, wie die Gesamtanzahl von Seiten angezeigt und den Seiten mit Zeilen- und Seitenkomprimierung gegenüber gestellt wird. Mithilfe dieser Informationen kann ermittelt werden, welche Vorteile diese Komprimierung für einen Index oder eine Tabelle hat.  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdmdbindexphysicalstats-in-sampled-mode"></a>F. Verwenden von „sys.dm_db_index_physical_stats“ im Modus SAMPLED  
 Im folgenden Beispiel wird gezeigt, wie vom Modus SAMPLED ein ungefährer Wert zurückgegeben wird, der sich von den Ergebnissen des Modus DETAILED unterscheidet.  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. Abfragen von Service Broker-Warteschlangen für Indexfragmentierung  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 In den folgenden Beispielen wird gezeigt, wie Server Broker-Warteschlangen Fragmentierung abgefragt wird.  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Index Related Dynamic Management Views and Functions (Transact-SQL) (Indexbezogene dynamische Verwaltungssichten und -funktionen (Transact-SQL))](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

