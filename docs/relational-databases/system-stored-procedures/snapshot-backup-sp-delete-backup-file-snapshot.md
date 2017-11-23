---
title: Sp_delete_backup_file_snapshot (Transact-SQL) | Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cf8bf8484e77c15c951ca548ce00baccfaf5b38
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="snapshot-backup---spdeletebackupfilesnapshot"></a>Momentaufnahmesicherung - sp_delete_backup_file_snapshot
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Löscht eine angegebene Sicherungsdatei-Momentaufnahme aus der angegebenen Datenbank. Verwenden Sie diese gespeicherte Systemprozedur in Verbindung mit der **fn_db_backup_file_snapshots** -Systemfunktion zum Identifizieren und löschen verwaister Sicherungsdatei Momentaufnahmen. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N’<database_name>  
    , [ @snapshot_url = ] N’<snapshot_url>  
```  
  
## <a name="arguments"></a>Argumente  
 *[ @db_name =] Datenbankname*  
 Der Name der Datenbank mit der Momentaufnahme gelöscht, werden als Unicode-Zeichenfolge bereitgestellt werden.  
  
 *[ @snapshot_url =] Snapshot_url*  
 Die URL der Momentaufnahme gelöscht, als eine Unicode-Zeichenfolge bereitgestellt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY DATABASE-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fn_db_backup_file_snapshots &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
