---
title: Erstellen einer EXTERNEN Tabelle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e9abb5affb76f0caac24e973928561939280ba40
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-table-transact-sql"></a>Erstellen einer EXTERNEN Tabelle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Erstellt eine externe PolyBase-Tabelle, die in einem Hadoop-Cluster oder Azure Blob-Speicher gespeicherte Daten verweist. Kann auch verwendet werden, zum Erstellen einer externen Tabelle [elastische Datenbankabfrage](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Verwenden Sie eine externe Tabelle zu:  
  
-   Hadoop oder Azure BLOB-Speicherdaten Abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen.  
  
-   Importieren und Speichern von Daten aus Hadoop oder Azure Blob-Speicher in Ihrem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.  
  
-   Erstellen Sie eine externe Tabelle für die Verwendung mit einer elastischen Datenbank  
     Abfrage.  
     
- Importieren und Speichern von Daten aus Azure Data Lake-Speicher in Azure SQL Data Warehouse
  
 Siehe auch [externe Datenquelle erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [löschen EXTERNAL TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
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
 *Database_name* . [Schema_name]. | Schema_name. ] *Table_name*  
 1 bis 3 - Teilenamens der Tabelle zu erstellen. Für eine externe Tabelle ist nur die Metadaten der Tabellen in SQL zusammen mit grundlegende Statistiken über die Datei oder Ordner verwiesen, die in Hadoop oder Azure Blob-Speicher gespeichert. Keine tatsächlichen Daten verschoben oder in gespeicherten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<Column_definition > [,...  *n*  ] CREATE EXTERNAL TABLE können eine oder mehrere Spaltendefinitionen. Verwenden die gleiche Syntax für eine Spalte definieren, CREATE EXTERNAL TABLE und CREATE TABLE. Eine Ausnahme, können Sie keine DEFAULT-Einschränkung in externen Tabellen. Die vollständigen Details Spaltendefinitionen und deren Datentypen finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) und [erstellt eine Tabelle in Azure SQL-Datenbank](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 Die Spaltendefinitionen, einschließlich der Datentypen und die Anzahl der Spalten der Daten in externen Dateien übereinstimmen. Wenn es ein Konflikt besteht, werden die Zeilen der Datei beim Abfragen der tatsächlichen Daten zurückgewiesen.  
  
 Für externe Tabellen, die auf Dateien in externen Datenquellen verweisen, müssen die Definitionen Spalte, und geben die genaue Schema der externen Datei zuordnen. Beim Datentypen definieren, die in Hadoop Hive/gespeicherte Daten zu verweisen, verwenden Sie die folgenden Zuordnungen zwischen Datentypen von SQL und Hive und wandeln Sie den Typ in einen SQL-Datentyp, wenn Sie daraus auswählen. Die folgenden Anweisungstypen alle Versionen von Hive, sofern nicht anders.  
  
|SQL-Datentyp|.NET-Datentyp|Hive-Datentyp|Hadoop/Java-Datentyp|Kommentare|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|Für unsignierte Zahlen.|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|float|Double|double|DoubleWritable||  
|real|Single|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|nchar|String<br /><br /> Char[]|Zeichenfolge|text||  
|nvarchar|String<br /><br /> Char[]|Zeichenfolge|Text||  
|char|String<br /><br /> Char[]|Zeichenfolge|Text||  
|varchar|String<br /><br /> Char[]|Zeichenfolge|Text||  
|binary|Byte[]|binary|BytesWritable|Gilt für Hive 0,8 und höher.|  
|varbinary|Byte[]|binary|BytesWritable|Gilt für Hive 0,8 und höher.|  
|Datum|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|datetime|DateTime|timestamp|TimestampWritable||  
|Uhrzeit|TimeSpan|timestamp|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|Gilt für Hive0.11 und später erneut.|  
  
 Speicherort = "*Folder_or_filepath*"  
 Gibt den Ordner oder Pfad und Dateinamen für die tatsächlichen Daten in Hadoop oder Azure Blob-Speicher an. Die Position beginnt im Stammordner. Der Stammordner ist der Speicherort des in der externen Datenquelle angegeben.  
  
 Wenn Sie Standort um einen Ordner angeben, werden eine PolyBase-Abfrage, die aus der externen Tabelle auswählt Dateien aus dem Ordner und allen Unterordnern abgerufen. Keinen wie Hadoop zurück versteckte Ordner PolyBase. Sie gibt auch keine Dateien zurück für die der Dateiname mit einem Unterstrich (_) oder einem Punkt (.) beginnt.  
  
 In diesem Beispiel wenn Speicherort = / Webdata/einer PolyBase-Abfrage werden Zeilen aus mydata.txt und mydata2.txt zurückgegeben.  Es wird nicht mydata3.txt zurückgegeben, da es sich um einen Unterordner des einen ausgeblendeten Ordner handelt. Es werden keine _hidden.txt zurückgegeben, da es sich um eine versteckte Datei handelt.  
  
 ![Rekursive Daten für externe Tabellen](../../t-sql/statements/media/aps-polybase-folder-traversal.png "rekursive Daten für externe Tabellen")  
  
 Um die Standardwebsite als auch nur Lesen aus dem Stammordner zu ändern, legen Sie das Attribut \<polybase.recursive.traversal > in der Konfigurationsdatei Core-site.xml auf "false". Diese Datei befindet sich unter `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Beispiel: `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *External_data_source_name*  
 Gibt den Namen der externen Datenquelle, die den Speicherort der externen Daten enthält. Dieser Speicherort kann entweder eine Hadoop oder Azure Blob-Speicher. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *External_file_format_name*  
 Gibt den Namen des externen Format Dateiobjekts, in dem die Datei Typ und Komprimierung die Methode für die externen Daten gespeichert. Verwenden Sie zum Erstellen eines externen Dateiformats [CREATE EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Ablehnen von Optionen  
 Sie können angeben, dass Reject-Parameter, die bestimmen, wie PolyBase behandelt *dirty* zeichnet er aus der externen Datenquelle abgerufen. Ein Datensatz gilt als "dirty", wenn sie tatsächliche Datentypen oder die Anzahl der Spalten entsprechen nicht den Spaltendefinitionen der externen Tabelle.  
  
 Wenn Sie nicht angeben oder ändern die Werte ablehnen, werden PolyBase Standardwerte verwendet. Diese Informationen zu den Parametern ablehnen wird als zusätzliche Metadaten gespeichert, wenn Sie eine externe Tabelle mit CREATE EXTERNAL TABLE-Anweisung erstellen.   Wenn eine zukünftige SELECT-Anweisung oder wählen Sie in SELECT-Anweisung Daten aus der externen Tabelle auswählt, wird PolyBase die Reject-Optionen verwenden, um zu bestimmen, die Anzahl oder den Prozentsatz der Zeilen, die zurückgewiesen werden kann, bevor die tatsächliche Abfrage fehlschlägt. zugreifen. Die Abfrage zurückgegeben wird (Teilergebnisse), bis der Schwellenwert zum Zurückweisen überschritten wird. Es wird dann ein Fehler auftritt, mit der entsprechenden Fehlermeldung.  
  
 REJECT_TYPE = **Wert** | Prozentsatz  
 Verdeutlicht, ob die Option "REJECT_VALUE" als ein Literalwert oder als Prozentsatz angegeben wird.  
  
 value  
 REJECT_VALUE ist ein Literalwert, kein Prozentsatz. Die PolyBase-Abfrage schlägt fehl, wenn die Anzahl der abgelehnten Zeilen überschreitet *Reject_value*.  
  
 Z. B. wenn REJECT_VALUE = 5 und REJECT_TYPE = Wert, der PolyBase-SELECT-Abfrage schlägt fehl, nachdem 5 Zeilen abgelehnt wurden.  
  
 Prozentsatz  
 REJECT_VALUE ist Prozentsatz, nicht auf einen literalen Wert. Eine PolyBase-Abfrage schlägt fehl, wenn die *Prozentsatz* fehlerhafter Zeilen überschreitet *Reject_value*. Der Prozentsatz fehlerhafter Zeilen wird in Abständen berechnet.  
  
 REJECT_VALUE = *Reject_value*  
 Gibt den Wert oder den Prozentsatz der Zeilen, die zurückgewiesen werden kann, bevor die Abfrage fehlschlägt.  
  
 Für die REJECT_TYPE = Value, *Reject_value* muss eine ganze Zahl zwischen 0 und 2.147.483.647 sein.  
  
 Für die REJECT_TYPE = Percentage, *Reject_value* muss ein float-Wert zwischen 0 und 100 sein.  
  
 REJECT_SAMPLE_VALUE = *Reject_sample_value*  
 Dieses Attribut ist erforderlich, bei der Angabe von REJECT_TYPE = Prozentsatz. Sie bestimmt die Anzahl der Zeilen abrufen, bevor die PolyBase berechnet den Prozentsatz der abgelehnten Zeilen neu versucht.  
  
 Die *Reject_sample_value* Parameter muss eine ganze Zahl zwischen 0 und 2.147.483.647 sein.  
  
 Z. B. wenn REJECT_SAMPLE_VALUE = 1000, PolyBase berechnet den Prozentsatz von fehlerhaften Zeilen aus, nachdem es versucht hat, können Sie 1000 Zeilen aus der externen Datendatei importieren. Wenn der Prozentsatz von fehlerhaften Zeilen ist kleiner als *Reject_value*, PolyBase versucht, eine andere 1000 Zeilen abzurufen. Es wird weiterhin den Prozentsatz von fehlerhaften Zeilen neu berechnet, nachdem er versucht, jede zusätzliche 1000 Zeilen importieren.  
  
> [!NOTE]  
>  Da PolyBase Intervallen den Prozentsatz von fehlerhaften Zeilen berechnet, kann der tatsächliche Prozentsatz fehlerhafter Zeilen überschreiten *Reject_value*.  
  
 Beispiel:  
  
 Dieses Beispiel zeigt, wie die drei REJECT-Optionen miteinander interagieren. Z. B. wenn REJECT_TYPE = Percentage "," REJECT_VALUE = 30 und REJECT_SAMPLE_VALUE = 100, das folgende Szenario auftreten:  
  
-   PolyBase versucht, die ersten 100 Zeilen abzurufen. 25 ein Fehler auftreten und 75 erfolgreich ausgeführt werden.  
  
-   Ist kleiner als der Reject-Wert von 30 % Prozent der fehlerhaften Zeilen als 25 %, berechnet. Daher werden PolyBase weiterhin Daten aus der externen Datenquelle abgerufen.  
  
-   PolyBase versucht, die nächsten 100 Zeilen zu laden; Dieses Mal 25 erfolgreich ausgeführt werden, und 75 fehl.  
  
-   Prozentsatz fehlerhafter Zeilen wird als 50 % neu berechnet. Der Prozentsatz von fehlerhaften Zeilen hat den ablehnungswert 30 % überschritten.  
  
-   Die PolyBase-Abfrage erzeugt abgelehnt von 50 % der Zeilen nach dem Versuch, die ersten 200 Zeilen zurückgeben. Beachten Sie, dass die übereinstimmende Zeilen zurückgegeben wurden, bevor die PolyBase-Abfrage erkennt, dass der Schwellenwert zum Zurückweisen überschritten wurde.  
  
 Externe shardtabelle-Optionen  
 Gibt an, der externen Datenquelle (eine nicht - SQL Server-Datenquelle) und eine Verteilungsmethode für die [elastische Datenbankabfrage](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Eine externe Datenquelle z. B. in einem Hadoop-Dateisystem, Azure-Blob-Speicher gespeicherten Daten oder eine [shardzuordnungs-Manager](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 Die SCHEMA_NAME-Klausel bietet die Möglichkeit, eine Tabelle in ein anderes Schema für die Remotedatenbank die externen Tabellendefinition zuordnen. Verwenden Sie diese Option, um zwischen Schemas zu unterscheiden, die auf den lokalen und Remotedatenbanken vorhanden.  
  
 OBJECT_NAME  
 Die OBJECT_NAME-Klausel bietet die Möglichkeit, eine Tabelle mit einem anderen Namen für die Remotedatenbank die externen Tabellendefinition zuordnen. Verwenden Sie diese Option, um zwischen Objektnamen zu unterscheiden, die auf den lokalen und Remotedatenbanken vorhanden.  
  
 VERTEILUNG  
 Optional. Dies ist nur erforderlich, die nur für Datenbanken des Typs SHARD_MAP_MANAGER. Steuert, ob eine Tabelle als eine Tabelle mit Shards oder einer replizierten Tabelle behandelt wird. Mit **SHARDED** (*Spaltenname*) Tabellen, die Daten aus unterschiedlichen Tabellen nicht überlappen. **REPLIZIERT** gibt an, dass Tabellen dieselben Daten auf jeder Shard enthalten. **ROUND_ROBIN** gibt an, dass eine anwendungsspezifische Methode zum Verteilen von Daten verwendet wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Berechtigungen erforderlich:  
  
-   **CREATE TABLE**  
  
-   **BELIEBIGES SCHEMA ÄNDERN**  
  
-   **ÄNDERN SIE JEDE EXTERNE DATENQUELLE**  
  
-   **ÄNDERN EINES BELIEBIGEN EXTERNEN DATEIFORMATS**  

-   **VERWALTUNGSDATENBANK**
  
 Beachten Sie, dass die Anmeldung, die von der externen Datenquelle erstellt benötigen die Berechtigung zum Lesen und Schreiben in die externe Datenquelle, die in Hadoop oder Azure Blob-Speicher gespeichert.  


 > [!IMPORTANT]  

>  Die Berechtigung ALTER ANY EXTERNAL DATA SOURCE gewährt Prinzipal die Fähigkeit zum Erstellen und ändern alle externen Datenquellenobjekt und daher auch erteilt den Zugriff auf alle datenbankweit gültige Anmeldeinformationen für die Datenbank. Diese Berechtigung muss berücksichtigt werden, wie hoch privilegierten und daher im System nur für vertrauenswürdige Prinzipale erteilt werden müssen.

## <a name="error-handling"></a>Fehlerbehandlung  
 PolyBase versucht, beim Ausführen der CREATE EXTERNAL TABLE-Anweisung, mit der externen Datenquelle herstellen. Schlägt der Verbindungsversuch die Anweisung fehl, und die externe Tabelle wird nicht erstellt werden. Eine Minute oder mehr, bis der Befehl schlägt fehl, da PolyBase, die Verbindung versucht, bevor Sie schließlich die Abfrage fehlschlägt, kann es dauern.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 PolyBase speichert in Szenarien für Ad-hoc-Abfrage, d. h. aus EXTERNEN Tabelle auswählen, die Zeilen aus der externen Datenquelle in einer temporären Tabelle abgerufen. Nachdem die Abfrage abgeschlossen ist, handelt es sich bei PolyBase entfernt und die temporäre Tabelle löscht. Keine permanente Daten in SQL-Tabellen gespeichert.  
  
 Im Gegensatz dazu werden PolyBase im Import-Szenario, d. h. in aus EXTERNEN Tabelle auswählen, die Zeilen aus der externen Datenquelle abgerufen werden, als permanente Daten in der SQL-Tabelle gespeichert. Die neue Tabelle wird beim Ausführen der Abfrage erstellt, wenn Polybase die externen Daten abruft.  
  
 PolyBase kann Teil der Abfrage Berechnung an Hadoop zur Verbesserung der Leistung von Abfragen per Push übertragen. Dies ist die prädikatweitergabe bezeichnet. Um dies zu aktivieren, geben Sie die Hadoop Resource Manager Location-Option in [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Sie können zahlreiche externe Tabellen erstellen, die die gleichen oder anderen externen Datenquellen verweisen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 In CTP2 wird die Export-Funktionalität nicht unterstützt z. B. dauerhaft Speichern von SQL-Daten in der externen Datenquelle. Diese Funktionalität wird in CTP3 verfügbar sein.  
  
 Da die Daten für eine externe Tabelle deaktiviert das Gerät befindet, kann es ist nicht unter der Kontrolle von PolyBase, und geändert oder entfernt werden jederzeit von einem externen Prozess. Aus diesem Grund sind neut Abfragen von Ergebnissen für eine externe Tabelle ist nicht gewährleistet deterministisch sein. Die gleiche Abfrage kann unterschiedliche Ergebnisse jedes Mal zurückgeben, die sie für eine externe Tabelle ausführt. Auf ähnliche Weise kann eine Abfrage fehl, wenn die externen Daten entfernt oder verschoben werden.  
  
 Sie können mehrere externe Tabellen erstellen, jeweils verschiedenen externen Datenquellen verweisen. Wenn Sie verschiedene Hadoop-Datenquellen gleichzeitig Abfragen ausführen, muss jedes Hadoop-Datenquelle jedoch die gleichen 'Hadoop Connectivity' serverkonfigurationseinstellung verwenden. Beispielsweise kann nicht gleichzeitig Ausführen einer Abfrage für einen Cloudera Hadoop-Cluster und einem Hortonworks Hadoop-Cluster seit diese unterschiedliche Konfigurationseinstellungen verwenden. Die Konfigurationseinstellungen und der unterstützten Kombinationen finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40; Transact-SQL &#41; ](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Nur diese (Data Definition Language, Datendefinitionssprache)-Anweisungen sind in externen Tabellen zulässig:  
  
-   CREATE TABLE und DROP TABLE  
  
-   CREATE STATISTICS und DROP STATISTICS  
  
-   CREATE VIEW und DROP VIEW  
  
 Konstrukte und Vorgänge, die nicht unterstützt:  
  
-   Die DEFAULT-Einschränkung auf externe Spalten  
  
-   Data Manipulation Language (DML) Vorgänge DELETE-, INSERT- und update  
  
 Abfrage-Einschränkungen:  
  
 PolyBase kann maximal 33 k Dateien pro Ordner nutzen, wenn Sie 32 gleichzeitige PolyBase-Abfragen ausgeführt. Diese maximale Anzahl enthält sowohl Dateien und Unterordner im jeweiligen Ordner HDFS an. Wenn der Grad an Parallelität höchstens 32 ist, kann ein Benutzer PolyBase-Abfragen für Ordner in HDFS ausführen, die mehr als 33 k-Dateien enthalten. Es wird empfohlen, dass Sie externe Dateipfade kurze beibehalten und nicht mehr als 30 KB Dateien pro Ordner HDFS verwenden. Wenn zu viele Dateien verwiesen werden, kann eine Out-of-Memory-Ausnahme von Java Virtual Machine (JVM) auftreten.  

Einschränkungen der Breite Tabelle: PolyBase in SQL Server 2016 verfügt über eine Breite Zeilenlimit von 32KB, die basierend auf einer gültigen Zeile die maximale Größe von Tabelle (Definition). Wenn die Summe des Spaltenschemas größer als 32 KB ist, werden PolyBase nicht können, um die Daten abzufragen. 

Diese Einschränkung wurde in SQL Data Warehouse auf 1 MB ausgelöst.


## <a name="locking"></a>Sperren  
 Freigegebene Sperre für das SCHEMARESOLUTION-Objekt.  
  
## <a name="security"></a>Sicherheit  
 Die Datendateien für eine externe Tabelle ist in Hadoop oder Azure Blob-Speicher gespeichert. Diese Dateien werden erstellt und von Ihren eigenen Prozessen verwaltet. Es liegt in Ihrer Verantwortung zum Verwalten der Sicherheit der externen Daten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Erstellen Sie eine externe Tabelle mit Daten im Format Texttrennzeichen an.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die Daten in Dateien Texttrennzeichen formatiert wurde. Definiert eine externe Datenquelle *Mydatasource* und ein externes Dateiformat *Myfileformat*. Diese Objekte auf Datenbankebene werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Erstellen Sie eine externe Tabelle mit Daten im RCFile-Format.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die Daten, die als RCFiles formatiert wurde. Definiert eine externe Datenquelle *Mydatasource_rc* und ein externes Dateiformat *Myfileformat_rc*. Diese Objekte auf Datenbankebene werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
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
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Erstellen Sie eine externe Tabelle mit Daten im Format ORC.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die formatierte Daten als ORC Dateien verfügt. Es definiert eine externe Quelle Mydatasource_orc und eine externe Datei Format Myfileformat_orc. Diese Objekte auf Datenbankebene werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 Clickstreamanalyse ist eine externe Tabelle, die mit der employee.tbl durch Tabstopps getrennte Textdatei in einem Hadoop-Cluster verbunden. Die folgende Abfrage sieht wie eine Abfrage für eine standardmäßige Tabelle. Allerdings wird diese Abfrage ruft Daten aus Hadoop ab und berechnet dann die Restuls.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Verknüpfen von Hadoop-Daten mit SQL-Daten  
 Diese Abfrage sieht wie ein standard-JOIN für zwei SQL-Tabellen. Der Unterschied ist, dass PolyBase Ruft die Clickstream-Daten aus Hadoop ab und ihn dann der UrlDescription-Tabelle fügt. Eine Tabelle ist eine externe Tabelle, und das andere ist eine standardmäßige SQL-Tabelle.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importieren von Daten aus Hadoop in einer SQL-Tabelle  
 Dieses Beispiel erstellt eine neue SQL Ms_user-Tabelle, die das Ergebnis einer Verknüpfung zwischen der standardmäßigen SQL-Tabelle dauerhaft speichert *Benutzer* und die externe Tabelle *Clickstreamanalyse*.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Erstellen Sie eine externe Tabelle für eine Datenquelle mit Shards  
 In diesem Beispiel ordnet eine remote-DMV in eine externe Tabelle mit den Klauseln SCHEMA_NAME und OBJECT_NAME.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-create-an-external-table-with-data-in-text-delimited-format"></a>H. Erstellen Sie eine externe Tabelle mit Daten im Format Texttrennzeichen an.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die Daten in Dateien Texttrennzeichen formatiert wurde. Es definiert eine externe Quelle Mydatasource und eine externe Datei Format Myfileformat. Diese Serverebene verwendete Objekte werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="i-create-an-external-table-with-data-in-rcfile-format"></a>I. Erstellen Sie eine externe Tabelle mit Daten im RCFile-Format.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die Daten, die als RCFiles formatiert wurde. Es definiert eine externe Quelle Mydatasource_rc und eine externe Datei Format Myfileformat_rc. Diese Serverebene verwendete Objekte werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
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
  
### <a name="j-create-an-external-table-with-data-in-orc-format"></a>J. Erstellen Sie eine externe Tabelle mit Daten im Format ORC.  
 Dieses Beispiel zeigt die Schritte, die erforderlich, um eine externe Tabelle zu erstellen, die formatierte Daten als ORC Dateien verfügt. Es definiert eine externe Quelle Mydatasource_orc und eine externe Datei Format Myfileformat_orc. Diese Serverebene verwendete Objekte werden dann in der CREATE EXTERNAL TABLE-Anweisung verwiesen werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) und [externes DATEIFORMAT erstellen &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="k-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>K. Importieren von Daten aus der ADLS in Azure[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
  
### <a name="l-join-external-tables"></a>L. Verknüpfen von externen Tabellen  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="m-join-hdfs-data-with-pdw-data"></a>M. Verknüpfen von HDFS-Daten mit PDW-Daten  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="n-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>N. Importieren von Zeilendaten aus HDFS in einer verteilten PDW-Tabelle  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="o-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>O. Importieren von Zeilendaten aus HDFS in eine replizierte Tabelle mit PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für Metadaten-Abfrage (SQLServer PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [Erstellen Sie die externe Tabelle AS SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Erstellen Sie die Tabelle als SELECT &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  




