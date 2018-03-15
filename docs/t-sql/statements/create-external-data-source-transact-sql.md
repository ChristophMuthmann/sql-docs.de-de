---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/06/2017
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
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9d7d610008b17db9fdec1e33b1577e38a3d9f3a9
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/24/2018
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Erstellt eine externe Datenquelle für PolyBase oder elastische Datenbankabfragen. Abhängig vom jeweiligen Szenario unterscheidet sich die Syntax deutlich. Eine externe Datenquelle, die für PolyBase erstellt wurde, kann nicht für elastische Datenbankabfragen verwendet werden.  Auf ähnliche Weise kann eine externe Datenquelle, die für elastische Datenbankenabfragen erstellt wurde, nicht für PolyBase, usw. verwendet werden. 
  
> [!NOTE]  
>  PolyBase wird nur auf SQL Server 2016 (oder höher), Azure SQL Data Warehouse und Parallel Data Warehouse unterstützt. Elastische Datenbankabfragen werden nur auf Azure SQL-Datenbank v12 oder höher unterstützt.  
  
 Für PolyBase-Szenarios ist die externe Datenquelle entweder ein Hadoop-Dateisystem (HDFS), ein Azure Storage Blob-Container oder Azure Data Lake Storage. Weitere Informationen finden Sie unter [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Erste Schritte mit PolyBase).  
  
 Für elastische Datenbankenabfrageszenarios ist die externe Quelle ein Shardzuordnungs-Manager (für Azure SQL-Datenbank) oder eine Remotedatenbank (für Azure SQL-Datenbank).  Verwenden Sie [sp_execute_remote &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) nach dem Erstellen einer externen Datenquelle. Weitere Informationen finden Sie unter [Elastische Datenbankabfrage](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  Die externe Datenquelle von Azure Blob Storage unterstützt die `BULK INSERT`- und `OPENROWSET`-Syntax und unterscheidet sich von Azure Blob Storage für PolyBase.
    
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
 *data_source_name* gibt den benutzerdefinierten Namen für die Datenquelle an. Der Name muss innerhalb der Datenbank in SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse eindeutig sein. Der Name muss innerhalb des Servers in Parallel Data Warehouse eindeutig sein.
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Gibt den Typ der Datenquelle an. Verwenden Sie HADOOP, wenn die externe Datenquelle Hadoop oder Azure Storage Blob für Hadoop sind. Verwenden Sie SHARD_MAP_MANAGER, wenn Sie eine externe Datenquelle für elastische Datenbankabfragen für das Sharding in Azure SQL-Datenbank erstellen. Verwenden Sie RDBMS mit externen Datenquellen für datenbankübergreifende Abfragen mit elastischen Datenbankabfragen in Azure SQL-Datenbank.  Verwenden Sie BLOB_STORAGE beim Ausführen von Massenvorgängen mithilfe von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
LOCATION = \<location_path> **HADOOP**    
Für HADOOP wird der Uniform Resource Indicator (URI) für ein Hadoop-Cluster angegeben.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: Der Computername oder die IP-Adresse von NameNode des Hadoop-Clusters.  
Port: Der IPC-Port von NameNode. Dies wird durch den Konfigurationsparameter „fs.default.name“ in Hadoop angegeben. Wenn der Wert nicht angegeben wird, wird standardmäßig 8020 verwendet werden.  
Beispiel: `LOCATION = 'hdfs://10.10.10.10:8020'`

Gibt den URI für die Verbindung mit Azure Blob Storage für Azure Blob Storage mit Hadoop an.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]: Gibt das Protokoll für Azure Blob Storage an. [s] ist optional und gibt eine sichere SSL-Verbindung an; von SQL Server gesendete Daten werden über das SSL-Protokoll sicher verschlüsselt. Es wird dringend empfohlen, „wasbs“ anstelle von „wasb“ zu verwenden. Beachten Sie, dass der Speicherort asv[s] anstelle von wasb[s] verwenden kann. Die asv[s]-Syntax ist als veraltet markiert und wird in einem zukünftigen Release entfernt.  
Container: Gibt den Namen des Azure Blob Storage-Containers an. Verwenden Sie den Domänennamen anstelle des Containernamens, um den Stammcontainer des Speicherkontos einer Domäne anzugeben. Stammcontainer sind schreibgeschützt, damit keine Daten zurück in den Container geschrieben werden können.  
account_name: Der vollständig qualifizierte Domänenname (FQDN) des Azure-Speicherkontos.  
Beispiel: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Der Speicherort für Azure Data Lake Store gibt den URI für das Herstellen einer Verbindung mit Azure Data Lake Storage an.



