---
title: Backupfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
caps.latest.revision: 53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 610967323ce513cf20749e75945e4b6efe74e986
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Dateigruppe in einer Datenbank zum Zeitpunkt der Sicherung. **Backupfilegroup** befindet sich in der **Msdb** Datenbank.  
  
> [!NOTE]  
>  Die **Backupfilegroup** Tabelle wird die dateigruppenkonfiguration der Datenbank, nicht des Sicherungssatzes. Um zu ermitteln, ob eine Datei im Sicherungssatz enthalten ist, verwenden die **Is_present** Spalte die [Backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) Tabelle.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Sicherungssatz, der diese Dateigruppe enthält.|  
|**name**|**sysname**|Name der Dateigruppe.|  
|**filegroup_id**|**int**|ID der Dateigruppe. Sie ist innerhalb der Datenbank eindeutig. Entspricht **Data_space_id** in **"Sys.FileGroups"**.|  
|**filegroup_guid**|**uniqueidentifier**|GUID der Dateigruppe. Kann den Wert NULL haben.|  
|**type**|**char(2)**|Inhaltstyp. Folgende Werte sind möglich:<br /><br /> FG = Zeilendateigruppe<br /><br /> SL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Protokolldateigruppe|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Funktionstyps. Folgende Werte sind möglich:<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|Die Standarddateigruppe, die verwendet wird, wenn keine Dateigruppe in CREATE TABLE oder CREATE INDEX angegeben ist.|  
|**is_readonly**|**bit**|1 = Die Dateigruppe ist schreibgeschützt.|  
|**log_filegroup_guid**|**uniqueidentifier**|Kann den Wert NULL haben.|  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Ein Dateigruppenname kann in unterschiedlichen Datenbanken auftreten. Jede Dateigruppe verfügt jedoch über eine eigene GUID. Aus diesem Grund **(Backup_set_id, Filegroup_guid)** ist ein eindeutiger Schlüssel, die Identifikation einer Dateigruppe in **Backupfilegroup**.  
  
 RESTORE VERIFYONLY FROM *Backup_device* WITH LOADHISTORY füllt die Spalten von der **Backupmediaset** Tabelle mit den entsprechenden Werten aus dem mediensatzheader.  
  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
