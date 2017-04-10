---
title: "Erste Schritte mit PolyBase | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, erste Schritte"
  - "Hadoop-Import"
  - "Hadoop-Export"
  - "Azure-BLOB-Speicherimport"
  - "Azure-BLOB-Speicherexport"
  - "Hadoop-Import, erste Schritte mit PolyBase"
  - "Hadoop-Export, erste Schritte mit PolyBase"
ms.assetid: c71ddc50-b4c7-416c-9789-264671bd9ecb
caps.latest.revision: 78
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 73
---
# Erste Schritte mit PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema behandelt die Grundlagen zum Installieren und Ausführen von PolyBase. Weitere Informationen finden Sie im [PolyBase Guide](../../relational-databases/polybase/polybase-guide.md) (PolyBase-Handbuch).  
  
 Nachdem Sie die Schritte unten ausgeführt haben, verfügen Sie über:  
  
-   Ein installiertes und ausführbares Exemplar von PolyBase auf Ihrem Server  
  
-   Beispiele für Anweisungen zum Erstellen von PolyBase-Objekten  
  
-   Grundkenntnisse zum Verwalten von PolyBase-Objekten in SQL Server Management Studio (SSMS)  
  
-   Beispiele für Abfragen, die PolyBase-Objekte verwenden  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Eine Instanz von [SQL Server (64-Bit)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016).  
  
-   Microsoft .NET Framework 4.5.  
  
