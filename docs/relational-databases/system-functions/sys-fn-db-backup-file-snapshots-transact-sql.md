---
title: Sys. fn_db_backup_file_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a6a4fc88e778b7384487aab34203341a61ef2ed8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>Sys. fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt die Datenbankdateien zugeordnete Azure-Momentaufnahmen zurück. Wenn die angegebene Datenbank nicht gefunden wird, oder wenn die Datenbankdateien nicht in Microsoft Azure Blob Storage Service gespeichert sind, werden keine Zeilen zurückgegeben. Verwenden von dieser Systemfunktion in Verbindung mit der **sp_delete_backup_file_snapshot** gespeicherte Systemprozedur, um zu identifizieren und löschen verwaiste Sicherungsdatei-Momentaufnahmen. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Datenbankname*  
 Der Name der Datenbank, die abgefragt wird. Wenn der Wert NULL ist, ist diese Funktion im aktuellen Datenbankbereich ausgeführt.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|file_id|**int**|Die Datei-ID für die Datenbank. Lässt keine NULL-Werte zu.|  
|snapshot_time|**nvarchar(260)**|Der Zeitstempel der Momentaufnahme, wie er wird von der REST-API zurückgegeben. Gibt NULL zurück, wenn keine Momentaufnahme vorhanden ist.|  
|snapshot_url|**nvarchar(360)**|Die vollständige URL der dateimomentaufnahme. Gibt NULL, wenn keine Momentaufnahme vorhanden sein.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
