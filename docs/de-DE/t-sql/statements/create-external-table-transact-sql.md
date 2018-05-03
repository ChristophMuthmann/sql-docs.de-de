---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 30
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 352bdf39861d8874f1e7b535c2ef954e65d48339
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Erstellt eine externe Tabelle für PolyBase oder elastische Datenbankabfragen. Abhängig vom jeweiligen Szenario unterscheidet sich die Syntax deutlich. Eine externe Tabelle, die für PolyBase erstellt wurde, kann nicht für elastische Datenbankabfragen verwendet werden.  Auf ähnliche Weise kann eine externen Tabelle, die für elastische Datenbankenabfragen erstellt wurde, nicht für PolyBase, usw. verwendet werden. 
  
> [!NOTE]  
>  PolyBase wird nur in SQL Server 2016 (oder höher), Azure SQL Data Warehouse und Parallel Data Warehouse unterstützt. Elastische Datenbankabfragen werden nur auf Azure SQL-Datenbank v12 oder höher unterstützt.  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet externe Tabellen, um auf Daten in einem Hadoop-Cluster oder in Azure Blob Storage zuzugreifen. Eine externe PolyBase-Tabelle, die auf Daten in einem Hadoop-Cluster oder in Azure Blob Storage verweist, kann auch zum Erstellen einer externen Tabelle für [elastische Datenbankabfragen](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) verwendet werden.  
  
 Verwenden Sie eine externe Tabelle, um:  
  
