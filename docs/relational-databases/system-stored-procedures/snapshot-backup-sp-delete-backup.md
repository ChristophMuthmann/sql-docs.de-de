---
title: Sp_delete_backup (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/03/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1dc3339403f7f39fef0e8fee4e3dbb05ea0a94b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="snapshot-backup---spdeletebackup"></a>Momentaufnahmesicherung - sp_delete_backup
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Löscht alle Momentaufnahmen und die Sicherungsdatei, aus denen einen Momentaufnahme Sicherungssatz aus der angegebenen Datenbank besteht. Diese gespeicherte Systemprozedur ist die einzige empfohlene Methode zum Verwalten von Momentaufnahme-Sicherungssätze. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argumente  
 *[ @backup_url =] Backup_meta_file_url*  
 Die URL der Sicherung gelöscht werden soll, die wodurch alle Momentaufnahmen, aus denen den angegebenen Sicherungssatz einschließlich der Sicherungsdatei selbst gelöscht.  
  
 *[ @db_name =] Datenbankname*  
 Der Name der Datenbank mit der Momentaufnahme gelöscht werden soll. Wenn ein Datenbankname angegeben ist, das System überprüft, ob die Sicherung angegebene URL ist eine Sicherung URL für die angegebene Datenbank und verwendet [Sp_delete_backup_file_snapshot &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) jede Momentaufnahme zu löschen. Wenn kein Datenbankname angegeben ist, wird diese Überprüfung nicht ausgeführt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY DATABASE-Berechtigung oder ALTER-Berechtigung für die angegebene Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fn_db_backup_file_snapshots &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
