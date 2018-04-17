---
title: Sys. master_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.master_files
- master_files_TSQL
- sys.master_files_TSQL
- master_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_files catalog view
ms.assetid: 803b22f2-0016-436b-a561-ce6f023d6b6a
caps.latest.revision: 56
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d56dde664eba328a74db87d7c3ce22aef014ff6e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmasterfiles-transact-sql"></a>sys.master_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Enthält eine Zeile pro Datei einer Datenbank, wie Sie in der master-Datenbank gespeichert. Dies ist eine einzelne, systemweite Sicht.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID der Datenbank, auf die sich diese Datei bezieht Die Masterdatabase_id ist immer 1.|  
|file_id|**int**|ID der Datei in der Datenbank Die ID der primären Datei ist immer 1.|  
|file_guid|**uniqueidentifier**|Der eindeutige Bezeichner der Datei.<br /><br /> NULL = Die Datenbank wurde von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert.|  
|Typ|**tinyint**|Dateityp:<br /><br /> 0 = Zeilen<br /><br /> 1 = Protokoll<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = Volltext (Volltextkataloge vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]; Volltextkataloge, die auf [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher aktualisiert oder darin erstellt wurden, geben den Dateityp 0 zurück.)|  
|type_desc|**nvarchar(60)**|Beschreibung des Dateityps:<br /><br /> ROWS<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT (Volltextkataloge vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].)|  
|data_space_id|**int**|Die ID des Datenspeicherplatzes, zu dem diese Datei gehört. Der Datenspeicherplatz ist eine Dateigruppe.<br /><br /> 0 = Protokolldateien|  
|name|**sysname**|Logischer Name der Datei in der Datenbank|  
|physical_name|**nvarchar(260)**|Betriebssystem-Dateiname|  
|state|**tinyint**|Dateistatus:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|state_desc|**nvarchar(60)**|Beschreibung des Dateistatus:<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> Weitere Informationen finden Sie im Abschnitt [Dateistatus](../../relational-databases/databases/file-states.md).|  
|size|**int**|Die aktuelle Dateigröße in Seiten mit einer Größe von 8 KB. Größe stellt bei einer Datenbank-Momentaufnahme den maximalen Speicherplatz, den die Momentaufnahme für die Datei verwenden kann.<br /><br /> Hinweis: Dieses Feld wird als 0 (null) für FILESTREAM-Container aufgefüllt. Abfrage der *Sys. database_files* -Katalogsicht für die tatsächliche Größe der FILESTREAM-Container.|  
|max_size|**int**|Maximale Dateigröße in Seiten mit einer Größe von 8 KB:<br /><br /> 0 = Keine Vergrößerung zulässig.<br /><br /> -1 = Datei wird vergrößert, bis der Datenträger voll ist.<br /><br /> 268435456 = Protokolldatei wird bis zu einer maximalen Größe von 2 TB vergrößert.<br /><br /> Hinweis: Datenbanken, die mit einer unbegrenzten Protokolldateigröße aktualisiert werden werden-1 für die maximale Größe der Protokolldatei gemeldet.|  
|growth|**int**|0 = Die Datei hat eine feste Größe und wird nicht vergrößert.<br /><br /> >0 = Die Datei wird automatisch vergrößert.<br /><br /> Wenn Is_percent_growth = 0, Schrittweite für die Vergrößerung in Schritten von 8-KB-Seiten, gerundet auf die nächsten 64 KB ist<br /><br /> Wenn Is_percent_growth = 1, Vergrößerung als ganzzahliger Prozentwert.|  
|is_media_read_onlyF|**bit**|1 = Die Datei befindet sich auf einem schreibgeschützten Medium.<br /><br /> 0 = Die Datei befindet sich auf einem Medium mit Lese-/Schreibzugriff.|  
|is_read_only|**bit**|1 = Die Datei ist als schreibgeschützt gekennzeichnet.<br /><br /> 0 = Die Datei ermöglicht den Lese-/Schreibzugriff.|  
|is_sparse|**bit**|1 = Die Datei ist eine Datei mit geringer Dichte.<br /><br /> 0 = Die Datei ist keine Datei mit geringer Dichte.<br /><br /> Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md).|  
|is_percent_growth|**bit**|1 = Die Vergrößerung der Datei erfolgt prozentual.<br /><br /> 0 = Absolute Vergrößerung in Seiten.|  
|is_name_reserved|**bit**|1 = Der gelöschte Dateiname kann wiederverwendet werden. Eine Sicherung des Protokolls muss vorgenommen werden, bevor Sie der Namen (Name oder Physical_name) für einen neuen Dateinamen wiederverwendet werden kann.<br /><br /> 0 = Der Dateiname kann nicht wiederverwendet werden.|  
|create_lsn|**numeric(25,0)**|Protokollfolgenummer (LSN, Log Sequence Number), bei der die Datei erstellt wurde|  
|drop_lsn|**numeric(25,0)**|LSN, bei der die Datei gelöscht wurde|  
|read_only_lsn|**numeric(25,0)**|LSN, bei der die Dateigruppe mit der Datei von Lesen/Schreiben in Schreibgeschützt geändert wurde (letzte Änderung)|  
|read_write_lsn|**numeric(25,0)**|LSN, bei der die Dateigruppe mit der Datei von Schreibgeschützt in Lesen/Schreiben geändert wurde (letzte Änderung)|  
|differential_base_lsn|**numeric(25,0)**|Die Basis für differenzielle Sicherungen. Datenblöcke, die nach dieser LSN geändert wurden, werden in eine differenzielle Sicherung eingeschlossen.|  
|differential_base_guid|**uniqueidentifier**|Der eindeutige Bezeichner der Basissicherung, auf der eine differenzielle Sicherung basiert.|  
|differential_base_time|**datetime**|Zeit, die differential_base_lsn entspricht.|  
|redo_start_lsn|**numeric(25,0)**|LSN, bei der das nächste Rollforward beginnen muss.<br /><br /> Ist NULL, es sei denn, Zustand = RESTORING oder Status = RECOVERY_PENDING.|  
|redo_start_fork_guid|**uniqueidentifier**|Eindeutiger Bezeichner des Verzweigungspunkts. Die First_fork_guid der nächsten protokollsicherung wiederhergestellt, muss dieser Wert übereinstimmen. Dies stellt den aktuellen Status des Containers dar.|  
|redo_target_lsn|**numeric(25,0)**|Die LSN, bei der das Onlinerollforward für diese Datei beendet werden kann.<br /><br /> Ist NULL, es sei denn, Zustand = RESTORING oder Status = RECOVERY_PENDING.|  
|redo_target_fork_guid|**uniqueidentifier**|Die Wiederherstellungsverzweigung, bei der der Container wiederhergestellt werden kann. Mit Redo_target_lsn gekoppelt.|  
|backup_lsn|**numeric(25,0)**|Die LSN der letzten Datensicherung oder differenziellen Sicherung der Datei.|  
|credential_id|**int**|Die `credential_id` aus `sys.credentials` zum Speichern der das verwendet. Beispielsweise, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf virtuellen Azure-Computer und die Datenbank ausgeführt wird im Azure-Blob-Speicher gespeichert werden, Anmeldeinformationen mit den Anmeldeinformationen für den Zugriff auf den Speicherort konfiguriert ist.|  
  
> [!NOTE]  
>  Löschen oder große Indizes neu erstellen oder löschen oder Abschneiden große Tabellen die [!INCLUDE[ssDE](../../includes/ssde-md.md)] orientiert sich die tatsächlichen aufgehobenen seitenzuordnungen sowie die zugehörigen sperren, bis nach dem Commit der Transaktion. Bei verzögerten Löschvorgängen wird der zugeordnete Speicherplatz nicht sofort freigegeben. Aus diesem Grund können von Sys. master_files sofort nach dem Löschen oder Abschneiden eines großen Objekts zurückgegebenen Werte nicht den tatsächlich verfügbaren Speicherplatz wider.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Anzeigen der entsprechenden Zeile ist mindestens eine der Berechtigungen CREATE DATABASE, ALTER ANY DATABASE oder VIEW ANY DEFINITION erforderlich.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbanken und Dateikatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Dateistatus](../../relational-databases/databases/file-states.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