-   Oracle Java SE RunTime Environment (JRE), Version 7.51 oder höher (64-Bit). (Entweder [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) oder [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funktioniert). Wechseln Sie zu [Java SE-Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Das Installationsprogramm löst einen Fehler aus, wenn JRE nicht vorhanden ist.   
  
-   Mindestens erforderlicher Arbeitsspeicher: 4 GB  
  
-   Mindestfestplattenspeicher: 2 GB  
  
-   TCP/IP-Konnektivität muss aktiviert sein. (Weitere Informationen finden Sie unter [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).)  
  
 Eine der folgenden externen Datenquellen:  
  
-   Hadoop-Cluster. Unterstützte Versionen finden Sie unter [Konfigurieren von PolyBase](#supported).  
  
-   Azure-BLOB-Speicher 

> [!NOTE]
> HDInsight-Cluster verwenden Azure-BLOB-Speicher als Dateisystem für ihren permanenten Speicher. Sie können mit PolyBase die Dateien abfragen, die von einem HDInsight-Cluster verwaltet werden. Erstellen Sie zu diesem Zweck eine externe Datenquelle, um auf das Blob zu verweisen, das als Speicher für den HDInsight-Cluster konfiguriert ist. 
  
## <a name="install-polybase"></a>Installieren von PolyBase  
 Installieren Sie PolyBase als Teil der Installation von SQL Server. Weitere Informationen finden Sie unter  [PolyBase installation](../../relational-databases/polybase/polybase-installation.md) (Installation von PolyBase).  
  
### <a name="how-to-confirm-installation"></a>So bestätigen Sie die Installation  
 Führen Sie nach der Installation den folgenden Befehl aus, um zu bestätigen, dass PolyBase erfolgreich installiert wurde. Wenn PolyBase installiert ist, wird 1 zurückgegeben, andernfalls 0.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="a-namesupporteda-configure-polybase"></a><a name="supported"></a> Konfigurieren von PolyBase  
 Nach der Installation müssen Sie SQL Server dafür konfigurieren, entweder Ihre Hadoop-Version oder Azure-BLOB-Speicher zu verwenden. PolyBase unterstützt zwei Hadoop-Anbieter, Hortonworks Data Platform (HDP) und Cloudera CDH. Hortonworks kann wahlweise auf einem Windows- oder einem Linux-Computer ausgeführt werden, und das muss in der Konfiguration berücksichtigt werden.  Zu den unterstützten externen Datenquellen gehören:  
  
-   Hortonworks HDP 1.3 auf Linux/Windows Server  
  
-   Hortonworks HDP 2.1 – 2.5 unter Linux

-   Hortonworks HDP 2.1 – 2.3 unter Windows Server  
  
-   Cloudera CDH 4.3 unter Linux  
  
-   Cloudera CDH 5.1 – 5.5, 5.9 unter Linux  
  
-   Azure BLOB-Speicher  
  
### <a name="external-data-source-configuration"></a>Konfigurieren der externen Datenquelle  
  
1.  Führen Sie [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ‘hadoop connectivity’ aus, und legen Sie einen geeigneten Wert fest.  Wie Sie den Wert ermitteln, erfahren Sie unter [PolyBase-Konfiguration &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  Sie müssen SQL Server mithilfe von **services.msc** neu starten. Durch den Neustart von SQL Server werden folgende Dienste neu gestartet:  
  
    -   SQL Server PolyBase-Datenverschiebungsdienst  
  
    -   SQL Server PolyBase-Modul  
  
 ![stop and start PolyBase services in services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "stop and start PolyBase services in services.msc")  
  
### <a name="pushdown-configuration"></a>Pushdown-Konfiguration  
 Um die Abfrageleistung zu verbessern, aktivieren Sie die Pushdown-Berechnung für einen Hadoop-Cluster:  
  
1.  Suchen Sie die Datei **yarn-site.xml** im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  Suchen Sie auf dem Hadoop-Computer die analoge Datei im Hadoop-Konfigurationsverzeichnis. Suchen Sie in der Datei den Wert des Konfigurationsschlüssels „yarn.application.classpath.“, und kopieren Sie diesen.  
  
3.  Suchen Sie auf dem SQL Server-Computer in der Datei **yarn.site.xml** die Eigenschaft **yarn.application.classpath**. Fügen Sie den Wert vom Hadoop-Computer in das Element „Value“ ein.  
  
## <a name="scale-out-polybase"></a>Horizontales Hochskalieren von PolyBase  
 Die PolyBase-Gruppenfunktion ermöglicht Ihnen die Erstellung eines Clusters aus SQL Server-Instanzen, um große Datasets aus externen Datenquellen in einer Skalierungsart zu verarbeiten, die zu besseren Abfrageleistungen führt.  
  
1.  Installieren Sie SQL Server mit PolyBase auf mehreren Computern.  
  
2.  Wählen eine SQL Server-Instanz als Hauptknoten aus.  
  
3.  Fügen Sie andere Instanzen durch Ausführung von [sp_polybase_join_group](../Topic/sp_polybase_join_group.md) als Serverknoten hinzu.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  Starten Sie den PolyBase-Datenverschiebungsdienst auf den Serverknoten neu.  
  
 Weitere Informationen finden Sie unter [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md) (PolyBase-Erweiterungsgruppen).  
  
## <a name="create-t-sql-objects"></a>Erstellen von T-SQL-Objekten  
 Erstellen Sie Objekte abhängig von der externen Datenquelle, entweder Hadoop oder Azure-Speicher.  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
-- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = MyHadoopCluster,  
        FILE_FORMAT = TextFileFormat  
);  
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Azure BLOB-Speicher  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = AzureStorage,  
        FILE_FORMAT = TextFileFormat  
);  
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>PolyBase-Abfragen  
 Es gibt drei Funktionen, für die PolyBase geeignet ist:  
  
-   Ad-hoc-Abfragen von externen Tabellen  
  
-   Importieren von Daten.  
  
-   Exportieren von Daten.  
  
### <a name="query-examples"></a>Beispiele für Abfragen  
  
-   Ad-hoc-Abfragen  
  
    ```tsql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   Importieren von Daten  
  
    ```tsql  
    -- PolyBase Scenario 2: Import external data into SQL Server.  
    -- Import data for fast drivers into SQL Server to do more in-depth analysis and  
    -- leverage Columnstore technology.  
  
    SELECT DISTINCT   
            Insured_Customers.FirstName, Insured_Customers.LastName,   
            Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
    INTO Fast_Customers from Insured_Customers INNER JOIN   
    (  
            SELECT * FROM CarSensor_Data where Speed > 35   
    ) AS SensorD  
    ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
    ORDER BY YearlyIncome  
  
    CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
    ```  
  
-   Exportieren von Daten  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
    reconfigure  
  
    -- Create an external table.   
    CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
            [FirstName] char(25) NOT NULL,   
            [LastName] char(25) NOT NULL,   
            [YearlyIncome] float NULL,   
            [MaritalStatus] char(1) NOT NULL  
    )  
    WITH (  
            LOCATION='/old_data/2009/customerdata',  
            DATA_SOURCE = HadoopHDP2,  
            FILE_FORMAT = TextFileFormat,  
            REJECT_TYPE = VALUE,  
            REJECT_VALUE = 0  
    );  
  
    -- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
    INSERT INTO dbo.FastCustomer2009  
    SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
    ON (T1.CustomerKey = T2.CustomerKey)  
    WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
    ```  
  
## <a name="managing-polybase-objects-in-ssms"></a>Verwalten von PolyBase-Objekten in SSMS  
 In SSMS werden externe Tabellen in einem separaten Ordner **Externe Tabellen** angezeigt. Externe Datenquellen und externe Dateiformate befinden sich in Unterordnern unter **Externe Ressourcen**.  
  
 ![PolyBase objects in SSMS](../../relational-databases/polybase/media/polybase-management.png "PolyBase objects in SSMS")  
  
## <a name="troubleshooting"></a>Problembehandlung  
 Verwenden Sie DMVs, um Leistungs- und Abfragenprobleme zu beheben. Weitere Informationen finden Sie unter [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md) (Problembehandlung in PolyBase).  
  
 Nach der Aktualisierung von SQL Server 2016 RC1 auf RC2 oder RC3 können Fehler bei Abfragen auftreten. Weitere Informationen und Abhilfe finden Sie unter [Versionsanmerkungen zu SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md), und suchen Sie nach „PolyBase“.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Grundlagen zum horizontalen Skalieren finden Sie unter [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md) (PolyBase-Erweiterungsgruppen).  Informationen zum Überwachen von PolyBase finden Sie unter [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md) (Problembehandlung in PolyBase). Informationen zur Problembehandlung bei der PolyBase-Leistung finden Sie unter [PolyBase troubleshooting](../Topic/PolyBase%20troubleshooting%20with%20dynamic%20management%20views.md) (Problembehandlung in PolyBase) in den Abschnitten zu dynamischen Verwaltungsansichten.  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [Gespeicherte PolyBase-Prozeduren](../Topic/PolyBase%20stored%20procedures.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  