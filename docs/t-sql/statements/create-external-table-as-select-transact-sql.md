---
title: CREATE EXTERNAL TABLE AS SELECT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2ca379cf30fe2e7d359a294a18804f0b5e6faeb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Erstellt eine externe Tabelle und exportiert gleichzeitig die Ergebnisse einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-SELECT-Anweisung in Hadoop oder Azure Storage Blob.  
  
 Verwenden Sie die Anweisung CREATE EXTERNAL TABLE AS SELECT (CETAS) für folgende Vorgänge:  
  
-   Exportieren einer Datenbanktabelle in Hadoop oder Azure Blob Storage  
  
-   Importieren von Daten aus Hadoop oder Azure Blob Storage und Speichern der Daten in der Datenbank  
  
-   Abfragen von Daten aus Hadoop oder Azure Blob Storage, Verknüpfen der Daten mit relationalen Datenbanktabellen und Zurückschreiben der Ergebnisse in Hadoop oder Azure Blob Storage  
  
-   Abfragen von Daten aus Hadoop oder Azure Blob Storage, Transformieren der Daten mithilfe der schnellen Verarbeitungsfunktionen der Datenbank und Zurückschreiben der Daten in Hadoop oder Azure Blob Storage  
  
 Weitere Informationen finden Sie unter [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Erste Schritte mit PolyBase).  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumente  
 [ [ *database_name* . [ *schema_name* ] . ] | *schema_name* . ] *table_name*  
 Ein- bis dreiteiliger Name der Tabelle, die in der Datenbank erstellt werden soll. Bei einer externen Tabelle werden nur die Metadaten der Tabelle in der relationalen Datenbank gespeichert.  
  
 LOCATION =  '*hdfs_folder*'  
 Gibt an, wohin die Ergebnisse der SELECT-Anweisung auf der externen Datenquelle geschrieben werden sollen. Der Speicherort ist ein Ordnername und kann wahlweise einen Pfad enthalten, der relativ zum Stammordner des Hadoop-Clusters oder von Azure Storage Blob ist.  Pfad und Ordner werden, wenn nicht bereits vorhanden, von PolyBase erstellt.  
  
 Die externen Dateien mit dem Namen *QueryID_date_time_ID.format* werden in *hdfs_folder* geschrieben, wobei *ID* ein inkrementeller Bezeichner ist und *format* das Format der exportierten Daten. Zum Beispiel QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *external_data_source_name*  
 Gibt den Namen des externen Datenquellenobjekts an, das den Speicherort enthält, an dem die externen Daten gespeichert sind oder noch gespeichert werden. Der Speicherort ist entweder ein Hadoop-Cluster oder ein Azure-Blobspeicher. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Gibt den Namen des externen Dateiformatobjekts an, das das Format für die externe Datendatei enthält. Verwenden Sie zum Erstellen eines externen Dateiformats [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 REJECT-Optionen  
 Die REJECT-Optionen werden nicht gleichzeitig mit der CREATE EXTERNAL TABLE AS SELECT-Anweisung ausgeführt. Sie werden hier vielmehr angegeben, damit die Datenbank sie zu einem späteren Zeitpunkt beim Importieren von Daten aus der externen Tabelle verwenden kann. Wenn die CREATE TABLE AS SELECT-Anweisung später Daten aus der externen Tabelle auswählt, verwendet die Datenbank die REJECT-Optionen, um die Anzahl oder den Prozentsatz an Zeilen zu bestimmen, für die ein Importfehler auftreten kann, bevor der Importvorgang beendet wird.  
  
 REJECT_VALUE = *reject_value*  
 Gibt die Anzahl oder den Prozentsatz an Zeilen an, für die ein Importfehler auftreten kann, bevor die Datenbank den Importvorgang anhält.  
  
 REJECT_TYPE = **value** | percentage  
 Gibt an, ob die Option „REJECT_VALUE“ als Literalwert oder als Prozentsatz angegeben wird.  
  
 Wert  
 REJECT_VALUE ist ein Literalwert und kein Prozentsatz.  Die Datenbank beendet das Importieren von Zeilen aus der externen Datendatei, wenn die Anzahl der fehlerhaften Zeilen den Wert von *reject_value* überschreitet.  
  
 Gilt beispielsweise REJECT_VALUE = 5 und REJECT_TYPE = Wert, dann beendet die Datenbank das Importieren von Zeilen, nachdem für fünf Zeilen ein Importfehler aufgetreten ist.  
  
 Prozentsatz  
 REJECT_VALUE ist ein Prozentsatz und kein Literalwert. Die Datenbank beendet das Importieren von Zeilen aus der externen Datendatei, wenn der *Prozentsatz* der fehlerhaften Zeilen den Prozentsatz von *reject_value* überschreitet. Der Prozentsatz der fehlerhaften Zeilen wird in Intervallen berechnet.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Ist erforderlich, wenn REJECT_TYPE = Prozentsatz. Gibt die Anzahl von Zeilen für den Importversuch an, bevor die Datenbank den Prozentsatz der fehlerhaften Zeilen neu berechnet.  
  
 Gilt beispielsweise REJECT_SAMPLE_VALUE = 1000, dann berechnet die Datenbank den Prozentsatz fehlerhafter Zeilen nach dem Importversuch von 1000 Zeilen aus der externen Datendatei. Ist der Prozentsatz fehlerhafter Zeilen kleiner als *reject_value*, führt die Datenbank einen erneuten Ladeversuch von 1000 Zeilen aus. Nach jedem weiteren Importversuch von 1000 Zeilen berechnet die Datenbank den Prozentsatz fehlerhafter Zeilen neu.  
  
> [!NOTE]  
>  Da die Berechnung des Prozentsatzes fehlerhafter Zeilen durch die Datenbank in Intervallen erfolgt, kann der tatsächliche Prozentsatz fehlerhafter Zeilen *reject_value* überschreiten.  
  
 Beispiel:  
  
 In diesem Beispiel wird verdeutlicht, wie die drei REJECT-Optionen interagieren. Gilt beispielsweise REJECT_TYPE = Prozentsatz, REJECT_VALUE = 30 und REJECT_SAMPLE_VALUE = 100, dann könnte das folgende Szenario auftreten:  
  
-   Die Datenbank versucht, die ersten 100 Zeilen zu laden. Davon sind 25 fehlerhaft und 75 erfolgreich.  
  
-   Der berechnete Prozentsatz fehlerhafter Zeilen ist mit 25 % kleiner als der REJECT-Wert von 30 %. Daher ist es nicht erforderlich, den Ladevorgang anzuhalten.  
  
-   Die Datenbank versucht, die nächsten 100 Zeilen zu laden. Dieses Mal sind 25 erfolgreich und 75 fehlerhaft.  
  
-   Der Prozentsatz fehlerhafter Zeilen wird mit 50 % neu berechnet. Der Prozentsatz fehlerhafter Zeilen hat den REJECT-Wert von 30 % überschritten.  
  
-   Nach dem Ladeversuch von 200 Zeilen schlägt der Ladevorgang mit 50 % fehlerhaften Zeilen fehl. Dieser Prozentsatz liegt über dem angegebenen Grenzwert von 30 %.  
  
 WITH *common_table_expression*  
 Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Weitere Informationen finden Sie unter [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> Füllt die neue Tabelle mit den Ergebnissen einer SELECT-Anweisung auf. *select_criteria* ist der Text der SELECT-Anweisung, die die Daten bestimmt, die in die neue Tabelle kopiert werden sollen. Informationen zu SELECT-Anweisungen finden Sie unter [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 **Datenbankbenutzer** benötigen alle folgenden Berechtigungen oder Mitgliedschaften, um diesen Befehl ausführen zu können:  
  
-   **ALTER SCHEMA**-Berechtigung für das lokale Schema, das die neue Tabelle oder Mitgliedschaft in der festen Datenbankrolle **db_ddladmin** enthält  
  
-   **CREATE TABLE**-Berechtigung oder -Mitgliedschaft in der festen Datenbankrolle **db_ddladmin**  
  
-   **SELECT**-Berechtigung für alle Objekte, auf die in *select_criteria* verwiesen wird  
  
 Eine Anmeldung erfordert alle folgenden Berechtigungen:  
  
-   **ADMINISTER BULK OPERATIONS**-Berechtigung  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**-Berechtigung  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**-Berechtigung  
  
-   Die Anmeldung muss über eine Schreibberechtigung verfügen, um im externen Ordner auf dem Hadoop-Cluster oder in Azure Storage Blob lesen und schreiben zu können.  
 
 > [!IMPORTANT]  
 >  Mit der Berechtigung ALTER ANY EXTERNAL DATA SOURCE besitzt jeder Prinzipal die Fähigkeit, beliebige externe Datenquellenobjekte zu erstellen und zu ändern. Damit ist auch der Zugriff auf alle datenbankweit gültigen Anmeldeinformationen der Datenbank möglich. Da es sich hierbei um eine weitreichende Berechtigung handelt, darf sie nur vertrauenswürdigen Prinzipalen innerhalb des Systems erteilt werden.
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Beim Exportieren von Daten mithilfe der CREATE EXTERNAL TABLE AS SELECT-Anweisung in eine Datei mit Texttrennzeichen gibt es keine Datei, die Zeilen ablehnt, für die ein Exportfehler aufgetreten ist.  
  
 Beim Erstellen der externen Tabelle versucht die Datenbank, eine Verbindung mit dem externen Hadoop-Cluster oder Azure Storage Blob herzustellen. Tritt bei der Verbindung ein Fehler auf, schlägt der Befehl fehl und die externe Tabelle wird nicht erstellt. Da mindestens drei Versuche für einen Verbindungsaufbau erfolgen, kann es eine Minute oder länger dauern, bis für den Befehl ein Fehler auftritt.  
  
 Tritt bei der CREATE EXTERNAL TABLE AS SELECT-Anweisung ein Fehler auf oder wird sie abgebrochen, erfolgt ein einmaliger Versuch durch die Datenbank, alle bereits erstellten Dateien und Ordner auf der externen Datenquelle zu entfernen.  
  
 Die Datenbank meldet alle Java-Fehler, die während des Datenexports auf der externen Datenquelle auftreten.  
  
##  <a name="GeneralRemarks"></a> Allgemeine Hinweise  
 Nachdem die CETAS-Anweisung abgeschlossen ist, können Sie [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen für die externe Tabelle ausführen. Diese Vorgänge importieren Daten für die Dauer der Abfrage in die Datenbank, sofern für den Import nicht die CREATE TABLE AS SELECT-Anweisung verwendet wird.  
  
 Der Name und die Definition der externen Tabelle werden in den Metadaten der Datenbank gespeichert. Die Daten werden in der externen Datenquelle gespeichert.  
  
 Die externen Dateien heißen *QueryID_date_time_ID.format*, wobei *ID* ein inkrementeller Bezeichner ist und *Format* das Format der exportierten Daten. Zum Beispiel QID776_20160130_182739_0.orc.  
  
 Die CETAS-Anweisung erstellt immer eine nicht partitionierte Tabelle, selbst wenn die Quelltabelle partitioniert ist.  
  
 Für Abfragepläne, die mit EXPLAIN erstellt wurden, verwendet die Datenbank die folgenden Abfrageplanvorgänge für externe Tabellen:  
  
-   Verschieben von externer Zufallswiedergabe  
  
-   Verschieben von externer Übertragung  
  
-   Verschieben von externer Partition  
  
 **GILT FÜR:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Als Voraussetzung für das Erstellen einer externen Tabelle muss der Applianceadministrator die Hadoop-Konnektivität konfigurieren. Weitere Informationen finden Sie in der APS-Dokumentation (Analytics Platform System) unter „Configure Connectivity to External Data“ (Konfigurieren der Konnektivität mit externen Daten), die Sie [hier](http://www.microsoft.com/download/details.aspx?id=48241) herunterladen können.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Daten aus externen Tabellen befinden sich außerhalb der Datenbank, weshalb Sicherungs- und Wiederherstellungsvorgänge nur für Daten ausgeführt werden, die in der Datenbank gespeichert sind. Dies bedeutet, dass nur die Metadaten gesichert und wiederhergestellt werden.  
  
 Die Datenbank überprüft beim Wiederherstellen einer Datenbanksicherung mit einer externen Tabelle nicht die Verbindung mit der externen Datenquelle. Die Metadaten der externen Tabelle können auch dann erfolgreich wiederhergestellt werden, wenn auf die ursprüngliche Quelle nicht zugegriffen werden kann. SELECT-Vorgänge für die externe Tabelle schlagen jedoch fehl.  
  
 Die Datenbank kann die Konsistenz der Daten zwischen Datenbank und externen Daten nicht garantieren. Sie als Benutzer tragen die alleinige Verantwortung für die Konsistenz zwischen externen Daten und Datenbank.  
  
 DML-Vorgänge (Data Manipulation Language, Datenbearbeitungssprache) werden für externe Tabellen nicht unterstützt. So können Sie beispielsweise die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen UPDATE, INSERT oder DELETE von [!INCLUDE[tsql](../../includes/tsql-md.md)] zum Ändern der externen Daten nicht verwenden.  
  
 Die Anweisungen CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW und DROP VIEW sind die einzigen DDL-Vorgänge (Data Definition Language, Datenbeschreibungssprache), die für externe Tabelle zulässig sind.  
  
 PolyBase kann bei 32 gleichzeitigen PolyBase-Abfragen maximal 33.000 Dateien pro Ordner verarbeiten. Diese maximale Anzahl schließt sowohl Dateien als auch Unterordner im jeweiligen HDFS-Ordner ein. Werden weniger als 32 Abfragen gleichzeitig ausgeführt, können auch PolyBase-Abfragen für Ordner in HDFS mit mehr als 33.000 Dateien ausgeführt werden. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt Hadoop- und PolyBase-Benutzern die Verwendung von kurzen Dateipfaden und von nicht mehr als 30.000 Dateien pro HDFS-Ordner. Das Verweisen auf eine zu große Anzahl von Dateien kann eine JVM-Ausnahme wegen unzureichenden Arbeitsspeichers erzeugen.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) hat keine Auswirkungen auf die CREATE EXTERNAL TABLE AS SELECT-Anweisung. Verwenden Sie [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md), um ein ähnliches Verhalten zu erzielen.  
  
 Wählt CREATE EXTERNAL TABLE AS SELECT aus dem Formattyp RCFILE aus, dürfen die Spaltenwerte in RCFILE nicht den senkrechten Strich (|) enthalten.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das SCHEMARESOLUTION-Objekt.  
  
##  <a name="Examples"></a> Beispiele  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Erstellen einer Hadoop-Tabelle mithilfe von CREATE EXTERNAL TABLE AS SELECT (CETAS)  
 Im folgenden Beispiel wird mithilfe der Spaltendefinitionen und Daten aus der Quelltabelle `dimCustomer` eine neue externe Tabelle mit dem Namen `hdfsCustomer` erstellt.  
  
 Die Tabellendefinition ist in der Datenbank gespeichert. Die Ergebnisse der SELECT-Anweisung werden in die Datei „/pdwdata/customer.tbl“ auf der externen Hadoop-Datenquelle *customer_ds* exportiert. Die Datei wird entsprechend dem externen Dateiformat *customer_ff* formatiert.  
  
 Der Dateiname wird von der Datenbank erzeugt und enthält die Abfrage-ID, um das Ausrichten der Datei auf die Abfrage, die sie erzeugt hat, zu vereinfachen.  
  
 Der Pfad `hdfs://xxx.xxx.xxx.xxx:5000/files/`, der dem Customer-Verzeichnis vorangeht, muss bereits vorhanden sein. Sollte das Customer-Verzeichnis jedoch noch nicht vorhanden sein, wird es von der Datenbank erstellt.  
  
> [!NOTE]  
>  In diesem Beispiel wird 5000 angegeben. Wird kein Port angegeben, verwendet die Datenbank 8020 als Standardport.  
  
 Dies ergibt `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.` als Hadoop-Speicherort und -Dateiname.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Verwenden eines Abfragehinweises mit CREATE EXTERNAL TABLE AS SELECT (CETAS)  
 Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines JOIN-Abfragehinweises mit der CETAS-Anweisung. Nach dem Senden der Abfrage verwendet die Datenbank die Hashjoinstrategie, um den Abfrageplan zu erzeugen. Weitere Informationen zu Joinhinweisen und der Verwendung der OPTION-Klausel finden Sie unter [OPTION-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  In diesem Beispiel wird 5000 angegeben. Wird kein Port angegeben, verwendet die Datenbank 8020 als Standardport.  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL Data Warehouse, Parallel Data Warehouse&#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


