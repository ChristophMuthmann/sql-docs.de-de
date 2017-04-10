---
title: "Verwalten von Datensammlungen | Microsoft Docs"
ms.custom: ""
ms.date: "07/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "Datensammlung"
helpviewer_keywords: 
  - "Datensammlung [SQL Server]"
  - "Datensammler [SQL Server], Transact-SQL"
  - "Datensammler [SQL Server], SQL Server Management Studio"
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# Verwalten von Datensammlungen
 Verwenden Sie gespeicherte Prozeduren und Funktionen von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)], um unterschiedliche Aspekte der Datensammlung zu verwalten, beispielsweise das Aktivieren oder Deaktivieren der Datensammlung, das Ändern einer Sammlungssatzkonfiguration oder das Anzeigen von Daten im Verwaltungs-Data Warehouse.  
  
## Verwalten der Datensammlung mithilfe von SSMS  
 Führen Sie die folgenden datensammlerbezogenen Aufgaben aus, indem Sie den Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden:  
  
-   [Konfigurieren des Verwaltungs-Data Warehouses &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Konfigurieren der Eigenschaften eines Datensammlers](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [Aktivieren oder Deaktivieren der Datensammlung](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Starten oder Beenden eines Sammlungssatzes](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Verwenden von SQL Server Profiler zum Erstellen eines Sammlungssatzes für die SQL-Ablaufverfolgung &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use sql server profiler to create a sql trace collection set.md)  
  
-   [Anzeigen von Sammlungssatzprotokollen &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Anzeigen oder Ändern von Sammlungssatz-Zeitplänen &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## Verwalten der Datensammlung mithilfe von Transact-SQL  
 Der Datensammler stellt eine umfassende Sammlung von gespeicherten Prozeduren bereit, die Sie verwenden können, um beliebige datensammlerbezogene Tasks auszuführen. Sie können mit [!INCLUDE[tsql](../../includes/tsql-md.md)] beispielsweise die folgenden Aufgaben ausführen:  
  
-   [Konfigurieren von Parametern für die Datensammlung &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [Aktivieren oder Deaktivieren der Datensammlung](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Starten oder Beenden eines Sammlungssatzes](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Erstellen eines benutzerdefinierten Sammlungssatzes, der einen generischen T-SQL-Abfragesammlertyp verwendet &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create custom collection set - generic t-sql query collector type.md)  
  
-   [Hinzufügen eines Sammelelements zu einem Sammlungssatz &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Außerdem gibt es Funktionen und Sichten, mit denen Konfigurationsdaten für die msdb- und Verwaltungs-Data Warehouse-Datenbanken, Ausführungsprotokolldaten und im Verwaltungs-Data Warehouse gespeicherte Daten abgerufen werden können.  
  
 Sie können die bereitgestellten gespeicherten Prozeduren, Funktionen und Sichten verwenden, um eigene End-to-End-Datensammlungszenarios zu erstellen.  
  
>**WICHTIG!** Im Gegensatz zu regulären gespeicherten Prozeduren verwenden die gespeicherten Prozeduren des Datensammlers genau eingegebene Parameter und unterstützen die automatische Datentypkonvertierung nicht. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um die bereitgestellten Codebeispiele zu erstellen und auszuführen. Weitere Informationen finden Sie unter [Objekt-Explorer](../../ssms/object/object-explorer.md). Alternativ können Sie die Abfrage in einem Editor erstellen und in einer Textdatei mit der Dateinamenerweiterung ".sql" speichern. Sie können die Abfrage mithilfe des Hilfsprogramms **sqlcmd** von der Windows-Eingabeaufforderung aus ausführen. Weitere Informationen finden Sie unter [Verwenden des Hilfsprogramms „sqlcmd“](../../relational-databases/scripting/use-the-sqlcmd-utility.md).  
  
### Gespeicherte Prozeduren und Sichten  
 **Arbeiten mit dem Datensammler**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit dem Datensammler verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|Aktiviert den Datensammler.|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|Deaktiviert den Datensammler.|  
  
 **Arbeiten mit Sammlungssätzen**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit Sammlungssätzen verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|Führt bei Bedarf einen Sammlungssatz aus.|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|Startet einen Sammlungssatz.|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|Beendet einen Sammlungssatz.|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|Erstellt einen Sammlungssatz.|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|Löscht einen Sammlungssatz.|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|Ändert die Konfiguration eines Sammlungssatzes.|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|Lädt Sammlungssatzdaten in das Management Data Warehouse hoch. Dies ist im Prinzip ein bedarfsgesteuerter Upload.|  
  
 **Arbeiten mit Sammelelementen**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit Sammelelementen verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|Erstellt ein Auflistelement.|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|Löscht ein Sammelelement.|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|Aktualisiert ein Sammelelement.|  
  
 **Arbeiten mit Sammlertypen**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit Sammlertypen verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|Erstellt einen Sammlertyp.|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|Aktualisiert einen Sammlertyp.|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|Löscht einen Sammlertyp.|  
  
 **Abrufen von Konfigurationsinformationen**  
  
 In der folgenden Tabelle werden die Sichten beschrieben, die Sie zum Abrufen von Konfigurationsinformationen und Ausführungsprotokolldaten verwenden können.  
  
|Sichtname|Beschreibung|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|Ruft die Datensammlerkonfiguration ab.|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|Ruft Informationen zum Sammelelement ab.|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|Ruft Informationen zum Sammlungssatz ab.|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|Ruft Informationen zum Sammlertyp ab.|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|Ruft Informationen über den Sammlungssatz und die Paketausführung ab.|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|Ruft Informationen über die Taskausführung ab.|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|Ruft Informationen ab, wenn das Ausführungsprotokoll voll ist.|  
  
 **Konfigurieren des Zugriffs auf das Management Date Warehouse**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Konfigurieren des Zugriffs auf das Management Data Warehouse verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|Gibt den in der Verbindungszeichenfolge für das Management Data Warehouse definierten Datenbanknamen an.|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|Gibt die in der Verbindungszeichenfolge für das Management Data Warehouse definierte Instanz an.|  
  
 **Konfigurieren des Management Date Warehouse**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit der Konfiguration des Management Data Warehouse verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|Erstellt einen Auflistungssnapshot im Management Data Warehouse.|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|Aktualisiert die Datenquelle für die Datensammlung.|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|Fügt dem Management Data Warehouse einen Sammlertyp hinzu.|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|Entfernt einen Sammlertyp aus dem Management Data Warehouse.|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|Löscht Daten aus dem Management Data Warehouse.|  
  
 **Arbeiten mit Uploadpaketen**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit Uploadpaketen verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|Konfiguriert die Anzahl von Wiederholungen für Datenuploads.|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|Gibt eine temporäre Speicherung für Daten zwischen Uploadwiederholungen an.|  
  
 **Arbeiten mit dem Ausführungsprotokoll der Datensammlung**  
  
 In der folgenden Tabelle werden die gespeicherten Prozeduren beschrieben, die Sie zum Arbeiten mit dem Ausführungsprotokoll der Datensammlung verwenden können.  
  
|Name der Prozedur|Beschreibung|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|Löscht Einträge des Sammlungssatzes aus dem Ausführungsprotokoll.|  
  
### Funktionen  
 In der folgenden Tabelle werden die Funktionen beschrieben, die Sie zum Abrufen von Ausführungs- und Überwachungsinformationen verwenden können.  
  
|Funktionsname|Beschreibung|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|Ruft [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Ausführungsprotokolldaten für ein bestimmtes Paket ab.|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|Ruft Ausführungsstatistiken für einen Sammlungssatz oder ein Paket ab. Diese Informationen umfassen Fehler, die protokolliert werden.|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|Ruft die Ereignisse ab, die protokolliert werden, wenn der generische SQL-Ablaufverfolgungs-Sammlertyp für das Sammeln von Daten verwendet wird.|  
  
## Siehe auch  
 [Ausführen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [Verwenden von SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  