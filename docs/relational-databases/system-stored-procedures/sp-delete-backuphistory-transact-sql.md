---
title: Sp_delete_backuphistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec51b862cbaf3709fa1eeedf41f2e8167b093184
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletebackuphistory-transact-sql"></a>sp_delete_backuphistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reduziert die Größe der Sicherungs- und Wiederherstellungsverlaufstabellen, indem die Einträge für Sicherungssätze gelöscht werden, die älter sind als das angegebene Datum. Zusätzliche Zeilen werden hinzugefügt, die zum Sichern und Wiederherstellen von Tabellen zur Versionsgeschichte nach jeder Sicherung oder Wiederherstellungsvorgang ausgeführt wird. Deshalb wird empfohlen, dass Sie in regelmäßigen Abständen ausführen **Sp_delete_backuphistory**.  
  
> [!NOTE]  
>  Tabellen zur Versionsgeschichte von Sicherung und Wiederherstellung befinden sich in der **Msdb** Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@oldest_date=** ] **"***Oldest_date***"**  
 Ist das älteste in den Sicherungs- und Wiederherstellungsverlaufstabellen beibehaltene Datum. *Oldest_date* ist **"DateTime"**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_delete_backuphistory** muss ausgeführt werden, aus der **Msdb** Datenbank und wirkt sich auf den folgenden Tabellen:  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 Die physischen Sicherungsdateien werden beibehalten, auch wenn der gesamte Verlauf gelöscht wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** festen Serverrolle "", doch die Berechtigungen können anderen Benutzern erteilt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Einträge in den Sicherungs- und Wiederherstellungsverlaufstabellen gelöscht, die weiter zurückliegen als der 14. Januar 2010, 00:00:00 Uhr.  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_delete_database_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
