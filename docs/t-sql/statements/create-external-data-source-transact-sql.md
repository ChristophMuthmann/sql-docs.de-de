---
title: Erstellen der EXTERNEN Datenquelle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: 58
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 477d2f682da2c91ba8e4bfd42186c4b1b9735f85
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="create-external-data-source-transact-sql"></a>Erstellen der EXTERNEN Datenquelle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Erstellt eine externe Datenquelle für PolyBase, elastischen Datenbankabfragen oder Azure Blob-Speicher. Abhängig vom jeweiligen Szenario unterscheidet sich deutlich die Syntax aus. Eine Datenquelle erstellt, für PolyBase kann nicht für elastische Datenbanken Abfragen verwendet werden.  Auf ähnliche Weise kann eine Datenquelle erstellt, die für elastische Datenbanken Abfragen für PolyBase usw. verwendet werden. 
  
> [!NOTE]  
>  PolyBase ist nur für SQL Server 2016, Azure SQL Data Warehouse und Parallel Data Warehouse unterstützt. Elastische Datenbankabfragen werden nur auf Azure SQL-Datenbank v12 oder höher unterstützt.  
  
 Für PolyBase-Szenarien ist die externe Datenquelle, entweder eine Hadoop-Datei System (HDFS), ein Azure-Blob-Speichercontainer oder Azure Data Lake-Speicher. Weitere Informationen finden Sie unter [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Erste Schritte mit PolyBase).  
  
 Für elastische Datenbanken Abfrageszenarien ist die externe Quelle ein shardzuordnungs-Manager (für Azure SQL-Datenbank) oder eine remote-Datenbank (auf Azure SQL-Datenbank).  Verwendung [Sp_execute_remote &#40; Azure SQL-Datenbank &#41; ](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) nach dem Erstellen einer externen Datenquelle. Weitere Informationen finden Sie unter [elastische Datenbankabfrage](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  Azure-Blob-Speicher externe Datenquellen unterstützt `BULK INSERT` und `OPENROWSET` -Syntax und unterscheidet sich von Azure-Blob-Speicher für PolyBase.
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
    )
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumente  
 *Data_source_name* gibt den benutzerdefinierten Namen für die Datenquelle. Der Name muss innerhalb der Datenbank in SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse eindeutig sein. Der Name muss innerhalb des Servers in Parallel Data Warehouse eindeutig sein.
  
 TYP = [HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Gibt den Datenquellentyp. HADOOP verwenden, wird die externen Datenquelle Hadoop oder Azure-Speicher-BLOBs für Hadoop. Verwenden Sie SHARD_MAP_MANAGER aus, wenn eine externe Datenquelle für elastische Datenbanken Abfrage für Sharding in Azure SQL-Datenbank zu erstellen. Verwenden Sie RDBMS mit externen Datenquellen für datenbankübergreifende Abfragen mit elastischen Datenbank in Azure SQL-Datenbank.  BLOB_STORAGE verwenden, beim Ausführen von Massenvorgängen mithilfe von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
Speicherort = \<Location_path > **HADOOP**    
Für HADOOP gibt den Uniform Resource Indicator (URI) für einen Hadoop-Cluster.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: Den Computernamen oder IP-Adresse des Hadoop-Clusters – Namenode.  
Port: die – Namenode IPC-Port. Dies wird durch die fs.default.name Konfigurationsparameter in Hadoop angegeben. Wenn der Wert nicht angegeben wird, wird standardmäßig 8020 verwendet werden.  
Beispiel:`LOCATION = 'hdfs://10.10.10.10:8020'`

Gibt den URI für die Verbindung mit Azure-Blob-Speicher für den Azure-Blob-Speicher mit Hadoop.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
Wasb [s]: Gibt das Protokoll für Azure Blob-Speicher. Die [s] ist optional und gibt eine sichere SSL-Verbindung; von SQL Server gesendete Daten werden sicher über das SSL-Protokoll verschlüsselt. Es wird dringend empfohlen, mithilfe von "Wasbs" anstelle von "Wasb". Beachten Sie, dass der Speicherort asv [s] statt Wasb [s]. Die Syntax der asv [s] ist veraltet und wird in einer zukünftigen Version entfernt.  
Container: Gibt den Namen des Azure-Blob-Speichercontainer. Um den Stammcontainer der einer Domäne Speicherkonto anzugeben, verwenden Sie den Domänennamen anstelle des Namens des Entitätencontainers. Root-Container sind schreibgeschützt, damit keine Daten zurück in den Container geschrieben werden.  
Account_name: den vollständig qualifizierten Domänennamen (FQDN) des Azure-Speicherkonto.  
Beispiel:`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Speicherort für Azure Data Lake-Speicher gibt an, dass der URI für das Herstellen einer Verbindung mit Ihrem Azure Data Lake-Speicher.



**SHARD_MAP_MANAGER**   
 Für SHARD_MAP_MANAGER gibt den Namen des logischen Servers, der die shardzuordnungs-Manager in Azure SQL-Datenbank oder SQL Server-Datenbanken auf virtuellen Azure-Computer hostet.
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

Ein schrittweises Lernprogramm finden Sie unter [erste Schritte mit flexible Abfragen für Sharding (horizontales partitionieren)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/).
  
**RDBMS**   
Für RDBMS gibt den Namen des logischen Servers der Remotedatenbank in Azure SQL-Datenbank.  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
Ein schrittweises Lernprogramm auf RDBMS, finden Sie unter [Einstieg in datenbankübergreifenden Abfragen, die (vertikale Partitionierung)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Für Massenvorgänge nur `LOCATION` muss gültig sein. die URL zum Azure-Blob-Speicher und Container. Nehmen Sie nicht  **/** , Dateinamen an oder freigegebene Signatur Zugriffsparameter am Ende der `LOCATION` URL.   
Die Anmeldeinformationen verwendet, muss erstellt werden, mithilfe von `SHARED ACCESS SIGNATURE` als Identität. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Ein Beispiel für den Zugriff auf Blob-Speicher finden Sie in Beispiel F [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 

  
 RESOURCE_MANAGER_LOCATION = "*ResourceManager_URI*[:*Port*]"  
 Gibt an, das Hadoop Ressourcenmanager-Speicherort. Wenn angegeben, kann der Abfrageoptimierer eine kostenbasierte Entscheidung für eine PolyBase-Abfrage Daten vorab zu verarbeiten, mithilfe Hadoops-Datenverarbeitungsfunktionen mit MapReduce stellen. Prädikatweitergabe wird aufgerufen, kann dies erheblich reduzieren die Datenmenge, die zwischen Hadoop und SQL übertragen und aus diesem Grund die abfrageleistung.  
  
 Wenn dies nicht angegeben ist, wird die Berechnung an Hadoop weitergegeben werden. für PolyBase-Abfragen deaktiviert.  
 
Wenn kein Port angegeben ist, wird der Standardwert mit die aktuelle Einstellung für die Konfiguration von 'Hadoop Connectivity' bestimmt.

|Hadoop-Konnektivität|Standardport für die Ressourcen-Manager|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Eine vollständige Liste der Hadoop-Distributionen und Versionen, die von jeder Konnektivität-Wert unterstützt, finden Sie unter [PolyBase-Konfiguration (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  Der RESOURCE_MANAGER_LOCATION-Wert ist eine Zeichenfolge und wird nicht überprüft werden, wenn Sie die externe Datenquelle erstellen. Eingabe eines falschen Werts kann die zukünftige Verzögerungen beim zugreifen, auf den Speicherort führen.  
  
 Hadoop-Beispiele:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. 2.3 unter Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 unter Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2 und 2.3 unter Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Hortonworks HDP 1.3 unter Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Cloudera 4.3 unter Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Cloudera 5.1 5.11 unter Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 Anmeldeinformationen = *Credential_name*  
 Gibt die datenbankbezogenen Anmeldeinformationen für die Authentifizierung mit der externen Datenquelle. Ein Beispiel finden Sie unter [C. erstellen eine Azure-Blob-Speicher des externen Datenquelle](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Zum Erstellen von Anmeldeinformationen finden Sie unter [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Beachten Sie, dass die Anmeldeinformationen nicht bei öffentlichen Datasets erforderlich ist, die den anonymen Zugriff zulassen. 
  
 Database_name = *"QueryDatabaseName"*  
 Der Name der Datenbank, die als die shardzuordnungs-Manager (für SHARD_MAP_MANAGER) besitzt oder die remote-Datenbank (für RDBMS).  
  
 SHARD_MAP_NAME = *"ShardMapName"*  
 Für SHARD_MAP_MANAGER. Der Name des der shardzuordnung. Weitere Informationen zum Erstellen einer shardzuordnung finden Sie unter [Einstieg in die Abfrage für elastische Datenbanken](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase-spezifischen Anmerkungen zu dieser  
Eine vollständige Liste der unterstützten externen Datenquellen finden Sie unter [PolyBase-Konfiguration (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Um PolyBase verwenden zu können, müssen Sie diese drei Objekte zu erstellen:  
  
-   Eine externe Datenquelle.  
  
-   Ein externes Dateiformat und  
  
-   Eine externe Tabelle, die auf der externen Datenquelle und externen Dateiformats verweist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Datenbank in SQL Data Warehouse, SQL Server 2016 APS und SQL-Datenbank.

> [!IMPORTANT]  
>  Erstellen Sie in früheren Versionen von PDW externe erforderlich, ALTER ANY EXTERNAL DATA SOURCE datenquellenberechtigungen.
  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Ein Laufzeitfehler treten auf, wenn die externe Hadoop-Datenquellen inkonsistent Vorteil RESOURCE_MANAGER_LOCATION definiert sind. Sie können nicht, also zwei externe Datenquellen angeben, die den gleichen Hadoop-Cluster und anschließend Ressourcenmanager-Speicherort für eine und nicht für die anderen verweisen.  
  
 SQL Engine überprüft nicht das Vorhandensein der externen Datenquelle, wenn das Quellobjekt für den externen Daten erstellt. Wenn die Datenquelle nicht während der abfrageausführung vorhanden ist, tritt ein Fehler auf.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Für PolyBase ist die externen Datenquelle in SQL Server und SQL Data Warehouse-Datenbank beschränkt. Serverbezogene ist in Parallel Data Warehouse.
  
Für PolyBase Wenn RESOURCE_MANAGER_LOCATION oder JOB_TRACKER_LOCATION definiert ist, wird vom Abfrageoptimierer berücksichtigt optimieren, jede Abfrage initiiert wird, eine Zuordnung zu reduzieren, Auftrag auf der externen Quelle für Hadoop und Berechnung weitergegeben werden. Dies ist vollständig eine kostenbasierte Entscheidung.  

Zum erfolgreichen PolyBase-Abfragen bei Hadoop NameNode Failover zu gewährleisten, sollten Sie in Betracht ziehen, eine virtuelle IP-Adresse für den – NameNode des Hadoop-Clusters zu verwenden. Wenn Sie eine virtuelle IP-Adresse für das Hadoop NameNode nicht verwenden, im Fall eines Failovers Hadoop NameNode müssen ALTER EXTERNAL DATA SOURCE-Objekt, zeigen Sie auf den neuen Speicherort Sie.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Alle Datenquellen, die auf den gleichen Speicherort des Hadoop-Cluster definiert, müssen dieselbe Einstellung für RESOURCE_MANAGER_LOCATION oder JOB_TRACKER_LOCATION verwenden. Falls es Inkonsistenz, wird ein Laufzeitfehler auftreten.  
  
 Wenn der Hadoop-Cluster mit einem Namen eingerichtet ist, und die externen Datenquelle die IP-Adresse für den Cluster-Speicherort verwendet, muss PolyBase werden immer noch auf den Namen des Clusters zu beheben, wenn die Datenquelle verwendet wird. Um den Namen zu beheben, müssen Sie eine DNS-Weiterleitung aktivieren.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für die EXTERNAL DATA SOURCE-Objekt.  
  
##  <a name="examples"></a>Beispiele: SQLServer 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Externe Datenquelle Verweis Hadoop erstellen  
Um eine externe Datenquelle, um Ihre Hortonworks oder Cloudera Hadoop-Cluster verweisen zu erstellen, geben Sie den Computernamen oder IP-Adresse des Hadoop Namenode und -Port.  
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Erstellen Sie die externe Datenquelle Verweis Hadoop mit Weitergabe aktiviert  
Angeben der Option RESOURCE_MANAGER_LOCATION Pushdown Berechnung an Hadoop für PolyBase-Abfragen zu aktivieren. Nach der Aktivierung verwendet PolyBase eine kostenbasierte Entscheidung, um zu bestimmen, ob die Abfrage Berechnung an Hadoop geschoben werden sollte, oder alle Daten, die zum Verarbeiten der Abfrage in SQL Server verschoben werden soll.
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Erstellen Sie die externe Datenquelle, um Kerberos-gesicherte Hadoop verweisen  
Um sicherzustellen, dass Kerberos-gesicherte Hadoop-Clusters ist, können überprüfen Sie den Wert der hadoop.security.authentication-Eigenschaft im Hadoop-Core-site.xml. Um ein Kerberos-gesicherten Hadoop-Cluster zu verweisen, müssen Sie die datenbankweit gültigen Anmeldeinformationen angeben, die Kerberos-Benutzernamen und Kennwort enthält. Datenbank-Hauptschlüssels wird verwendet, um Bereichsbezogene Anmeldeinformation Datenbank zu verschlüsseln. 
  
```tsql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Erstellen Sie die externe Datenquelle, um die Azure-Blob-Speicher verweisen
Geben Sie zum Erstellen einer externen Datenquelle, um Ihren Azure-Blob-Speichercontainer verweisen der Azure-Blob-Speicher-URI und datenbankweit gültigen Anmeldeinformationen, die Ihren Azure-speicherkontoschlüssel enthält.

In diesem Beispiel ist die externen Datenquelle ein Azure-Blob-Speichercontainer Dailylogs unter Azure Storage-Konto mit dem Namen Myaccount aufgerufen. Die externe Datenquelle für die Azure-Speicher ist für die Datenübertragung nur; und die prädikatweitergabe wird nicht unterstützt.

Dieses Beispiel zeigt, wie Sie die datenbankbezogenen Anmeldeinformationen für die Authentifizierung beim Azure-Speicher zu erstellen. Geben Sie den Azure-Speicher-kontoschlüssel in der Datenbank-Anmeldeinformation an. Geben Sie eine beliebige Zeichenfolge in die Datenbank im Bereich einer Identität der Anmeldeinformationen, er wird nicht für die Authentifizierung beim Azure-Speicher verwendet. Anschließend wird die Anmeldeinformationen in der Anweisung verwendet, die von einer externen Datenquelle erstellt.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Beispiele: Azure SQL-Datenbank

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Erstellen einer Shard Zuordnung Manager externe-Datenquelle
Geben Sie den Namen des logischen Servers, der die shardzuordnungs-Manager in Azure SQL-Datenbank oder SQL Server-Datenbanken auf virtuellen Azure-Computer hostet, zum Erstellen einer externen Datenquelle, um eine SHARD_MAP_MANAGER zu verweisen.

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. Erstellen einer externen RDBMS-Datenquelle
Zum Erstellen einer externen Datenquelle ein RDBMS verweisen gibt den Namen des logischen Servers der Remotedatenbank in Azure SQL-Datenbank.

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>Beispiele: SQL Azure Datawarehouse

### <a name="g-create-external-data-source-to-reference-azure-blob-storage"></a>G. Erstellen Sie die externe Datenquelle, um die Azure-Blob-Speicher verweisen
Geben Sie zum Erstellen einer externen Datenquelle, um Ihren Azure-Blob-Speichercontainer verweisen der Azure-Blob-Speicher-URI und datenbankweit gültigen Anmeldeinformationen, die Ihren Azure-speicherkontoschlüssel enthält.

In diesem Beispiel ist die externen Datenquelle ein Azure-Blob-Speichercontainer Dailylogs unter Azure Storage-Konto mit dem Namen Myaccount aufgerufen. Die externe Datenquelle für die Azure-Speicher ist für die Datenübertragung nur und prädikatweitergabe nicht unterstützt.

Dieses Beispiel zeigt, wie Sie die datenbankbezogenen Anmeldeinformationen für die Authentifizierung beim Azure-Speicher zu erstellen. Geben Sie den Azure-Speicher-kontoschlüssel in der Datenbank-Anmeldeinformation an. Geben Sie eine beliebige Zeichenfolge in die Datenbank im Bereich einer Identität der Anmeldeinformationen, er wird nicht für die Authentifizierung beim Azure-Speicher verwendet. Anschließend wird die Anmeldeinformationen in der Anweisung verwendet, die von einer externen Datenquelle erstellt.

```tsql
-- Create a database master key if one does not already exist. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage 
WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```
### <a name="h-create-external-data-source-to-reference-azure-data-lake-store"></a>H. Erstellen der externen Datenquelle zu verweisen Azure Data Lake-Speicher
Azure Data Lake-Speicher-Konnektivität basiert auf der ADLS-URI und dem Dienstprinzipal Ihrer Azure Active Directory-Anwendung. Dokumentation zum Erstellen dieser Anwendung finden Sie unter[Data Lake-Speicher-Authentifizierung mithilfe von Active Directory](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```tsql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>Beispiele: Parallel Datawarehouse

### <a name="i-create-external-data-source-to-reference-hadoop"></a>I. Externe Datenquelle Verweis Hadoop erstellen
Um eine externe Datenquelle, um Ihre Hortonworks oder Cloudera Hadoop-Cluster verweisen zu erstellen, geben Sie den Computernamen oder IP-Adresse des Hadoop Namenode und -Port.

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);
```

### <a name="j-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>J. Erstellen Sie die externe Datenquelle Verweis Hadoop mit Weitergabe aktiviert
Angeben der Option JOB_TRACKER_LOCATION Pushdown Berechnung an Hadoop für PolyBase-Abfragen zu aktivieren. Nach der Aktivierung verwendet PolyBase eine kostenbasierte Entscheidung, um zu bestimmen, ob die Abfrage Berechnung an Hadoop geschoben werden sollte, oder alle Daten, die zum Verarbeiten der Abfrage in SQL Server verschoben werden soll. 

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="k-create-external-data-source-to-reference-azure-blob-storage"></a>K. Erstellen Sie die externe Datenquelle, um die Azure-Blob-Speicher verweisen
So erstellen eine externe Datenquelle für Ihren Azure-Blob-Speichercontainer verweisen, geben Sie dem Azure-Blob-Speicher-URI als die externen Daten Quellspeicherort. PDW-Core-site.xml-Datei für die Authentifizierung Ihrer Azure-speicherkontoschlüssel hinzugefügt.

In diesem Beispiel ist die externen Datenquelle ein Azure-Blob-Speichercontainer Dailylogs unter Azure Storage-Konto mit dem Namen Myaccount aufgerufen. Die externe Datenquelle für die Azure-Speicher ist für die Datenübertragung nur und prädikatweitergabe nicht unterstützt.

```tsql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Beispiele: Massenvorgänge   
### <a name="l-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>L. Erstellen einer externen Datenquelle für Massenvorgänge Abrufen von Daten aus dem Azure-Blob-Speicher.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Verwenden Sie die folgende Datenquelle für Massenvorgänge mit [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). Die Anmeldeinformationen verwendet, muss erstellt werden, mithilfe von `SHARED ACCESS SIGNATURE` als Identität. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```tsql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
In diesem Beispiel verwendet, finden Sie unter [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch
[Ändern der EXTERNEN Datenquelle (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[Erstellen Sie die externe Tabelle AS SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[Erstellen Sie die Tabelle als SELECT &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[Sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  


