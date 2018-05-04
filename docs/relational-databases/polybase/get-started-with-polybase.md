---
title: Erste Schritte mit PolyBase | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
caps.latest.revision: 78
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c406a55361eb8a948f385f3bf7e76257c216720
ms.sourcegitcommit: f3aa02a0f27cc1d3d5450f65cc114d6228dd9d49
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="get-started-with-polybase"></a>Erste Schritte mit PolyBase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema behandelt die Grundlagen zum Installieren und Ausführen von PolyBase auf einer SQL Server-Instanz.
  
 Nachdem Sie die Schritte unten ausgeführt haben, verfügen Sie über:  
  
-   Ein installiertes und ausführbares Exemplar von PolyBase auf Ihrem Server  
  
-   Beispiele für Anweisungen zum Erstellen von PolyBase-Objekten  
  
-   Grundkenntnisse zum Verwalten von PolyBase-Objekten in SQL Server Management Studio (SSMS)  
  
-   Beispiele für Abfragen, die PolyBase-Objekte verwenden    

## <a name="install-polybase"></a>Installieren von PolyBase  
Wenn Sie PolyBase nicht installiert haben, finden Sie weitere Informationen unter [PolyBase installation (Installieren von PolyBase)](../../relational-databases/polybase/polybase-installation.md). Die Voraussetzungen für die Installation werden im entsprechenden Artikel erläutert.
  
### <a name="how-to-confirm-installation"></a>So bestätigen Sie die Installation  
 Führen Sie nach der Installation den folgenden Befehl aus, um zu bestätigen, dass PolyBase erfolgreich installiert wurde. Wenn PolyBase installiert ist, wird 1 zurückgegeben, andernfalls 0.  
  
```sql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> Konfigurieren von PolyBase  
 Nach der Installation müssen Sie SQL Server dafür konfigurieren, entweder Ihre Hadoop-Version oder Azure-BLOB-Speicher zu verwenden. PolyBase unterstützt zwei Hadoop-Anbieter: Hortonworks Data Platform (HDP) und Cloudera Distributed Hadoop (CDH).  Zu den unterstützten externen Datenquellen gehören:  
  
-   Hortonworks HDP 1.3 auf Linux/Windows Server  
  
-   Hortonworks HDP 2.1 – 2.6 unter Linux

-   Hortonworks HDP 2.1 – 2.3 unter Windows Server  
  
-   Cloudera CDH 4.3 unter Linux  
  
-   Cloudera CDH 5.1 bis 5.5, 5.9 bis 5.12 unter Linux  
  
-   Azure BLOB-Speicher  
 
Hadoop folgt bei neuen Releases dem Muster „Hauptversion.Nebenversion“. Alle Versionen, die innerhalb der unterstützten Haupt- und Nebenversionen liegen, werden unterstützt.
 

>  [!NOTE]
> Azure Data Lake Store-Konnektivität wird nur in Azure SQL Data Warehouse unterstützt.
  
### <a name="external-data-source-configuration"></a>Konfigurieren der externen Datenquelle  
  
1.  Führen Sie [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ‘hadoop connectivity’ aus, und legen Sie einen geeigneten Wert fest. Standardmäßig ist die Hadoop-Konnektivität auf 7 festgelegt. Informationen zum Ermitteln des Werts finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
      ```sql  
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
  
 ![Beenden und starten Sie PolyBase-Dienste in services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "stop and start PolyBase services in services.msc")  
  
### <a name="pushdown-configuration"></a>Pushdown-Konfiguration  
 Um die Abfrageleistung zu verbessern, aktivieren Sie die Pushdown-Berechnung für einen Hadoop-Cluster:  
  
1.  Suchen Sie die Datei **yarn-site.xml** im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  Suchen Sie auf dem Hadoop-Computer die analoge Datei im Hadoop-Konfigurationsverzeichnis. Suchen Sie in der Datei den Wert des Konfigurationsschlüssels „yarn.application.classpath.“, und kopieren Sie diesen.  
  
3.  Suchen Sie auf dem SQL Server-Computer in der Datei **yarn.site.xml** die Eigenschaft **yarn.application.classpath** . Fügen Sie den Wert vom Hadoop-Computer in das Element „Value“ ein.  
  
4. Für alle CDH 5.X-Versionen müssen Sie die Konfigurationsparameter „mapreduce.application.classpath“ entweder ans Ende der Datei „yarn.site.xml“ oder in die Datei „mapred-site.xml“ einfügen. HortonWorks enthält diese Konfigurationen in den yarn.application.classpath-Konfigurationen. Weitere Beispiele finden Sie unter [PolyBase-Konfiguration](../../relational-databases/polybase/polybase-configuration.md).

 
## <a name="scale-out-polybase"></a>Horizontales Hochskalieren von PolyBase  
 Die PolyBase-Gruppenfunktion ermöglicht Ihnen die Erstellung eines Clusters aus SQL Server-Instanzen, um große Datasets aus externen Datenquellen in einer Skalierungsart zu verarbeiten, die zu besseren Abfrageleistungen führt.  
  
1.  Installieren Sie SQL Server mit PolyBase auf mehreren Computern.  
  
2.  Wählen eine SQL Server-Instanz als Hauptknoten aus.  
  
3.  Fügen Sie andere Instanzen durch Ausführung von [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)als Serverknoten hinzu.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  Starten Sie den PolyBase-Datenverschiebungsdienst auf den Serverknoten neu.  
  
 Weitere Informationen finden Sie unter [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(PolyBase-Erweiterungsgruppen).  
  
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
  
CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH (  
       FORMAT_TYPE = DELIMITEDTEXT,   
       FORMAT_OPTIONS (
         FIELD_TERMINATOR ='|',   
         USE_TYPE_DEFAULT = TRUE
       )
);
         
  
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
  
    ```sql  
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
  
    ```sql  
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
 In SSMS werden externe Tabellen in einem separaten Ordner **Externe Tabellen**angezeigt. Externe Datenquellen und externe Dateiformate befinden sich in Unterordnern unter **Externe Ressourcen**.  
  
 ![PolyBase-Objekte in SSMS](../../relational-databases/polybase/media/polybase-management.png "PolyBase objects in SSMS")  
  
## <a name="troubleshooting"></a>Problembehandlung  
 Verwenden Sie DMVs, um Leistungs- und Abfragenprobleme zu beheben. Weitere Informationen finden Sie unter [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(Problembehandlung in PolyBase).  
  
 Nach der Aktualisierung von SQL Server 2016 RC1 auf RC2 oder RC3 können Fehler bei Abfragen auftreten. Weitere Informationen und Abhilfe finden Sie unter [Versionsanmerkungen zu SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) , und suchen Sie nach „PolyBase“.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Grundlagen zum horizontalen Skalieren finden Sie unter [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(PolyBase-Erweiterungsgruppen).  Informationen zum Überwachen von PolyBase finden Sie unter [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(Problembehandlung in PolyBase). Informationen zur Problembehandlung der PolyBase-Leistung finden Sie unter [PolyBase troubleshooting with dynamic management views (Problembehandlung in PolyBase mit dynamischen Verwaltungssichten)](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [Gespeicherte PolyBase-Prozeduren](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
