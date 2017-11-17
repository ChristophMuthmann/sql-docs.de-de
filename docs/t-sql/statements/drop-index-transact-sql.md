---
title: DROP INDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_INDEX_TSQL
- DROP INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- nonclustered indexes [SQL Server], removing
- MAXDOP index option, DROP INDEX statement
- index removal [SQL Server]
- spatial indexes [SQL Server], dropping
- removing indexes
- deleting indexes
- dropping indexes
- MOVE TO clause
- clustered indexes, removing
- indexes [SQL Server], dropping
- filtered indexes [SQL Server], dropping
- ONLINE option
- indexes [SQL Server], moving
- XML indexes [SQL Server], dropping
- DROP INDEX statement
ms.assetid: 2b1464c8-934c-405f-8ef7-2949346b5372
caps.latest.revision: 99
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 59f78a8c62e8257eb09327d4b629ad678d9c0e69
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="drop-index-transact-sql"></a>DROP INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt einen oder mehrere relationale Indizes, räumliche Indizes, gefilterte Indizes oder XML-Indizes aus der aktuellen Datenbank. Sie können einen gruppierten Index löschen und die daraus resultierende Tabelle in einer einzigen Transaktion in eine andere Dateigruppe oder in ein anderes Partitionsschema verschieben, indem Sie die Option MOVE TO angeben.  
  
 Die DROP INDEX-Anweisung gilt nicht für Indizes, die durch Definieren der Einschränkung PRIMARY KEY oder UNIQUE erstellt wurden. Um die Einschränkung und den entsprechenden Index entfernen möchten, verwenden Sie [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) mit der DROP CONSTRAINT-Klausel.  
  
> [!IMPORTANT]  
>  Die Syntax, die in definierten `<drop_backward_compatible_index>` wird in einer zukünftigen Version entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung dieser Syntax bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen diese Funktion zurzeit verwendet wird. Verwenden Sie stattdessen die unter `<drop_relational_or_xml_index>` angegebene Syntax. XML-Indizes können mit abwärtskompatibler Syntax nicht gelöscht werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server (All options except filegroup and filestream apply to Azure SQL Database.)  
  
DROP INDEX [ IF EXISTS ]   
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
| <drop_backward_compatible_index> [ ,...n ]  
}  
  
<drop_relational_or_xml_or_spatial_index> ::=  
    index_name ON <object>   
    [ WITH ( <drop_clustered_index_option> [ ,...n ] ) ]  
  
<drop_backward_compatible_index> ::=  
    [ owner_name. ] table_or_view_name.index_name  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<drop_clustered_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
  | ONLINE = { ON | OFF }  
  | MOVE TO { partition_scheme_name ( column_name )   
            | filegroup_name  
            | "default"   
            }  
  [ FILESTREAM_ON { partition_scheme_name   
            | filestream_filegroup_name   
            | "default" } ]  
}  
```  
  
```  
-- Syntax for Azure SQL Database  
  
DROP INDEX  
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
}  
  
