---
title: Erstellen Sie die externe Tabelle AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
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
caps.latest.revision: 16
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 716c0fdaa701865e8d35154cd19068051e0ab017
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-table-as-select-transact-sql"></a>Erstellen Sie die externe Tabelle AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Eine externe Tabelle erstellt und dann exportiert, parallel, die Ergebnisse einer [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT-Anweisung in Hadoop oder Azure-Speicher-Blob.  
  
 Verwenden Sie das Erstellen externer Tabelle AS auswählen (CETAS)-Anweisung, um:  
  
-   Exportieren einer Datenbanktabelle in Hadoop oder Azure Blob-Speicher.  
  
-   Importieren von Daten aus Hadoop oder Azure blob-Speicher und in der Datenbank zu speichern.  
  
-   Abfragen von Daten aus Hadoop oder Azure Blob-Speicher, verknüpfen Sie ihn mit relationalen Datenbanktabellen und die Ergebnisse zurück in Hadoop oder Azure Blob-Speicher geschrieben.  
  
-   Fragen Sie Daten aus Hadoop oder Azure Blob-Speicher ab, transformieren Sie ihn mithilfe der schnellen Verarbeitungsfunktionen der Datenbank und in Hadoop oder Azure Blob-Speicher zurückschreiben.  
  
 Weitere Informationen finden Sie unter [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Erste Schritte mit PolyBase).  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [[ *Database_name* . [ *Schema_name* ]. ] | *Schema_name* . ] *Table_name*  
 1 bis 3 - Teilenamens der Tabelle, die in der Datenbank erstellen. Für eine externe Tabelle ist nur die Metadaten der Tabellen in der relationalen Datenbank gespeichert.  
  
 Speicherort = "*Hdfs_folder*"  
 Gibt an, wo die Ergebnisse der SELECT-Anweisung auf der externen Datenquelle zu schreiben. Der Speicherort ist ein Ordnername und kann optional einen Pfad, der relativ zum Stammordner des Hadoop-Clusters oder des Azure-Speicher-Blob enthalten.  PolyBase wird der Pfad und den Ordner erstellt, wenn sie nicht bereits vorhanden ist.  
  
 Externen Dateien werden geschrieben, um *Hdfs_folder* und benannte *QueryID_date_time_ID.format*, wobei *ID* ein inkrementeller Bezeichner und *Format* ist das Format der exportierten Daten. Zum Beispiel QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *External_data_source_name*  
 Gibt den Namen des Quellobjekts externe Daten, die den Speicherort enthält, in dem die externen Daten gespeichert werden oder gespeichert werden. Der Speicherort ist ein Hadoop-Cluster oder ein Azure-Blob-Speicher. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *External_file_format_name*  
 Gibt den Namen des externen Format Dateiobjekts, das das Format der externen Datendatei enthält. Verwenden Sie zum Erstellen eines externen Dateiformats [CREATE EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Ablehnen von Optionen  
 Die Reject-Optionen gelten nicht zu dem Zeitpunkt, die diese CREATE EXTERNAL TABLE AS SELECT-Anweisung ausgeführt wird. Stattdessen werden sie hier angegeben, damit die Datenbank zu einem späteren Zeitpunkt einsatzmöglichkeiten beim Import von Daten aus der externen Tabelle. Später, wenn die CREATE TABLE AS SELECT-Anweisung Daten aus der externen Tabelle auswählt, wird die Datenbank die ablehnen Optionen verwenden, um zu bestimmen, die Anzahl oder den Prozentsatz der Zeilen, die auftreten kann, bevor der Import wird beendet.  
  
 REJECT_VALUE = *Reject_value*  
 Gibt den Wert oder den Prozentsatz der Zeilen, die Indizierung fehlschlagen darf, importieren, bevor die Datenbank der Importvorgang angehalten wird.  
  
 REJECT_TYPE = **Wert** | Prozentsatz  
 Verdeutlicht, ob die Option "REJECT_VALUE" als ein Literalwert oder als Prozentsatz angegeben wird.  
  
 value  
 REJECT_VALUE ist ein Literalwert, kein Prozentsatz.  Die Datenbank wird beendet, Zeilen aus der externen Datendatei importieren, wenn die Anzahl der fehlerhaften Zeilen überschreitet *Reject_value*.  
  
 Z. B. wenn REJECT_VALUE = 5 und REJECT_TYPE = Wert, wird die Datenbank beendet wird, importieren Zeilen aus, nachdem 5 Zeilen wurde nicht importiert.  
  
 Prozentsatz  
 REJECT_VALUE ist Prozentsatz, nicht auf einen literalen Wert. Die Datenbank wird beendet, Importieren von Zeilen aus der externen Datendatei, die bei der *Prozentsatz* fehlerhafter Zeilen überschreitet *Reject_value*. Der Prozentsatz fehlerhafter Zeilen wird in Abständen berechnet.  
  
 REJECT_SAMPLE_VALUE = *Reject_sample_value*  
 Erforderlich, wenn REJECT_TYPE = Percentage, gibt die Anzahl der Zeilen, die versuchen, importieren, bevor die Datenbank den Prozentsatz von fehlerhaften Zeilen berechnet.  
  
 Z. B. wenn REJECT_SAMPLE_VALUE = 1000, die Datenbank berechnet den Prozentsatz von fehlerhaften Zeilen aus, nachdem es versucht hat, können Sie 1000 Zeilen aus der externen Datendatei importieren. Wenn der Prozentsatz von fehlerhaften Zeilen ist kleiner als *Reject_value*, die Datenbank versucht, eine andere 1000 Zeilen zu laden. Die Datenbank weiterhin, den Prozentsatz von fehlerhaften Zeilen neu zu berechnen, nachdem er versucht, jede zusätzliche 1000 Zeilen importieren.  
  
> [!NOTE]  
>  Da die Datenbank in Intervallen den Prozentsatz von fehlerhaften Zeilen berechnet, kann der tatsächliche Prozentsatz fehlerhafter Zeilen überschreiten *Reject_value*.  
  
 Beispiel:  
  
 Dieses Beispiel zeigt, wie die drei REJECT-Optionen miteinander interagieren. Z. B. wenn REJECT_TYPE = Percentage "," REJECT_VALUE = 30 und REJECT_SAMPLE_VALUE = 100, das folgende Szenario auftreten:  
  
-   Die Datenbank versucht, die ersten 100 Zeilen zu laden; 25 ein Fehler auftreten und 75 erfolgreich ausgeführt werden.  
  
-   Ist kleiner als der Reject-Wert von 30 % Prozent der fehlerhaften Zeilen als 25 %, berechnet. Daher nicht erforderlich, um die Last anzuhalten.  
  
-   Die Datenbank versucht, die nächsten 100 Zeilen zu laden; Dieses Mal 25 erfolgreich ausgeführt werden, und 75 fehl.  
  
-   Prozentsatz fehlerhafter Zeilen wird als 50 % neu berechnet. Der Prozentsatz von fehlerhaften Zeilen hat den ablehnungswert 30 % überschritten.  
  
-   Die Last schlägt fehl mit Fehler von 50 % der Zeilen nach dem Versuch, das Laden von 200 Zeilen ist größer als das angegebene Limit von 30 %.  
  
 MIT *Common_table_expression*  
 Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Weitere Informationen finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Wählen Sie \<Select_criteria > füllt die neue Tabelle mit den Ergebnissen einer SELECT-Anweisung. *Select_criteria* ist der Hauptteil der SELECT-Anweisung, der bestimmt, welche Daten in die neue Tabelle kopieren. Informationen zur SELECT-Anweisungen finden Sie unter [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen dieses Befehls die **Datenbankbenutzer** benötigt alle dieser Berechtigungen oder Gruppenmitgliedschaften:  
  
-   **ALTER SCHEMA** -Berechtigung für die lokale Schema, das die neue Tabelle oder die Mitgliedschaft in enthält die **Db_ddladmin** festen Datenbankrolle "".  
  
-   **CREATE TABLE** Berechtigung oder die Mitgliedschaft in der **Db_ddladmin** festen Datenbankrolle "".  
  
-   **Wählen Sie** -Berechtigung für alle Objekte der *Select_criteria*.  
  
 Die Anmeldung erfordert alle diese Berechtigungen:  
  
-   **ADMINISTER BULK OPERATIONS** Berechtigung  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** Berechtigung  
  
-   **ALTER ANY EXTERNAL FILE FORMAT** Berechtigung  
  
-   Die Anmeldung muss über die Schreibberechtigung für Lese- und Schreibberechtigungen für den externen Ordner auf dem Hadoop-Cluster oder Azure-Speicher-Blob verfügen.  
 
 > [!IMPORTANT]  
 >  Die Berechtigung ALTER ANY EXTERNAL DATA SOURCE gewährt Prinzipal die Fähigkeit zum Erstellen und ändern alle externen Datenquellenobjekt und daher auch erteilt den Zugriff auf alle datenbankweit gültige Anmeldeinformationen für die Datenbank. Diese Berechtigung muss berücksichtigt werden, wie hoch privilegierten und daher im System nur für vertrauenswürdige Prinzipale erteilt werden müssen.
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn Daten in eine Datei mit Texttrennzeichen CREATE EXTERNAL TABLE AS SELECT exportiert werden, besteht keine Ablehnung-Datei für Zeilen, die nicht zu exportieren.  
  
 Wenn Sie die externe Tabelle zu erstellen, versucht die Datenbank für die Verbindung zur externen Hadoop-Cluster oder Azure-Speicher-Blob. Wenn die Verbindung fehlschlägt, der Befehl fehl, und die externe Tabelle nicht erstellt werden. Es kann eine Minute oder mehr für den Befehl zum seit Wiederholungen der Datenbank die Verbindung fehl, mindestens 3 Mal dauern.  
  
 Wenn CREATE EXTERNAL TABLE AS SELECT abgebrochen wird oder fehlschlägt, wird die Datenbank einen einmaligen Versuch, entfernen Sie alle neuen Dateien und Ordner, die bereits auf der externen Datenquelle erstellt werden.  
  
 Die Datenbank, meldet alle Java-Fehler, die auf die externe Datenquelle während des Datenexports auftreten.  
  
##  <a name="GeneralRemarks"></a>Allgemeine Hinweise  
 Nachdem die CETAS-Anweisung abgeschlossen ist, können Sie ausführen [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfragen für externe Tabelle. Diese Vorgänge werden Daten in der Datenbank für die Dauer der Abfrage importieren, wenn Sie mithilfe der CREATE TABLE AS SELECT-Anweisung importieren.  
  
 Den Tabellennamen der externen und Definitionen werden in den Datenbankmetadaten gespeichert. Die Daten werden in der externen Datenquelle gespeichert.  
  
 Die externen Dateien heißen *QueryID_date_time_ID.format*, wobei *ID* ein inkrementeller Bezeichner ist und *Format* das Format der exportierten Daten. Zum Beispiel QID776_20160130_182739_0.orc.  
  
 Immer die CETAS-Anweisung erstellt eine Tabelle nicht partitioniert, auch wenn die Quelltabelle partitioniert ist.  
  
 Abfragepläne erstellt mit der Erklärung der Databaseuses diesen Abfrage-Plan-Vorgängen für externe Tabellen:  
  
-   Externe zufällige Verschiebung  
  
-   Verschieben von externen broadcast  
  
-   Externe Partition verschieben  
  
 **GILT für:**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]als Voraussetzung für das Erstellen einer externen Tabelle, muss der Administrator Appliance Hadoop-Konnektivität konfigurieren.   Weitere Informationen finden Sie unter Konfigurieren Sie Verbindungen zu externen Daten (Analytics Platform System) in der APS-Dokumentation, das Sie herunterladen können [hier](http://www.microsoft.com/download/details.aspx?id=48241).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Da externe Tabellendaten befindet sich außerhalb der Datenbank, Sichern und Wiederherstellen funktionieren Vorgänge nur auf Daten in der Datenbank gespeichert. Dies bedeutet, dass nur die Metadaten gesichert und wiederhergestellt werden.  
  
 Die Datenbank wird nicht die Verbindung mit der externen Datenquelle überprüft, wenn eine Sicherung wiederherstellen, die eine externe Tabelle enthält. Wenn die ursprüngliche Quelle nicht zugänglich ist, wird die Wiederherstellung der Metadaten der externen Tabelle trotzdem erfolgreich bereitgestellt werden, SELECT-Vorgänge in der externen Tabelle schlägt jedoch fehl.  
  
 Die Datenbank garantiert nicht die Konsistenz der Daten zwischen den Zíelknoten die externen Daten. Sie Kunden tragen die alleinige Verantwortung, um die Konsistenz zwischen den externen Daten und der Datenbank aufrechtzuerhalten.  
  
 Data Manipulation Language (DML)-Vorgänge werden in externen Tabellen nicht unterstützt. Angenommen, Sie können keine der [!INCLUDE[tsql](../../includes/tsql-md.md)] aktualisieren, einfügen oder löschen [!INCLUDE[tsql](../../includes/tsql-md.md)]Anweisungen so ändern Sie die externen Daten.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW und DROP VIEW werden nur Daten, die Definition Language (DDL) Vorgänge für externe Tabellen zulässig sind.  
  
 PolyBase kann maximal 33 k Dateien pro Ordner nutzen, wenn Sie 32 gleichzeitige PolyBase-Abfragen ausgeführt. Diese maximale Anzahl enthält sowohl Dateien und Unterordner im jeweiligen Ordner HDFS an. Wenn der Grad an Parallelität höchstens 32 ist, kann ein Benutzer PolyBase-Abfragen für Ordner in HDFS ausführen, die mehr als 33 k-Dateien enthalten. [!INCLUDE[msCoName](../../includes/msconame-md.md)]empfiehlt Benutzern Hadoop und PolyBase Dateipfade kurze beibehalten und nicht mehr als 30 KB Dateien pro HDFS-Ordner. Tritt auf, eine JVM-Out-of-Memory-Ausnahme, wenn zu viele Dateien verwiesen werden.  
  
 [SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) hat keine Auswirkung auf diese CREATE EXTERNAL TABLE AS SELECT. Um ein ähnliches Verhalten zu erzielen, verwenden [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 Wenn CREATE EXTERNAL TABLE AS SELECT aus einer RCFile auswählt, die Spaltenwerte in die RCFile darf keinen die Pipe "|" Zeichen.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das SCHEMARESOLUTION-Objekt.  
  
##  <a name="Examples"></a> Beispiele  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Erstellen Sie eine Hadoop-Tabelle, die mit erstellen EXTERNEN Tabelle AS auswählen (CETAS)  
 Das folgende Beispiel erstellt eine neue externe Tabelle namens `hdfsCustomer`, mithilfe der Spaltendefinitionen und die Daten aus der Quelltabelle `dimCustomer`.  
  
 Die Tabellendefinition ist in der Datenbank gespeichert, und die Ergebnisse der SELECT-Anweisung werden exportiert, auf die "/ pdwdata/customer.tbl"-Datei auf der externen Datenquelle Hadoop *Customer_ds*. Die Datei wird entsprechend der externen Dateiformats formatiert *Customer_ff*.  
  
 Der Dateiname wird von der Datenbank generiert und enthält die ID der Abfrage zur Vereinfachung der Ausrichten von der Datei mit der Abfrage, die sie generiert.  
  
 Der Pfad `hdfs://xxx.xxx.xxx.xxx:5000/files/` vor Verzeichnis des Kunden muss bereits vorhanden. Wenn das Verzeichnis nicht vorhanden ist, wird die Datenbank das Verzeichnis erstellen.  
  
> [!NOTE]  
>  In diesem Beispiel gibt für 5000. Wenn kein Port angegeben ist, wird die Datenbank 8020 als den Standardport verwendet.  
  
 Die resultierende Hadoop Speicherort und Dateinamen werden `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Verwenden mit CREATE für externe Tabelle als Abfragehinweis auswählen (CETAS)  
 Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines Join-Abfragehinweis mit der CETAS-Anweisung. Nachdem die Abfrage, dass die Datenbank den Hash Join-Strategie verwendet übermittelt wird, um den Abfrageplan zu generieren. Weitere Informationen zu joinhinweise und wie Sie die OPTION-Klausel verwenden, finden Sie unter [OPTION-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  In diesem Beispiel gibt für 5000. Wenn kein Port angegeben ist, wird die Datenbank 8020 als den Standardport verwendet.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Erstellen von Tabellen &#40; Azure SQL Datawarehouse, Parallel Datawarehouse &#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [Erstellen Sie die Tabelle als SELECT &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  



