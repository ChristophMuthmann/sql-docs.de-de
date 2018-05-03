---
title: Problembehandlung in PolyBase | Microsoft-Dokumentation
ms.custom: ''
ms.date: 8/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f75c81eb0b2cdcf8fdc68ba5ac1a21ba62481eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="polybase-troubleshooting"></a>Problembehandlung in PolyBase
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie die in diesem Thema vorgestellten Methoden, um in PolyBase eine Problembehandlung durchzuführen.  
  
## <a name="catalog-views"></a>Katalogsichten  
 Verwenden Sie die hier aufgelisteten Katalogsichten, um PolyBase-Vorgänge zu verwalten.  
  
|||  
|-|-|  
|Anzeigen|Description|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|Identifiziert externe Tabellen.|  
|[sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|Identifiziert externe Datenquellen.|  
|[sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|Identifiziert externe Dateiformate.|  
  
## <a name="dynamic-management-views"></a>Dynamische Verwaltungssichten  
  
|||  
|-|-|  
|[sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  
  
  PolyBase-Abfragen werden in eine Reihe von Schritten innerhalb von sys.dm_exec_distributed_request_steps unterteilt. Die folgende Tabelle enthält eine Zuordnung zwischen der Bezeichnung des jeweiligen Schritts und der DMV.
  
 |PolyBase-Schritt|Zugeordnete DMV|  
 |-|-| 
 |HadoopJobOperation | sys.dm_exec_external_operations|
 |RandomIdOperation | sys.dm_exec_distributed_request_steps|
 |HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
 |StreamingReturnOperation | sys.dm_exec_dms_workers|
 |OnOperation | sys.dm_exec_distributed_sql_requests |
  
  
## <a name="to-monitor-polybase-queries-using-dmvs"></a>So überwachen Sie PolyBase-Abfragen mit DMVs  
 Sie können PolyBase-Abfragen mithilfe der folgenden DMVs überwachen und eine Problembehandlung durchführen.  
  
1.  **Suchen der am längsten ausgeführten Abfrage**  
  
     Notieren Sie die Ausführungs-ID der am längsten ausgeführten Abfrage.  
  
    ```sql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **Suchen des am längsten ausgeführten Schritts der verteilten Abfrage**  
  
     Verwenden Sie die im vorherigen Schritt notierte Ausführungs-ID. Notieren Sie den Schrittindex des am längsten ausgeführten Schritts.  
  
     Überprüfen Sie „location_type“ für den am längsten ausgeführten Schritt:  
  
    -   Head oder Compute: impliziert einen SQL-Vorgang. Fahren Sie mit Schritt 3a fort.  
  
    -   DMS: impliziert einen Vorgang des PolyBase-Datenverschiebungsdiensts. Fahren Sie mit Schritt 3b fort.  
  
    ```sql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **Suchen des Ausführungsprozesses des am längsten ausgeführten Schritts**  
  
    1.  **Suchen des Ausführungsstatus eines SQL-Schritts**  
  
         Verwenden Sie die in den vorherigen Schritten notierte Ausführungs-ID und den Schrittindex. Verwenden Sie die in den vorherigen Schritten notierte Ausführungs-ID und den Schrittindex.  
  
        ```sql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **Suchen des Ausführungsstatus eines DMS-Schritts**  
  
         Verwenden Sie die in den vorherigen Schritten notierte Ausführungs-ID und den Schrittindex.  
  
        ```sql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **Suchen der Informationen über externe DMS-Vorgänge**  
  
     Verwenden Sie die in den vorherigen Schritten notierte Ausführungs-ID und den Schrittindex.  
  
    ```sql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>So zeigen Sie den PolyBase-Abfrageplan an  
  
1.  Aktivieren Sie in SSMS **Tatsächlichen Ausführungsplan einschließen** (STRG+M), und führen Sie die Abfrage aus.  
  
2.  Klicken Sie auf die Registerkarte **Ausführungsplan** .  
  
     ![PolyBase-Abfrageplan](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase-Abfrageplan")  
  
3.  Klicken Sie mit der rechten Maustaste auf den Operator **Remote Query** (Remoteabfrage), und wählen Sie **Eigenschaften**.  
  
4.  Kopieren Sie den Remote Query-Wert in einen Text-Editor, um den XML-Remote-Abfrageplan anzuzeigen.  Das folgende Beispiel soll dies erläutern:  
  
    ```xml  
  
    <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
           [T1_1].[CustomerKey] AS [CustomerKey],  
           [T1_1].[GeographyKey] AS [GeographyKey],  
           [T1_1].[Speed] AS [Speed],  
           [T1_1].[YearMeasured] AS [YearMeasured]  
    FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                   [T2_1].[CustomerKey] AS [CustomerKey],  
                   [T2_1].[GeographyKey] AS [GeographyKey],  
                   [T2_1].[Speed] AS [Speed],  
                   [T2_1].[YearMeasured] AS [YearMeasured]  
            FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
            WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
    </dsql_query>  
    ```  
  
## <a name="to-monitor-nodes-in-a-polybase-group"></a>So überwachen Sie Knoten in einer PolyBase-Gruppe  
 Nachdem Sie eine Gruppe von Computern als Teil einer PolyBase-Erweiterungsgruppe konfiguriert haben, können Sie den Status der Computer überwachen. Weitere Informationen zum Erstellen einer Erweiterungsgruppe finden Sie unter [PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/polybase-scale-out-groups.md).  
  
1.  Stellen Sie auf dem Hauptknoten einer Gruppe eine Verbindung mit SQL Server her.  
  
2.  Führen Sie die DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) zur Anzeige aller Knoten in der PolyBase-Gruppe aus.  
  
3.  Führen Sie die DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) zur Anzeige des Status aller Knoten in der PolyBase-Gruppe aus.  
  
 ## <a name="known-limitations"></a>Bekannte Einschränkungen
 
 PolyBase weist folgende Einschränkungen auf: 
 - Die maximale Zeilengröße, einschließlich der vollständigen Länge der Spalten mit variabler Länge, darf in SQL Server nicht mehr als 32 KB und in Azure SQL Data Warehouse nicht mehr als 1 MB betragen. 
 - PolyBase unterstützt Hive 0.12 und Datentypen (z.B. Char(), VarChar()) nicht.   
 - Beim Exportieren von Daten aus SQL Server oder Azure SQL Data Warehouse in das Dateiformat ORC können umfangreiche Textspalten wegen Java-Fehlermeldungen aufgrund von nicht ausreichendem Arbeitsspeicher auf höchstens 50 Spalten begrenzt werden. Um das Problem zu umgehen, exportieren Sie nur eine Teilmenge der Spalten.
 - Das Lesen oder Schreiben von verschlüsselten Daten im Ruhezustand in Hadoop ist nicht möglich. Dies schließt HDFS Encrypted Zones oder Transparent Encryption ein.
 - PolyBase kann sich nicht mit einer Hortonworks-Instanz verbinden, wenn KNOX aktiviert ist. 
 - Wenn Sie Hive-Tabellen mit „transactional = true“ verwenden, kann PolyBase nicht auf die Daten im Verzeichnis der Hive-Tabelle zugreifen. 


[PolyBase wird nicht installiert, wenn Sie einem SQL Server 2016-Failovercluster einen Knoten hinzufügen.](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

## <a name="hadoop-name-node-high-availability"></a>Hadoop-Namenknoten mit Hochverfügbarkeit
PolyBase ist heute nicht mehr mit Hochverfügbarkeitsdiensten für Namenknoten wie Zookeeper oder KNOX verbunden. Es gibt jedoch eine bewährte Problemumgehung, die verwendet werden kann, um die Funktionalität bereitzustellen. 

Problemumgehung: Verwenden Sie den DNS-Namen, um Verbindungen zum aktiven Namenknoten umzuleiten. Dafür müssen Sie sicherstellen, dass die externe Datenquelle einen DNS-Namen verwendet, um mit dem Namenknoten zu kommunizieren. Wenn ein Failover des Namenknotens auftritt, müssen Sie die IP-Adresse ändern, die dem DNS-Namen zugeordnet ist, der in der Definition der externen Datenquelle verwendet wird. Dadurch werden alle neuen Verbindungen zum richtigen Namenknoten umgeleitet. Vorhandene Verbindungen schlagen fehl, wenn ein Failover auftritt. Ein „Takt“ kann den aktiven Namenknoten pingen, um diesen Prozess zu automatisieren. Wenn der Takt fehlschlägt, ist anzunehmen, dass ein Failover aufgetreten ist, und ein automatischer Wechsel zur sekundären IP-Adresse kann vorgenommen werden.


## <a name="error-messages-and-possible-solutions"></a>Fehlermeldungen und mögliche Lösungen

Weitere Informationen zum Beheben von Fehlern in externen Tabellen finden Sie auf Murshed Zamans Blog unter [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase setup errors and possible solutions (Setupfehler von PolyBase und mögliche Lösungen)").

## <a name="see-also"></a>Siehe auch
[Troubleshoot PolyBase Kerberos connectivity (Problembehandlung: PolyBase-Kerberos-Konnektivität)](polybase-troubleshoot-connectivity.md)
