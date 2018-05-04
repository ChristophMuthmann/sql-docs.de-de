---
title: Sysmail_delete_log_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09c9ebf289e6ecc73afeea6a9370bf32696cf0bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmaildeletelogsp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht Ereignisse aus dem Datenbank-E-Mail-Protokoll. Es werden entweder alle Ereignisse im Protokoll gelöscht oder nur die Ereignisse, die einem Datums- oder Typkriterium entsprechen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@logged_before** =] **"***Logged_before***"**  
 Löscht Einträge bis zu dem Datum und der Uhrzeit, die vom *logged_before* -Argument angegeben werden. *logged_before* ist vom Datentyp **datetime** . Der Standardwert ist NULL. NULL steht für alle Daten.  
  
 [ **@event_type** = ] **'***event_type***'**  
 Löscht Protokolleinträge, die den als *event_type*angegebenen Typ aufweisen. *event_type* ist vom Datentyp **varchar(15)** und besitzt keinen Standardwert. Gültige Einträge sind **success**, **warning**, **error**und **informational**. NULL steht für alle Ereignistypen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie die gespeicherte Prozedur **sysmail_delete_log_sp** , um Einträge dauerhaft aus dem Datenbank-E-Mail-Protokoll zu löschen. Mithilfe eines optionalen Arguments können Sie nur ältere Datensätze löschen, indem Sie ein Datum und eine Uhrzeit angeben. Ereignisse, die älter sind als dieses Argument, werden gelöscht. Mithilfe eines optionalen Arguments können Sie nur Ereignisse eines bestimmten Typs löschen. Diese werden als **event_type** -Argument angegeben.  
  
 Durch Löschen der Einträge im Datenbank-E-Mail-Protokoll werden die E-Mail-Einträge nicht aus den Datenbank-E-Mail-Tabellen gelöscht. Verwendung [Sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) -e-Mail aus den Datenbank-Mail-Tabellen zu löschen.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können auf diese Prozedur zugreifen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-deleting-all-events"></a>A. Löschen aller Ereignisse  
 Im folgenden Beispiel werden alle Ereignisse im Datenbank-E-Mail-Protokoll gelöscht.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>B. Löschen der ältesten Ereignisse  
 Im folgenden Beispiel werden Ereignisse im Datenbank-E-Mail-Protokoll gelöscht, die vor dem 9. Oktober 2005 liegen.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. Löschen aller Ereignisse eines bestimmten Typs  
 Im folgenden Beispiel werden Erfolgsmeldungen im Datenbank-E-Mail-Protokoll gelöscht.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [Erstellen eines Auftrags des SQL Server-Agents zum Archivieren von Datenbank-E-Mail-Nachrichten und Ereignisprotokollen](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
