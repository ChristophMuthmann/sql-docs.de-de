---
title: managed_backup.sp_backup_on_demand (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6db602abb8706f94c90b0b583f2468b7a02a251d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Weist [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] an, eine Sicherung der angegebenen Datenbank auszuführen.  
  
 Führen Sie mithilfe dieser gespeicherten Prozedur Ad-hoc-Sicherungen für eine mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] konfigurierte Datenbank aus. Auf diese Weise ist gewährleistet, dass die Sicherungskette nicht unterbrochen wird, Prozesse von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] erkannt werden und die Sicherung im selben Windows Azure-BLOB-Speichercontainer gespeichert wird.  
  
 Nach dem erfolgreichen Abschluss der Sicherung wird der vollständige Sicherungsdateipfad zurückgegeben. Dieser schließt den Namen und den Speicherort der neuen Sicherungsdatei ein, die durch den Sichervorgang erzeugt wird.  
  
 Ein Fehler wird zurückgegeben, wenn [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] im Begriff ist, eine Sicherung eines bestimmten Typs für die angegebene Datenbank auszuführen. In diesem Fall enthält die zurückgegebene Fehlermeldung den vollständigen Sicherungsdateipfad, unter dem die aktuelle Sicherung hochgeladen wird.  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> Argumente  
 @database_name  
 Der Name der Datenbank, für die die Sicherung ausgeführt werden soll. Die @database_name ist **SYSNAME**.  
  
 @type  
 Der Typ der auszuführenden Sicherung: Datenbank- oder Protokollsicherung. Die @type Parameter ist **NVARCHAR(32)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in **Db_backupoperator** -Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen und **EXECUTE** Berechtigungen für **Sp_delete_ Backuphistory**gespeicherte Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Datenbanksicherungsanforderung für die Datenbank "TestDB" ausgegeben. Für diese Datenbank ist [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aktiviert.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 Wählen Sie für jeden Codeausschnitt "tsql" im Sprachattributfeld aus.  
  
  