-   Daten in Hadoop oder in Azure Blob Storage mit [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen abzufragen.  
  
-   Daten aus Hadoop oder Azure Blob Storage in Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zu importieren und speichern.  
  
-   Eine externe Tabelle für die Verwendung mit einer elastischen Datenbankabfrage  
     zu erstellen.  
     
- Die Daten aus Azure Data Lake Store in Azure SQL Data Warehouse zu importieren und zu speichern
  
 Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) und [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name* . [ schema_name ] . | schema_name. ] *table_name*  
 Ein- bis dreiteiliger Name der Tabelle, die erstellt werden soll. Für eine externe Tabelle werden nur die Metadaten der Tabelle zusammen mit den grundlegenden Statistiken über die Datei oder Ordner, auf die in Hadoop oder Azure Blob Storage verwiesen wird, gespeichert. Es werden keine tatsächlichen Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben oder gespeichert.  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE erlaubt eine oder mehrere Spaltendefinitionen. CREATE EXTERNAL TABLE und CREATE TABLE verwenden dieselbe Syntax zur Spaltendefinition. Eine Ausnahme ist die Tatsache, dass Sie DEFAULT CONSTRAINT nicht in externen Tabellen verwenden können. Die vollständigen Details zu Spaltendefinitionen und deren Datentypen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) und [CREATE TABLE in der Azure SQL-Datenbank](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 Die Spaltendefinitionen, einschließlich der Datentypen und die Anzahl der Spalten, müssen mit den Daten in externen Dateien übereinstimmen. Wenn ein Konflikt besteht, werden die Zeilen der Datei beim Abfragen der tatsächlichen Daten zurückgewiesen.  
  
 Für externe Tabellen, die auf Dateien in externen Datenquellen verweisen, müssen die Spalten- und Typdefinitionen dem genauen Schema der externen Datei zugeordnet werden. Beim Definieren von Datentypen, die auf Daten verweisen, die in Hadoop/Hive gespeichert sind, verwenden Sie die folgenden Zuordnungen zwischen Datentypen von SQL und Hive und wandeln Sie den Typ in einen SQL-Datentyp um, wenn Sie daraus auswählen. Die Typen umfassen alle Versionen von Hive, sofern nicht anders angegeben.

> [!NOTE]  
>  SQL Server unterstützt den Datenwert _unendlich_ von Hive nicht in beliebigen Konvertierungen. PolyBase schlägt mit einem Datentypkonvertierungsfehler fehl.


|SQL-Datentyp|.NET-Datentyp|Hive-Datentyp|Hadoop/Java-Datentyp|Kommentare|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|Nur für unsignierte Zahlen.|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|ssNoversion|Int32|ssNoversion|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|FLOAT|Double|double|DoubleWritable||  
|REAL|Single|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|Zeichenfolge<br /><br /> Char[]|Zeichenfolge|text||  
|NVARCHAR|Zeichenfolge<br /><br /> Char[]|Zeichenfolge|Textmodus||  
|char|Zeichenfolge<br /><br /> Char[]|Zeichenfolge|Textmodus||  
|varchar|Zeichenfolge<br /><br /> Char[]|Zeichenfolge|Textmodus||  
|BINARY|Byte[]|BINARY|BytesWritable|Gilt für Hive 0.8 und höher.|  
|varbinary|Byte[]|BINARY|BytesWritable|Gilt für Hive 0.8 und höher.|  
|date|datetime|timestamp|TimestampWritable||  
|smalldatetime|datetime|timestamp|TimestampWritable||  
|datetime2|datetime|timestamp|TimestampWritable||  
|DATETIME|datetime|timestamp|TimestampWritable||  
|Uhrzeit|TimeSpan|timestamp|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|Gilt für Hive 0.11 und höher.|  
  
 LOCATION =  '*folder_or_filepath*'  
 Gibt den Ordner oder den Dateipfad und Dateinamen für die tatsächlichen Daten in Hadoop oder Azure Blob Storage an. Der Speicherort beginnt im Stammordner. Der Stammordner ist der in der externen Datenquelle angegebene Datenspeicherort.  


In SQL Server erstellt die Anweisung CREATE EXTERNAL TABLE den Pfad und den Ordner, wenn diese noch nicht vorhanden sind. Sie können dann INSERT INTO zum Exportieren von Daten aus einer lokalen SQL Server-Tabelle in die externe Datenquelle verwenden. Weitere Informationen finden Sie unter [PolyBase-Abfragen](/sql/relational-databases/polybase/polybase-queries). 

In SQL Data Warehouse und Analytics Platform System erstellt die Anweisung [CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) den Pfad und den Ordner, wenn diese noch nicht vorhanden sind. In diesen zwei Produkten erstellt CREATE EXTERNAL TABLE den Pfad und den Ordner nicht.

  
 Wenn LOCATION als Ordner angegeben wird, ruft eine PolyBase-Abfrage, die aus der externen Tabelle auswählt, Dateien aus dem Ordner und allen Unterordnern ab. Hadoop und PolyBase geben keine ausgeblendeten Ordner zurück. Es werden auch keine Dateien zurückgegeben, deren Dateiname mit einem Unterstrich (_) oder einem Punkt (.) beginnt.  
  
 In diesem Beispiel gibt eine PolyBase-Abfrage Zeilen aus „mydata.txt“ und „mydata2.txt“ zurück, wenn LOCATION='/webdata/'.  „Mydata3.txt“ wird nicht zurückgegeben, da es sich um einen Unterordner des ausgeblendeten Ordners handelt. Es werden keine „_hidden.txt“-Dateien zurückgegeben, da es sich um eine ausgeblendete Datei handelt.  
  
 ![Rekursive Daten für externe Tabellen](../../t-sql/statements/media/aps-polybase-folder-traversal.png "Recursive data for external tables")  
  
 Um den Standardordner zu ändern, und nur aus dem Stammordner zu lesen, legen Sie das Attribut \<polybase.recursive.traversal> in der Konfigurationsdatei „core-site.xml“ auf FALSE fest. Diese Datei befindet sich unter `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Beispiel: `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Gibt den Namen der externen Datenquelle an, die den Speicherort der externen Daten enthält. Dieser Speicherort ist entweder eine Hadoop oder ein Azure Blob Storage. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Gibt den Namen des externen Dateiformatobjekts an, das den Dateityp und die Komprimierungsmethode für die externen Daten enthält. Verwenden Sie zum Erstellen eines externen Dateiformats [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Reject-Optionen  
 Sie können Reject-Parameter angeben, die bestimmen, wie PolyBase *modifizierte* Datensätze behandelt, die aus der externen Datenquelle abgerufen werden. Ein Datensatz gilt als „dirty“ (modifiziert), wenn die tatsächlichen Datentypen oder die Anzahl der Spalten nicht den Spaltendefinitionen der externen Tabelle entsprechen.  
  
 Wenn Sie die Reject-Werte nicht angeben oder ändern, verwendet PolyBase Standardwerte. Diese Informationen über die Reject-Parameter werden als zusätzliche Metadaten gespeichert, wenn Sie eine externe Tabelle mit der CREATE EXTERNAL TABLE-Anweisung erstellen.   Wenn eine zukünftige SELECT- oder SELECT INTO SELECT-Anweisung Daten aus der externen Tabelle auswählt, wird PolyBase die Reject-Optionen verwenden, um die Anzahl oder den Prozentsatz der Zeilen zu bestimmen, die zurückgewiesen werden können, bevor die tatsächliche Abfrage fehlschlägt. zugreifen. Die Abfrage wird (Teil-) Ergebnisse zurückgeben, bis der Reject-Schwellenwert überschritten wird. Es wird dann eine entsprechende Fehlermeldung ausgelöst.  
  
 REJECT_TYPE = **value** | percentage  
 Gibt an, ob die Option „REJECT_VALUE“ als Literalwert oder als Prozentsatz angegeben wird.  
  
 Wert  
 REJECT_VALUE ist ein Literalwert und kein Prozentsatz. Die PolyBase-Abfrage schlägt fehl, wenn die Anzahl der abgelehnten Zeilen *reject_value* überschreitet.  
  
 Wenn beispielsweise REJECT_VALUE = 5 und REJECT_TYPE = Wert, wird die PolyBase-SELECT-Abfrage fehlschlagen, nachdem 5 Zeilen abgelehnt wurden.  
  
 Prozentwert  
 REJECT_VALUE ist ein Prozentsatz und kein Literalwert. Eine PolyBase-Abfrage schlägt fehl, wenn der *Prozentsatz* fehlerhafter Zeilen *reject_value* überschreitet. Der Prozentsatz der fehlerhaften Zeilen wird in Intervallen berechnet.  
  
 REJECT_VALUE = *reject_value*  
 Gibt den Wert oder den Prozentsatz der Zeilen an, die zurückgewiesen werden können, bevor die Abfrage fehlschlägt.  
  
 Wenn REJECT_TYPE = Wert, muss *reject_value* eine ganze Zahl zwischen 0 und 2.147.483.647 sein.  
  
 Wenn REJECT_TYPE = Prozentzahl, muss *reject_value* eine Gleitkommazahl zwischen 0 und 100 sein.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Dieses Attribut ist erforderlich, wenn Sie REJECT_TYPE = Prozentsatz angeben. Bestimmt die Anzahl der Zeilen, bei denen versucht wird, sie abzurufen, bevor die PolyBase den Prozentsatz der abgelehnten Zeilen neu berechnet.  
  
 Der *reject_sample_value*-Parameter muss eine ganze Zahl zwischen 0 und 2.147.483.647 sein.  
  
 Ist beispielsweise REJECT_SAMPLE_VALUE = 1000, dann berechnet PolyBase den Prozentsatz von fehlerhaften Zeilen nach dem Importversuch von 1000 Zeilen aus der externen Datendatei. Ist der Prozentsatz von fehlerhaften Zeilen kleiner als *reject_value*, führt PolyBase einen erneuten Abrufversuch von 1000 Zeilen aus. Nach jedem weiteren Importversuch von 1000 Zeilen wird der Prozentsatz von fehlerhaften Zeilen weiterhin neu berechnet.  
  
> [!NOTE]  
>  Da die Berechnung des Prozentsatzes von fehlerhaften Zeilen durch PolyBase in Intervallen erfolgt, kann der tatsächliche Prozentsatz fehlerhafter Zeilen *reject_value* überschreiten.  
  
 Beispiel:  
  
 In diesem Beispiel wird verdeutlicht, wie die drei REJECT-Optionen interagieren. Gilt beispielsweise: REJECT_TYPE = Prozentsatz, REJECT_VALUE = 30 und REJECT_SAMPLE_VALUE = 100, dann könnte das folgende Szenario auftreten:  
  
-   PolyBase versucht, die ersten 100 Zeilen abzurufen. Davon sind 25 fehlerhaft und 75 erfolgreich.  
  
-   Der Prozentsatz der berechneten fehlerhaften Zeilen ist mit 25 % kleiner als der REJECT-Wert von 30 %. Daher wird PolyBase weiterhin versuchen, Daten aus der externen Datenquelle abzurufen.  
  
-   PolyBase versucht, die nächsten 100 Zeilen zu laden. Dieses Mal sind 25 erfolgreich und 75 fehlerhaft.  
  
-   Der Prozentsatz fehlerhafter Zeilen wird mit 50 % neu berechnet. Der Prozentsatz fehlerhafter Zeilen hat den REJECT-Wert von 30 % überschritten.  
  
-   Die PolyBase-Abfrage schlägt fehl, da nach der Rückgabe der ersten 200 Zeilen 50 % der Zeilen abgelehnt werden. Beachten Sie, dass übereinstimmende Zeilen zurückgegeben wurden, bevor die PolyBase-Abfrage erkennt, dass der Schwellenwert zum Zurückweisen überschritten wurde.  
  
 Externe Shardtabellenoptionen  
 Gibt die externe Datenquelle (eine nicht-SQL Server-Datenquelle) und eine Verteilungsmethode für die [elastische Datenbankabfrage](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) an.  
  
 DATA_SOURCE  
 Eine externe Datenquelle wie Daten, die in einem Hadoop-Dateisystem, Azure Blob Storage oder in einem [Shardzuordnungs-Manager](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/) gespeichert sind.  
  
 SCHEMA_NAME  
 Die SCHEMA_NAME-Klausel bietet die Möglichkeit, die externe Tabellendefinition einer Tabelle in einem anderen Schema auf der Remotedatenbank zuzuordnen. Verwenden Sie diese Option, um zwischen Schemas zu unterscheiden, die auf den lokalen und Remotedatenbanken vorhanden sind.  
  
 OBJECT_NAME  
 Die OBJECT_NAME-Klausel bietet die Möglichkeit, die externe Tabellendefinition einer Tabelle mit einem anderen Namen auf der Remotedatenbank zuzuordnen. Verwenden Sie diese Option, um zwischen Objektnamen zu unterscheiden, die auf den lokalen und Remotedatenbanken vorhanden sind.  
  
 DISTRIBUTION  
 Optional. Dies ist nur für Datenbanken des Typs SHARD_MAP_MANAGER erforderlich. Steuert, ob eine Tabelle als Tabelle mit Shards oder replizierte Tabelle behandelt wird. Mit **SHARDED**-Tabellen (*Spaltenname*) überlappen die Daten aus unterschiedlichen Tabellen nicht. **REPLICATED** gibt an, dass Tabellen dieselben Daten auf jeder Shard enthalten. **ROUND_ROBIN** gibt an, dass eine anwendungsspezifische Methode zum Verteilen von Daten verwendet wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Folgende Benutzerberechtigungen sind erforderlich:  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 Beachten Sie, dass die Anmeldung, die die externe Datenquelle erstellt, die Berechtigung zum Lesen und Schreiben in der externen Datenquelle, die in Hadoop oder Azure Blob Storage gespeichert ist, benötigt.  


 > [!IMPORTANT]  

>  Mit der Berechtigung ALTER ANY EXTERNAL DATA SOURCE besitzt jeder Prinzipal die Fähigkeit, alle externen Datenquellenobjekte zu erstellen und zu ändern. Damit können sie auch auf alle datenbankweit gültigen Anmeldeinformationen der Datenbank zugreifen. Da es sich hierbei um eine weitreichende Berechtigung handelt, darf sie nur vertrauenswürdigen Prinzipalen innerhalb des Systems erteilt werden.

## <a name="error-handling"></a>Fehlerbehandlung  
 Beim Ausführen der CREATE EXTERNAL TABLE-Anweisung versucht PolyBase, eine Verbindung mit der externen Datenquelle herzustellen. Tritt bei der Verbindung ein Fehler auf, schlägt die Anweisung fehl. Die externe Tabelle wird nicht erstellt. Da PolyBase erneut versucht, die Verbindung aufzubauen, bevor die Abfrage endgültig fehlschlägt, kann es eine Minute oder länger dauern, bis der Befehl fehlschlägt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 PolyBase speichert die aus der externen Datenquelle abgerufenen Zeilen in Szenarios mit Ad-hoc-Abfragen, d.h. bei SELECT FROM EXTERNAL TABLE, in einer temporären Tabelle. Nachdem die Abfrage abgeschlossen ist, entfernt und löscht PolyBase die temporäre Tabelle. Es werden keine permanenten Daten in SQL-Tabellen gespeichert.  
  
 Im Gegensatz dazu speichert PolyBase die aus der externen Datenquelle abgerufenen Zeilen in Importszenarios, d.h. bei SELECT INTO FROM EXTERNAL TABLE, permanent in einer SQL-Tabelle. Die neue Tabelle wird beim Ausführen der Abfrage erstellt, wenn Polybase die externen Daten abruft.  
  
 PolyBase kann einen Teil der Abfrageberechnung an Hadoop übertragen, um die Abfrageleistung zu verbessern. Dies wird als Prädikatweitergabe bezeichnet. Um dies zu aktivieren, geben Sie die Option „Resource Manager Location“ von Hadoop in [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) an.  
  
 Sie können zahlreiche externe Tabellen erstellen, die auf die gleichen oder andere externe Datenquellen verweisen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 In CTP2 wird die Exportfunktion nicht unterstützt. Beispielsweise werden SQL-Daten in der externen Datenquelle permanent gespeichert. Diese Funktion wird in CTP3 verfügbar sein.  
  
 Da sich die Daten für eine externe Tabelle nicht auf dem Gerät befinden, werden sie nicht von PolyBase kontrolliert und können jederzeit von einem externen Prozess geändert oder gelöscht werden. Aus diesem Grund sind Abfrageergebnisse für eine externe Tabelle nicht garantiert deterministisch. Die gleiche Abfrage kann bei jeder Ausführung für eine externe Tabelle unterschiedliche Ergebnisse zurückgeben. Auf ähnliche Weise kann eine Abfrage fehlschlagen, wenn die externen Daten entfernt oder verschoben werden.  
  
 Sie können zahlreiche externe Tabellen erstellen, die alle auf unterschiedliche externe Datenquellen verweisen. Wenn Sie jedoch Abfragen für verschiedene Hadoop-Datenquellen gleichzeitig ausführen, muss jede Hadoop-Datenquelle die gleiche „Hadoop Connectivity“-Serverkonfigurationseinstellung verwenden. Beispielsweise können Sie nicht gleichzeitig eine Abfrage für einen Cloudera Hadoop-Cluster und einen Hortonworks Hadoop-Cluster ausführen, da diese unterschiedliche Konfigurationseinstellungen verwenden. Weitere Informationen zu den Konfigurationseinstellungen und den unterstützten Kombinationen finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Nur diese DDL-Anweisungen (Data Definition Language) sind in externen Tabellen zulässig:  
  
-   CREATE TABLE und DROP TABLE  
  
-   CREATE STATISTICS und DROP STATISTICS  
Hinweis: CREATE und DROP STATISTICS werden nicht auf externen Tabellen in der Azure SQL-Datenbank unterstützt. 
  
-   CREATE VIEW und DROP VIEW  
  
 Nicht unterstützte Konstruktionen und Operationen:  
  
-   Die DEFAULT-Einschränkung auf externen Tabellenspalten  
  
-   DML-Vorgänge (Data Manipulation Language): DELETE, INSERT und UPDATE  
  
 Abfrageeinschränkungen:  
  
 PolyBase kann bei 32 gleichzeitigen PolyBase-Abfragen maximal 33.000 Dateien pro Ordner verarbeiten. Diese maximale Anzahl schließt sowohl Dateien als auch Unterordner im jeweiligen HDFS-Ordner ein. Werden weniger als 32 Abfragen gleichzeitig ausgeführt, können auch PolyBase-Abfragen für Ordner in HDFS mit mehr als 33.000 Dateien ausgeführt werden. Es wird empfohlen, dass Sie externe Dateipfade kurz halten und nicht mehr als 30.000 Dateien pro HDFS-Ordner verwenden. Wenn auf zu viele Dateien verwiesen wird, kann eine Out-of-Memory-Ausnahme von Java Virtual Machine (JVM) auftreten.  

Einschränkungen der Tabellenbreite: PolyBase in SQL Server 2016 verfügt über eine Begrenzung für die Zeilenbreite von 32 KB, basierend auf der Maximalgröße einer einzelnen gültigen Zeile je Tabellendefinition. Wenn die Summe des Spaltenschemas größer als 32 KB ist, wird PolyBase die Daten nicht abfragen können. 

Diese Einschränkung wurde in SQL Data Warehouse auf 1 MB erhöht.


## <a name="locking"></a>Sperren  
 Freigegebene Sperre für das SCHEMARESOLUTION-Objekt.  
  
## <a name="security"></a>Security  
 Die Datendateien für eine externe Tabelle werden in Hadoop oder Azure Blob Storage gespeichert. Diese Datendateien werden von Ihrem eigenen Prozess erstellt und verwaltet. Die Sicherheit der externen Daten liegt in Ihrer Verantwortung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Erstellen einer externen Tabelle mit Daten im Texttrennzeichenformat  
 Dieses Beispiel zeigt die erforderlichen Schritte zur Erstellung einer externen Tabelle, die Daten in Texttrennzeichendateien formatiert. Es definiert eine externe Datenquelle *mydatasource* und ein externes Dateiformat *myfileformat*. In der CREATE EXTERNAL TABLE-Anweisung wird dann auf diese Objekte auf Datenbankebene verwiesen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) und unter [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Erstellen einer externen Tabelle mit Daten im RCFile-Format  
 Dieses Beispiel zeigt die erforderlichen Schritte zur Erstellung einer externen Tabelle, die Daten als RCFiles formatiert. Es definiert eine externe Datenquelle *mydatasource_rc* und ein externes Dateiformat *mfileformat_rc*. In der CREATE EXTERNAL TABLE-Anweisung wird dann auf diese Objekte auf Datenbankebene verwiesen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) und unter [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Erstellen einer externen Tabelle mit Daten im ORC-Format  
 Dieses Beispiel zeigt die erforderlichen Schritte zur Erstellung einer externen Tabelle, die Daten als ORC-Dateien formatiert. Es definiert eine externe Datenquelle mydatasource_orc und ein externes Dateiformat myfileformat_orc. In der CREATE EXTERNAL TABLE-Anweisung wird dann auf diese Objekte auf Datenbankebene verwiesen. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) und unter [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. Abfragen von Hadoop-Daten  
 Clickstream ist eine externe Tabelle, die mit der durch Tabstopps getrennte Textdatei „employee.tbl“ in einem Hadoop-Cluster verbunden ist. Die folgende Abfrage sieht wie eine Abfrage für eine Standardtabelle aus. Allerdings ruft diese Abfrage Daten aus Hadoop ab und berechnet dann die Ergebnisse.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Verknüpfen von Hadoop-Daten mit SQL-Daten  
 Diese Abfrage sieht wie ein Standard-JOIN für zwei SQL-Tabellen aus. Der Unterschied besteht darin, dass PolyBase die Clickstream-Daten aus Hadoop abruft und sie dann der UrlDescription-Tabelle hinzufügt. Eine Tabelle ist eine externe Tabelle, und die andere ist eine standardmäßige SQL-Tabelle.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importieren Sie Daten aus Hadoop in eine SQL-Tabelle  
 Dieses Beispiel erstellt eine neue „ms_user“-SQL-Tabelle, die das Ergebnis einer Verknüpfung zwischen der standardmäßigen SQL-Tabelle *user* und der externen Tabelle *ClickStream* permanent speichert.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Erstellen einer externen Tabelle für eine Datenquelle mit Shards  
 In diesem Beispiel wird eine Remote-DMV mithilfe der Klauseln SCHEMA_NAME und OBJECT_NAME einer externen Tabelle zugeordnet.  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importieren von Daten aus ADLS in Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. Verknüpfen externer Tabellen  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Verknüpfen von HDFS-Daten mit PDW-Daten  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importieren von Zeilendaten aus HDFS in eine verteilte PDW-Tabelle  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importieren von Zeilendaten aus HDFS in eine replizierte PDW-Tabelle  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beispiele für Metadatenabfrage (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



