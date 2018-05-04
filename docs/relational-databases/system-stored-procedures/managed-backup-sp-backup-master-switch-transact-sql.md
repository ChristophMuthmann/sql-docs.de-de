---
title: managed_backup.sp_ Backup_master_switch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_ backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fdf26a8bc2f75e4f39074be86571b8b9acc87200
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupsp-backupmasterswitch-transact-sql"></a>managed_backup.sp_ Backup_master_switch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Hält [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] an bzw. setzt den Dienst fort.  
  
 Verwenden Sie diese gespeicherte Prozedur, um [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] vorübergehend anzuhalten und anschließend wieder fortzusetzen. Damit wird sichergestellt, dass alle Konfigurationseinstellungen erhalten bleiben und bei Fortsetzung der Vorgänge beibehalten werden. Beim Anhalten von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] wird die Beibehaltungsdauer nicht erzwungen. Das heißt, es erfolgt keine Überprüfung, um zu bestimmen, ob Dateien aus dem Speicher gelöscht werden müssen, ob Sicherungsdateien beschädigt sind oder ob eine Unterbrechung der Protokollkette vorliegt.  
  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@state = ] { 0 | 1}  
```  
  
##  <a name="Arguments"></a> Argumente  
 @state  
 Legt den Status von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] fest. Die @state Parameter ist **BIT**. Beim Wert 0 werden die Vorgänge angehalten, während der Vorgang beim Wert 1 fortgesetzt wird.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="security"></a>Sicherheit  
 Beschreibt Sicherheitsaspekte in Bezug auf die statement.Include-Berechtigung in einem Unterabschnitt (H3-Überschrift). Erwägen Sie, ggf. weitere Unterabschnitte für Besitzverkettung und Überwachung einzuschließen.  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in **Db_backupoperator** -Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen und **EXECUTE** Berechtigungen für **Sp_delete_ Backuphistory**gespeicherte Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel kann verwendet werden, um [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die Instanz anzuhalten, für die es ausgeführt wird:  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=0;  
Go  
  
```  
  
 Das folgende Beispiel kann verwendet werden, um [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] fortzusetzen.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=1;  
Go  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Managed Backup für Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
