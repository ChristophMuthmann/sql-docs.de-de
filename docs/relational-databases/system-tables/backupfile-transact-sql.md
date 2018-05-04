---
title: Backupfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8ea3efdd53390b14e3e934a708bf75682145bde
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Daten- oder Protokolldatei einer Datenbank. In den Spalten wird die Dateikonfiguration zu dem Zeitpunkt beschrieben, an dem die Sicherung erstellt wurde. Und zwar unabhängig davon, ob die Datei in der Sicherung enthalten ist richtet sich nach der **Is_present** Spalte. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Eindeutige ID der Datei, die den Sicherungssatz enthält. Verweise **backupset(backup_set_id)**.|  
|**first_family_number**|**tinyint**|Familiennummer des ersten Mediums, das diese Sicherungsdatei enthält. Kann den Wert NULL haben.|  
|**first_media_number**|**smallint**|Mediennummer des ersten Mediums, das diese Sicherungsdatei enthält. Kann den Wert NULL haben.|  
|**filegroup_name**|**nvarchar(128)**|Name der Dateigruppe, die eine gesicherte Datenbankdatei enthält. Kann den Wert NULL haben.|  
|**page_size**|**int**|Größe der Seite in Bytes.|  
|**file_number**|**numeric(10,0)**|Datei-ID eindeutig innerhalb einer Datenbank (entspricht **Sys. database_files**. **FILE_ID**).|  
|**backed_up_page_count**|**numeric(10,0)**|Anzahl der gesicherten Seiten. Kann den Wert NULL haben.|  
|**file_type**|**char(1)**|Die gesicherte Datei. Folgende Werte sind möglich:<br /><br /> D = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datendatei.<br /><br /> L = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Protokolldatei.<br /><br /> F = Volltextkatalog.<br /><br /> Kann den Wert NULL haben.|  
|**source_file_block_size**|**numeric(10,0)**|Medium, auf dem sich die ursprüngliche Daten- bzw. Protokolldatei befand, als sie gesichert wurde. Kann den Wert NULL haben.|  
|**file_size**|**numeric(20,0)**|Länge der gesicherten Datei in Bytes. Kann den Wert NULL haben.|  
|**logical_name**|**nvarchar(128)**|Logischer Name der Datei, die gesichert wird. Kann den Wert NULL haben.|  
|**physical_drive**|**nvarchar(260)**|Name des physischen Laufwerks oder der physischen Partition. Kann den Wert NULL haben.|  
|**physical_name**|**nvarchar(260)**|Rest des physischen (Betriebssystem-) Dateinamens. Kann den Wert NULL haben.|  
|**state**|**tinyint**|Status der Datei. Folgende Werte sind möglich:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY PENDING<br /><br /> 4 = SUSPECT<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = GELÖSCHT<br /><br /> Hinweis: Der Wert 5 wird übersprungen, sodass diese Werte den Werten für den Datenbankstatus entsprechen.|  
|**state_desc**|**nvarchar(64)**|Beschreibung des Dateistatus. Folgende Werte sind möglich:<br /><br /> ONLINE RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|Protokollfolgenummer, bei der die Datei erstellt wurde.|  
|**drop_lsn**|**numeric(25,0)**|Protokollfolgenummer, bei der die Datei gelöscht wurde. Kann den Wert NULL haben.<br /><br /> Wurde die Datei nicht gelöscht, ist dieser Wert NULL.|  
|**file_guid**|**uniqueidentifier**|Der eindeutige Bezeichner der Datei.|  
|**read_only_lsn**|**numeric(25,0)**|Protokollfolgenummer, bei der die Dateigruppe mit der Datei von Lesen/Schreiben zu Schreibgeschützt geändert wurde (letzte Änderung). Kann den Wert NULL haben.|  
|**read_write_lsn**|**numeric(25,0)**|Protokollfolgenummer, bei der die Dateigruppe mit der Datei von Nur Lesen zu Schreibgeschützt geändert wurde (letzte Änderung). Kann den Wert NULL haben.|  
|**differential_base_lsn**|**numeric(25,0)**|Basis-LSN für differenzielle Sicherungen. Eine differenzielle Sicherung schließt nur Datenblöcke mit einer Protokollsequenz größer als oder gleich **Differential_base_lsn**.<br /><br /> Bei anderen Sicherungstypen ist der Wert NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Bei einer differenziellen Sicherung der eindeutige Bezeichner der letzten Datensicherung, die die Basis für die differenzielle Sicherung der Datei bildet. Ist dieser Wert NULL, wurde die Datei in die differenzielle Sicherung eingeschlossen, aber erst nach der Erstellung der Basis hinzugefügt.<br /><br /> Bei anderen Sicherungstypen ist der Wert NULL.|  
|**backup_size**|**numeric(20,0)**|Größe der Sicherung dieser Datei in Bytes.|  
|**filegroup_guid**|**uniqueidentifier**|ID der Dateigruppe. Verwenden Sie zum Suchen von Dateigruppeninformationen in der Backupfilegroup-Tabelle **Filegroup_guid** mit **Backup_set_id**.|  
|**is_readonly**|**bit**|1 = Die Datei ist schreibgeschützt.|  
|**is_present**|**bit**|1 = Die Datei ist im Sicherungssatz enthalten.|  
  
## <a name="remarks"></a>Hinweise  
 RESTORE VERIFYONLY FROM *Backup_device* WITH LOADHISTORY füllt die Spalten von der **Backupmediaset** Tabelle mit den entsprechenden Werten aus dem mediensatzheader.  
  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
