---
title: Sys. dm_db_xtp_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 507a42fbb349ce9dca17d3221fe3b001dffe4bbe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtpcheckpointfiles-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Zeigt Informationen zu Prüfpunktdateien, einschließlich Dateigröße, physischem Speicherort und der Transaktions-ID an.  
  
> **Hinweis:** für den aktuellen Prüfpunkt, der nicht die Spalte State s geschlossen hat`ys.dm_db_xtp_checkpoint_files` werden für neue Dateien UNDER CONSTRUCTION. Ein Prüfpunkt wird automatisch geschlossen, wenn ausreichend Wachstumsrate des Transaktionsprotokolls seit dem letzten Prüfpunkt vorhanden ist oder wenn Sie ausgeben der `CHECKPOINT` Befehl ([PRÜFPUNKT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)).  
  
 Eine Speicheroptimierte Dateigruppe verwendet intern nur Anhängen-Dateien um eingefügten und gelöschten Zeilen für speicherinterne Tabellen zu speichern. Es gibt zwei Typen von Dateien. Eine Datendatei enthält eingefügte Zeilen an, während eine Änderungsdatei Verweise auf gelöschte Zeilen enthält. 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] unterscheidet sich deutlich von neueren Versionen und wird unten im Thema zur erläutert [SQL Server 2014](#bkmk_2014).  
  
 Weitere Informationen finden Sie unter [erstellen und Verwalten von Speicher für arbeitsspeicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und höher  
 Die folgende Tabelle beschreibt die Spalten für `sys.dm_db_xtp_checkpoint_files`ab **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|Die ID des Containers (in sys.database_files als Datei vom Typ FILESTREAM dargestellt), dem die Daten- oder Änderungsdatei angehört. Joins mit File_id in [Sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|Die GUID des Containers, der den Stamm, Daten- oder Änderungsdatei angehört. Joins mit File_guid in der Sys. database_files-Tabelle.|  
|checkpoint_file_id|**uniqueidentifier**|Die GUID der Prüfpunktdatei.|  
|relative_file_path|**nvarchar(256)**|Pfad der Datei relativ zum Container, der er zugeordnet ist.|  
|file_type|**smallint**|-1 für frei<br /><br /> 0 für die Datendatei.<br /><br /> 1 für Änderungsdatei.<br /><br /> 2 für Stammdatei<br /><br /> 3 für große Datendatei|  
|file_type_desc|**nvarchar(60)**|FREE - All-Dateien, die als frei verwaltet stehen für die Zuordnung zur Verfügung. Kostenlose Dateien können vom System Größe sich je nach Voraussichtlicher Anforderungen variieren. Die maximale Größe beträgt 1GB.<br /><br /> Daten per Push – Datendateien enthalten Zeilen, die in speicheroptimierten Tabellen eingefügt wurden.<br /><br /> DELTA - Änderungsdateien enthalten Verweise auf die Zeilen in den Datendateien, die gelöscht wurden.<br /><br /> ROOT - Stammdateien enthalten Systemmetadaten für Speicheroptimierte und systemintern kompilierten Objekte.<br /><br /> UMFANGREICHE Daten – von großen Datendateien enthalten Werte eingefügt ((n)varchar(max) und 'varbinary(max)' Spalten sowie die spaltensegmente, die Teil des columnstore-Indizes für Speicheroptimierte Tabellen sind.|  
|internal_storage_slot|**int**|Der Index der Datei im internen Speicherarray. NULL für den Stamm oder für den Status als 1.|  
|checkpoint_pair_file_id|**uniqueidentifier**|Datei der entsprechenden Daten- oder ÄNDERUNGSDATEI. NULL für den Stamm.|  
|file_size_in_bytes|**bigint**|Die Größe der Datei auf dem Datenträger.|  
|file_size_used_in_bytes|**bigint**|Bei Prüfpunktdateipaaren, die noch mit Daten aufgefüllt werden, wird diese Spalte nach dem nächsten Prüfpunkt aktualisiert.|  
|logical_row_count|**bigint**|Für Daten, die Anzahl der eingefügten Zeilen.<br /><br /> Delta Anzahl der Zeilen nach Berücksichtigung tabellenlöschung gelöscht.<br /><br /> Für den Stamm NULL zurück.|  
|state|**smallint**|0 – PRECREATED<br /><br /> 1 – IN BEARBEITUNG<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 8 – AUF PROTOKOLLKÜRZUNG WARTENDE|  
|state_desc|**nvarchar(60)**|PRECREATED – sind eine Reihe von Prüfpunktdateien vorab zugeordnete minimieren oder eliminieren Wartezeiten bei der Zuordnung neuer Dateien während der Ausführung von Transaktionen. Diese vorab erstellten Dateien können variieren, je nach den geschätzten Teil der arbeitsauslastung die Größe, aber keine Daten enthalten. Dies ist eine speichermehraufwand in Datenbanken mit einer MEMORY_OPTIMIZED_DATA-Dateigruppe.<br /><br /> UNDER CONSTRUCTION – diese Prüfpunktdateien sind noch nicht abgeschlossen, was bedeutet, dass sie basierend auf der Protokolldatensätze, die von der Datenbank erzeugte aufgefüllt werden und sind noch nicht Teil eines Prüfpunkts.<br /><br /> ACTIVE – diese eingefügten/gelöschten Zeilen aus den vorherigen geschlossenen Prüfpunkten enthalten. Sie enthalten den Inhalt der Tabellen, die Bereich in den Speicher eingelesen wird, vor dem Anwenden des aktiven Teils des Transaktionsprotokolls beim Neustart Datenbank. Wir erwarten, dass diese Größe dieser Dateien Prüfpunkt sein, dass der in-Memory-Größe der speicheroptimierten Tabellen verwendet werden, vorausgesetzt die Merge-Vorgang etwa 2 X mit der transaktionsarbeitslast Schritt halten kann.<br /><br /> MERGE TARGET – das Ziel des Merge-Operationen - diese Prüfpunktdateien speichern Sie die konsolidierten Datenzeilen aus der Quelldateien, die von der Zusammenführungsrichtlinie identifiziert wurden. Nachdem die Zusammenführung installiert wurde, befinden sich die MERGE TARGET-Übergänge im Status ACTIVE.<br /><br /> Auf PROTOKOLLKÜRZUNG WARTENDE – sobald die Zusammenführung installiert wurde und das Ziel-CFP ZUSAMMENFÜHREN Teil dauerhaften Prüfpunkt, den Übergang Merge Source Prüfpunkt Dateien in diesen Zustand. Dateien in diesem Status werden für einen korrekten Betrieb der Datenbank mit einer speicheroptimierten Tabelle benötigt.  Dies gilt beispielsweise für die Wiederherstellung von einem dauerhaften Prüfpunkt, um zu einem früheren Zustand zurückzukehren.|  
|lower_bound_tsn|**bigint**|Untere Grenze der Transaktion in der Datei; NULL, wenn Sie nicht im Status (1, 3).|  
|upper_bound_tsn|**bigint**|Obergrenze für die Transaktion in der Datei; NULL, wenn Sie nicht im Status (1, 3).|  
|begin_checkpoint_id|**bigint**|Die ID des Prüfpunkts beginnen.|  
|end_checkpoint_id|**bigint**|Die ID des Prüfpunkts End.|  
|last_updated_checkpoint_id|**bigint**|Die ID des letzten Prüfpunkts, der die Datei aktualisiert.|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = &GT; UNENCRTPTED<br /><br /> 1 = &GT; VERSCHLÜSSELT MIT SCHLÜSSEL 1<br /><br /> 2 = &GT; MIT SCHLÜSSEL 2 VERSCHLÜSSELT. Dies gilt nur für aktive Dateien.|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 Die folgende Tabelle beschreibt die Spalten für `sys.dm_db_xtp_checkpoint_files`, für **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|Die ID des Containers (in sys.database_files als Datei vom Typ FILESTREAM dargestellt), dem die Daten- oder Änderungsdatei angehört. Joins mit File_id in [Sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|Die GUID des Containers, dem die Daten- oder Änderungsdatei angehört.|  
|checkpoint_file_id|**GUID**|Die ID der Daten- oder Änderungsdatei.|  
|relative_file_path|**nvarchar(256)**|Der Pfad zu der Daten- oder Änderungsdatei relativ zum Speicherort des Containers.|  
|file_type|**tinyint**|0 für die Datendatei.<br /><br /> 1 für die Änderungsdatei.<br /><br /> NULL, wenn die Zustandsspalte auf 7 festgelegt ist.|  
|file_type_desc|**nvarchar(60)**|Dateityp: DATA_FILE, DELTA_FILE oder NULL, wenn die Zustandsspalte auf 7 festgelegt ist.|  
|internal_storage_slot|**int**|Der Index der Datei im internen Speicherarray. NULL, wenn die Zustandsspalte auf 2 oder 3 festgelegt ist.|  
|checkpoint_pair_file_id|**uniqueidentifier**|Die entsprechende Daten- oder Änderungsdatei.|  
|file_size_in_bytes|**bigint**|Die Größe der Datei, die verwendet wird. NULL, wenn die Zustandsspalte auf 5, 6 oder 7 festgelegt ist.|  
|file_size_used_in_bytes|**bigint**|Die verwendete Größe der betreffenden Datei. NULL, wenn die Zustandsspalte auf 5, 6 oder 7 festgelegt ist.<br /><br /> Bei Prüfpunktdateipaaren, die noch mit Daten aufgefüllt werden, wird diese Spalte nach dem nächsten Prüfpunkt aktualisiert.|  
|inserted_row_count|**bigint**|Die Anzahl der Zeilen in der Datendatei.|  
|deleted_row_count|**bigint**|Die Anzahl der gelöschten Zeilen in der Änderungsdatei.|  
|drop_table_deleted_row_count|**bigint**|Die Anzahl der Zeilen in den Datendateien, auf die sich die Tabellenlöschung auswirkt. Gilt für Datendateien, wenn die Zustandsspalte gleich 1 ist.<br /><br /> Zeigt die Anzahl der aus gelöschten Tabellen gelöschten Zeilen an. Statistiken drop_table_deleted_row_count werden kompiliert, nachdem die Arbeitsspeicher-Garbage Collection für die Zeilen aus gelöschten Tabellen abgeschlossen und ein Prüfpunkt erstellt wurde. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu starten, bevor die Statistiken zu gelöschten Tabellen in dieser Spalte angezeigt werden, werden sie im Rahmen der Wiederherstellung aktualisiert. Bei der Wiederherstellung werden keine Zeilen aus gelöschten Tabellen geladen. Statistiken zu gelöschten Tabellen werden während der Ladephase kompiliert und in dieser Spalte wiedergegeben, sobald die Wiederherstellung abgeschlossen ist.|  
|state|**int**|0 – PRECREATED<br /><br /> 1 – UNDER CONSTRUCTION<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 4 – MERGED SOURCE<br /><br /> 5 – REQUIRED FOR BACKUP/HA<br /><br /> 6 – IN TRANSITION TO TOMBSTONE<br /><br /> 7 – TOMBSTONE|  
|state_desc|**nvarchar(60)**|PRECREATED – Eine kleine Menge von Daten- und Änderungsdateipaaren, auch bekannt als Prüfpunktdateipaare (Checkpoint File Pairs, CFPs), wird dauerhaft vorab zugeordnet, um während der Ausführung von Transaktionen Wartezeiten bei der Zuordnung neuer Dateien zu minimieren oder zu vermeiden. Dabei handelt es sich um Datendateien mit der vollständigen Größe von 128 MB und 8 MB große Änderungsdateien, die jedoch keine Daten enthalten. Die Anzahl der CFPs wird aus der Anzahl von logischen Prozessoren oder Zeitplanungsmodulen (einer pro Kern, kein Höchstwert) berechnet und beträgt mindestens 8. Dies ist ein fester Speichermehraufwand in Datenbanken mit speicheroptimierten Tabellen.<br /><br /> UNDER CONSTRUCTION – Eine Anzahl von CFPs, in denen neu eingefügte Datenzeilen und Datenzeilen, die seit dem letzten Prüfpunkt möglicherweise gelöscht wurden, gespeichert werden.<br /><br /> ACTIVE – Diese enthalten die eingefügten und gelöschten Zeilen aus den vorherigen geschlossenen Prüfpunkten. Diese CFPs enthalten alle erforderlichen eingefügten und gelöschten Zeilen, bevor der aktive Teil des Transaktionsprotokolls beim Neustart der Datenbank angewendet wird. Diese CFPs sind etwa doppelt so groß wie die In-Memory-Größe speicheroptimierter Tabellen, vorausgesetzt, die Zusammenführung hält mit der Transaktionsarbeitsauslastung mit.<br /><br /> MERGE TARGET – Das CFP speichert die konsolidierten Datenzeilen aus den CFPs, die von der Zusammenführungsrichtlinie identifiziert wurden. Nachdem die Zusammenführung installiert wurde, befinden sich die MERGE TARGET-Übergänge im Status ACTIVE.<br /><br /> MERGED SOURCE – Nachdem der Zusammenführungsvorgang installiert wurde, sind die Quell-CFPs als MERGED SOURCE gekennzeichnet. Beachten Sie, dass die Auswertung der Zusammenführungsrichtlinie mehrere Zusammenführungen identifizieren kann, ein CFP jedoch nur an einem Zusammenführungsvorgang beteiligt sein darf.<br /><br /> REQUIRED FOR BACKUP/HA – Sobald die Zusammenführung installiert ist und das MERGE TARGET-CFP einem dauerhaften Prüfpunkt angehört, gehen die CFPs der Zusammenführungsquelle in diesen Zustand über. CFPs in diesem Zustand werden benötigt, um die nahtlose Verwendung der Datenbank mit der speicheroptimierten Tabelle sicherzustellen.  Dies gilt beispielsweise für die Wiederherstellung von einem dauerhaften Prüfpunkt, um zu einem früheren Zustand zurückzukehren. Ein CFP kann für die Garbage Collection gekennzeichnet werden, sobald der Protokollkürzungspunkt hinter dem Transaktionsbereich liegt.<br /><br /> IN TRANSITION TO TOMBSTONE – Diese CFPs werden nicht vom In-Memory-OLTP-Modul benötigt und können durch die Garbage Collection bereinigt werden. Dieser Status gibt an, dass diese CFPs warten, bis sie vom Hintergrundthread in den nächsten Zustand (d. h. TOMBSTONE) versetzt werden.<br /><br /> TOMBSTONE – Diese CFPs warten, bis sie vom FILESTREAM-Garbage Collector durch eine Garbage Collection bereinigt werden. ([Sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|Die untere Grenze für Transaktionen, die in der Datei enthalten sind. NULL, wenn die Zustandsspalte ungleich 2, 3 oder 4 ist.|  
|upper_bound_tsn|**bigint**|Die obere Grenze für Transaktionen, die in der Datei enthalten sind. NULL, wenn die Zustandsspalte ungleich 2, 3 oder 4 ist.|  
|last_backup_page_count|**int**|Die logische Seitenanzahl, die bei der letzten Sicherung bestimmt wird. Diese gilt, wenn die Zustandsspalte auf 2, 3, 4 oder 5 festgelegt ist. NULL, wenn die Seitenanzahl unbekannt ist.|  
|delta_watermark_tsn|**int**|Die Transaktion des letzten Prüfpunkts, von dem in diese Änderungsdatei geschrieben wurde. Dies ist das Wasserzeichen der Änderungsdatei.|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|Die Wiederherstellungs-Protokollfolgenummer des letzten Prüfpunkts, von dem die Datei noch benötigt wird.|  
|tombstone_operation_lsn|**nvarchar(23)**|Die Datei wird gelöscht, sobald tombstone_operation_lsn hinter der Protokollfolgenummer des Protokollkürzungspunkts zurückfällt.|  
|logical_deletion_log_block_id|**bigint**|Gilt nur für Zustand 5.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW DATABASE STATE`-Berechtigung auf dem Server.  
  
## <a name="use-cases"></a>Einsatzgebiete  
 Sie können den Speicher von In-Memory OLTP verwendet wird wie folgt schätzen:  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
Um eine Aufschlüsselung der speicherauslastung von Status und dem Dateityp entspricht, führen Sie die folgende Abfrage finden Sie unter:
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
