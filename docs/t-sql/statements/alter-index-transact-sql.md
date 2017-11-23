---
title: ALTER INDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: "222"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 39f0a539906f192c39599dda94dfa150c13fdeca
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert einen vorhandenen Tabellen- oder Sichtindex (relational oder XML), indem der Index deaktiviert, neu erstellt oder neu organisiert wird oder indem Optionen für den Index festgelegt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>Argumente  
 *index_name*  
 Der Name des Indexes. Indexnamen müssen für eine Tabelle oder Sicht eindeutig sein, können aber innerhalb einer Datenbank mehrfach vorkommen. Indexnamen müssen den Regeln der [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 ALL  
 Gibt alle Indizes an, die unabhängig vom Indextyp der Tabelle oder Sicht zugeordnet sind. Die Angabe von ALL verursacht bei der Anweisung einen Fehler, wenn mindestens ein Index in einer Offlinedateigruppe oder schreibgeschützten Dateigruppe enthalten ist oder der angegebene Vorgang für mindestens einen Indextyp nicht zulässig ist. In der folgenden Tabelle werden die Indexvorgänge und die nicht zulässigen Indextypen aufgelistet.  
  
|Mithilfe des Schlüsselworts ALL mit diesem Vorgang|Erzeugt einen Fehler, wenn mindestens einer dieser Indextypen in der Tabelle enthalten ist|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|XML-Index<br /><br /> Räumlicher Index<br /><br /> Columnstore-Index: **gilt für:** SQL Server (beginnend mit SQL Server 2012) und Azure SQL-Datenbank.|  
|REBUILD PARTITION = *Partitionsnummer*|Nicht partitionierter Index, XML-Index, räumlicher Index oder deaktivierter Index|  
|REORGANIZE|Indizes, für die ALLOW_PAGE_LOCKS auf OFF festgelegt wurde|  
|REORGANIZE PARTITION = *Partitionsnummer*|Nicht partitionierter Index, XML-Index, räumlicher Index oder deaktivierter Index|  
|IGNORE_DUP_KEY = ON|XML-Index<br /><br /> Räumlicher Index<br /><br /> Columnstore-Index: **gilt für:** SQL Server (beginnend mit SQL Server 2012) und Azure SQL-Datenbank.|  
|ONLINE = ON|XML-Index<br /><br /> Räumlicher Index<br /><br /> Columnstore-Index: **gilt für:** SQL Server (beginnend mit SQL Server 2012) und Azure SQL-Datenbank.|
| FORTSETZBARE = ON  | Fortsetzbare Indizes nicht unterstützt, mit **alle** Schlüsselwort. <br /><br /> **Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank |   
  
> [!WARNING]
>  Ausführlichere Informationen zu indexvorgängen, die online ausgeführt werden können, finden Sie unter [Richtlinien für Onlineindexvorgänge](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

 Bei Angabe von ALL mit PARTITION = *Partition_number*, müssen alle Indizes ausgerichtet sein. Das bedeutet, dass sie auf der Grundlage der entsprechenden Partitionsfunktionen partitioniert sind. Verwenden von ALL mit PARTITION führt dazu, dass alle Indexpartitionen mit demselben *Partition_number* neu erstellt oder neu organisiert werden. Weitere Informationen zu partitionierten Indizes finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehört.  
  
 *table_or_view_name*  
 Der Name der Tabelle oder Sicht, die dem Index zugeordnet ist. Um einen Bericht über die Indizes eines Objekts anzuzeigen, verwenden die [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
 SQL-Datenbank unterstützt drei Teilen bestehende Format Database_name. [Schema_name] .table_or_view_name Wenn Database_name die aktuelle Datenbank oder Database_name Tempdb und den Table_or_view_name beginnt mit #.  
  
 REBUILD [WITH **(**\<Rebuild_index_option > [ **,**... *n*]**)** ]  
 Gibt an, dass der Index mit denselben Spalten, demselben Indextyp, demselben Eindeutigkeitsattribut und derselben Sortierreihenfolge neu erstellt wird. Diese Klausel entspricht [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md). Mit REBUILD wird ein deaktivierter Index aktiviert. Durch das Neuerstellen eines gruppierten Indexes erfolgt nicht die Neuerstellung von zugeordneten nicht gruppierten Indizes, es sei denn, das Schlüsselwort ALL ist angegeben. Wenn Indexoptionen nicht angegeben werden, die vorhandenen Indexoptionen in gespeicherten [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) angewendet werden. Für alle Indexoptionen, deren Wert sich nicht in befindet **sys.indexes**, gilt die Standardeinstellung, die in der argumentdefinition der Option angegeben.  
  
 Wenn ALL angegeben ist und die zugrunde liegende Tabelle ein Heap ist, hat die Neuerstellung keine Auswirkungen auf die Tabelle. Alle nicht gruppierten Indizes, die der Tabelle zugeordnet sind, werden neu erstellt.  
  
 Der Neuerstellungsvorgang kann minimal protokolliert werden, wenn die Datenbankwiederherstellung auf das massenprotokollierte oder einfache Wiederherstellungsmodell festgelegt ist.  
  
> [!NOTE]
>  Wenn Sie einen primären XML-Index neu erstellen, ist die zugrunde liegende Benutzertabelle während des Indexvorgangs nicht verfügbar.  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2012) und Azure SQL-Datenbank.
  
 Für columnstore-Indizes, der Neuerstellungsvorgang:  
  
1.  Die Sortierreihenfolge wird nicht verwendet werden.  
  
2.  Abrufen einer exklusiven Sperre für die Tabelle oder Partition, während die Neuerstellung ausgeführt wird.  Die Daten sind während der Neuerstellung „offline“ und nicht verfügbar, sogar wenn Sie NOLOCK, RCSI oder SI verwenden.  
  
3.  Neukomprimierung aller Daten im Columnstore. Während die Neuerstellung ausgeführt wird, gibt es zwei Kopien des columnstore-Indexes. Nach Abschluss der Neuerstellung wird der ursprüngliche columnstore-Index in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht.  
  
 Weitere Informationen zu columnstore-Indizes neu erstellt werden, finden Sie unter [columnstore-Indizes - Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 Gibt an, dass nur eine Partition eines Indexes neu erstellt oder neu organisiert wird. PARTITION kann nicht angegeben werden, wenn *Index_name* ist kein partitionierter Index.  
  
 PARTITION = ALL erstellt alle Partitionen neu.  
  
> [!WARNING]
>  Das Erstellen bzw. Neuerstellen von nicht ausgerichteten Indizes für eine Tabelle mit mehr als 1.000 Partitionen ist möglich, wird aber nicht unterstützt. Dies hätte Leistungseinbußen oder eine zu hohe Speicherauslastung während der Vorgänge zur Folge. Es empfiehlt sich, bei mehr als 1.000 Partitionen nur ausgerichtete Indizes zu verwenden.  
  
 *Partitionsnummer*  
   
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.
  
 Die Partitionsnummer eines partitionierten Indexes, der neu erstellt oder neu organisiert werden soll. *Partitionsnummer* ist ein konstanter Ausdruck, die auf Variablen verweisen kann. Bei diesen Variablen kann es sich um Funktionen und benutzerdefinierte Variablen oder Funktionen handeln, die jedoch nicht auf eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung verweisen können. *Partitionsnummer* muss vorhanden sein, oder die Anweisung schlägt fehl.  
  
 MIT **(**\<Single_partition_rebuild_index_option >**)**  
   
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 SORT_IN_TEMPDB, MAXDOP und DATA_COMPRESSION sind die Optionen, die angegeben werden können, wenn Sie eine einzelne Partition neu erstellen (PARTITION =  *n* ). XML-Indizes können nicht bei der Neuerstellung einer einzelnen Partition angegeben werden.  
  
 DISABLE  
 Markiert den Index als deaktiviert und als nicht verfügbar für das [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Jeder Index kann deaktiviert werden. Die Indexdefinition eines deaktivierten Indexes bleibt weiterhin im Systemkatalog ohne zugrunde liegende Indexdaten bestehen. Durch das Deaktivieren eines gruppierten Indexes wird der Benutzerzugriff auf die zugrunde liegenden Tabellendaten verhindert. Verwenden Sie ALTER INDEX REBUILD oder CREATE INDEX WITH DROP_EXISTING, um einen Index zu aktivieren. Weitere Informationen finden Sie unter [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md) und [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
 Einen Rowstore-Index neu organisieren  
 Gibt an für Rowstore-Indizes neu organisieren der Blattebene des Indexes neu zu organisieren.  Der neuorganisationsvorgang wird:  
  
-   Immer online ausgeführt. Das bedeutet, dass blockierende Langzeitsperren für Tabellen nicht aufrechterhalten werden und Abfragen oder Updates der zugrunde liegenden Tabelle während der ALTER INDEX REORGANIZE-Transaktion fortgesetzt werden können.  
  
-   Für einen deaktivierten Index zulässig nicht.  
  
-   Nicht zulässig, wenn ALLOW_PAGE_LOCKS auf OFF festgelegt ist  
  
-   Nicht zurückgesetzt werden, wenn sie innerhalb einer Transaktions ausgeführt wird und die Transaktion zurückgesetzt wird.  
  
REORGANIZE MIT **(** LOB_COMPACTION = { **ON** | {OFF} **)**  
 Gilt für Rowstore-Indizes.  
  
LOB_COMPACTION = ON  
  
-   Gibt an, dass alle Seiten komprimiert, die Daten dieser Datentypen für große Objekte (LOB) enthalten: Image, Text, Ntext, varchar(max), nvarchar(max), varbinary(max) und Xml. Durch das Komprimieren dieser Daten kann Daten auf der Festplatte verkleinern.  
  
-   Für einen gruppierten Index komprimiert dies alle LOB-Spalten, die in der Tabelle enthalten sind.  
  
-   Für einen nicht gruppierten Index werden diese alle LOB-Spalten, die (eingeschlossene) Nichtschlüsselspalten im Index komprimiert.  
  
-   ALLE neu organisieren führt LOB_COMPACTION auf alle Indizes ein. Für jeden Index komprimiert dies alle LOB-Spalten im gruppierten Index, in der zugrunde liegenden Tabelle oder eingeschlossene Spalten in einem nicht gruppierten Index.  
  
LOB_COMPACTION = OFF  
  
-   Seiten, die LOB-Daten enthalten, werden nicht komprimiert.  
  
-   Die Einstellung OFF hat keine Auswirkungen auf einen Heap.  
  
Einen columnstore-Index neu organisieren  
REORGANIZE ist online durchgeführt.  
  
Für columnstore-Indizes komprimiert REORGANIZE jede GESCHLOSSENEN Delta-Zeilengruppe im Columnstore als eine komprimierte Zeilengruppe.  
  
-   REORGANIZE ist nicht erforderlich, um die GESCHLOSSENEN Delta-Zeilengruppen in komprimierte Zeilengruppen verschoben. Der Hintergrund (TM) tupelverschiebungsvorgang reaktiviert, in regelmäßigen Abständen GESCHLOSSENEN Delta-Zeilengruppen zu komprimieren. Es wird empfohlen, REORGANIZE verwenden, wenn Tuple Mover im Rückstand ist. REORGANIZE kann Zeilengruppen genauer komprimieren.  
  
-   Um alle öffnen "und" CLOSED-Zeilengruppen zu komprimieren, finden Sie unter der Option REORGANIZE mit (COMPRESS_ALL_ROW_GROUPS) in diesem Abschnitt.  
  
Für columnstore-Indizes in SQL Server (ab 2016) und SQL-Datenbank führt REORGANIZE online die folgende zusätzliche Defragmentierung-Optimierungen:  
  
-   Physisch entfernt Zeilen aus einer Zeilengruppe, wenn mindestens 10 % der Zeilen logisch gelöscht wurden. Die gelöschten Bytes werden auf dem physischen Medium freigegeben. Beispielsweise verfügt eine komprimierte Zeilengruppe mit 1 Million Zeilen 100 KB Zeilen gelöscht, SQL Server die gelöschten Zeilen zu entfernen und komprimieren die Zeilengruppe mit 900 k-Zeilen. Er speichert im Speicher durch Entfernen von gelöschten Zeilen.  
  
-   Kombiniert einen oder mehrere komprimierte Zeilengruppen, um Zeilen pro Zeilengruppe das Maximum von 1,024,576 Zeilen zu erhöhen. Z. B. Wenn Sie einen Massenexport 5 Batches von 102.400 Zeilen importieren erhalten Sie 5 komprimierte Zeilengruppen. Wenn Sie die REORGANIZE ausführen, werden diese Zeilengruppen in 1 komprimierte Zeilengruppe Größe 512,000 Zeilen zusammengeführt abrufen. Dies setzt voraus, dass es kein Wörterbuch Größe oder zu speicherbeschränkungen waren.  
  
-   Bei Zeilengruppen, in denen mindestens 10 % der Zeilen logisch gelöscht wurden, versucht SQL Server, die dieser Zeilengruppe mit ein oder mehrere Zeilengruppen zu kombinieren.    Beispielsweise Zeilengruppe 1 mit 500.000 Zeilen komprimiert wird und Zeilengruppe 21 mit dem Maximum von 1.048.576 Zeilen komprimiert wird.  Zeilengruppe 21 hat 60 % der Zeilen gelöscht 409,830 Zeilen zu verwerfen. SQL Server wird bevorzugt, kombinieren diese zwei Zeilengruppen, um eine neue Zeilengruppe zu komprimieren, die 909,830 Zeilen enthält.  
  
MIT NEU ORGANISIEREN (COMPRESS_ALL_ROW_GROUPS = {ON | **OFF** })  
 In SQL Server (ab 2016) und SQL-Datenbank bietet die COMPRESS_ALL_ROW_GROUPS eine Möglichkeit zum Öffnen oder CLOSED Delta-Zeilengruppen in den Columnstore zu zwingen. Mit dieser Option ist es nicht notwendig, um die Delta-Zeilengruppen zu leeren der columnstore-Index neu.  In Kombination mit dem anderen entfernen und Merge Defragmentierung Funktionen wird nicht mehr notwendig, dass der Index in den meisten Situationen neu erstellt.    
-   ON erzwingt, dass alle Zeilengruppen in den Columnstore, unabhängig von der Größe und Status (geschlossen oder geöffnet).  
  
-   Erzwingt die deaktiviert alle CLOSED-Zeilengruppen in den Columnstore.  
  
Legen Sie **(** \<Set_index Option > [ **,**... *n*] **)**  
 Gibt Indexoptionen ohne das Neuerstellen oder Neuorganisieren des Indexes an. SET kann für einen deaktivierten Index nicht angegeben werden.  
  
PAD_INDEX = { ON | OFF }  
   
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 ON  
 Der Prozentsatz des mit FILLFACTOR angegebenen freien Speicherplatzes wird für die Zwischenebenenseiten des Indexes angewendet. Wenn FILLFACTOR nicht angegeben wird zur gleichen Zeit PAD_INDEX auf ON festgelegt ist, die gespeicherte Füllfaktorwert [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) verwendet wird.  
  
 Deaktivieren oder *Fillfactor* ist nicht angegeben.  
 Die Zwischenebenenseiten werden nahezu vollständig gefüllt. Dabei bleibt genügend Platz für mindestens eine Zeile der maximal zulässigen Größe eines Indexes erhalten. Dies erfolgt auf der Grundlage des Schlüsselsatzes in den Zwischenseiten.  
  
 Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
FILLFACTOR = *Fillfactor*  
 
 **Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.
  
 Gibt einen Prozentwert an, der dem Füllfaktor entspricht. Dieser Faktor legt fest, wie weit die [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung auffüllen soll.  *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0. Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
 Eine explizite FILLFACTOR-Einstellung gilt nur bei der erstmaligen Erstellung oder bei der Neuerstellung des Indexes. [!INCLUDE[ssDE](../../includes/ssde-md.md)] hält den angegebenen Prozentsatz des Speicherplatzes nicht dynamisch auf den Seiten frei. Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 Verwenden Sie zum Anzeigen der füllfaktoreinstellung **sys.indexes**.  
  
> [!IMPORTANT]
>  Das Erstellen oder Ändern eines gruppierten Indexes mit einem FILLFACTOR-Wert wirkt sich auf den Speicherplatz aus, den die Daten belegen, da das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Daten beim Erstellen des gruppierten Indexes neu verteilt.  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 

**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 Gibt an, ob zum Speichern der Ergebnisse des Sortierens in **Tempdb**. Der Standardwert ist OFF.  
  
 ON  
 Die Zwischenergebnisse, die zum Erstellen des Indexes verwendet werden, sind in gespeicherten **Tempdb**. Wenn **Tempdb** wird auf einem anderen Datenträgersatz befindet als die Benutzerdatenbank, kann dies die Zeit zum Erstellen eines Indexes reduzieren. Sie erhöht jedoch den Betrag an Speicherplatz, der während der Indexerstellung verwendet wird.  
  
 OFF  
 Die Zwischenergebnisse der Sortierung werden in derselben Datenbank gespeichert wie der Index.  
  
 Wenn kein Sortierungsvorgang erforderlich ist oder wenn die Sortierung im Arbeitsspeicher ausgeführt werden kann, wird die SORT_IN_TEMPDB-Option ignoriert.  
  
 Weitere Informationen finden Sie unter [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY  **=**  {ON | {OFF}  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Der Standardwert ist OFF.  
  
 ON  
 Eine Warnmeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Es schlagen nur die Zeilen fehl, die gegen die Eindeutigkeitseinschränkung verstoßen.  
  
 OFF  
 Eine Fehlermeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Für den gesamten INSERT-Vorgang wird ein Rollback ausgeführt.  
  
 IGNORE_DUP_KEY kann für Indizes, die für eine Sicht erstellt, nicht eindeutige Indizes, XML-Indizes, räumlichen Indizes und gefilterte Indizes auf ON festgelegt werden.  
  
 Um IGNORE_DUP_KEY anzuzeigen, verwenden Sie [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 In abwärtskompatibler Syntax ist WITH IGNORE_DUP_KEY gleichwertig mit WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | {OFF}  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ON  
 Veraltete Indexstatistiken werden nicht automatisch neu berechnet.  
  
 OFF  
 Die automatischen Updates der Statistiken sind aktiviert.  
  
 Um das automatische Aktualisieren von Statistiken wiederherzustellen, müssen Sie STATISTICS_NORECOMPUTE auf OFF festlegen oder die UPDATE STATISTICS-Anweisung ohne die NORECOMPUTE-Klausel ausführen.  
  
> [!IMPORTANT]
>  Wenn Sie die automatische Neuberechnung von Verteilungsstatistiken deaktivieren, wählt der Abfrageoptimierer möglicherweise nicht die optimalen Ausführungspläne für Abfragen, an denen die Tabelle beteiligt ist.  
  
 STATISTICS_INCREMENTAL = {ON | **OFF** }  
 Wenn **ON**, die Statistiken erstellt werden, pro Partition. Wenn **OFF**, wird die statistikstruktur gelöscht und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Statistiken neu berechnet. Die Standardeinstellung ist **OFF**.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird die Option ignoriert und eine Warnung generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
-   Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
  
-   Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
  
-   Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
  
-   Statistiken, die für gefilterte Indizes erstellt wurden.  
  
-   Statistiken, die für Sichten erstellt wurden.  
  
-   Statistiken, die für interne Tabellen erstellt wurden.  
  
-   Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
 
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.  
  
 ONLINE  **=**  {ON | **OFF** } \<wie für Rebuild_index_option >  
 Gibt an, ob die zugrunde liegenden Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF.  
  
 Bei XML-Indizes oder räumlichen Indizes wird nur ONLINE = OFF unterstützt, und wenn ONLINE auf ON festgelegt wird, wird ein Fehler ausgelöst.  
  
> [!NOTE]
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Während der Hauptphase des Indexvorgangs wird nur eine beabsichtigte freigegebene Sperre (IS) für die Quelltabelle aufrechterhalten. Auf diese Weise können Abfragen oder Updates der zugrunde liegenden Tabelle und Indizes fortgesetzt werden. Zu Beginn des Vorgangs wird das Quellobjekt für sehr kurze Zeit mit einer gemeinsamen Sperre (S) belegt. Am Ende des Vorgangs wird für kurze Zeit eine S-Sperre für die Quelle eingerichtet, wenn ein nicht gruppierter Index erstellt wird, oder es wird eine Sch-M-Sperre (Schema Modification, Schemaänderung) eingerichtet, wenn ein gruppierter Index online erstellt oder gelöscht wird oder wenn ein gruppierter oder nicht gruppierter Index neu erstellt wird. ONLINE kann nicht auf ON festgelegt werden, wenn ein Index auf einer lokalen temporären Tabelle erstellt wird.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Ein Offlineindexvorgang, durch den ein gruppierter, räumlicher oder XML-Index erstellt, neu erstellt oder gelöscht wird bzw. ein nicht gruppierter Index neu erstellt oder gelöscht wird, aktiviert eine Sch-M-Sperre für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können. Ein Offlineindexvorgang, bei dem ein nicht gruppierter Index erstellt wird, aktiviert eine freigegebene Sperre (S) für die Tabelle. Dadurch werden Updates der zugrunde liegenden Tabelle verhindert. Lesevorgänge, wie SELECT-Anweisungen, sind jedoch zulässig.  
  
 Weitere Informationen finden Sie unter [wie Onlineindexvorgängen](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Indizes, einschließlich Indizes globaler temporärer Tabellen, können online neu erstellt werden, mit Ausnahme von:  
  
-   XML-Indizes  
  
-   Indizes für lokale temporäre Tabellen  
  
-   Eine Teilmenge eines partitionierten Indexes (ein vollständiger partitionierter Index kann online neu erstellt werden).  

-  SQL-Datenbank vor V12 und SQL Server vor SQL Server 2012, lässt nicht die `ONLINE` option für den gruppierten Index erstellen oder Vorgänge neu zu erstellen, wenn die Basistabelle enthält **varchar(max)** oder **varbinary(max)**  Spalten.

FORTSETZBARE  **=**  {ON | **OFF**}

**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank   

 Gibt an, ob ein Onlineindexvorgang kann wieder aufgenommen wird.

 Index ist der Vorgang fortgesetzt werden können.

 DEAKTIVIERT den Index ist der Vorgang nicht fortgesetzt werden können.

MAX_DURATION  **=**  *Zeit* [**Minuten**] mit verwendet **kann wieder aufgenommen werden = ON** (erfordert **ONLINE = ON**).
 
**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank 

Gibt die Zeit (ein Integerwert in Minuten angegeben), dass eine fortsetzbar online-Vorgang Index werden ausgeführt, bevor er angehalten wurde. 

ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Zeilensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.  
  
 OFF  
 Zeilensperren werden nicht verwendet.  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.
  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Seitensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.  
  
 OFF  
 Seitensperren werden nicht verwendet.  
  
> [!NOTE]
>  Ein Index kann nicht neu organisiert werden, wenn ALLOW_PAGE_LOCKS auf OFF festgelegt ist.  
  
 MAXDOP  **=**  Max_degree_of_parallelism  
 
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption für die Dauer des Indexvorgangs. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
> [!IMPORTANT]
>  Obwohl die MAXDOP-Option syntaktisch für alle XML-Indizes unterstützt wird, verwendet ALTER INDEX gegenwärtig für einen räumlichen Index oder einen primären XML-Index nur einen einzelnen Prozessor.  
  
 *Max_degree_of_parallelism* sind möglich:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Begrenzt die Höchstzahl von Prozessoren in einem parallelen Indexvorgang auf die angegebene Zahl  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]
>  Parallele Indexvorgänge sind nicht verfügbar in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 COMPRESSION_DELAY  **=**  { **0** |*Dauer [Minuten]* }  
 Dieses Feature steht ab SQL Server 2016  
  
 Verzögerung gibt die minimale Anzahl von Minuten an, die eine Delta-Zeilengruppen in den GESCHLOSSENEN Zustand verbleiben muss für eine datenträgerbasierte Tabelle in der deltazeilengruppe, vor SQL Server in der komprimierten Zeilengruppe komprimiert werden können. Da es sich bei datenträgerbasierten Tabellen nicht nachverfolgen einfügen und aktualisieren Zeiten für einzelne Zeilen, SQL Server gilt die Verzögerung in Delta-Zeilengruppen in den GESCHLOSSENEN Zustand übergeht.  
Der Standardwert beträgt 0 Minuten.  
  
 Der Standardwert beträgt 0 Minuten.  
  
 Für Empfehlungen dazu, wann COMPRESSION_DELAY verwenden, finden Sie unter columnstore-Indizes für die operative Analyse in Echtzeit.  
  
 DATA_COMPRESSION  
 Gibt die Datenkomprimierungsoption für den angegebenen Index, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
  
 Keine  
 Der Index oder die angegebenen Partitionen werden nicht komprimiert. Gilt nicht für columnstore-Indizes.  
  
 ROW  
 Der Index oder die angegebenen Partitionen werden mit Zeilenkomprimierung komprimiert. Gilt nicht für columnstore-Indizes.  
  
 PAGE  
 Der Index oder die angegebenen Partitionen werden mit Seitenkomprimierung komprimiert. Gilt nicht für columnstore-Indizes.  
  
 COLUMNSTORE  
   
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.
  
 Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. COLUMNSTORE gibt an, dass der Index oder angegebene Partitionen, die mit der COLUMNSTORE_ARCHIVE-Option komprimiert wurden, dekomprimiert werden sollen. Nachdem die Daten wiederhergestellt wurden, sind sie weiterhin mit der columnstore-Komprimierung komprimiert, die für alle columnstore-Indizes verwendet wird.  
  
 COLUMNSTORE_ARCHIVE  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.
  
 Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. Durch COLUMNSTORE_ARCHIVE wird die angegebene Partition weiter in eine geringere Größe komprimiert. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speichergröße und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
 Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 AUF PARTITIONEN **(** { \<Partition_number_expression > | \<Bereich >} [**,**... n] **)**  
    
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank. 
  
 Gibt die Partitionen an, für die die DATA_COMPRESSION-Einstellung gilt. Wenn der Index nicht partitioniert ist, erzeugt das ON PARTITIONS-Argument einen Fehler. Wenn die ON PARTITIONS-Klausel nicht angegeben wird, gilt die DATA_COMPRESSION-Option für alle Partitionen eines partitionierten Indexes.  
  
 \<Partition_number_expression > kann auf folgende Weise angegeben werden:  
  
-   Geben Sie die Nummer der Partition an, beispielsweise: ON PARTITIONS (2).  
  
-   Geben Sie die Partitionsnummern mehrerer einzelner Partitionen durch Trennzeichen getrennt an, beispielsweise: ON PARTITIONS (1, 5).  
  
-   Geben Sie sowohl Bereiche als auch einzelne Partitionen an: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<Range > können durch das Wort TO, z. B. getrennte Partitionsnummern angegeben werden: ON PARTITIONS (6 TO 8).  
  
 Wenn Sie für verschiedene Partitionen unterschiedliche Datenkomprimierungstypen festlegen möchten, geben Sie die Option DATA_COMPRESSION mehrmals an, beispielsweise:  
  
```tsql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 ONLINE  **=**  {ON | **OFF** } \<wie für Single_partition_rebuild_index_option >  
 Gibt an, ob ein Index oder eine Indexpartition einer zugrunde liegenden Tabelle online oder offline neu erstellt werden kann. Wenn **REBUILD** online ausgeführt wird (**ON**) die Daten in dieser Tabelle sind für Abfragen und datenänderungen während des Indexvorgangs verfügbar.  Die Standardeinstellung ist **OFF**.  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Während der Hauptphase des Indexvorgangs wird nur eine beabsichtigte freigegebene Sperre (IS) für die Quelltabelle aufrechterhalten. Eine S-Sperre für die Tabelle ist am Anfang der indexneuerstellung und eine Sch-M-Sperre für die Tabelle am Ende der online-indexneuerstellung erforderlich. Obwohl beide Sperren kurze Metadatensperren sind, muss insbesondere die Sch-M-Sperre auf den Abschluss aller blockierenden Transaktionen warten. Während der Wartezeit sperrt die Sch-M-Sperre alle anderen Transaktionen, die an dieser Sperre warten, wenn sie auf die gleiche Tabelle zugreifen.  
  
> [!NOTE]
>  Neuerstellung von Onlineindizes kann festlegen, die *Low_priority_lock_wait* weiter unten in diesem Abschnitt beschriebenen Optionen.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können.  
  
 WAIT_AT_LOW_PRIORITY mit verwendet **ONLINE = ON** nur.  
 
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.
  
 Bei der Onlineindexneuerstellung muss auf blockierende Vorgänge für diese Tabelle gewartet werden. **WAIT_AT_LOW_PRIORITY** gibt an, dass der Vorgang zur onlineindexneuerstellung Sperren mit niedriger Priorität, sodass andere Vorgänge, während die onlineindexerstellung wartet gewartet wird. Das Weglassen der **WAIT AT LOW PRIORITY** -Option ist gleichwertig mit `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Weitere Informationen finden Sie unter [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 
  
 MAX_DURATION = *Zeit* [**Minuten**]  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.
  
 Die Wartezeit (ein ganzzahliger Wert in Minuten), während der die Sperren der Onlineindexneuerstellung mit niedriger Priorität warten, wenn der DDL-Befehl ausgeführt wird. Wenn der Vorgang blockiert wird die **MAX_DURATION** Zeit, eines der **ABORT_AFTER_WAIT** -Aktionen ausgeführt. **MAX_DURATION** ist immer in Minuten, und das Wort **Minuten** kann ausgelassen werden.  
 
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERN** }]  
   
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.
  
 Keine  
 Es wird weiterhin mit normaler (regulärer) Priorität auf die Sperre gewartet.  
  
 SELF  
 Beendet den DDL-Vorgang zur Onlineindexneuerstellung, der derzeit ausgeführt wird, ohne weitere Aktionen auszuführen.  
  
 BLOCKERS  
 Bricht alle Benutzertransaktionen ab, die den DDL-Vorgang zur Onlineindexneuerstellung blockieren, sodass der Vorgang fortgesetzt werden kann. Die **BLOCKERN** Option erfordert die Anmeldung **ALTER ANY CONNECTION** Berechtigung.  
 
 RESUME 
 
**Gilt für**: ab SQLServer 2017  

Fortsetzen eines Indexvorgangs, das manuell oder aufgrund eines Fehlers angehalten wurde.

Mit MAX_DURATION verwendet **kann wieder aufgenommen werden = ON**

 
**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank

Die Zeit (ein ganzzahliger Wert, der in Minuten angegeben ist) die fortsetzbar Onlineindexvorgang wird ausgeführt, nachdem das wieder aufgenommen wird. Nach Ablauf dieses Zeitraums ist fortsetzbare Vorgang angehalten, wenn er immer noch ausgeführt wird.

WAIT_AT_LOW_PRIORITY mit verwendet **kann wieder aufgenommen werden = ON** und **ONLINE = ON**.  
  
**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank 
  
 Eine online-indexneuerstellung wird fortgesetzt, nachdem eine Pause auf blockierende Vorgänge für diese Tabelle gewartet hat. **WAIT_AT_LOW_PRIORITY** gibt an, dass der Vorgang zur onlineindexneuerstellung Sperren mit niedriger Priorität, sodass andere Vorgänge, während die onlineindexerstellung wartet gewartet wird. Das Weglassen der **WAIT AT LOW PRIORITY** -Option ist gleichwertig mit `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Weitere Informationen finden Sie unter [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 


ANHALTEN
 
**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank 
  
Anhalten eines fortsetzbar Vorgangs zur onlineindexneuerstellung an.

ABBRECHEN

**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank   

Abbrechen eines ausgeführten oder angehaltenen Indexvorgangs, der als fortsetzbar deklariert wurde. Müssen Sie explizit ausführen, eine **ABORT** -Neuerstellungsvorgang von Befehl zum Beenden eines Indexes kann wieder aufgenommen. Fehler oder einen fortsetzbaren Indexvorgang Anhalten wird nicht seine Ausführung beendet; Stattdessen bewirkt, dass sie den Vorgang unbestimmtes anhalten.
  
## <a name="remarks"></a>Hinweise  
 ALTER INDEX kann nicht verwendet werden, um einen Index neu zu partitionieren oder ihn in eine andere Dateigruppe zu verschieben. Diese Anweisung kann nicht verwendet werden, um die Indexdefinition, wie z. B. das Hinzufügen oder Löschen von Spalten oder das Ändern der Spaltenreihenfolge, zu ändern. Verwenden Sie CREATE INDEX mit der DROP_EXISTING-Klausel zum Ausführen dieser Vorgänge.  
  
 Wenn eine Option nicht explizit angegeben ist, wird die aktuelle Einstellung angewendet. Wenn in der REBUILD-Klausel beispielsweise keine FILLFACTOR-Einstellung angegeben ist, wird der im Systemkatalog gespeicherte Füllfaktorwert während der Neuerstellung verwendet. Verwenden Sie zum Anzeigen der aktuellen indexoptionseinstellungen [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!NOTE]
>  Die Werte für ONLINE, MAXDOP und SORT_IN_TEMPDB werden nicht im Systemkatalog gespeichert. Der Standardwert der Option wird verwendet, sofern die Option nicht in der Indexanweisung angegeben ist.
  
 Auf Mehrprozessorcomputern werden für ALTER INDEX REBUILD wie bei allen anderen Abfragen automatisch mehr Prozessoren verwendet, um bei Indexänderungen Scan- und Sortierungsvorgänge auszuführen. Wenn Sie ALTER INDEX REORGANIZE, mit oder ohne LOB_COMPACTION Ausführen der **Max. Grad an Parallelität** Wert ist einem einzelnen Threadvorgang. Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 Ein Index kann nicht neu organisiert oder neu erstellt werden, wenn die Dateigruppe, in der er enthalten ist, eine Offline- oder schreibgeschützte Dateigruppe ist. Wenn das Schlüsselwort ALL angegeben ist und mindestens ein Index in einer Offline- oder schreibgeschützten Dateigruppe enthalten ist, erzeugt die Anweisung einen Fehler.  
  
## <a name="rebuilding-indexes"></a>Neuerstellen von Indizes  
 Beim Neuerstellen eines Indexes wird der Index gelöscht und neu erstellt. Bei diesem Vorgang wird die Fragmentierung entfernt, Speicherplatz wird freigegeben, indem die Seiten auf der Grundlage der angegebenen oder vorhandenen Füllfaktoreinstellung komprimiert werden, und die Indexzeilen werden in aufeinanderfolgenden Seiten neu geordnet. Wenn ALL angegeben ist, werden alle Indizes der Tabelle in einer einzelnen Transaktion gelöscht und neu erstellt. FOREIGN KEY-Einschränkungen müssen nicht im Voraus gelöscht werden. Wenn Indizes mit mindestens 128 Blöcken neu erstellt werden, verzögert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die tatsächlichen aufgehobenen Seitenzuordnungen sowie deren zugeordnete Sperren, bis für die Transaktion ein Commit ausgeführt wird.  
  
 Durch das erneute Erstellen oder Organisieren kleiner Indizes lässt sich die Fragmentierung häufig nicht verringern. Die Seiten kleiner Indizes werden manchmal in gemischten Blöcken gespeichert. Da gemischte Blöcke von bis zu acht Objekten gemeinsam genutzt werden, lässt sich die Fragmentierung in einem kleinen Index durch die erneute Erstellung oder Organisation des Indexes möglicherweise nicht verringern.  
  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]werden Statistiken nicht durch das Scannen aller Zeilen in der Tabelle erstellt, wenn ein partitionierter Index erstellt oder neu erstellt wird. Der Abfrageoptimierer generiert stattdessen Statistiken mithilfe des Standardalgorithmus zur Stichprobenentnahme. Um Statistiken zu partitionierten Indizes durch das Scannen aller Zeilen in der Tabelle abzurufen, verwenden Sie CREATE STATISTICS oder UPDATE STATISTICS mit der FULLSCAN-Klausel.  
  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konnte in einigen Fällen ein nicht gruppierter Index neu erstellt werden, um durch Hardwarefehler verursachte Inkonsistenzen zu korrigieren. Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sind Sie u. U. weiterhin in der Lage, derartige Inkonsistenzen zwischen dem Index und dem gruppierten Index zu beheben, indem Sie einen nicht gruppierten Index offline erstellen. Sie können die Inkonsistenzen eines nicht gruppierten Indexes jedoch nicht beheben, indem Sie den Index online neu erstellen, da der Onlineneuerstellungsmechanismus den vorhandenen nicht gruppierten Index als Grundlage für die Neuerstellung verwendet und somit die Inkonsistenzen bestehen bleiben. Wird der Index offline neu erstellt, wird in manchen Fällen ein Scan des gruppierten Indexes (oder Heaps) erzwungen. um dadurch Inkonsistenzen zu entfernen. Um eine Neuerstellung des gruppierten Indexes zu gewährleisten, löschen Sie den nicht gruppierten Index und erstellen Sie ihn neu. Wie in früheren Versionen wird zum Entfernen von Inkonsistenzen empfohlenen, die betroffenen Daten aus einer Sicherung wiederherzustellen. Die Inkonsistenzen des Indexes können möglicherweise auch behoben werden, indem der nicht gruppierte Index offline neu erstellt wird. Weitere Informationen finden Sie unter [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
 Die Neuerstellung eines gruppierten columnstore-Indexes verläuft in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wie folgt:  
  
1.  Abrufen einer exklusiven Sperre für die Tabelle oder Partition, während die Neuerstellung ausgeführt wird. Die Daten sind während der Neuerstellung "offline" und nicht verfügbar.  
  
2.  Defragmentieren des Columnstore, indem physisch Zeilen gelöscht werden, die logisch aus der Tabelle gelöscht wurden. Die gelöschten Bytes werden auf dem physischen Medium freigegeben.  
  
3.  Liest alle Daten aus dem ursprünglichen Columnstore-Index, einschließlich des Deltastore. Die Daten werden in neuen Zeilengruppen zusammengefasst, und die Zeilengruppen werden in den Columnstore-Index komprimiert.  
  
4.  Auf dem physischen Medium muss ausreichend freier Speicherplatz zur Verfügung stehen, um während der Neuerstellung zwei Kopien des Columnstore-Indexes speichern zu können. Nach Abschluss der Neuerstellung wird der ursprüngliche gruppierte Columnstore-Index von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht.  
  
## <a name="reorganizing-indexes"></a>Neuorganisieren von Indizes  
 Das Neuorganisieren eines Indexes beansprucht minimale Systemressourcen. Dabei wird die Blattebene von gruppierten und nicht gruppierten Indizes in Tabellen und Sichten defragmentiert, indem die Blattebenenseiten physisch neu geordnet werden, damit sie mit der logischen Reihenfolge der Blattknoten von links nach rechts übereinstimmen. Durch das Neuorganisieren werden die Indexseiten auch komprimiert. Die Komprimierung basiert auf dem vorhandenen Füllfaktorwert. Verwenden Sie zum Anzeigen der füllfaktoreinstellung [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Wenn ALL angegeben ist,  werden relationale Indizes, sowohl gruppierte als auch nicht gruppierte, und XML-Indizes der Tabelle neu organisiert. Bei Angabe von ALL gelten einige Einschränkungen; diese finden Sie in der Definition zu ALL im Abschnitt "Argumente".  
  
 Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="disabling-indexes"></a>Deaktivieren von Indizes  
 Durch das Deaktivieren eines Indexes wird der Benutzerzugriff auf den Index sowie auf die zugrunde liegenden Tabellendaten gruppierter Indizes verhindert. Die Indexdefinition bleibt im Systemkatalog erhalten. Beim Deaktivieren eines nicht gruppierten oder gruppierten Indexes in einer Sicht werden die Indexdaten physisch gelöscht. Durch das Deaktivieren eines gruppierten Indexes wird der Benutzerzugriff auf die Daten verhindert; die Daten bleiben jedoch in der B-Struktur unverwaltet, bis der Index gelöscht oder neu erstellt wird. Um den Status eines aktivierten oder deaktivierten Indexes anzuzeigen, Fragen den **Is_disabled** Spalte in der **sys.indexes** -Katalogsicht angezeigt.  
  
 Befindet sich eine Tabelle in einer Transaktionsreplikationsveröffentlichung, können die Indizes, die mit Primärschlüsselspalten verknüpft sind, nicht deaktiviert werden, weil diese Indizes von der Replikation benötigt werden. Wenn Sie einen Index deaktivieren möchten, müssen Sie zuerst die Tabelle aus der Veröffentlichung löschen. Weitere Informationen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Verwenden Sie die ALTER INDEX REBUILD-Anweisung oder die CREATE INDEX WITH DROP_EXISTING-Anweisung, um den Index zu aktivieren. Das Neuerstellen eines deaktivierten gruppierten Indexes kann nicht durchgeführt werden, wenn die ONLINE-Option auf ON festgelegt ist. Weitere Informationen finden Sie unter [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
## <a name="setting-options"></a>Festlegen von Optionen  
 Sie können die Optionen ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY und STATISTICS_NORECOMPUTE für einen angegebenen Index festlegen, ohne den Index neu zu erstellen oder zu organisieren. Die geänderten Werte werden sofort auf den Index angewendet. Verwenden Sie zum Anzeigen dieser Einstellungen **sys.indexes**. Weitere Informationen finden Sie unter [Festlegen von Indexoptionen](../../relational-databases/indexes/set-index-options.md).  
  
### <a name="row-and-page-locks-options"></a>Zeilen- und Seitensperren (Optionen)  
 Wenn ALLOW_ROW_LOCKS und ALLOW_PAGE_LOCK auf ON festgelegt sind, sind Sperren auf Zeilen-, Seiten- und Tabellenebene beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] wählt die geeignete Sperre aus und kann die Sperre von einer Zeilen- oder Seitensperre auf eine Tabellensperre ausweiten.  
  
 Wenn ALLOW_ROW_LOCKS auf OFF und ALLOW_PAGE_LOCK auf OFF festgelegt sind, sind beim Zugriff auf den Index nur Sperren auf Tabellenebene zulässig.  
  
 Wenn beim Festlegen der Optionen für Zeilen- oder Seitensperren ALL angegeben ist, werden die Einstellungen auf alle Indizes angewendet. Wenn es sich bei der zugrunde liegenden Tabelle um einen Heap handelt, werden die Einstellungen folgendermaßen angewendet:  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON oder OFF|Für den Heap und alle zugeordneten nicht gruppierten Indizes.|  
|ALLOW_PAGE_LOCKS = ON|Für den Heap und alle zugeordneten nicht gruppierten Indizes.|  
|ALLOW_PAGE_LOCKS = OFF|Vollständig für die nicht gruppierten Indizes. Dies bedeutet, dass für die nicht gruppierten Indizes keine Seitensperren zulässig sind. Beim Heap sind nur gemeinsame Sperren (S, Shared), Updatesperren (U, Update) und exklusive Sperren (X, Exclusive) für die Seite unzulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann weiterhin eine beabsichtigte Seitensperre (IS, IU oder IX) für interne Zwecke abrufen.|  
  
## <a name="online-index-operations"></a>Onlineindexvorgänge  
 Wenn Sie einen Index neu erstellen, und die ONLINE-Option ist auf ON festgelegt, sind die zugrunde liegenden Objekte, die Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen verfügbar. Sie können auch einen Teil eines Indexes online neu erstellen, der sich in einer einzelnen Partition befindet. Exklusive Tabellensperren werden während des Änderungsprozesses nur für einen kurzen Zeitraum aufrechterhalten.  
  
 Das Neuorganisieren eines Indexes wird stets online durchgeführt. Bei dem Prozess werden Sperren nicht dauerhaft aufrechterhalten; daher werden Abfragen oder Updates, die ausgeführt werden, nicht blockiert.  
  
 Gleichzeitige Onlineindexvorgänge können in derselben Tabelle oder Tabellenpartition nur bei den folgenden Aktionen ausgeführt werden:  
  
-   Erstellen mehrerer nicht gruppierter Indizes.  
  
-   Neuorganisieren unterschiedlicher Indizes in derselben Tabelle.  
  
-   Neuorganisieren unterschiedlicher Indizes während der Neuerstellung von nicht überlappenden Indizes derselben Tabelle.  
  
 Alle anderen gleichzeitig durchgeführten Onlineindexvorgänge erzeugen einen Fehler. Sie können beispielsweise nicht zwei oder mehr Indizes zur gleichen Zeit für dieselbe Tabelle neu erstellen bzw. beim Neuerstellen eines vorhandenen Indexes keinen neuen Index für dieselbe Tabelle erstellen.  

### <a name="resumable-index-operations"></a>Fortsetzbare Indexvorgänge

**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank 

ONLINE INDEX REBUILD angegeben ist, als fortsetzbar mithilfe der kann wieder aufgenommen werden = Option. 
-  Die FORTSETZBARE Option wird nicht in den Metadaten für einen bestimmten Index beibehalten und gelten nur für die Dauer der aktuellen DDL-Anweisung. Aus diesem Grund die ANWENDUNGSUNABHÄNGIG = ON-Klausel muss explizit angegeben werden, um Resumability zu aktivieren.

-  Beachten Sie zwei verschiedene MAX_DURATION-Optionen an. Eine bezieht sich auf Low_priority_lock_wait und die andere bezieht sich auf kann wieder aufgenommen werden = Option.
   -  MAX_DURATION-Option wird für kann wieder aufgenommen werden unterstützt = Option oder der **Low_priority_lock_wait** Argument-Option. 
   MAX_DURATION für FORTSETZBAR Option gibt das Zeitintervall für einen Index neu erstellen. Sobald dieser verwendet wird, wenn der indexneuerstellung entweder angehalten wurde, oder es wird deren Ausführung beendet. Benutzer entscheidet sich, wenn eine Wiederherstellung für einen angehaltenen Index fortgesetzt werden kann. Die **Zeit** in Minuten für MAX_DURATION muss größere als 0 Minuten und kleiner oder gleich einer Woche (7 x 24 x 60 = 10080 Minuten) sein. Mit einer langen Pause für einen Indexvorgang möglicherweise die DML-Leistung beeinträchtigen auf eine bestimmte Tabelle als auch die Datenträgerkapazität Datenbank, da beide Indizes ursprünglichen Zeichensatz und die neu erstellte eine erfordern, Speicherplatz und müssen aktualisiert werden, während DML-Vorgänge. Wenn MAX_DURATION-Option nicht angegeben ist, wird der Indexvorgang fortgesetzt, bis dessen Abschluss oder bis ein Fehler auftritt. 
-   Die \<Low_priority_lock_wait >-Argument-Option können Sie entscheiden, wie der Index-Vorgang fortgesetzt werden kann, wenn auf die SCH-M-Sperre blockiert.
 
-  Die ursprüngliche ALTER INDEX REBUILD-Anweisung mit den gleichen Parametern erneut ausführen, wird eine angehaltene indexneuerstellungsvorgangs fortgesetzt. Sie können auch einen angehaltenen indexneuerstellungsvorgangs fortsetzen, durch Ausführen der Anweisung ALTER INDEX fortsetzen.
-  Die SORT_IN_TEMPDB = ON Option wird für fortsetzbar Index nicht unterstützt. 
-  Der DDL-Befehl mit kann wieder aufgenommen werden = ON kann nicht innerhalb einer expliziten Transaktion ausgeführt werden (nicht Teil der begin Tran... Commit-Block).
-  Nur Indexvorgänge, die angehalten werden sind fortsetzbar.
-   Wenn ein Indexerstellungsvorgang fortsetzen, die angehalten wurde, können Sie die MAXDOP-Wert in einen neuen Wert ändern.  Wenn MAXDOP nicht angegeben wird, wenn ein Indexerstellungsvorgang fortsetzen, die angehalten wurde, wird der letzte MAXDOP-Wert übernommen. Wenn die MAXDOP-Option für die Neuerstellung des Index überhaupt nicht angegeben ist, wird der Standardwert übernommen.
- Um den Vorgang sofort zu unterbrechen, können Sie den laufenden Befehl (STRG-C) beenden, oder können Sie den Befehl ALTER INDEX anhalten oder die KILL ausführen *Session_id* Befehl. Sobald der Befehl angehalten wird können sie mithilfe der Option RESUME fortgesetzt werden.
-  Die ABORT-Befehl beendet die Sitzung, die der ursprünglichen indexneuerstellung gehostet und bricht den Vorgang ab  
-  Keine zusätzlichen Ressourcen sind für fortsetzbar indexneuerstellung mit Ausnahme von erforderlich
   -    Zusätzlicher Speicherplatz erforderlich, um den Index erstellt wird, beibehalten, einschließlich der Zeit, wenn Index angehalten wird
   -    Ein DDL-Zustand, der verhindert, dass alle DDL-Änderung
-  Bereinigung der inaktiven Datensätze werden während der Index Pause-Phase ausgeführt werden, aber es wird angehalten werden, während der indexerstellung ausgeführt   
Die folgende Funktionalität ist für Neuerstellungsvorgänge fortsetzbar Index deaktiviert
   -    Beim Neuerstellen eines Indexes, die deaktiviert ist mit kann wieder aufgenommen werden nicht unterstützt wird = ON
   -    ALTER INDEX REBUILD Befehl
   -    ALTER TABLE, die mithilfe von Indizes  
   -    DDL-Befehl mit "RESUMEABLE = ON" kann nicht innerhalb einer expliziten Transaktion ausgeführt werden (nicht Teil der begin Tran... Commit-Block)
   -    Erstellen Sie einen Index, der eine berechnete Spaltenangabe oder TIMESTAMP-Spalten als Schlüsselspalten neu.
-   Für den Fall, dass die Basistabelle LOB-Spalten fortsetzbar gruppiert enthält erfordert indexneuerstellung am Anfang dieses Vorgangs eine Sch-M-Sperre
   -    Die SORT_IN_TEMPDB = ON Option wird für fortsetzbar Index nicht unterstützt. 

> [!NOTE]
> Der DDL-Befehl ausgeführt wird, bis er abgeschlossen ist, hält oder ein Fehler auftritt. Für den Fall, dass der Befehl angehalten wird, wird ein Fehler ausgegeben, dass der Vorgang angehalten wurde und dass es sich bei die Erstellung eines Indexes nicht abgeschlossen wurde. Weitere Informationen zum aktuellen Indexstatus abgerufen werden kann, aus [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). Wie vor im Falle eines Fehlers ein Fehler auch ausgegeben wird. 

  
 Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>WAIT_AT_LOW_PRIORITY mit online-Indexvorgänge  
  
 Um die DDL-Anweisung für eine Onlineindexneuerstellung auszuführen, müssen alle aktiven blockierenden Transaktionen, die für eine bestimmte Tabelle ausgeführt werden, abgeschlossen sein. Wenn die Onlineindexneuerstellung ausgeführt wird, werden alle neuen Transaktionen, die zur Ausführung in dieser Tabelle bereit sind, blockiert. Obwohl die Sperre für die Onlineindexneuerstellung nur kurz dauert, kann das Warten auf den Abschluss aller noch offenen Transaktionen und das Blockieren aller neuen, zu startenden Transaktionen für eine bestimmte Tabelle den Durchsatz beeinträchtigen, eine Verlangsamung oder einen Ausfall der Arbeitsauslastung verursachen und den Zugriff auf die zugrunde liegende Tabelle deutlich einschränken. Die **WAIT_AT_LOW_PRIORITY** -Option können Datenbankadministratoren zum Verwalten der s- und Sch-M-Sperren muss für die onlineneuerstellung von Indizes und zum Auswählen eines 3-Optionen angegeben. In allen Fällen 3, wenn während der Wartezeit ( `(MAX_DURATION = n [minutes])` ), es sind keine blockierenden Aktivitäten, die onlineindexneuerstellung ohne Wartezeit sofort ausgeführt wird und die DDL-Anweisung abgeschlossen ist.  
  
## <a name="spatial-index-restrictions"></a>Einschränkungen für räumliche Indizes  
 Wenn Sie einen räumlichen Index neu erstellen, ist die zugrunde liegende Benutzertabelle während des Indexvorgangs nicht verfügbar, weil der räumliche Index eine Schemasperre eingerichtet hat.  
  
 Die PRIMARY KEY-Einschränkung der Benutzertabelle kann nicht geändert werden, solange ein räumlicher Index für eine Spalte der betreffenden Tabelle definiert ist. Die PRIMARY KEY-Einschränkung kann erst geändert werden, nachdem alle räumlichen Indizes aus der Tabelle gelöscht wurden. Nach der Änderung der PRIMARY Key-Einschränkung können die einzelnen räumlichen Indizes neu erstellt werden.  
  
 Räumliche Indizes können in einem Neuerstellungsvorgang einer einzelnen Partition nicht angegeben werden. Sie können räumliche Indizes jedoch bei einer vollständigen Neuerstellung der Partition angeben.  
  
 Zum Ändern von Optionen, die einem bestimmten räumlichen Index eigen sind, beispielsweise BOUNDING_BOX oder GRID, können Sie entweder eine CREATE SPATIAL INDEX-Anweisung mit der Angabe DROP_EXISTING = ON verwenden, oder Sie löschen den räumlichen Index und erstellen einen neuen räumlichen Index. Für ein Beispiel gehen Sie unter [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
## <a name="data-compression"></a>Datenkomprimierung  
 Weitere Informationen zur Datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 Verwenden Sie zum Auswerten, wie eine Änderung Seiten- und zeilenkomprimierung eine Tabelle, einen Index oder eine Partition auswirkt, die [Sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) gespeicherte Prozedur.  
  
 Für partitionierte Indizes gelten die folgenden Einschränkungen:  
  
-   Bei Verwendung von `ALTER INDEX ALL ...`, Sie können nicht geändert, die komprimierungseinstellung einer einzelnen Partition, wenn die Tabelle nicht ausgerichtete Indizes.  
  
-   Die ALTER INDEX \<Index >... REBUILD PARTITION ...-Syntax wird die angegebene Partition des Indexes neu erstellt.  
  
-   Die ALTER INDEX \<Index >... REBUILD WITH ...-Syntax werden alle Partitionen des Indexes neu erstellt.  
  
## <a name="statistics"></a>Statistik  
 Beim Ausführen **ALTER INDEX ALL...** für eine Tabelle werden nur die statistikmitarbeiter mit Indizes aktualisiert. Automatische oder manuelle Statistiken, die statt eines Indexes in der Tabelle erstellt wurden, werden nicht aktualisiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von ALTER INDEX benötigen Sie mindestens die ALTER-Berechtigung auf der Tabelle bzw. Sicht.  
  
## <a name="version-notes"></a>Die Anmerkungen zu dieser Version  
  
-   SQL-Datenbank verwendet Dateigruppe und die Filestream-Optionen nicht.  
  
-   Columnstore-Indizes sind nicht vor SQL Server 2012 verfügbar. 

-  Fortsetzbare Indexvorgänge sind mit SQL Server-2017 und Azure SQL-Datenbank ab   
  
## <a name="basic-syntax-example"></a>Einfaches Syntaxbeispiel:   
  
```tsql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>Beispiele: Columnstore-Indizes  
 Diese Beispiele gelten für columnstore-Indizes.  
  
### <a name="a-reorganize-demo"></a>A. REORGANIZE demo  
 Dieses Beispiel veranschaulicht die Funktionsweise des ALTER INDEX REORGANIZE-Befehls.  Erstellt eine Tabelle, die mehrere Zeilengruppen und anschließend wird veranschaulicht, wie REORGANIZE die Zeilengruppen werden zusammengeführt.  
  
```  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```tsql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 Verwenden Sie die TABLOCK-Option zum Einfügen von Zeilen parallel. Beginnend mit SQL Server 2016, kann der INSERT INTO-Vorgangs parallel ausgeführt, wenn TABLOCK verwendet wird.  
  
```tsql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 Führen Sie diesen Befehl, um die offenen Delta-Zeilengruppen finden Sie unter. Die Anzahl der Zeilengruppen hängt von den Grad der Parallelität.  
  
```tsql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 Führen Sie diesen Befehl, um alle geschlossen und OPEN-Zeilengruppen in den Columnstore zu zwingen.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 Führen Sie diesen Befehl erneut aus, und sehen Sie, dass eine komprimierte Zeilengruppe kleinere Zeilengruppen zusammengeführt werden.  
  
```tsql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. Komprimieren von GESCHLOSSENEN Delta-Zeilengruppen in den columnstore  
 Dieses Beispiel verwendet die REORGANIZE-option zu komprimieren jede GESCHLOSSENEN Delta-Zeilengruppe im columnstore-Index als eine komprimierte Zeilengruppe.   Dies ist nicht erforderlich, aber es ist nützlich, wenn die tupelverschiebungsfunktion CLOSED-Zeilengruppen schnell genug ist, nicht komprimiert wird.  
  
```tsql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. Komprimieren Sie alle GEÖFFNETEN und "geschlossen" Delta-Zeilengruppen in den columnstore  
 Gilt nicht für: SQL Server 2012 und 2014  
  
 Ab SQL Server 2016 können Sie REORGANIZE WITH ausführen können (COMPRESS_ALL_ROW_GROUPS = ON) jede geöffnet und geschlossen Delta-Zeilengruppe im columnstore-Index als eine komprimierte Zeilengruppe komprimiert.    Leert die Deltastores, und erzwingt die Übernahme aller Zeilen in den Columnstore komprimiert. Dies ist hilfreich, insbesondere nach vielen Insert-Vorgänge ausführen, da diese Vorgänge die Zeilen in einem oder mehreren Deltastores gespeichert werden.  
  
 REORGANIZE kombiniert Zeilengruppen zum Füllen von Zeilengruppen, bis eine maximale Anzahl von Zeilen \<= 1,024,576. Aus diesem Grund alle öffnen "und" CLOSED-Zeilengruppen zu komprimieren wird nicht Sie mit vielen komprimierten Zeilengruppen annehmen, die nur wenige Zeilen enthalten. Zeilengruppen, reduzieren Sie die komprimierte Größe und Verbessern der Leistung von Abfragen möglichst als gefüllt werden soll.  
  
```tsql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. Defragmentieren eines columnstore-Index online  
 Gilt nicht für: SQL Server 2012 und 2014.  
  
 Beginnend mit SQL Server 2016, REORGANIZE mehr als Delta-Zeilengruppen in den Columnstore komprimiert. Er führt außerdem die Onlinedefragmentierung. Zunächst wird die Größe des Columnstore von gelöschten Zeilen physisch zu entfernen, wenn mindestens 10 % der Zeilen in einer Zeilengruppe gelöscht wurden.  Klicken Sie dann, kombiniert er Zeilengruppen kombinieren, um größere Zeilengruppen bilden, für die sind bis zu maximal 1,024,576 Zeilen pro Zeilengruppen.  Alle Zeilengruppen, die geändert werden, erhalten erneut komprimiert.  
  
> [!NOTE]
>  Beginnend mit SQL Server 2016, ist das Neuerstellen eines columnstore-Indexes nicht mehr in den meisten Situationen erforderlich da REORGANIZE physisch entfernt gelöschte Zeilen und Zeilengruppen zusammengeführt. Die Option COMPRESS_ALL_ROW_GROUPS zwingt alle geöffnet oder geschlossen Delta-Zeilengruppen in den Columnstore die zuvor nur mit einer Wiederherstellung ausgeführt werden konnte.   REORGANIZE online ist und erfolgt im Hintergrund, damit Abfragen fortgesetzt werden können, wie der Vorgang erfolgt.  
  
```tsql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. Erstellen Sie einen gruppierten columnstore-Index offline neu.  
 Gilt für: SQLServer 2012, SqlServer 2014  
  
 Starten von SQL Server 2016 und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], es wird empfohlen, ALTER INDEX REORGANIZE anstelle von ALTER INDEX REBUILD.  
  
> [!NOTE]
>  In SQL Server 2012 und 2014 wird nur REORGANIZE verwendet, um CLOSED-Zeilengruppen in den Columnstore zu komprimieren. Die einzige Möglichkeit, Defragmentierung Vorgänge auszuführen und alle Delta-Zeilengruppen in den Columnstore zu zwingen, wird den Index neu erstellt.  
  
 Dieses Beispiel zeigt, wie Sie einen gruppierten columnstore-Index neu erstellen und alle Delta-Zeilengruppen in den Columnstore zu zwingen. Im ersten Schritt wird die FactInternetSales2-Tabelle mit einem gruppierten columnstore-Index vorbereitet, und es werden Daten aus den ersten vier Spalten eingefügt.  
  
```tsql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Die Ergebnisse zeigen, es ist eine OPEN-Zeilengruppe, d. h. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet darauf, dass weitere Zeilen hinzugefügt werden, bevor sie die Zeilengruppe geschlossen wird und die Daten in den Columnstore verschoben. Mit der nächsten Anweisung erstellt den gruppierten columnstore-Index, der alle Zeilen im columnstore-Index erzwingt neu.  
  
```tsql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Die Ergebnisse der SELECT-Anweisung zeigen, dass die Zeilengruppe als COMPRESSED gekennzeichnet ist. Dies bedeutet, dass die Spaltensegmente der Zeilengruppe jetzt komprimiert und im Columnstore gespeichert sind.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. Erstellen Sie eine Partition eines gruppierten columnstore-Index offline neu  
 Verwenden Sie diese für: SQLServer 2012, SqlServer 2014  
  
 Verwenden Sie ALTER INDEX REBUILD mit der Partitionsoption, um eine Partition eines großen gruppierten columnstore-Index neu zu erstellen. In diesem Beispiel wird die Partition 12 neu erstellt. Beginnend mit SQL Server 2016, empfehlen wir, und Ersetzen Sie dabei mit REORGANIZE neu erstellen.  
  
```tsql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. Ändern Sie einen gruppierten rowstore-Index, um die archivierungskomprimierung zu verwenden  
 Gilt nicht für: SQL Server 2012  
  
 Sie können auswählen, um die Größe eines gruppierten columnstore-Index noch weiter zu reduzieren, indem Sie mit der COLUMNSTORE_ARCHIVE-Datenkomprimierungsoption. Dies ist praktisch für ältere Daten, die auf den kostengünstiger Speicher beibehalten werden sollen. Es wird empfohlen, dass ein langsamer als bei der normalen columnstore-Komprimierung wird nur mit dies auf, die da häufig nicht abgefragte, Daten zu dekomprimieren.  
  
 Im folgenden Beispiel wird ein gruppierter columnstore-Index für die Verwendung der Archivierungskomprimierung neu erstellt. Anschließend wird gezeigt, wie die Archivierungskomprimierung entfernt wird. Letztendlich wird nur die columnstore-Komprimierung verwendet.  
  
```tsql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>Beispiele: Rowstore-Indizes  
  
### <a name="a-rebuilding-an-index"></a>A. Neuerstellen eines Index  
 Im folgenden Beispiel wird ein einzelner Index für die `Employee`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank neu erstellt.  
  
```tsql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. Neuerstellen aller Indizes einer Tabelle und Angeben von Optionen  
 Im folgenden Beispiel wird das Schlüsselwort `ALL` angegeben. Dadurch werden alle Indizes neu erstellt, die der Production.Product-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zugeordnet sind. Es werden drei Optionen angegeben.  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
 Im folgenden Beispiel werden die ONLINE-Option einschließlich der Option für Sperren mit niedriger Priorität sowie die Zeilenkomprimierungsoption hinzugefügt.  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.  
  
```tsql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>C. Neuorganisieren eines Indexes mit LOB-Komprimierung  
 Im folgenden Beispiel wird ein einzelner gruppierter Index in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank neu organisiert. Da der Index einen LOB-Datentyp in der Blattebene enthält, komprimiert die Anweisung auch alle Seiten, die die LOB-Daten enthalten. Beachten Sie, dass die Angabe der WITH (LOB_COMPACTION)-Option nicht erforderlich ist, da der Standardwert auf ON festgelegt ist.  
  
```tsql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. Festlegen von Optionen für einen Index  
 Im folgenden Beispiel werden mehrere Optionen für den `AK_SalesOrderHeader_SalesOrderNumber`-Index in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank festgelegt.  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2008) und Azure SQL-Datenbank.  
  
```tsql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>E. Deaktivieren eines Indexes  
 Im folgenden Beispiel wird ein nicht gruppierter Index für die `Employee`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank deaktiviert.  
  
```tsql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. Deaktivieren von Einschränkungen  
 Im folgende Beispiel wird eine PRIMARY KEY-Einschränkung deaktiviert, durch das Deaktivieren des PRIMARY KEY-Indexes in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank. Die FOREIGN KEY-Einschränkung für die zugrunde liegende Tabelle wird automatisch deaktiviert, und eine Warnmeldung wird angezeigt.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
 Das Resultset gibt diese Warnmeldung zurück.  
  
 ```tsql  
 Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
 on table 'EmployeeDepartmentHistory' referencing table 'Department'  
 was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
 ```  
  
### <a name="g-enabling-constraints"></a>G. Aktivieren von Einschränkungen  
 Im folgenden Beispiel werden die in Beispiel F deaktivierten PRIMARY KEY- und FOREIGN KEY-Einschränkungen aktiviert.  
  
 Die PRIMARY KEY-Einschränkung wird aktiviert, indem der PRIMARY KEY-Index neu erstellt wird.  
  
```tsql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
 Anschließend wird die FOREIGN KEY-Einschränkung aktiviert.  
  
```tsql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. Neuerstellen eines partitionierten Indexes  
 Im folgenden Beispiel wird eine einzelne Partition mit der Partitionsnummer `5` des partitionierten `IX_TransactionHistory_TransactionDate`-Indexes in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank neu erstellt. Partition 5 wird online neu erstellt, und die zehnminütige Wartezeit für die Sperre mit niedriger Priorität gilt für jede einzelne Sperre, die durch die Indexneuerstellung abgerufen wird. Wenn während dieser Zeit die Sperre nicht für die komplette Neuerstellung des Indexes reicht, wird die Anweisung für die Neuerstellung abgebrochen.  
  
**Gilt für**: SQL Server (beginnend mit SQL Server 2014) und Azure SQL-Datenbank.  
  
```tsql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>I. Ändern der Komprimierungseinstellung eines Indexes  
 Im folgenden Beispiel wird ein Index für eine nicht partitionierte rowstore-Tabelle neu erstellt.  
  
```tsql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
 Zusätzliche Beispiele zur datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
 
### <a name="j-online-resumable-index-rebuild"></a>J. Fortsetzbare onlineneuerstellung von Indizes

**Gilt für**: ab SQL Server-2017 und Azure SQL-Datenbank   

 Die folgenden Beispiele zeigen, wie fortsetzbar onlineneuerstellung von Indizes verwendet wird. 

1. Führen Sie eine online-indexneuerstellung als fortsetzbar Vorgang mit MAXDOP = 1.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. Ausführung derselben wird nachdem ein Indexvorgang angehalten wurde, Befehl erneut aus (siehe oben) automatisch die Neuerstellung des Index.

3. Führen Sie eine online-indexneuerstellung als fortsetzbar Vorgang mit MAX_DURATION auf 240 Minuten festgelegt ist.

   ```tsql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. Anhalten einer laufenden fortsetzbar online-indexneuerstellung.

   ```tsql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. Fortsetzen einer online-indexneuerstellung für das Neuerstellen eines Index, das ausgeführt wurde, als fortsetzbar Vorgang unter Angabe einen neuen Wert für MAXDOP auf 4 festgelegt.

   ```tsql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. Fortsetzen eines Vorgangs zur onlineindexneuerstellung für eine indexneuerstellung online, die als fortsetzbar ausgeführt wurde. MAXDOP auf 2 festgelegt, legen Sie die Ausführungszeit für den Index als Resmumable ausgeführt werden, und 240 Minuten eingestellt und im Falle eines Indexes, 10 Minuten auf den Wartevorgang auf eine Sperre blockiert, und beenden Sie danach alle Hindernisse. 

   ```tsql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. Brechen Sie fortsetzbar indexneuerstellungsvorgangs die ausgeführt oder angehalten wird ab.

   ```tsql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>Siehe auch  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Erstellen Sie SPATIAL INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [Erstellen von XML-INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [Ausführen von Onlineindexvorgängen](../../relational-databases/indexes/perform-index-operations-online.md)   
 [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


