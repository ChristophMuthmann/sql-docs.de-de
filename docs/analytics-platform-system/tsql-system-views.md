---
title: Systemsichten – Analytics Platform System Parallel Data Warehouse | Microsoft Docs
description: Systemsichten für analytische Platform System (APS) SQL Server Parallel Data Warehouse (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 35cf9252b43fd4ec52b81cd02fa1e7e777bdbe93
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="system-views-for-analytics-platform-system-parallel-data-warehouse"></a>Systemsichten für Analytics Platform System Parallel Data Warehouse
Systemsichten für analytische Platform System (APS) SQL Server Parallel Data Warehouse (PDW).

## <a name="parallel-data-warehouse-catalog-views"></a>Parallel Data Warehouse-Katalogsichten
* [sys.pdw_column_distribution_properties](http://msdn.microsoft.com/library/mt204022.aspx)
* [sys.pdw_database_mappings](http://msdn.microsoft.com/library/mt203891.aspx)
* [sys.pdw_distributions](http://msdn.microsoft.com/library/mt203892.aspx)
* [sys.pdw_index_mappings](http://msdn.microsoft.com/library/mt203912.aspx)
* [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
* [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
* [sys.pdw_nodes_column_store_dictionaries](http://msdn.microsoft.com/library/mt203902.aspx)
* [sys.pdw_nodes_column_store_row_groups](http://msdn.microsoft.com/library/mt203880.aspx)
* [sys.pdw_nodes_column_store_segments](http://msdn.microsoft.com/library/mt203916.aspx)
* [sys.pdw_nodes_columns](http://msdn.microsoft.com/library/mt203881.aspx)
* [sys.pdw_nodes_indexes](http://msdn.microsoft.com/library/mt203885.aspx)
* [sys.pdw_nodes_partitions](http://msdn.microsoft.com/library/mt203908.aspx)
* [sys.pdw_nodes_pdw_physical_databases](http://msdn.microsoft.com/library/mt203897.aspx)
* [sys.pdw_nodes_tables](http://msdn.microsoft.com/library/mt203886.aspx)
* [sys.pdw_table_distribution_properties](http://msdn.microsoft.com/library/mt203896.aspx)
* [sys.pdw_table_mappings](http://msdn.microsoft.com/library/mt203876.aspx)

## <a name="parallel-data-warehouse-dynamic-management-views-dmvs"></a>Parallel Data Warehouse dynamische Verwaltungssichten (DMVs)
* [sys.dm_pdw_dms_cores](http://msdn.microsoft.com/library/mt203911.aspx)
* [sys.dm_pdw_dms_external_work](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)
* [sys.dm_pdw_dms_workers](http://msdn.microsoft.com/library/mt203878.aspx)
* [sys.dm_pdw_errors](http://msdn.microsoft.com/library/mt203904.aspx)
* [sys.dm_pdw_exec_connections](http://msdn.microsoft.com/library/mt203882.aspx)
* [sys.dm_pdw_exec_requests](http://msdn.microsoft.com/library/mt203887.aspx)
* [sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/library/mt203883.aspx)
* [sys.dm_pdw_hadoop_operations](../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)
* [sys.dm_pdw_lock_waits](http://msdn.microsoft.com/library/mt203901.aspx)
* [sys.dm_pdw_nodes](http://msdn.microsoft.com/library/mt203907.aspx)
* [sys.dm_pdw_nodes_database_encryption_keys](http://msdn.microsoft.com/library/mt203922.aspx)
* [sys.dm_pdw_os_threads](http://msdn.microsoft.com/library/mt203917.aspx)
* [sys.dm_pdw_request_steps](http://msdn.microsoft.com/library/mt203913.aspx)
* [sys.dm_pdw_resource_waits](http://msdn.microsoft.com/library/mt203906.aspx)
* [sys.dm_pdw_sql_requests](http://msdn.microsoft.com/library/mt203889.aspx)
* [sys.dm_pdw_sys_info](http://msdn.microsoft.com/library/mt203900.aspx)
* [sys.dm_pdw_wait_stats](http://msdn.microsoft.com/library/mt203909.aspx)
* [sys.dm_pdw_waits](http://msdn.microsoft.com/library/mt203909.aspx)

## <a name="sql-server-dmvs-applicable-to-parallel-data-warehouse"></a>SQL Server-DMVs für Parallel Data Warehouse
Die folgenden DMVs auf Parallel Data Warehouse anwendbar sind, jedoch muss ausgeführt werden, durch das Herstellen einer Verbindung mit der **master** Datenbank.

* [sys.database_service_objectives](../relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database.md)
* [sys.dm_operation_status](../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)
* [sys.fn_helpcollations()](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)

## <a name="sql-server-catalog-views"></a>SQL Server-Katalogsichten
* [sys.all_columns](http://msdn.microsoft.com/library/ms177522.aspx)
* [sys.all_objects](http://msdn.microsoft.com/library/ms178618.aspx)
* [sys.all_parameters](http://msdn.microsoft.com/library/ms190340.aspx)
* [sys.all_sql_modules](http://msdn.microsoft.com/library/ms184389.aspx)
* [sys.all_views](http://msdn.microsoft.com/library/ms189510.aspx)
* [sys.assemblies](http://msdn.microsoft.com/library/ms189790.aspx)
* [sys.assembly_modules](http://msdn.microsoft.com/library/ms180052.aspx)
* [sys.assembly_types](http://msdn.microsoft.com/library/ms178020.aspx)
* [sys.certificates](http://msdn.microsoft.com/library/ms189774.aspx)
* [sys.check_constraints](http://msdn.microsoft.com/library/ms187388.aspx)
* [sys.columns](http://msdn.microsoft.com/library/ms176106.aspx)
* [sys.computed_columns](http://msdn.microsoft.com/library/ms188744.aspx)
* [sys.credentials](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)
* [sys.data_spaces](http://msdn.microsoft.com/library/ms190289.aspx)
* [sys.database_credentials](../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md)
* [sys.database_files](http://msdn.microsoft.com/library/ms174397.aspx)
* [sys.database_permissions](http://msdn.microsoft.com/library/ms188367.aspx)
* [sys.database_principals](http://msdn.microsoft.com/library/ms187328.aspx)
* [sys.database_role_members](http://msdn.microsoft.com/library/ms189780.aspx)
* [sys.databases](http://msdn.microsoft.com/library/ms178534.aspx)
* [sys.default_constraints](http://msdn.microsoft.com/library/ms173758.aspx)
* [sys.external_data_sources](http://msdn.microsoft.com/library/dn935019.aspx)
* [sys.external_file_formats](http://msdn.microsoft.com/library/dn935025.aspx)
* [sys.external_tables](http://msdn.microsoft.com/library/dn935029.aspx)
* [sys.filegroups](http://msdn.microsoft.com/library/ms187782.aspx)
* [sys.foreign_key_columns](http://msdn.microsoft.com/library/ms186306.aspx)
* [sys.foreign_keys](http://msdn.microsoft.com/library/ms189807.aspx)
* [sys.identity_columns](http://msdn.microsoft.com/library/ms187334.aspx)
* [sys.index_columns](http://msdn.microsoft.com/library/ms175105.aspx)
* [sys.indexes](http://msdn.microsoft.com/library/ms173760.aspx)
* [sys.key_constraints](http://msdn.microsoft.com/library/ms174321.aspx)
* [sys.numbered_procedures](http://msdn.microsoft.com/library/ms179865.aspx)
* [sys.objects](http://msdn.microsoft.com/library/ms190324.aspx)
* [sys.parameters](http://msdn.microsoft.com/library/ms176074.aspx)
* [sys.partition_functions](http://msdn.microsoft.com/library/ms187381.aspx)
* [sys.partition_parameters](http://msdn.microsoft.com/library/ms175054.aspx)
* [sys.partition_range_values](http://msdn.microsoft.com/library/ms187780.aspx)
* [sys.partition_schemes](http://msdn.microsoft.com/library/ms189752.aspx)
* [sys.partitions](http://msdn.microsoft.com/library/ms175012.aspx)
* [sys.procedures](http://msdn.microsoft.com/library/ms188737.aspx)
* [sys.schemas](http://msdn.microsoft.com/library/ms176011.aspx)
* [sys.securable_classes](http://msdn.microsoft.com/library/ms408301.aspx)
* [sys.sql_expression_dependencies](http://msdn.microsoft.com/library/bb677315.aspx)
* [sys.sql_modules](http://msdn.microsoft.com/library/ms175081.aspx)
* [sys.stats](http://msdn.microsoft.com/library/ms177623.aspx)
* [sys.stats_columns](http://msdn.microsoft.com/library/ms187340.aspx)
* [sys.symmetric_keys](../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)
* [sys.synonyms](../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)
* [sys.syscharsets](../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)
* [sys.syscolumns](../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)
* [sys.sysdatabases](../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)
* [sys.syslanguages](../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)
* [sys.sysobjects](../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)
* [sys.sysreferences](../relational-databases/system-compatibility-views/sys-sysreferences-transact-sql.md)
* [sys.system_columns](http://msdn.microsoft.com/library/ms178596.aspx)
* [sys.system_objects](http://msdn.microsoft.com/library/ms173551.aspx)
* [sys.system_parameters](../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)
* [sys.system_sql_modules](http://msdn.microsoft.com/library/ms188034.aspx)
* [sys.system_views](http://msdn.microsoft.com/library/ms187764.aspx)
* [sys.systypes](../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)
* [sys.sysusers](../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)
* [sys.tables](http://msdn.microsoft.com/library/ms187406.aspx)
* [sys.types](http://msdn.microsoft.com/library/ms188021.aspx)
* [sys.views](http://msdn.microsoft.com/library/ms190334.aspx)

## <a name="sql-server-dmvs-available-in-parallel-data-warehouse"></a>SQL Server DMVs in Parallel Data Warehouse zur Verfügung
Parallel Data Warehouse stellt viele der dynamischen Verwaltungssichten (DMVs) von SQL Server. Diese Sichten, wenn in Parallel Data Warehouse abgefragt, die den Status des SQL Server-Datenbanken, die auf die Verteilungen ausgeführt untergeordnet sind.

Jedes dieser DMV verfügt über eine bestimmte Spalte Pdw_node_id aufgerufen. Dies ist der der Bezeichner für die Computeknoten. 

> [!NOTE]
> Um diese Ansicht verwenden, legen Sie "Pdw_nodes_" in den Namen, wie in der folgenden Tabelle gezeigt.
> 
> 

| DMV-Namen in Parallel Data Warehouse | Verknüpfen Sie mit SQL Server T-SQL-Thema |
|:--- |:--- |
| sys.dm_pdw_nodes_db_file_space_usage |[sys.dm_db_file_space_usage](http://msdn.microsoft.com/library/ms174412.aspx) |
| sys.dm_pdw_nodes_db_index_usage_stats |[sys.dm_db_index_usage_stats](http://msdn.microsoft.com/library/ms188755.aspx) |
| sys.dm_pdw_nodes_db_partition_stats |[sys.dm_db_partition_stats](http://msdn.microsoft.com/library/ms187737.aspx) |
| sys.dm_pdw_nodes_db_session_space_usage |[sys.dm_db_session_space_usage](http://msdn.microsoft.com/library/ms187938.aspx) |
| sys.dm_pdw_nodes_db_task_space_usage |[sys.dm_db_task_space_usage](http://msdn.microsoft.com/library/ms190288.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue |[sys.dm_exec_background_job_queue](http://msdn.microsoft.com/library/ms173512.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue_stats |[sys.dm_exec_background_job_queue_stats](http://msdn.microsoft.com/library/ms176059.aspx) |
| sys.dm_pdw_nodes_exec_cached_plans |[sys.dm_exec_cached_plans](http://msdn.microsoft.com/library/ms187404.aspx) |
| sys.dm_pdw_nodes_exec_connections |[sys.dm_exec_connections](http://msdn.microsoft.com/library/ms181509.aspx) |
| sys.dm_pdw_nodes_exec_procedure_stats |[sys.dm_exec_procedure_stats](http://msdn.microsoft.com/library/cc280701.aspx) |
| sys.dm_pdw_nodes_exec_query_memory_grants |[sys.dm_exec_query_memory_grants](http://msdn.microsoft.com/library/ms365393.aspx) |
| sys.dm_pdw_nodes_exec_query_optimizer_info |[sys.dm_exec_query_optimizer_info](http://msdn.microsoft.com/library/ms175002.aspx) |
| sys.dm_pdw_nodes_exec_query_resource_semaphores |[sys.dm_exec_query_resource_semaphores](http://msdn.microsoft.com/library/ms366321.aspx) |
| sys.dm_pdw_nodes_exec_query_stats |[sys.dm_exec_query_stats](http://msdn.microsoft.com/library/ms189741.aspx) |
| sys.dm_pdw_nodes_exec_requests |[sys.dm_exec_requests](http://msdn.microsoft.com/library/ms177648.aspx) |
| sys.dm_pdw_nodes_exec_sessions |[sys.dm_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) |
| sys.dm_pdw_nodes_io_pending_io_requests |[sys.dm_io_pending_io_requests](http://msdn.microsoft.com/library/ms188762.aspx) |
| sys.dm_pdw_nodes_os_buffer_descriptors |[sys.dm_os_buffer_descriptors](http://msdn.microsoft.com/library/ms173442.aspx) |
| sys.dm_pdw_nodes_os_child_instances |[sys.dm_os_child_instances](http://msdn.microsoft.com/library/ms165698.aspx) |
| sys.dm_pdw_nodes_os_cluster_nodes |[sys.dm_os_cluster_nodes](http://msdn.microsoft.com/library/ms187341.aspx) |
| sys.dm_pdw_nodes_os_dispatcher_pools |[sys.dm_os_dispatcher_pools](http://msdn.microsoft.com/library/bb630336.aspx) |
| sys.dm_pdw_nodes_os_dispatchers |Transact-SQL-Dokumentation ist nicht verfügbar. |
| sys.dm_pdw_nodes_os_hosts |[sys.dm_os_hosts](http://msdn.microsoft.com/library/ms187800.aspx) |
| sys.dm_pdw_nodes_os_latch_stats |[sys.dm_os_latch_stats](http://msdn.microsoft.com/library/ms175066.aspx) |
| sys.dm_pdw_nodes_os_memory_brokers |[sys.dm_os_memory_brokers](http://msdn.microsoft.com/library/bb522548.aspx) |
| Sys.dm_pdw_nodes_os_memory_cache_clock_hands |[sys.dm_os_memory_cache_clock_hands](http://msdn.microsoft.com/library/ms173786.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_counters |[sys.dm_os_memory_cache_counters](http://msdn.microsoft.com/library/ms188760.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_entries |[sys.dm_os_memory_cache_entries](http://msdn.microsoft.com/library/ms189488.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_hash_tables |[sys.dm_os_memory_cache_hash_tables](http://msdn.microsoft.com/library/ms182388.aspx) |
| sys.dm_pdw_nodes_os_memory_clerks |[sys.dm_os_memory_clerks](http://msdn.microsoft.com/library/ms175019.aspx) |
| sys.dm_pdw_nodes_os_memory_node_access_stats |Transact-SQL-Dokumentation ist nicht verfügbar. |
| sys.dm_pdw_nodes_os_memory_nodes |[sys.dm_os_memory_nodes](http://msdn.microsoft.com/library/bb510622.aspx) |
| Sys.dm_pdw_nodes_os_memory_objects |[sys.dm_os_memory_objects](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) |
| sys.dm_pdw_nodes_os_memory_pools |[sys.dm_os_memory_pools](http://msdn.microsoft.com/library/ms175022.aspx) |
| sys.dm_pdw_nodes_os_nodes |[sys.dm_os_nodes](http://msdn.microsoft.com/library/bb510628.aspx) |
| sys.dm_pdw_nodes_os_performance_counters |[sys.dm_os_performance_counters](http://msdn.microsoft.com/library/ms187743.aspx) |
| sys.dm_pdw_nodes_os_process_memory |[sys.dm_os_process_memory](http://msdn.microsoft.com/library/bb510747.aspx) |
| sys.dm_pdw_nodes_os_schedulers |[sys.dm_os_schedulers](http://msdn.microsoft.com/library/ms177526.aspx) |
| sys.dm_pdw_nodes_os_spinlock_stats |Transact-SQL-Dokumentation ist nicht verfügbar. |
| sys.dm_pdw_nodes_os_sys_info |[sys.dm_os_sys_info](http://msdn.microsoft.com/library/ms175048.aspx) |
| sys.dm_pdw_nodes_os_sys_memory |[sys.dm_os_memory_nodes](http://msdn.microsoft.com/library/bb510622.aspx) |
| sys.dm_pdw_nodes_os_tasks |[sys.dm_os_tasks](http://msdn.microsoft.com/library/ms174963.aspx) |
| sys.dm_pdw_nodes_os_threads |[sys.dm_os_threads](http://msdn.microsoft.com/library/ms187818.aspx) |
| sys.dm_pdw_nodes_os_virtual_address_dump |[sys.dm_os_virtual_address_dump](../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md) |
| sys.dm_pdw_nodes_os_wait_stats |[sys.dm_os_wait_stats](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
| sys.dm_pdw_nodes_os_waiting_tasks |[sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md) |
| sys.dm_pdw_nodes_os_workers |[sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md) |
| sys.dm_pdw_nodes_resource_governor_resource_pools |[sys.dm_resource_governor_resource_pools](http://msdn.microsoft.com/library/bb934023.aspx) |
| Sys.dm_pdw_nodes_resource_governor_workload_groups |[sys.dm_resource_governor_workload_groups](http://msdn.microsoft.com/library/bb934197.aspx) |
| sys.dm_pdw_nodes_tran_active_snapshot_database_transactions |[sys.dm_tran_active_snapshot_database_transactions](http://msdn.microsoft.com/library/ms180023.aspx) |
| sys.dm_pdw_nodes_tran_active_transactions |[sys.dm_tran_active_transactions](http://msdn.microsoft.com/library/ms174302.aspx) |
| sys.dm_pdw_nodes_tran_commit_table |[sys.dm_tran_commit_table](../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md) |
| sys.dm_pdw_nodes_tran_current_snapshot |[sys.dm_tran_current_snapshot](http://msdn.microsoft.com/library/ms184390.aspx) |
| sys.dm_pdw_nodes_tran_current_transaction |[sys.dm_tran_current_transaction](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md) |
| sys.dm_pdw_nodes_tran_database_transactions |[Sys. dm_tran_database_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) |
| sys.dm_pdw_nodes_tran_locks |[sys.dm_tran_locks](http://msdn.microsoft.com/library/ms190345.aspx) |
| sys.dm_pdw_nodes_tran_session_transactions |[sys.dm_tran_session_transactions](http://msdn.microsoft.com/library/ms188739.aspx) |
| sys.dm_pdw_nodes_tran_top_version_generators |[sys.dm_tran_top_version_generators](http://msdn.microsoft.com/library/ms188778.aspx) |

## <a name="sql-server-2016-polybase-dmvs-available-in-parallel-data-warehouse"></a>SQL Server 2016 PolyBase DMVs verfügbar in Parallel Data Warehouse
* [sys.dm_exec_compute_node_errors](http://msdn.microsoft.com/library/mt146380.aspx)
* [sys.dm_exec_compute_node_status](http://msdn.microsoft.com/library/mt146382.aspx)
* [sys.dm_exec_compute_nodes](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)
* [sys.dm_exec_distributed_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)
* [sys.dm_exec_distributed_requests](http://msdn.microsoft.com/library/mt146385.aspx)
* [sys.dm_exec_distributed_sql_requests](http://msdn.microsoft.com/library/mt146390.aspx)
* [sys.dm_exec_dms_services](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)
* [sys.dm_exec_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)
* [sys.dm_exec_external_operations](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)
* [sys.dm_exec_external_work](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)

## <a name="sql-server-informationschema-views"></a>SQL Server-INFORMATION_SCHEMA-Sichten
* [CHECK_CONSTRAINTS](http://msdn.microsoft.com/library/ms189772.aspx)
* [COLUMNS](http://msdn.microsoft.com/library/ms188348.aspx)
* [PARAMETERS](http://msdn.microsoft.com/library/ms173796.aspx)
* [ROUTINES](../relational-databases/system-information-schema-views/routines-transact-sql.md)
* [SCHEMATA](../relational-databases/system-information-schema-views/schemata-transact-sql.md)
* [TABLES](http://msdn.microsoft.com/library/ms186224.aspx)
* [VIEW_COLUMN_USAGE](../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)
* [VIEW_TABLE_USAGE](../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)
* [VIEWS](http://msdn.microsoft.com/library/ms181381.aspx)

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie unter [T-SQL-Sprachelemente](tsql-language-elements.md) und [T-SQL-Anweisungen](tsql-statements.md).

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse reference overview]: sql-data-warehouse-overview-reference.md

<!--MSDN references-->


<!--Other Web references-->
