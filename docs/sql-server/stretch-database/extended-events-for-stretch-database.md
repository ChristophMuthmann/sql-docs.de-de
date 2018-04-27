---
title: Erweiterte Ereignisse für Stretch Database | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 70485e74-2e25-4e7e-be6c-9dd1780a42e3
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d43be04bcbd1304ee6934135367ebd2272934442
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="extended-events-for-stretch-database"></a>Erweiterte Ereignisse für Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


Stretch-Datenbank stellt eine Reihe von erweiterten Ereignissen für die Problembehandlung bereit.  
  
Weitere Informationen finden Sie unter [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md). Informationen dazu, wie Sie eine Sitzung für erweiterte Ereignisse zur Problembehandlung starten, finden Sie unter [Erstellen einer Sitzung für erweiterte Ereignisse](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74).  
  
## <a name="list-of-extended-events-for-stretch-database"></a>Liste der erweiterten Ereignisse für Stretch-Datenbank  
  
Ereignisname|Ereignisbeschreibung   
---------|---------  
remote_data_archive_db_ddl|Tritt auf, wenn die T-SQL-Datenbank-DDL für das Stretching von Daten verarbeitet wird.  
remote_data_archive_provision_operation|Tritt am Anfang oder Ende eines Bereitstellungsvorgangs auf.  
remote_data_archive_query_rewrite|Tritt auf, wenn „RelOp_Get“ während des Neuschreibens der Abfrage für die Streckung (Strech) ersetzt wird.  
remote_data_archive_table_ddl|Tritt auf, wenn die T-SQL-Tabellen-DDL für das Stretching von Daten verarbeitet wird.  
remote_data_archive_telemetry|Tritt immer dann auf, wenn ein lokales System ein Telemetrieereignis an die Azure-DB überträgt.  
remote_data_archive_telemetry_rejected|Tritt immer dann auf, wenn ein AzureDB-Stretch-Telemetrieereignis abgelehnt wurde.  
repopulate_stretch_schema_task_queue_complete|Gibt den Abschluss des erneuten Auffüllens der Taskwarteschlange für das Stretchingschema an.  
repopulate_stretch_schema_task_queue_start|Gibt den Start des erneuten Auffüllens der Taskwarteschlange für das Stretchingschema an.  
stretch_codegen_errorlog|Gibt die Ausgabe des Codegenerators an.  
stretch_codegen_start|Gibt den Start der Stretchcodegenerierung an.  
stretch_create_remote_table_start|Gibt den Start der Remotetabellenerstellung an.  
stretch_database_disable_completed|Gibt den Abschluss eines ALTER DATABASE SET REMOTE_DATA_ARCHIVE OFF-Befehls an.  
stretch_database_enable_completed|Gibt den Abschluss eines ALTER DATABASE SET REMOTE_DATA_ARCHIVE ON-Befehls an.  
stretch_database_enable_completed|Gibt den Abschluss einer sp_rda_reauthorize_db-Spezifikationsprozedur an.  
stretch_index_reconciliation_codegen_completed|Gibt den Abschluss der Codegenerierung für den Stretchremoteindex-Vorgang an.  
stretch_index_update_step_completed|Gibt die Dauer eines Aktualisierungsvorgangs für einen Stretchindex an.  
stretch_migration_debug_trace|Die Debugablaufverfolgung von Stretchmigrationsaktionen.  
stretch_migration_dequeue_migration|Ereignis, das ausgelöst wird, wenn ein Task zur Stretchmigration für eine Datenbank aus der Warteschlange entfernt wird.  
stretch_migration_queue_migration|Verschiebt ein Paket in die Warteschlange, um die Migration der Datenbank und des Objekts zu starten.  
stretch_migration_requeue_migration|Ereignis, das ausgelöst wird, wenn ein Taskpaket zur Stretchmigration erneut der Warteschlange hinzugefügt wird.  
stretch_migration_start_migration|Starten der Migration der Datenbank und des Objekts.  
stretch_migration_start_unmigration|Starten des Vorgangs zum Rückgängigmachen der Migration der Datenbank und des Objekts.  
stretch_remote_column_execution_completed|Gibt den Abschluss einer Remoteausführung für den generierten Code für eine Stretchingspalte an.  
stretch_remote_column_reconciliation_codegen_completed|Gibt den Abschluss der Codegenerierung für die Abstimmung der Stretchremotespalten an.  
stretch_remote_index_execution_completed|Gibt den Abschluss der Remoteausführung für den generierten Code für einen Stretchindex an  
stretch_schema_queue_task|Gibt an, wann ein Paket zum Verarbeiten einer Schemaaufgabe für die Datenbank oder das Objekt in die Warteschlange gestellt wird.  
stretch_schema_script_execution_completed|Gibt den Abschluss der Stretchingskriptausführung während der Verarbeitung eines Stretchingschematasks an.  
stretch_schema_script_execution_skipped|Gibt das Überspringen der Stretchingskriptausführung während der Verarbeitung eines Stretchingschematasks an.  
stretch_schema_script_execution_start|Gibt den Start der Stretchingskriptausführung während der Verarbeitung eines Stretchingschematasks an.  
stretch_schema_task_failed|Gibt einen Fehler bei einer Stretchingschemafunktion während des Stretchingschematasks an.  
stretch_schema_task_skipped|Gibt an, dass der Stretchingschematask während der Stretchingschemafunktion übersprungen wird.  
stretch_schema_task_start|Gibt den Start der Stretchingschemafunktion während des Stretchingschematasks an.  
stretch_schema_task_succeeded|Gibt den erfolgreichen Abschluss einer Stretchingschemafunktion während des Stretchingschematasks an.  
stretch_sp_migration_get_batch_id|Ruft „sp_stretch_get_batch_id“ auf.  
stretch_sync_metadata_start|Gibt den Start von Metadatenprüfungen während des Migrationstasks an.  
stretch_table_codegen_completed|Gibt den Abschluss der Codegenerierung für eine Stretchingtabelle an.  
stretch_table_complete_data_reconciliation|Gibt den Abschluss der Datenabstimmung der Datenbank und des Objekts an.  
stretch_table_data_reconciliation_event|Gibt den Abschluss der Datenabstimmung eines Zeilenbatches an.  
stretch_table_data_reconciliation_results_event|Gibt einen Fehler oder den Abschluss einer erfolgreichen Datenabstimmung einer Reihe von Zeilenbatches an.  
stretch_table_hinted_admin_delete_event|Gibt die Ausführung eines Stretch-DML-Löschvorgangs an, der einen Administratorhinweis verwendet.  
stretch_table_hinted_admin_update_event|Gibt die Ausführung eines Stretch-DML-Aktualisierungsvorgangs an, der einen Administratorhinweis verwendet.  
stretch_table_provisioning_step_completed|Gibt die Dauer der Bereitstellung einer Stretchingtabelle an.  
stretch_table_query_error|Gibt einen Fehler an, der während des Neuschreibens der Abfrage für die Streckung ausgelöst wurde.  
stretch_table_remote_creation_completed|Gibt den Abschluss der Remoteausführung für den generierten Code für eine Tabelle an, für die ein Stretching durchgeführt wurde.  
stretch_table_row_migration_event|Gibt den Abschluss der Migration für einen Zeilenbatch an.  
stretch_table_row_migration_results_event|Gibt einen Fehler oder den Abschluss einer erfolgreichen Migration einer Reihe von Zeilenbatches an.  
stretch_table_row_unmigration_event|Gibt den Abschluss der Migrationsaufhebung für einen Zeilenbatch an.  
stretch_table_row_unmigration_results_event|Gibt einen Fehler oder den Abschluss einer erfolgreich rückgängig gemachten Migration einer Reihe von Zeilenbatches an.  
stretch_table_start_data_reconciliation|Startet die Datenabstimmung der Datenbank und des Objekts.  
stretch_table_unprovision_completed|Gibt den Abschluss der Entfernung von lokalen Ressourcen für eine Tabelle an, deren Streckung aufgehoben wurde.  
stretch_table_validation_error|Gibt den Abschluss der Überprüfung für eine Tabelle an, wenn der Benutzer Stretch aktiviert.  
stretch_unprovision_table_start|Gibt den Start der Aufhebung der Bereitstellung der Stretchingtabelle an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwalten und Problembehandlung von Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  