<drop_relational_or_xml_or_spatial_index> ::=   
    index_name ON <object>  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP INDEX index_name ON [ database_name . [schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht den Index nur dann, wenn sie bereits vorhanden ist.  
  
 *index_name*  
 Der Name des zu löschenden Index.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehört.  
  
 *table_or_view_name*  
 Der Name der Tabelle oder Sicht, die dem Index zugeordnet ist. Räumliche Indizes werden nur für Tabellen unterstützt.  
  
 Um einen Bericht über die Indizes eines Objekts anzuzeigen, verwenden die [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
 Die Windows Azure SQL-Datenbank unterstützt das aus drei Teilen bestehende Format database_name.[schema_name].object_name, wenn database_name die aktuelle Datenbank bzw. database_name tempdb ist und object_name mit # beginnt.  
  
 \<Drop_clustered_index_option >  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Steuert die Optionen für den gruppierten Index. Diese Optionen können nicht mit anderen Indextypen verwendet werden.  
  
 MAXDOP = *Max_degree_of_parallelism*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (Leistungsstufen P2 und P3 nur).  
  
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption für die Dauer des Indexvorgangs. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
> [!IMPORTANT]  
>  MAXDOP ist für räumliche Indizes oder XML-Indizes nicht zulässig.  
  
 *Max_degree_of_parallelism* sind möglich:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Begrenzt die Höchstzahl von Prozessoren in einem parallelen Indexvorgang auf die angegebene Zahl  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ONLINE = ON | **OFF**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob die zugrunde liegenden Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF.  
  
 ON  
 Langfristigen Tabellensperren werden nicht aufrechterhalten. Abfragen oder Updates der zugrunde liegenden Tabelle können fortgesetzt werden.  
  
 OFF  
 Tabellensperren werden angewendet, und die Tabelle steht für die Dauer der Indexerstellungsvorgangs nicht zur Verfügung.  
  
 Die Option ONLINE kann nur dann angegeben werden, wenn Sie gruppierte Indizes löschen. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MOVE TO { *Partition_scheme_name***(***Column_name***)** | *Filegroup_name*  |  **"**Standard**"**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]unterstützt "Default" als Dateigruppenname.  
  
 Gibt einen Speicherort an, an den die Datenzeilen verschoben werden, die sich zurzeit auf der Blattebene des gruppierten Index befinden. Die Daten werden in einen Heap an den neuen Speicherort verschoben. Als neuen Speicherort können Sie entweder ein Partitionsschema oder eine Dateigruppe angeben, das Partitionsschema oder die Dateigruppe muss jedoch bereits vorhanden sein. MOVE TO ist für indizierte Sichten oder nicht gruppierte Indizes nicht gültig. Wird kein Partitionsschema oder keine Dateigruppe angegeben, dann befindet sich die daraus resultierende Tabelle entsprechend der Definition für den gruppierten Index im Partitionsschema oder in der Dateigruppe.  
  
 Wird ein gruppierter Index mit MOVE TO gelöscht, werden alle nicht gruppierten Indizes für die Basistabelle neu erstellt. Sie verbleiben jedoch in ihren ursprünglichen Dateigruppen oder Partitionsschemas. Wenn die Basistabelle in eine andere Dateigruppe oder ein anderes Partitionsschema verschoben wird, werden die nicht gruppierten Indizes nicht verschoben, um dem neuen Speicherort der Basistabelle (Heap) zu entsprechen. Deshalb ist es möglich, dass die nicht gruppierten Indizes nicht mehr mit dem Heap ausgerichtet sind, selbst wenn sie vorher mit dem gruppierten Index ausgerichtet wurden. Weitere Informationen zur partitionierten indexausrichtung finden Sie unter [partitionierte Tabellen und Indizes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 *Partition_scheme_name* **(** *Column_name* **)**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt ein Partitionsschema als Speicherort für die resultierende Tabelle an. Das Partitionsschema muss bereits erstellt wurden durch Ausführen [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) oder [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). Wird kein Speicherort angegeben und ist die Tabelle partitioniert, dann wird die Tabelle in das Partitionsschema des vorhandenen gruppierten Index aufgenommen.  
  
 Für den Spaltennamen im Schema gibt es keine Beschränkung auf die Spalten in der Indexdefinition. Jede beliebige Spalte in der Basistabelle kann angegeben werden.  
  
 *filegroup_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt eine Dateigruppe als Speicherort für die resultierende Tabelle an. Wird kein Speicherort angegeben und ist die Tabelle nicht partitioniert, dann wird die resultierende Tabelle in die Dateigruppe aufgenommen, in der sich der gruppierte Index befindet. Die Dateigruppe muss bereits vorhanden sein.  
  
 **"**Standard**"**  
 Gibt den Standardspeicherort für die resultierende Tabelle an.  
  
> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in MOVE TO **"**Standard**"** oder MOVE TO **[**Standard**]**. Wenn **"**Standard**"** angegeben wird, muss die QUOTED_IDENTIFIER-Option ON festgelegt, für die aktuelle Sitzung. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FILESTREAM_ON { *Partition_scheme_name* | *Filestream_filegroup_name* | **"**Standard**"** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt einen Speicherort an, an den die FILESTREAM-Tabelle verschoben wird, die sich zurzeit auf der Blattebene des gruppierten Index befindet. Die Daten werden in einen Heap an den neuen Speicherort verschoben. Als neuen Speicherort können Sie entweder ein Partitionsschema oder eine Dateigruppe angeben, das Partitionsschema oder die Dateigruppe muss jedoch bereits vorhanden sein. FILESTREAM ON ist für indizierte Sichten oder nicht gruppierte Indizes unzulässig. Wird kein Partitionsschema angegeben, werden die Daten in demselben Partitionsschema platziert, das für den gruppierten Index definiert war.  
  
 *partition_scheme_name*  
 Gibt ein Partitionsschema für FILESTREAM-Daten an. Das Partitionsschema muss bereits erstellt wurden durch Ausführen [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) oder [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). Wird kein Speicherort angegeben und ist die Tabelle partitioniert, dann wird die Tabelle in das Partitionsschema des vorhandenen gruppierten Index aufgenommen.  
  
 Wenn Sie ein Partitionsschema für MOVE TO angeben, müssen Sie dasselbe Partitionsschema für FILESTREAM ON verwenden.  
  
 *filestream_filegroup_name*  
 Gibt eine FILESTREAM-Dateigruppe für FILESTREAM-Daten an. Wenn kein Speicherort angegeben und die Tabelle nicht partitioniert ist, werden die Daten in die FILESTREAM-Standarddateigruppe eingefügt.  
  
 **"**Standard**"**  
 Gibt den Standardspeicherort für FILESTREAM-Daten an.  
  
> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in MOVE TO **"**Standard**"** oder MOVE TO **[**Standard**]**. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein nicht gruppierter Index gelöscht wird, wird die Indexdefinition aus den Metadaten entfernt, und die Indexdatenseiten (in der B-Struktur) werden aus den Datenbankdateien entfernt. Wenn ein gruppierter Index gelöscht wird, wird die Indexdefinition aus den Metadaten entfernt und die auf der Blattebene des gruppierten Indexes gespeicherten Datenzeilen werden in der daraus resultierenden, nicht sortierten Tabelle (Heap) gespeichert. Der gesamte Speicherplatz, der vorher für den Index benötigt wurde, wird wieder freigegeben. Dieser Speicherplatz kann dann für beliebige Datenbankobjekte verwendet werden.  
  
 Ein Index kann nicht gelöscht werden, wenn die Dateigruppe, in der sich der Index befindet, offline oder schreibgeschützt ist.  
  
 Wenn der gruppierte Index einer indizierten Sicht gelöscht wird, dann werden alle nicht gruppierten Indizes und automatisch erstellten Statistiken dieser Sicht automatisch gelöscht. Manuell erstellte Statistiken werden nicht gelöscht.  
  
 Die Syntax*Table_or_view_name***.** *Index_name* wird aus Gründen der Abwärtskompatibilität beibehalten. XML-Indizes oder räumliche Indizes können mit abwärtskompatibler Syntax nicht gelöscht werden.  
  
 Werden Indizes mit 128 oder mehr Blöcken gelöscht, verzögert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Aufhebung der Seitenzuordnungen und der dazugehörigen Sperren, bis ein Commit für die Transaktion ausgeführt wurde.  
  
 Gelegentlich werden Indizes gelöscht und neu erstellt, um den Index neu zu organisieren oder neu zu erstellen, beispielsweise um einen neuen Füllfaktorwert anzuwenden oder um Daten nach dem Massenladen neu zu organisieren. Hierzu verwenden [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)ist jedoch effizienter, insbesondere bei gruppierten Indizes. ALTER INDEX REBUILD verwendet Optimierungen, um den Aufwand der Neuerstellung der nicht gruppierten Indizes zu vermeiden.  
  
## <a name="using-options-with-drop-index"></a>Verwenden von Optionen mit DROP INDEX  
 Sie können folgende Indexoptionen festlegen, wenn Sie einen gruppierten Index löschen: MAXDOP, ONLINE und MOVE TO.  
  
 Verwenden Sie MOVE TO, um den gruppierten Index zu löschen und um die daraus resultierende Tabelle in einer einzigen Transaktion in eine andere Dateigruppe oder in ein anderes Partitionsschema zu verschieben.  
  
 Wenn Sie ONLINE = ON angeben, werden Abfragen und Änderungen der zugrunde liegenden Daten und dazugehörigen nicht gruppierten Indizes nicht von den DROP INDEX-Transaktion blockiert. Online kann jeweils nur ein gruppierter Index gelöscht werden. Eine vollständige Beschreibung der Option "ONLINE", finden Sie unter [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 Sie können einen gruppierten Index online löschen, wenn der Index für eine Sicht deaktiviert ist oder enthält **Text**, **Ntext**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **Xml** Spalten in den Datenzeilen auf Blattebene.  
  
 Für das Verwenden der Optionen ONLINE = ON und MOVE TO wird zusätzlicher temporärer Speicherplatz benötigt.  
  
 Nachdem ein Index gelöscht wird, wird der daraus resultierende Heap in der **sys.indexes** -Katalogsicht mit NULL-Wert in der **Namen** Spalte. Zum Anzeigen des Tabellennamens verknüpfen **sys.indexes** mit **sys.tables** auf **Object_id**. Unter Beispiel D finden Sie eine Beispielabfrage.  
  
 Auf Multiprozessorcomputern, auf denen [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] oder höher ausgeführt wird, kann DROP INDEX mehr Prozessoren zum Ausführen von Scan- und Sortierungsvorgängen verwenden, die dem Löschen des gruppierten Index zugeordnet sind. Dies geschieht in gleicher Weise wie für andere Abfragen. Sie können die Anzahl der Prozessoren, die zur Ausführung der DROP INDEX-Anweisung verwendet werden, durch Angeben der MAXDOP-Indexoption manuell konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 Beim Löschen eines gruppierten Indexes behalten die entsprechenden Heappartitionen ihre Einstellung für die Datenkomprimierung bei, sofern nicht das Partitionierungsschema geändert wird. Wenn das Partitionierungsschema geändert wird, werden alle Partitionen in einem unkomprimierten Status (DATA_COMPRESSION = NONE) neu erstellt. Um einen gruppierten Index zu löschen und das Partitionierungsschema zu ändern, sind die beiden folgenden Schritte erforderlich:  
  
1.  Löschen Sie den gruppierten Index.  
  
2.  Ändern Sie die Tabelle mit der Option ALTER TABLE ... REBUILD ..., die die Komprimierungsoption angibt.  
  
Wenn ein gruppierter Index OFFLINE gelöscht wird, werden nur die oberen Ebenen des gruppierten Index entfernt. Daher wird dieser Vorgang ziemlich schnell ausgeführt. Wenn ein gruppierter Index ONLINE gelöscht wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt den Heap zwei Mal neu, Mal für Schritt 1 und einmal für Schritt 2. Weitere Informationen zur datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
## <a name="xml-indexes"></a>XML-Indizes  
 Optionen können nicht angegeben werden, wenn Sie AnXML Index löschen. Darüber hinaus können keine der *Table_or_view_name***.** *Index_name* Syntax. Wird ein primärer XML-Index gelöscht, werden alle dazugehörigen sekundären XML-Indizes automatisch gelöscht. Weitere Informationen finden Sie unter [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="spatial-indexes"></a>Räumliche Indizes  
 Räumliche Indizes werden nur für Tabellen unterstützt. Wenn Sie einen räumlichen Index löschen, Sie können nicht angeben von Optionen oder **.** *Index_name*. Die korrekte Syntax lautet wie folgt:  
  
 DROP INDEX *Spatial_index_name* ON *Spatial_table_name*;  
  
 Weitere Informationen zu räumlichen Indizes finden Sie unter [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Für das Ausführen von DROP INDEX ist mindestens eine ALTER-Berechtigung für die Tabelle oder Sicht erforderlich. Über diese Berechtigungen verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** und die Mitglieder der festen Datenbankrollen **db_ddladmin** und **db_owner** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-an-index"></a>A. Löschen eines Indexes  
 Das folgende Beispiel löscht den Index `IX_ProductVendor_VendorID` auf die `ProductVendor` -Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank.  
  
```  
DROP INDEX IX_ProductVendor_BusinessEntityID   
    ON Purchasing.ProductVendor;  
GO  
```  
  
### <a name="b-dropping-multiple-indexes"></a>B. Löschen mehrerer Indizes  
 Im folgenden Beispiel werden zwei Indizes in einer einzelnen Transaktion in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank gelöscht.  
  
```  
DROP INDEX  
    IX_PurchaseOrderHeader_EmployeeID ON Purchasing.PurchaseOrderHeader,  
    IX_Address_StateProvinceID ON Person.Address;  
GO  
```  
  
### <a name="c-dropping-a-clustered-index-online-and-setting-the-maxdop-option"></a>C. Onlinelöschen eines gruppierten Indexes und Festlegen der MAXDOP-Option  
 Im folgenden Beispiel wird ein gruppierter Index gelöscht, wobei für die Option `ONLINE` die Einstellung `ON` und für `MAXDOP` die Einstellung `8` festgelegt ist. Da die Option MOVE TO nicht angegeben wurde, wird die daraus resultierende Tabelle in der gleichen Dateigruppe wie der Index gespeichert. In diesem Beispiel verwendet die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
```  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials WITH (ONLINE = ON, MAXDOP = 2);  
GO  
```  
  
### <a name="d-dropping-a-clustered-index-online-and-moving-the-table-to-a-new-filegroup"></a>D. Onlinelöschen eines gruppierten Indexes und Verschieben der Tabelle in eine neue Dateigruppe  
 Im folgenden Beispiel wird ein gruppierter Index online gelöscht, und die daraus resultierende Tabelle (Heap) wird in die Dateigruppe `NewGroup` verschoben, wofür die `MOVE TO` -Klausel verwendet wird. Die Katalogsichten `sys.indexes`, `sys.tables`und `sys.filegroups` werden abgefragt, um die Platzierung von Index und Tabelle in den Dateigruppen vor und nach der Verschiebung zu prüfen. (Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie die DROP INDEX IF EXISTS-Syntax verwenden.)  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
--Create a clustered index on the PRIMARY filegroup if the index does not exist.  
CREATE UNIQUE CLUSTERED INDEX  
    AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
        ON Production.BillOfMaterials (ProductAssemblyID, ComponentID,   
        StartDate)  
    ON 'PRIMARY';  
GO  
-- Verify filegroup location of the clustered index.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U')  
GO  
--Create filegroup NewGroup if it does not exist.  
IF NOT EXISTS (SELECT name FROM sys.filegroups  
                WHERE name = N'NewGroup')  
    BEGIN  
    ALTER DATABASE AdventureWorks2012  
        ADD FILEGROUP NewGroup;  
    ALTER DATABASE AdventureWorks2012  
        ADD FILE (NAME = File1,  
            FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\File1.ndf')  
        TO FILEGROUP NewGroup;  
    END  
GO  
--Verify new filegroup  
SELECT * from sys.filegroups;  
GO  
-- Drop the clustered index and move the BillOfMaterials table to  
-- the Newgroup filegroup.  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials   
    WITH (ONLINE = ON, MOVE TO NewGroup);  
GO  
-- Verify filegroup location of the moved table.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U');  
GO  
```  
  
### <a name="e-dropping-a-primary-key-constraint-online"></a>E. Onlinelöschen einer PRIMARY KEY-Einschränkung  
 Indizes, die als Ergebnis der Erstellung von PRIMARY KEY- oder UNIQUE-Einschränkungen erstellt werden, können nicht mit DROP INDEX gelöscht werden. Vielmehr werden sie mit der ALTER TABLE DROP CONSTRAINT-Anweisung gelöscht. Weitere Informationen finden Sie unter [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 Im folgenden Beispiel wird ein gruppierter Index mit einer PRIMARY KEY-Einschränkung gelöscht, indem die Einschränkung gelöscht wird. Die Tabelle `ProductCostHistory` besitzt keine FOREIGN KEY-Einschränkung. Wenn dem so wäre, müssten diese Einschränkungen zuerst entfernt werden.  
  
```  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
```  
  
### <a name="f-dropping-an-xml-index"></a>F. Löschen eines XMl-Indexes  
 Im folgenden Beispiel wird ein XML-Index in der `ProductModel`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank gelöscht.  
  
```  
DROP INDEX PXML_ProductModel_CatalogDescription   
    ON Production.ProductModel;  
```  
  
### <a name="g-dropping-a-clustered-index-on-a-filestream-table"></a>G. Löschen eines gruppierten Indexes in einer FILESTREAM-Tabelle  
 Im folgenden Beispiel wird ein gruppierter Index online gelöscht, und die daraus resultierende Tabelle (Heap) und die FILESTREAM-Daten werden in das `MyPartitionScheme`-Partitionsschema verschoben, wofür die `MOVE TO`-Klausel und die `FILESTREAM ON`-Klausel verwendet werden.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
DROP INDEX PK_MyClusteredIndex   
    ON dbo.MyTable   
    WITH (MOVE TO MyPartitionScheme,  
          FILESTREAM_ON MyPartitionScheme);  
GO  
```  

  
## <a name="see-also"></a>Siehe auch  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [Erstellen Sie SPATIAL INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [Erstellen von XML-INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  