**SHARD_MAP_MANAGER**   
 Für SHARD_MAP_MANAGER wird der Name des logischen Servers angegeben, der den Shardzuordnungs-Manager in Azure SQL-Datenbank oder einer SQL Server-Datenbank auf einer Azure-VM hostet.
 
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

Sie finden ein ausführliches Tutorial unter [Getting started with elastic queries for sharding (horizontal partitioning) (Erste Schritte mit elastischen Abfragen für Sharding (horizontales Partitionieren))](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/).
  
**RDBMS**   
Für RDBMS wird der Name des logischen Servers der Remotedatenbank in Azure SQL-Datenbank angegeben.  

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
  
Sie finden ein ausführliches Tutorial für RDBMS unter [Getting started with cross-database queries (vertical partitioning) (Erste Schritte mit datenbankübergreifenden Abfragen (vertikale Partitionierung))](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Nur bei Massenvorgängen muss `LOCATION` die gültige URL für Azure Blob Storage und den Container sein. Fügen Sie weder **/**, Dateinamen noch Shared Access Signature-Parameter am Ende der `LOCATION`-URL ein.   
Die verwendeten Anmeldeinformationen müssen mithilfe von `SHARED ACCESS SIGNATURE` als Identität erstellt werden. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Ein Beispiel für den Zugriff auf Blob Storage finden Sie in Beispiel F [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 Gibt den Speicherort für den Hadoop-Ressourcen-Manager an. Wenn angegeben, kann der Abfrageoptimierer eine kostenorientierte Entscheidung treffen, dass Daten für eine PolyBase-Abfrage mithilfe der Berechnungsfunktionen von Hadoop und MapReduce vorverarbeitet werden. Durch den Aufruf der Prädikatweitergabe kann dies die Menge der zwischen Hadoop und SQL übertragenen Daten deutlich reduzieren und damit die Abfrageleistung verbessern.  
  
 Wenn dies nicht angegeben ist, wird die Weitergabe der Berechnung an Hadoop für PolyBase-Abfragen deaktiviert.  
 
Wenn kein Port angegeben ist, wird der Standardwert mit der aktuellen Einstellung für die Konfiguration von „Hadoop Connectivity“ bestimmt.

|Hadoop Connectivity|Standardport des Ressourcen-Managers|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Eine vollständige Liste der Hadoop-Distributionen und -Versionen, die von jedem Konnektivitätswert unterstützt werden, finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  Der RESOURCE_MANAGER_LOCATION-Wert ist eine Zeichenfolge und wird nicht überprüft, wenn Sie die externe Datenquelle erstellen. Die Eingabe eines falschen Werts kann zukünftige Verzögerungen beim Zugriff auf den Speicherort auslösen.  
  
 Hadoop-Beispiele:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. 2.3 unter Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 unter Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2, 2.3 unter Linux:   
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
  
-   Cloudera 5.1 - 5.11 unter Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 Gibt die datenbankbezogenen Anmeldeinformationen für die Authentifizierung mit der externen Datenquelle an. Ein Beispiel finden Sie unter [C. Create an Azure blob storage external data source (C. Erstellen einer externen Datenquelle für Azure Blob Storage)](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Informationen zum Erstellen von Anmeldeinformationen finden Sie unter [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Beachten Sie, dass CREDENTIAL nicht bei öffentlichen Datasets erforderlich ist, die den anonymen Zugriff zulassen. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 Der Name der Datenbank, die als die Shardzuordnungs-Manager (für SHARD_MAP_MANAGER) oder als Remotedatenbank (für RDBMS) fungiert.  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Nur für SHARD_MAP_MANAGER. Der Name der Shardzuordnung. Weitere Informationen zum Erstellen einer Shardzuordnung finden Sie unter [Einstieg in die Abfrage für elastische Datenbanken](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase-spezifische Notizen  
Eine vollständige Liste der unterstützten externen Datenquellen finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Um PolyBase verwenden zu können, müssen Sie diese drei Objekte erstellen:  
  
-   Eine externe Datenquelle.  
  
-   Ein externes Dateiformat und  
  
-   Eine externe Tabelle, die auf die externe Datenquelle und das externe Dateiformat verweist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Datenbank in SQL Data Warehouse, SQL Server, APS 2016 und SQL-Datenbank.

> [!IMPORTANT]  
>  In früheren Releases von PDW erforderten externe Datenquellen ALTER ANY EXTERNAL DATA SOURCE-Berechtigungen.
  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Ein Laufzeitfehler tritt auf, wenn die externen Hadoop-Datenquellen inkonsistent mit der Definition von RESOURCE_MANAGER_LOCATION sind. Das heißt, dass Sie nicht zwei externe Datenquellen angeben können, die auf den gleichen Hadoop-Cluster verweisen und anschließend den Speicherort des Ressourcen-Managers für eine und nicht für die andere bereitstellen können.  
  
 Die SQL Engine überprüft das Vorhandensein der externen Datenquelle nicht, wenn das Quellobjekt für die externen Daten erstellt wird. Wenn die Datenquelle während der Abfrageausführung nicht vorhanden ist, tritt ein Fehler auf.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Die externe Datenquelle für PolyBase ist in SQL Server und SQL Data Warehouse datenbankweit gültig. In Parallel Data Warehouse ist sie serverweit gültig.
  
Wenn RESOURCE_MANAGER_LOCATION oder JOB_TRACKER_LOCATION für PolyBase definiert ist, berücksichtigt der Abfrageoptimierer jede Abfrage, indem er einen MapReduce-Auftrag auf der externen Hadoop-Quelle initiiert und die Berechnung weitergibt. Dies ist eine vollständig kostenorientierte Entscheidung.  

Für erfolgreiche PolyBase-Abfragen bei Hadoop-NameNode-Failovern sollten Sie in Betracht ziehen, eine virtuelle IP-Adresse für den NameNode des Hadoop-Clusters zu verwenden. Wenn Sie keine virtuelle IP-Adresse für NameNode von Hadoop verwenden, muss im Fall eines Failovers von Hadoop NameNode das ALTER EXTERNAL DATA SOURCE-Objekt auf den neuen Speicherort zeigen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Alle Datenquellen, die auf dem gleichen Speicherort des Hadoop-Clusters definiert sind, müssen dieselbe Einstellung für RESOURCE_MANAGER_LOCATION oder JOB_TRACKER_LOCATION verwenden. Im Falle einer Inkonsistenz wird ein Laufzeitfehler auftreten.  
  
 Wenn der Hadoop-Cluster mit einem Namen eingerichtet ist, und die externen Datenquelle die IP-Adresse für den Clusterstandort verwendet, muss PolyBase immer noch den Clusternamen beheben können, wenn die Datenquelle verwendet wird. Sie müssen eine DNS-Weiterleitung aktivieren, um den Namen aufzulösen.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das EXTERNAL DATA SOURCE-Objekt.  
  
##  <a name="examples"></a> Beispiele: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Erstellen einer externen Datenquelle, um auf Hadoop zu verweisen  
Um eine externe Datenquelle zu erstellen, die auf Ihre Hortonworks- oder Cloudera-Hadoop-Cluster verweist, geben Sie den Computernamen oder die IP-Adresse von Hadoop-NameNode und des -Ports an.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Erstellen einer externen Datenquelle, um mit der aktivierten Weitergabe auf Hadoop zu verweisen  
Geben Sie die Option RESOURCE_MANAGER_LOCATION an, um die Berechnung für PolyBase-Abfragen an Hadoop weiterzugeben. Nach der Aktivierung verwendet PolyBase eine kostenorientierte Entscheidung, um zu bestimmen, ob die Abfrageberechnung an Hadoop gegeben, oder alle Daten verschoben werden sollten, um die Abfrage in SQL Server zu verarbeiten.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Erstellen einer externen Datenquelle, um auf Kerberos-gesicherte Hadoop-Software zu verweisen  
Um sicherzustellen, dass das Hadoop-Cluster mit Kerberos gesichert ist, können Sie den Wert der hadoop.security.authentication-Eigenschaft in „Hadoop-Core-site.xml“ überprüfen. Um auf ein Kerberos-gesichertes Hadoop-Cluster zu verweisen, müssen Sie datenbankweit gültige Anmeldeinformationen angeben, die Ihren Kerberos-Benutzernamen und Ihr Kennwort enthalten. Der Hauptschlüssel der Datenbank wird verwendet, um datenbankspezifische Anmeldeinformationen zu verschlüsseln. 
  
```sql  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Erstellen einer externen Datenquelle, um auf Azure Blob Storage zu verweisen
Geben Sie den URI von Azure Blob Storage und datenbankweit gültige Anmeldeinformationen an, die Ihren Azure-Speicherkontoschlüssel enthalten, um eine externe Datenquelle zu erstellen, die auf Ihren Azure Blob Storage-Container verweist.

In diesem Beispiel ist die externe Datenquelle ein Azure Blob Storage-Container namens „dailylogs“ im Azure Storage-Konto „myaccount“. Die externe Datenquelle für Azure Storage steht nur für die Datenübertragung zur Verfügung. Die Prädikatweitergabe wird nicht unterstützt.

Dieses Beispiel zeigt, wie Sie die datenbankweit gültigen Anmeldeinformationen für die Authentifizierung für Azure Storage erstellen. Geben Sie den Azure-Speicherkontoschlüssel in den Anmeldeinformation für die Datenbank an. Geben Sie eine beliebige Zeichenfolge in der datenbankweit gültigen Identität der Anmeldeinformationen an. Sie wird nicht für die Authentifizierung bei Azure Storage verwendet. Anschließend werden die Anmeldeinformationen in der Anweisung verwendet, die eine externe Datenquelle erstellt.

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

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Erstellen einer externen Datenquelle für einen Shardzuordnungs-Manager
Zur Erstellung einer externen Datenquelle, die auf SHARD_MAP_MANAGER verweist, wird der Name des logischen Servers angegeben, der den Shardzuordnungs-Manager in Azure SQL-Datenbank oder einer SQL Server-Datenbank auf einer Azure-VM hostet.

```sql
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
Zur Erstellung einer externen Datenquelle, die auf RDBMS verweist, wird der Name des logischen Servers der Remotedatenbank in Azure SQL-Datenbank angegeben.

```sql
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

## <a name="examples-azure-sql-data-warehouse"></a>Beispiele: Azure SQL Data Warehouse

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. Erstellen einer externen Datenquelle, um auf Azure Data Lake Store zu verweisen
Die Azure Data Lake Store-Konnektivität basiert auf Ihrer ADLS-URI und dem Dienstprinzipal Ihrer Azure Active Directory-Anwendung. Dokumentation zum Erstellen dieser Anwendung finden Sie unter[Data lake store authentication using Active Directory (Authentifizierung in Data Lake Store mit Active Directory)](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
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



## <a name="examples-parallel-data-warehouse"></a>Beispiele: Parallel Data Warehouse

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. Erstellen einer externen Datenquelle, um mit der aktivierten Weitergabe auf Hadoop zu verweisen
Geben Sie die Option JOB_TRACKER_LOCATION an, um die Berechnung für PolyBase-Abfragen an Hadoop weiterzugeben. Nach der Aktivierung verwendet PolyBase eine kostenorientierte Entscheidung, um zu bestimmen, ob die Abfrageberechnung an Hadoop gegeben, oder alle Daten verschoben werden sollten, um die Abfrage in SQL Server zu verarbeiten. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. Erstellen einer externen Datenquelle, um auf Azure Blob Storage zu verweisen
Geben Sie den Azure Blob Storage-URI als Speicherort der externen Datenquelle an, um eine externe Datenquelle zu erstellen, die auf Ihren Azure Blob Storage-Container verweist. Fügen Sie Ihren Azure-Speicherkontoschlüssel zur Authentifizierung zur PDW-Datei „core-site.xml“ hinzu.

In diesem Beispiel ist die externe Datenquelle ein Azure Blob Storage-Container namens „dailylogs“ im Azure Storage-Konto „myaccount“. Die externe Datenquelle für Azure Storage steht nur für die Datenübertragung zur Verfügung. Die Prädikatweitergabe wird nicht unterstützt.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Beispiele: Massenvorgänge   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. Erstellen einer externen Datenquelle für Massenvorgänge, die Daten aus Azure Blob Storage abruft.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Verwenden Sie die folgende Datenquelle für Massenvorgänge mit [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). Die verwendeten Anmeldeinformationen müssen mithilfe von `SHARED ACCESS SIGNATURE` als Identität erstellt werden. Weitere Informationen zu SAS finden Sie unter [Verwenden von Shared Access Signatures (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Sie finden dieses Beispiel unter [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

