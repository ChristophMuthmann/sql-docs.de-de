---
title: "Planen von SSIS-paketausführung in Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 2130e68d5e29671a2881d8762666cf852ff51259
ms.contentlocale: de-de
ms.lasthandoff: 10/18/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Planen der Ausführung eines SSIS-Pakets in Azure
Sie können die Ausführung von Paketen, die in der Datenbank SSISDB-Katalog auf einer Azure SQL-Datenbankserver gespeichert werden, durch Auswahl einer der folgenden Planungsoptionen planen:
-   [SQL Server-Agent](#agent)
-   [Elastischer SQL-Datenbank-Aufträge](#elastic)
-   [Azure Data Factory SQL Server Stored Procedure-Aktivität](#sproc)

## <a name="agent"></a>Planen eines Pakets mit SQL Server-Agent

### <a name="prerequisite"></a>Voraussetzung

Bevor Sie SQL Server-Agent lokal so planen Sie die Ausführung auf einer Azure SQL-Datenbank-Server gespeicherten Pakete verwenden können, müssen Sie die SQL-Datenbankserver als Verbindungsserver hinzufügen. Weitere Informationen finden Sie unter [Verbindungsserver erstellen](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) und [Verbindungsserver](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Erstellen eines SQL Server-Agent-Auftrags

Planen eines Pakets mit SQL Server-Agent lokal, Erstellen eines Auftrags mit eines Auftragsschritts ausgeführt, die aufruft, SSIS-Katalog gespeicherte Prozeduren `[catalog].[create_execution]` und dann `[catalog].[start_execution]`. Weitere Informationen finden Sie unter [Aufträge des SQL Server-Agents für Pakete](../packages/sql-server-agent-jobs-for-packages.md).

1.  Verbinden Sie in SQL Server Management Studio mit einer lokalen SQL Server-Datenbank auf der Sie den Auftrag erstellen möchten.

2.  Mit der rechten Maustaste auf die **SQL Server-Agent** Knoten **neu**, und wählen Sie dann **Auftrag** So öffnen die **neuer Auftrag** (Dialogfeld).

3.  In der **neuer Auftrag** wählen Sie im Dialogfeld die **Schritte** Seite, und wählen Sie dann **neu** So öffnen die **Neuer Auftragsschritt** (Dialogfeld).

4.  In der **Neuer Auftragsschritt** wählen Sie im Dialogfeld `SSISDB` als die **Datenbank.**

5.  Geben Sie im Befehlfeld ein Transact-SQL-Skript, das ähnlich wie das Skript im folgenden Beispiel gezeigt:

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  Fertig stellen, konfigurieren und planen den Auftrag.

## <a name="elastic"></a>Planen eines Pakets mit elastischen Aufträge des SQL-Datenbank

Weitere Informationen zur elastischen Aufträge für SQL-Datenbank finden Sie unter [Verwalten von horizontaler Cloud-Datenbanken](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie elastischen Aufträge so planen Sie SSIS-Pakete, die in der Datenbank SSISDB-Katalog auf einer Azure SQL-Datenbankserver gespeichert verwenden können, müssen Sie folgende Schritte auszuführen:

1.  Installieren Sie und konfigurieren Sie die Komponenten der elastischen Datenbank Aufträge. Weitere Informationen finden Sie unter [elastischen Datenbank installieren Aufträge (Übersicht)](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Erstellen Sie die datenbankbezogenen Anmeldeinformationen, die Aufträge zum Senden von Befehlen, die SSIS-Katalogdatenbank verwenden können. Weitere Informationen finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Elastische-Auftrag erstellen

Erstellen Sie den Auftrag mithilfe eines Transact-SQL-Skripts, die ähnlich wie das Skript im folgenden Beispiel gezeigt:

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a>Planen eines Pakets mit der Azure Data Factory SQL Server Stored Procedure-Aktivität

> [!IMPORTANT]
> Verwenden Sie die JSON-Skripts im folgenden Beispiel mit der Azure Data Factory Version 1 gespeicherte Prozedur-Aktivität.

Informationen zum Planen eines Pakets mit der Azure Data Factory SQL Server Stored Procedure-Aktivität führen Sie folgende Schritte aus:

1.  Erstellen einer Data Factory an.

2.  Erstellt einen verknüpften Dienst für die SQL-Datenbank, die von SSISDB gehostet.

3.  Erstellen Sie eine ausgabedataset, das die Planung Laufwerke.

4.  Erstellen Sie eine Data Factory-Pipeline, die die SQL Server Stored Procedure-Aktivität zum Ausführen des SSIS-Pakets verwendet.

Dieser Abschnitt enthält einen Überblick über die folgenden Schritte aus. Ein umfassendes Lernprogramm der Data Factory ist nicht Gegenstand dieses Artikels. Weitere Informationen finden Sie unter [SQL Server gespeicherte Prozedur-Aktivität](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity).

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Erstellt einen verknüpften Dienst für die SQL-Datenbank, der als Host SSISDB
Der verknüpfte Dienst kann Data Factory SSISDB herstellen.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>Erstellen Sie eine ausgabedataset
Das ausgabedataset enthält die Planung Informationen.

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>Erstellen Sie eine Data Factory-pipeline
Die Pipeline verwendet die SQL Server Stored Procedure-Aktivität zum Ausführen des SSIS-Pakets.

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

Sie müssen eine neue gespeicherte Prozedur zum kapseln die Transact-SQL-Befehle zum Erstellen und starten die SSIS-paketausführung erstellen. Sie können das gesamte Skript bereitstellen, als Wert für die `stmt` Parameter im vorhergehenden Beispiel JSON. Hier ist ein Beispielskript:

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

Weitere Informationen über den Code in diesem Skript finden Sie unter [bereitstellen und Ausführen von SSIS-Paketen mithilfe von gespeicherten Prozeduren](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu SQL Server-Agent, finden Sie unter [Aufträge des SQL Server-Agents für Pakete](../packages/sql-server-agent-jobs-for-packages.md).

Weitere Informationen zur elastischen Aufträge für SQL-Datenbank finden Sie unter [Verwalten von horizontaler Cloud-Datenbanken](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).

