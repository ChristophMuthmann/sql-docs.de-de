---
title: "Planen der Ausführung von SSIS-Paketen in Azure | Microsoft-Dokumentation"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b8dbc635523b33a480ad887b73d9f395d71c8d
ms.sourcegitcommit: ffa4ce9bd71ecf363604966c20cbd2710d029831
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Planen der Ausführung von SSIS-Paketen in Azure
Sie können die Ausführung von Paketen, die in der SSIS-Katalogdatenbank auf einem Azure SQL-Datenbankserver gespeichert sind, mithilfe einer der folgenden Planungsoptionen planen:
-   [SQL Server-Agent](#agent)
-   [SQL-Datenbank für elastische Aufträge](#elastic)
-   [Die Azure Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren](#sproc)

## <a name="agent"></a> Planen eines Pakets mit SQL Server-Agent

### <a name="prerequisite"></a>Voraussetzung

Bevor Sie SQL Server-Agent lokal zum Planen der Ausführung von auf einem Azure SQL-Datenbankserver gespeicherten Paket verwenden können, müssen Sie SQL-Datenbankserver als Verbindungsserver hinzufügen. Weitere Informationen finden Sie unter [Erstellen von Verbindungsservern](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) und [Linked Servers (Verbindungsserver)](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Erstellen eines Auftrags für SQL Server-Agent

Erstellen Sie mithilfe eines Auftragsschritts einen Auftrag, der die gespeicherten SSIS-Katalog-Prozeduren `[catalog].[create_execution]` und `[catalog].[start_execution]` aufruft, um ein Paket lokal mit SQL Server-Agent zu planen. Weitere Informationen finden Sie unter [SQL Server Agent Jobs for Packages (Aufträge für SQL Server-Agent für Pakete)](../packages/sql-server-agent-jobs-for-packages.md).

1.  Stellen Sie in SQL Server Management Studio eine Verbindung mit der lokalen SQL Server-Datenbank her, auf der Sie den Auftrag erstellen möchten.

2.  Klicken Sie mit der rechten Maustaste auf den Knoten **SQL Server-Agent**, wählen Sie **Neu** aus, und klicken Sie anschließend auf **Auftrag**, damit das Dialogfeld **Neuer Auftrag** geöffnet wird.

3.  Wählen Sie im Dialogfeld **Neuer Auftrag** die Seite **Schritte** aus, und klicken Sie dann auf **Neu**, um das Dialogfeld **Neuer Auftragsschritt** zu öffnen.

4.  Wählen Sie im Dialogfeld **Neuer Auftragsschritt** `SSISDB` als **Datenbank** aus.

5.  Geben Sie im Befehlsfeld ein Transact-SQL-Skript ein, das dem im folgenden Beispiel dargestellten Skript gleicht:

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  Stellen Sie die Konfiguration und die Planung des Auftrags fertig.

## <a name="elastic"></a> Planen eines Pakets mit SQL-Datenbank für elastische Aufträge

Weitere Informationen zu elastischen Aufträgen auf SQL-Datenbank finden Sie unter [Verwalten von Scale Out-Clouddatenbanken](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Erforderliche Komponenten

Sie müssen zunächst folgende Schritte ausführen, damit Sie elastische Aufträge verwenden können, um SSIS-Pakete zu planen, die in der SSIS-Katalogdatenbank auf einem Azure SQL-Datenbankserver gespeichert sind:

1.  Installieren und Konfigurieren Sie die Komponenten für Aufträge für die elastische Datenbank. Informationen dazu finden Sie unter [Installieren von Aufträgen für die elastische Datenbank – Übersicht](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Erstellen Sie datenbankbezogene Anmeldeinformationen, die Aufträge nutzen können, um Befehle an die SSIS-Katalogdatenbank zu senden. Informationen dazu finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) (Erstellen von datenbankbezogenen Anmeldeinformationen (Transact-SQL))](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Erstellen eines elastischen Auftrags

Sie können den Auftrag erstellen, indem Sie ein Transact-SQL-Skript verwenden, das dem im folgenden Beispiel dargestellten Skript gleicht:

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

## <a name="sproc"></a> Planen eines Pakets mithilfe der Azure Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren

> [!IMPORTANT]
> Verwenden Sie die im folgenden Beispiel genannten JSON-Skripts mit Version 1 der Azure Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren.

Führen Sie die folgenden Schritte aus, um ein Paket mithilfe der Azure Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren zu planen:

1.  Erstellen Sie eine Data Factory.

2.  Erstellen Sie einen verknüpften Dienst für die SQL-Datenbank, die SSISDB hostet.

3.  Erstellen Sie ein Ausgabedataset, das die Planung vorantreibt.

4.  Erstellen Sie eine Data Factory-Pipeline, die die Aktivität für gespeicherte SQL Server-Prozeduren verwendet, um das SSIS-Paket auszuführen.

In diesem Abschnitt wird eine Übersicht über diese Schritte bereitgestellt. Ein vollständiges Tutorial für Data Factory kann in diesem Artikel nicht abgedeckt werden. Weitere Informationen finden Sie unter [SQL Server-Aktivität „Gespeicherte Prozedur“](https://docs.microsoft.com/azure/data-factory/data-factory-stored-proc-activity).

Wenn eine geplante Ausführung fehlschlägt, und die ADF-Aktivität für gespeicherte Prozeduren eine Ausführungs-ID für die fehlgeschlagene Ausführung bereitstellt, überprüfen Sie den Ausführungsbericht für diese ID in SSMS im SSIS-Katalog.

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Erstellen eines verknüpften Diensts für die SQL-Datenbank, die SSISDB hostet
Mithilfe des verknüpften Diensts stellt Data Factory eine Verbindung mit SSISDB her.

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

### <a name="create-an-output-dataset"></a>Erstellen eines Ausgabedatasets
Das Ausgabedataset enthält Informationen zur Planung.

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
### <a name="create-a-data-factory-pipeline"></a>Erstellen einer Data Factory-Pipeline
Die Pipeline verwendet die Aktivität für gespeicherte SQL Server-Prozeduren zum Ausführen des SSIS-Pakets.

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

Sie müssen keine neue gespeicherte Prozedur erstellen, um den Transact-SQL-Befehl zu kapseln, der zum Erstellen und Starten der Ausführung eines SSIS-Pakets erforderlich ist. Sie können im folgenden JSON-Beispiel das gesamte Skript als Wert des `stmt`-Parameters bereitstellen. Beispielskript:

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

Um das oben gezeigte SQL-Skript als den Wert des `stmt`-Parameters festzulegen, müssen Sie für gewöhnlich das gesamte Skript in eine einzige Zeile schreiben, so wie im folgenden Beispiel dargestellt. (Der [JSON-Standard](https://json.org/) unterstützt keine Steuerzeichen, einschließlich des Steuerzeichens `\n` für eine Zeile, das in anderen Sprachen verwendet wird, um Zeichen in mehrzeiligen Zeichenfolgen zu trennen.)

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'test', @project_name=N'TestProject', @package_name=N'STestPackage.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Minute",
                    "interval": 15
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2017-12-06T12:00:00Z",
        "end": "2017-12-06T12:30:00Z",
        "isPaused": false,
        "hubName": "test_hub",
        "pipelineMode": "Scheduled"
    }
}
```

Weitere Informationen zum Code in diesem Skript finden Sie unter [Deploy and Execute SSIS Packages using Stored Procedures (Bereitstellen und Ausführen von SSIS-Paketen mithilfe gespeicherter Prozeduren)](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu SQL Server-Agent finden Sie unter [SQL Server Agent Jobs for Packages (Aufträge für SQL Server-Agent für Pakete)](../packages/sql-server-agent-jobs-for-packages.md).

Weitere Informationen zu elastischen Aufträgen auf SQL-Datenbank finden Sie unter [Verwalten von Scale Out-Clouddatenbanken](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).
