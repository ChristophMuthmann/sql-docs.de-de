---
title: Erstellen von columnstore-INDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
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
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs: TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
caps.latest.revision: "76"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: ccf03c6b2d3d7798f3bad65b340657bf2b21b751
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Konvertieren einer Rowstore-Tabelle einen gruppierten columnstore-Index, oder erstellen Sie einen nicht gruppierten columnstore-Index. Verwenden Sie einen columnstore-Index aus, um effizient operative Echtzeitanalyse auf einer OLTP-Arbeitslast auszuführen oder um Daten datenkomprimierung und abfrageleistung für Data warehousing-arbeitsauslastungen zu verbessern.  
  
> [!NOTE]  
> Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], können Sie die Tabelle als gruppierten columnstore-Index erstellen.   Es ist nicht mehr notwendig, erstellen Sie zuerst eine Rowstore-Tabelle, und klicken Sie dann in einen gruppierten columnstore-Index zu konvertieren.  

> [!TIP]
> Informationen zu Richtlinien zum Entwerfen Indizes, finden Sie in der [SQL Server Handbuch zum Indexentwurf](../../relational-databases/sql-server-index-design-guide.md).

Fahren Sie mit Beispielen:  
-   [Beispiele zum Konvertieren einer Rowstore-Tabelle in columnstore](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [Beispiele für nicht gruppierte columnstore-Indizes](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
Zu den Szenarien wechseln:  
-   [Columnstore-Indizes für die operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [Columnstore-Indizes für Datawarehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
Weitere Informationen:  
-   [Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [Featurezusammenfassung für columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]   
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )   
    | filegroup_name   
    | "default"   
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name   
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
CREATE CLUSTERED COLUMNSTORE INDEX  
Erstellen Sie einen gruppierten columnstore-Index, in dem alle Daten komprimiert und nach Spalten gespeichert werden. Der Index beinhaltet alle Spalten der Tabelle und speichert die gesamte Tabelle. Wenn die vorhandene Tabelle ein Heap oder gruppierter Index ist, wird die Tabelle einen gruppierten columnstore-Index konvertiert. Wenn die Tabelle bereits als gruppierter columnstore-Index gespeichert ist, wird der vorhandene Index gelöscht und neu erstellt.  
  
*index_name*  
Gibt den Namen für den neuen Index.  
  
Wenn die Tabelle bereits einen gruppierten columnstore-Index verfügt, können Sie den gleichen Namen wie des vorhandenen Indexes angeben, oder verwenden Sie die DROP EXISTING Option, um einen neuen Namen angeben.  
  
ON [*Database_name*. [*schema_name* ] . | *schema_name* . ] *table_name*  
   Gibt den ein-, zwei- oder dreiteiligen Namen der Tabelle an, die als gruppierter Columnstore-Index gespeichert werden soll. Wenn die Tabelle ein Heap ist oder gruppierter Index der Tabelle von Rowstore in einen Columnstore konvertiert. Wenn die Tabelle bereits einen Columnstore ist, wird diese Anweisung den gruppierten columnstore-Index neu erstellt.  
  
mit  
DROP_EXISTING = [AUS] | ON  
   DROP_EXISTING = ON gibt an, dass die vorhandenen gruppierten columnstore-Index löschen und erstellen Sie einen neuen columnstore-Index.  

   Die Standardeinstellung, DROP_EXISTING = OFF erwartet, dass der Indexname ist identisch mit den vorhandenen Namen. Ein Fehler auftritt, wird der angegebene Indexname bereits vorhanden ist.  
  
MAXDOP = *max_degree_of_parallelism*  
   Überschreibt die Serverkonfiguration für den maximalen Grad an Parallelität für die Dauer des Indexvorgangs. Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
   *Max_degree_of_parallelism* Werte sind möglich:  
   - 1 - Unterdrückt die Generierung paralleler Pläne.  
   - \>1 - beschränkt die maximale Anzahl der Prozessoren, die in einem parallelen Indexvorgang auf die angegebene Anzahl verwendet oder weniger basierend auf der aktuellen systemarbeitsauslastung. Zum Beispiel wenn MAXDOP = 4, die Anzahl der Prozessoren, die verwendet wird, 4 oder weniger.  
   - 0 (Standard) - Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
   Weitere Informationen finden Sie unter [Konfigurieren der max Degree of Parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md), und [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
 
COMPRESSION_DELAY = **0** | *Verzögerung* [Minuten]  
   Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

   Für eine datenträgerbasierte Tabelle *Verzögerung* gibt die minimale Anzahl von Minuten, die eine Delta-Zeilengruppen in den GESCHLOSSENEN Zustand verbleiben muss, in der deltazeilengruppe an, bevor SQL Server in der komprimierten Zeilengruppe komprimiert werden können. Da es sich bei datenträgerbasierten Tabellen nicht nachverfolgen einfügen und aktualisieren Zeiten für einzelne Zeilen, SQL Server gilt die Verzögerung in Delta-Zeilengruppen in den GESCHLOSSENEN Zustand übergeht.  
   Der Standardwert beträgt 0 Minuten.  
   Empfehlungen zur Verwendung von COMPRESSION_DELAY, finden Sie unter [erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Gibt die Datenkomprimierungsoption für die angegebene Tabelle, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:   
COLUMNSTORE  
   COLUMNSTORE ist die Standardeinstellung und gibt an, dass Sie mit der meisten leistungsfähiger columnstore-Komprimierung zu komprimieren. Dies ist die typische Wahl.  
  
COLUMNSTORE_ARCHIVE  
   COLUMNSTORE_ARCHIVE weiter komprimiert, die Tabelle oder Partition auf eine geringere Größe an. Verwenden Sie diese Option für Situationen, z. B. Archivierung, erfordern eine geringere Speichergröße und mehr Zeit für die Speicherung und Abruf leisten können.  
  
   Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  

ON  
   Mit den ON-Optionen können Sie Optionen für die Datenspeicherung, wie ein Partitionsschema, eine bestimmte Dateigruppe oder die Standarddateigruppe, angeben. Wenn die Option nicht angegeben ist, verwendet der Index die einstellungspartition oder dateigruppeneinstellungen-Einstellungen der vorhandenen Tabelle.  
  
   *partition_scheme_name* **(** *column_name* **)**  
   Gibt das Partitionsschema für die Tabelle an. Das Partitionsschema muss in der Datenbank bereits vorhanden sein. Um das Partitionsschema zu erstellen, finden Sie unter [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md).  
 
   *Column_name* gibt die Spalte für die ein partitionierter Index partitioniert ist. Diese Spalte muss den Datentyp, Länge, übereinstimmen und der Genauigkeit des Arguments der Partition, *Partition_scheme_name* verwendet.  

   *filegroup_name*  
   Gibt die Dateigruppe zum Speichern des gruppierten Columnstore-Indexes an. Wenn kein Speicherort angegeben und die Tabelle nicht partitioniert ist, verwendet der Index die gleiche Dateigruppe wie die zugrunde liegende Tabelle oder Sicht. Die Dateigruppe muss bereits vorhanden sein.  

   **"**default**"**  
   Um den Index in der Standarddateigruppe erstellen, verwenden Sie "Default" oder [Default].  
  
   Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. QUOTED_IDENTIFIER hat standardmäßig den Wert ON. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
[NICHT GRUPPIERTEN] COLUMNSTORE-INDEX ERSTELLEN  
Erstellen Sie einen nicht gruppierten in-Memory-columnstore-Index für eine Rowstore-Tabelle als einen Heap oder gruppierten Index gespeichert. Der Index eine filterbedingung aufweisen und muss nicht alle Spalten der zugrunde liegenden Tabelle enthalten. Der columnstore-Index erfordert ausreichend Speicherplatz zum Speichern einer Kopie der Daten. Es ist aktualisierbar, und wird aktualisiert, während die zugrunde liegende Tabelle geändert wird. Der nicht gruppierten columnstore-Index für einen gruppierten Index ermöglicht Echtzeitanalyse.  
  
*index_name*  
   Gibt den Namen des Indexes an. *Index_name* muss innerhalb der Tabelle eindeutig sein, aber keinen innerhalb der Datenbank eindeutig sein. Indexnamen müssen den Regeln der [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 **(** *Spalte* [ **,**... *n* ] **)**  
    Gibt die zu speichernden Spalten an. Ein nicht gruppierter columnstore-Index ist auf 1024 Spalten beschränkt.  
   Jede Spalte muss ein unterstützter Datentyp für columnstore-Indizes sein. Finden Sie unter [Einschränkungen](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest) eine Liste der unterstützten Datentypen.  

ON [*Database_name*. [*schema_name* ] . | *schema_name* . ] *table_name*  
   Gibt den ein-, zwei- oder dreiteiligen Namen der Tabelle, die den Index enthält.  

MIT DROP_EXISTING = [DEAKTIVIERT] | ON  
   DROP_EXISTING = ON der vorhandene Index gelöscht und neu erstellt wird. Der angegebene Indexname muss mit dem Namen eines derzeit vorhandenen Index übereinstimmen. Die Indexdefinition kann jedoch geändert werden. Sie können z. B. andere Spalten oder Indexoptionen angeben.
  
   DROP_EXISTING = OFF, wenn der angegebene Indexname bereits vorhanden ist, wird ein Fehler angezeigt. Der Indextyp kann nicht mithilfe von DROP_EXISTING geändert werden. In abwärtskompatibler Syntax ist WITH DROP_EXISTING gleichwertig mit WITH DROP_EXISTING = ON.  

MAXDOP = *max_degree_of_parallelism*  
   Überschreibt die [Konfigurieren der max Degree of Parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) Konfigurationsoption für die Dauer des Indexvorgangs. Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
   *Max_degree_of_parallelism* Werte sind möglich:  
   - 1 - Unterdrückt die Generierung paralleler Pläne.  
   - \>1 - beschränkt die maximale Anzahl der Prozessoren, die in einem parallelen Indexvorgang auf die angegebene Anzahl verwendet oder weniger basierend auf der aktuellen systemarbeitsauslastung. Zum Beispiel wenn MAXDOP = 4, die Anzahl der Prozessoren, die verwendet wird, 4 oder weniger.  
   - 0 (Standard) - Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
   Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht verfügbar in jeder Edition von [!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
ONLINE = [ON | OFF]   
   Gilt für: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], nur nicht gruppierte columnstore-Indizes.
ON gibt an, dass der nicht gruppierten columnstore-Index online bleibt und verfügbar ist, während die neue Kopie des Indexes ist, die erstellt wird.

   Gibt an, dass der Index nicht für die Verwendung verfügbar ist, während die neue Kopie erstellt wird, deaktiviert. Weil es sich handelt es sich um einen nicht gruppierten Index nur die Basistabelle bleibt verfügbar ist, wird nur der nicht gruppierten columnstore-Index nicht verwendet wird, um Abfragen zu erfüllen, bis der neue Index abgeschlossen ist. 

COMPRESSION_DELAY = **0** | \<Verzögerung > [Minuten]  
   Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
   Gibt eine Untergrenze für wie lange eine Zeile in der Delta-Zeilengruppe bleiben soll, bevor er für die Migration in die komprimierte Zeilengruppe geeignet ist. Beispielsweise kann ein Kunde angenommen, die, wenn eine Zeile für 120 Minuten unverändert ist geeignet für die Komprimierung von Format für spaltenweise Speicherung erleichtern. Für columnstore-Index auf datenträgerbasierte Tabellen, wir die Zeit, wenn eine Zeile eingefügt oder aktualisiert wird, wurde, keine nachverfolgen wir stattdessen die Delta-Zeilengruppe geschlossen Zeit als Proxy für die Zeile. Der Standardzeitraum beträgt 0 Minuten. Eine Zeile ist auf spaltenweise Speicherung migriert, sobald 1 Million Zeilen in Delta-Zeilengruppe gesammelt wurden, und es geschlossen gekennzeichnet wurde.  
  
DATA_COMPRESSION  
   Gibt die Datenkomprimierungsoption für die angegebene Tabelle, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
COLUMNSTORE  
   Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. COLUMNSTORE ist die Standardeinstellung und gibt an, dass Sie mit der meisten leistungsfähiger columnstore-Komprimierung zu komprimieren. Dies ist die typische Wahl.  
  
COLUMNSTORE_ARCHIVE  
   Gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. COLUMNSTORE_ARCHIVE weiter komprimiert, die Tabelle oder Partition auf eine geringere Größe an. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speichergröße und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
 Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
WOBEI \<Filter_expression > [AND \<Filter_expression >] gilt für: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
   Ein Filterprädikat wird aufgerufen, gibt dies die Zeilen im Index enthalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt gefilterte Statistiken für die Datenzeilen im gefilterten Index.  
  
   Das Filterprädikat verwendet einfache Vergleichslogik. Vergleiche mit NULL-Literalen sind mit den Vergleichsoperatoren nicht zulässig. Verwenden Sie stattdessen den IS NULL-Operator und den IS NOT NULL-Operator.  
  
   Es folgen einige Beispiele für Filterprädikate für die `Production.BillOfMaterials`-Tabelle:  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   Anleitungen für gefilterte Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
ON  
   Diese Optionen geben die Dateigruppen, die auf denen der Index erstellt wird.  
  
*partition_scheme_name* **(** *column_name* **)**  
   Gibt das Partitionsschema, das definiert, die Dateigruppen, denen die Partitionen eines partitionierten Index zugeordnet ist. Das Partitionsschema muss in der Datenbank vorhanden, durch das Ausführen [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). 
   *Column_name* gibt die Spalte für die ein partitionierter Index partitioniert ist. Diese Spalte muss den Datentyp, Länge, übereinstimmen und der Genauigkeit des Arguments der Partition, *Partition_scheme_name* verwendet. *Column_name* ist nicht auf die Spalten in der Indexdefinition beschränkt. Wenn Sie einen columnstore-Index partitionieren, fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Partitionierungsspalte als Spalte des Index hinzu, wenn sie noch nicht angegeben ist.  
   Wenn *Partition_scheme_name* oder *Dateigruppe* nicht angegeben wird und die Tabelle partitioniert ist, wird der Index in demselben Partitionsschema, mit der gleichen Partitionsspalte, wie die zugrunde liegende Tabelle platziert.  
   Ein columnstore-Index einer partitionierten Tabelle muss über eine Partitionsausrichtung verfügen.  
   Weitere Informationen zum Partitionieren von Indizes finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  

*filegroup_name*  
   Gibt den Namen einer Dateigruppe an, für die der Index erstellt werden soll. Wenn *Filegroup_name* nicht angegeben wird und die Tabelle nicht partitioniert ist, der Index verwendet die gleiche Dateigruppe wie die zugrunde liegende Tabelle. Die Dateigruppe muss bereits vorhanden sein.  
 
**"**default**"**  
Erstellt den angegebenen Index für die Standarddateigruppe.  
  
Die Benennung default ist in diesem Kontext kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in ON **"**Standard**"** oder ON **[**Standard**]**. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
##  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="GenRemarks"></a>Allgemeine Hinweise  
 Ein columnstore-Index kann für eine temporäre Tabelle erstellt werden. Wenn die Tabelle gelöscht oder die Sitzung beendet wird, wird der Index ebenfalls gelöscht.  
 
## <a name="filtered-indexes"></a>Gefilterten Indizes  
Ein gefilterter Index ist ein optimierter nicht gruppierter Index, der sich für Abfragen eignet, mit denen ein kleiner Prozentsatz von Zeilen in einer Tabelle ausgewählt wird. Es wird ein Filterprädikat verwendet, um einen Teil der Daten in der Tabelle zu indizieren. Ein gut entworfener gefilterter Index kann die Abfrageleistung verbessern, den Speicheraufwand verringern und Wartungskosten reduzieren.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Erforderliche SET-Optionen für gefilterte Indizes  
Die SET-Optionen in der Spalte Erforderlicher Wert sind immer dann erforderlich, wenn eine der folgenden Bedingungen auftritt:  
- Es wird ein gefilterter Index erstellt.  
- Ein INSERT-, UPDATE-, DELETE- oder MERGE-Vorgang ändert die Daten in einem gefilterten Index.  
- Der gefilterte Index wird vom Abfrageoptimierer verwendet, um den Abfrageplan zu erstellen.  
  
    |SET-Optionen|Erforderlicher Wert|Standardserverwert|Standardwert<br /><br /> OLE DB- und ODBC-Wert|Standardwert<br /><br /> DB-Library-Wert|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *Durch Festlegen von ANSI_WARNINGS auf ON wird implizit ARITHABORT auf ON festgelegt, wenn der Kompatibilitätsgrad der Datenbank auf 90 oder höher festgelegt ist. Wird der Kompatibilitätsgrad der Datenbank auf 80 oder niedriger festgelegt, muss die ARITHABORT-Option explizit auf ON festgelegt werden.  
  
 Wenn die SET-Optionen falsch sind, können die folgenden Bedingungen auftreten:  
  
-   Der gefilterte Index wird nicht erstellt.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] generiert einen Fehler und führt ein Rollback aller INSERT-, UPDATE-, DELETE- oder MERGE-Anweisungen aus, die im Index gespeicherte Daten ändern.  
  
-   Der Abfrageoptimierer berücksichtigt den Index des Abfrageausführungsplans von Transact-SQL-Anweisungen nicht.  
  
 Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md). 
  
##  <a name="LimitRest"></a> Einschränkungen  

**Jede Spalte in einem columnstore-Index muss eines der folgenden allgemeinen Geschäftsdatentypen sein:** 
-   datetimeoffset [ ( *n* ) ]  
-   datetime2 [ ( *n* ) ]  
-   datetime  
-   smalldatetime  
-   Datum  
-   Zeit [(  *n*  )]  
-   "float" [(  *n*  )]  
-   echte [(  *n*  )]  
-   Dezimal [( *Genauigkeit* [ *, Skalierung* ] **)** ]
-   numerische [( *Genauigkeit* [ *, Skalierung* ] **)** ]    
-   money  
-   smallmoney  
-   bigint  
-   int  
-   smallint  
-   tinyint  
-   bit  
-   nvarchar [ ( *n* ) ] 
-   nvarchar(max) (gilt für [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und Azure SQL-Datenbank auf Premium Tarif, in nur gruppierte columnstore-Indizes)   
-   nchar [ ( *n* ) ]  
-   Varchar [(  *n*  )]  
-   varchar(max) (gilt für [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und Azure SQL-Datenbank auf Premium Tarif, in nur gruppierte columnstore-Indizes)
-   char [ ( *n* ) ]  
-   varbinary [ ( *n* ) ] 
-   Varbinary (Max) (gilt für [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und Azure SQL-Datenbank auf Premium Tarif, in nur gruppierte columnstore-Indizes)
-   Binary [(  *n*  )]  
-   "uniqueidentifier" (gilt für [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und höher)
  
Wenn die zugrunde liegenden Tabelle eine Spalte mit einem Datentyp, die für columnstore-Indizes nicht unterstützt wird verfügt, müssen Sie diese Spalte aus dem nicht gruppierten columnstore-Index auslassen.  
  
**Spalten, die keines der folgenden Datentypen verwenden, können nicht in einen columnstore-Index enthalten sein:**
-   ntext, text und image  
-   nvarchar(max), varchar(max) und varbinary(max) (gilt für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und früheren Versionen sowie nicht gruppierten columnstore-Indizes) 
-   rowversion (und timestamp)  
-   sql_variant  
-   CLR-Typen (hierarchyid- und räumliche Typen)  
-   xml  
-   "uniqueidentifier" (gilt für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**Nicht gruppierte columnstore-Indizes:**
-   Kann nicht mehr als 1024 Spalten enthalten.  
-   Eine Tabelle mit einem nicht gruppierten columnstore-Index kann über UNIQUE-, PRIMARY KEY- oder FOREIGN KEY-Einschränkungen verfügen, die Einschränkungen können aber nicht in den nicht gruppierten columnstore-Index eingeschlossen werden.  
-   Kann nicht für eine Sicht oder indizierte Sicht erstellt werden.  
-   Kann keine Sparsespalte enthalten.  
-   Kann nicht geändert werden, mithilfe der **ALTER INDEX** Anweisung. Um den nicht gruppierten Index zu ändern, müssen Sie stattdessen den columnstore-Index löschen und neu erstellen. Sie können **ALTER INDEX** deaktivieren und neu Erstellen eines columnstore-Indexes.  
-   Kann nicht erstellt werden, mithilfe der **INCLUDE** Schlüsselwort.  
-   Darf keine enthalten die **ASC** oder **"DESC"** Schlüsselwörter zum Sortieren des Index. Columnstore-Indizes werden gemäß den Komprimierungsalgorithmen sortiert. Durch die Sortierung würden viele der Leistungsvorteile entfernt werden.  
-   Darf keine großer Objekte (LOB) Spalten vom Typ nvarchar(max), varchar(max) und varbinary(max) nicht gruppierten columnstore-Indizes enthalten. Nur gruppierte columnstore-Indizes LOB-Typen unterstützt, beginnend [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] Version und Azure SQL-Datenbank auf Premium-Tarif konfiguriert. Beachten Sie, dass frühere Versionen nicht LOB-Typen in gruppierten und nicht gruppierten columnstore-Indizes unterstützen.


 **Columnstore-Indizes können nicht mit den folgenden Funktionen kombiniert werden:**  
-   Berechnete Spalten. Beginnend mit SQL Server-2017 kann ein gruppierten columnstore-Index eine nicht permanente berechnete Spalte enthalten. Allerdings in SQL Server 2017 gruppierte columnstore-Indizes können nicht persistente berechnete Spalten enthalten, und erstellt nicht gruppierte Indizes für berechnete Spalten nicht möglich. 
-   Seiten- und zeilenkomprimierung, und **Vardecimal** Speicherformat (ein columnstore-Index ist bereits in einem anderen Format komprimiert.)  
-   Replikation  
-   Filestream

Sie können keine Cursor oder Trigger für eine Tabelle mit einem gruppierten columnstore-Index verwenden. Diese Einschränkung gilt nicht für nicht gruppierte columnstore-Indizes; Sie können den Cursor und Trigger für eine Tabelle mit einem nicht gruppierten columnstore-Index verwenden.

**Bestimmte Einschränkungen für SQL Server 2014**  
Diese Einschränkungen gelten nur für SQL Server 2014. In dieser Version werden aktualisierbare gruppierte columnstore-Indizes vorgestellt. Nicht gruppierte columnstore-Indizes werden immer noch schreibgeschützt waren.  

-   "Änderungen Sie nachverfolgen". Sie können keine änderungsnachverfolgung mit nicht gruppierten columnstore-Indizes (NCCI), da sie schreibgeschützt sind. Es funktioniert für gruppierte columnstore-Indizes (CCI).  
-   Ändern Sie die Datenerfassung. Sie können keine Änderung, die Daten für nicht gruppierte columnstore-Index (NCCI) zu erfassen, da sie schreibgeschützt sind. Es funktioniert für gruppierte columnstore-Indizes (CCI).  
-   Lesbare sekundäre Rolle. Sie können keinen gruppierten gruppierten Columnstore-Index (CCI) über ein lesbares sekundäres Replikat einer verfügbarkeitsgruppe stets OnReadable zugreifen.  Sie können einen nicht gruppierten columnstore-Index (NCCI) aus einer lesbaren sekundären Datenbank zugreifen.  
-   Multiple Active Result Sets (MARS). SQL Server 2014 verwendet MARS für schreibgeschützte Verbindungen zu Tabellen mit einem columnstore-Index.    SQL Server 2014 unterstützt jedoch nicht MARS für gleichzeitige Data Manipulation Language (DML)-Vorgängen für eine Tabelle mit einem columnstore-Index. In diesem Fall wird von SQL Server beendet die Verbindungen und Transaktionen abgebrochen.  
  
 Informationen zu den Leistungsvorteilen und Einschränkungen von columnstore-Indizes finden Sie unter [Übersicht über columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
##  <a name="Metadata"></a> Metadaten  
 Alle Spalten in einem Columnstore-Index werden in den Metadaten als eingeschlossene Spalten gespeichert. Der Columnstore-Index weist keine Schlüsselspalten auf. Diese Systemsichten enthalten Informationen zu Columnstore-Indizes.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>Beispiele zum Konvertieren einer Rowstore-Tabelle in columnstore  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>A. Konvertieren eines Heaps in einen gruppierten Columnstore-Index  
 In diesem Beispiel wird eine Tabelle als Heap erstellt und anschließend in einen gruppierten Columnstore-Index mit dem Namen cci_Simple konvertiert. Dadurch wird der Speicher für die gesamte Tabelle von rowstore in columnstore geändert.  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. Konvertiert einen gruppierten Index in einen gruppierten Columnstore-Index mit demselben Namen.  
 In diesem Beispiel wird eine Tabelle mit einem gruppierten Index erstellt. Anschließend wird die Syntax zum Konvertieren des gruppierten Indexes in einen gruppierten Columnstore-Index veranschaulicht. Dadurch wird der Speicher für die gesamte Tabelle von rowstore in columnstore geändert.  
  
```  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. Beim Konvertieren einer Rowstore-Tabelle in eine columnstore-Index nicht gruppierte Indizes zu behandeln.  
 In diesem Beispiel wird das Behandeln von nicht gruppierten Indizes beim Konvertieren einer Rowstore-Tabelle in eine columnstore-Index veranschaulicht. Tatsächlich, beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ist keine spezielle Handlung erforderlich; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch definiert und erstellt die nicht gruppierten Indizes für den neuen gruppierten columnstore-Index neu.  
  
 Wenn Sie die nicht gruppierten Indizes löschen möchten, verwenden Sie die DROP INDEX-Anweisung vor der Erstellung des columnstore-Index. Der DROP EXISTING-Option löscht nur den gruppierten Index, der konvertiert wird. Nicht gruppierte Indizes werden nicht gelöscht.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], einen nicht gruppierten Index konnte nicht erstellt werden, für einen columnstore-Index. Dieses Beispiel zeigt, wie in früheren Versionen müssen Sie die nicht gruppierten Indizes zu löschen, bevor Sie den columnstore-Index erstellen.  
  
```  
  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. Konvertieren einer großen Faktentabelle von einem Rowstore in einen Columnstore  
 In diesem Beispiel wird erläutert, wie eine große Faktentabelle von einer Rowstore-Tabelle in eine Columnstore-Tabelle konvertiert wird.  
  
 So konvertieren Sie eine Rowstore-Tabelle in eine Columnstore-Tabelle:  
  
1.  Erstellen Sie zunächst eine kleine Tabelle, die für das Beispiel verwendet werden kann.  
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  Löschen Sie alle nicht gruppierten Indizes aus der Rowstore-Tabelle.  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  Löschen Sie den gruppierten Index.  
  
    -   Führen Sie diesen Schritt nur aus, wenn Sie beim Konvertieren in einen gruppierten Columnstore-Index einen neuen Namen für den Index angeben möchten. Wenn Sie den gruppierten Index nicht löschen, hat der neue gruppierte columnstore-Index den gleichen Namen.  
  
        > [!NOTE]  
        >  Der Indexname ist möglicherweise einprägsamer, wenn Sie einen eigenen Namen angeben. Alle gruppierten Rowstore-Indizes verwenden Sie den Standardnamen also "ClusteredIndex_\<GUID >".  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  Konvertieren Sie die Rowstore-Tabelle in eine Columnstore-Tabelle mit einem gruppierten Columnstore-Index.  
  
    ```  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. Konvertieren einer Columnstore-Tabelle in eine Rowstore-Tabelle mit einem gruppierten Index  
 Verwenden Sie die CREATE INDEX-Anweisung mit der DROP_EXISTING-Option, um eine Columnstore-Tabelle in eine Rowstore-Tabelle mit einem gruppierten Index zu konvertieren.  
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. Konvertieren einer Columnstore-Tabelle in einen Rowstore-Heap  
 Löschen Sie zum Konvertieren einer Columnstore-Tabelle in einen Rowstore-Heap einfach den gruppierten Columnstore-Index.  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. Defragmentiert werden durch Neuerstellen des gesamten gruppierten columnstore-Indexes  
   Gilt für: SQLServer 2014  
  
 Es gibt zwei Möglichkeiten, den gesamten gruppierten Columnstore-Index neu zu erstellen. Sie können CREATE CLUSTERED COLUMNSTORE INDEX, oder [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md) und die REBUILD-Option. Mit beiden Methoden werden die gleichen Ergebnisse erzielt.  
  
> [!NOTE]  
>  Ab SQL Server 2016, ALTER INDEX REORGANIZE verwenden Sie anstatt mit den Methoden, die in diesem Beispiel beschriebene neu erstellt.  
  
```  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
  
```  
  
##  <a name="nonclustered"></a>Beispiele für nicht gruppierte columnstore-Indizes  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>A. Erstellen Sie einen columnstore-Index als sekundären Index für eine Rowstore-Tabelle  
 In diesem Beispiel erstellt einen nicht gruppierten columnstore-Index für eine Rowstore-Tabelle. In diesem Fall kann nur über einen columnstore-Index erstellt werden. Der columnstore-Index erfordert zusätzlichen Speicherplatz, da es sich um eine Kopie der Daten in die Rowstore-Tabelle enthält. In diesem Beispiel wird eine einfache Tabelle und ein gruppierter Index erstellt und anschließend wird die Syntax zum Erstellen eines nicht gruppierten columnstore-Indexes veranschaulicht.  
  
```  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>B. Erstellen eines einfachen nicht gruppierten columnstore-Indexes mit allen Optionen  
 Im folgenden Beispiel wird die Syntax zum Erstellen eines nicht gruppierten Columnstore-Indexes unter Verwendung aller Optionen veranschaulicht.  
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 Ein komplexeres Beispiel mit partitionierten Tabellen, finden Sie unter [Übersicht über columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. Erstellen Sie einen nicht gruppierten columnstore-Index mit einer gefilterten Prädikat  
 Das folgende Beispiel erstellt einen gefilterter nicht gruppierter columnstore-Index für die Production.BillOfMaterials-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank. Das Filterprädikat kann Spalten einschließen, die keine Schlüsselspalten im gefilterten Index sind. Das Prädikat in diesem Beispiel wählt nur die Zeilen aus, in denen EndDate nicht NULL ist.  
  
```  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
  
```  
  
###  <a name="ncDML"></a> D. Ändern Sie die Daten in einem nicht gruppierten columnstore-index  
   Gilt für: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].
  
 Wenn Sie einen nicht gruppierten Columnstore-Index für eine Tabelle erstellen, können Sie die Daten in dieser Tabelle nicht mehr direkt ändern. Eine Abfrage mit INSERT, UPDATE, DELETE oder MERGE schlägt fehl, und es wird eine Fehlermeldung zurückgegeben. Um Daten in der Tabelle hinzuzufügen oder zu ändern, können Sie eine der folgenden Aktionen ausführen:  
  
-   Deaktivieren oder löschen Sie den Columnstore-Index. Anschließend können Sie die Daten in der Tabelle aktualisieren. Wenn Sie den Columnstore-Index deaktivieren, können Sie den Columnstore-Index nach dem Aktualisieren der Daten neu erstellen. Beispiel:  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Laden Sie Daten in eine Stagingtabelle ohne Columnstore-Index. Erstellen Sie einen Columnstore-Index für die Stagingtabelle. Wechseln Sie für die Stagingtabelle in eine leere Partition der Haupttabelle.  
  
-   Wechseln Sie für eine Partition in der Tabelle mit dem Columnstore-Index in eine leere Stagingtabelle. Wenn die Stagingtabelle über einen Columnstore-Index verfügt, deaktivieren Sie den Columnstore-Index. Nehmen Sie die gewünschten Updates vor. Erstellen bzw. erstellen Sie den Columnstore-Index neu. Wechseln Sie für die Stagingtabelle zurück in die (nun leere) Partition der Haupttabelle.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>A. Ändern Sie einen gruppierten Index in einen gruppierten columnstore-index  
 Mit der CREATE CLUSTERED COLUMNSTORE INDEX-Anweisung mit DROP_EXISTING = ON verwenden, können Sie:  
  
-   Ändern Sie einen gruppierten Index in einen gruppierten columnstore-Index.  
  
-   Erstellen Sie einen gruppierten columnstore-Index neu.  
  
 In diesem Beispiel erstellt die xDimProduct-Tabelle als eine Rowstore-Tabelle mit einem gruppierten Index und verwendet dann die gruppierten columnstore-INDEX erstellen, um die Tabelle aus einer Rowstore-Tabelle in eine columnstore-Tabelle zu ändern.  
  
```  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. Erstellen Sie einen gruppierten columnstore-Index neu  
 Baut auf dem vorherigen Beispiel und verwendet in diesem Beispiel CREATE CLUSTERED columnstore-INDEX, um den vorhandenen gruppierten columnstore-Index aufgerufen Cci_xDimProduct neu erstellen.  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. Ändern Sie den Namen eines gruppierten columnstore-Indexes  
 Um den Namen eines gruppierten columnstore-Index zu ändern, löschen Sie den vorhandenen gruppierten columnstore-Index, und klicken Sie dann erstellen Sie den Index mit einem neuen Namen neu zu.  
  
 Es wird empfohlen, diesen Vorgang eine kleine Tabelle oder eine leere Tabelle nur Aktionen. Er nimmt viel Zeit einen großen gruppierten columnstore-Index löschen und neu erstellen, mit einem anderen Namen.  
  
 Mithilfe des Cci_xDimProduct gruppierten columnstore-Indexes aus dem vorherigen Beispiel in diesem Beispiel löscht den Cci_xDimProduct gruppierten columnstore-Index, und klicken Sie dann neu erstellt den gruppierten columnstore-Index mit dem Namen Mycci_xDimProduct.  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. Konvertieren einer Columnstore-Tabelle in eine Rowstore-Tabelle mit einem gruppierten Index  
 Es gibt möglicherweise eine Situation, die für die Sie einen gruppierten columnstore-Index löschen und einen gruppierten Index erstellen möchten. Die Tabelle wird in der Rowstore-Format gespeichert. In diesem Beispiel konvertiert eine columnstore-Tabelle in eine Rowstore-Tabelle mit einem gruppierten Index mit dem gleichen Namen. Keine der Daten geht verloren. Alle Daten an die Rowstore-Tabelle und die aufgelisteten Spalten wird die Schlüsselspalten in dem gruppierten Index.  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. Konvertieren einer columnstore-Tabelle wieder in einen Rowstore-heap  
 Verwendung [DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32) den gruppierten columnstore-Index löschen und die Tabelle in einen Rowstore-Heap konvertieren. In diesem Beispiel konvertiert die Cci_xDimProduct-Tabelle in einen Rowstore-Heap an. Die Tabelle weiterhin verteilt werden, aber als Heap gespeichert wird.  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  

