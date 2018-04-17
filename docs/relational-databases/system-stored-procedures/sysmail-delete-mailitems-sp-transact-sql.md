---
title: Sysmail_delete_mailitems_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d518e72a5ad45147bc9cdf3316c7bd2eba07e7fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmaildeletemailitemssp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht E-Mail-Nachrichten dauerhaft aus den internen Tabellen der Datenbank-E-Mail.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@sent_before=** ] **'***sent_before***'**  
 Löscht E-mails bis zu dem Datum und Uhrzeit als die *Sent_before* Argument. *Sent_before* ist **"DateTime"** und hat den Standardwert NULL. NULL steht für alle Daten.  
  
 [ **@sent_status=** ] **'***sent_status***'**  
 Löscht E-mails mit den vom angegebenen Typ *Sent_status*. *Sent_status* ist **varchar(8)** hat keinen Standardwert. Gültige Einträge sind **gesendet**, **unsent**, **Wiederholung**, und **Fehler**. NULL steht für alle Status.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Datenbank-Mail-Nachrichten und deren Anlagen werden gespeichert, der **Msdb** Datenbank. Nachrichten sollten in regelmäßigen Abständen gelöscht werden, um zu verhindern, dass **Msdb** stärker als erwartet vergrößert und zur Einhaltung des Programms Aufbewahrung Dokument Organisationen. Verwenden der **Sysmail_delete_mailitems_sp** gespeicherte Prozedur, um e-Mail-Nachrichten dauerhaft aus den Datenbank-Mail-Tabellen zu löschen. Mithilfe eines optionalen Arguments können Sie nur ältere E-Mails löschen, indem Sie ein Datum und eine Uhrzeit angeben. E-Mails, die älter sind als dieses Argument, werden gelöscht. Eine andere optionalen Arguments können Sie nur E-mails eines bestimmten Typs, angegeben als Löschen der **Sent_status** Argument. Sie müssen ein Argument angeben, entweder für **@sent_before** oder **@sent_status**. Verwenden Sie zum Löschen aller Nachrichten  **@sent_before = getdate()**.  
  
 Mit den E-Mails werden auch die Anlagen gelöscht, die zu diesen Nachrichten gehören. Durch Löschen der e-Mails löscht keine entsprechenden Einträge in **Sysmail_event_log**. Verwendung [Sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) um Elemente aus dem Protokoll zu löschen.  
  
## <a name="permissions"></a>Berechtigungen  
 Werden standardmäßig, diese gespeicherte Prozedur Berechtigungen für die Ausführung auf Elemente aus der **Sysadmin** -Serverrolle sysadmin und **DatabaseMailUserRole**. Mitglieder der **Sysadmin** -Serverrolle kann diese Prozedur zum Löschen von allen Benutzern gesendete E-mails ausführen. Mitglieder der **DatabaseMailUserRole** können nur von diesem Benutzer gesendeten E-mails löschen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-deleting-all-e-mails"></a>A. Löschen aller E-Mails  
 Im folgenden Beispiel werden alle E-Mails im Datenbank-E-Mail-System gelöscht.  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>B. Löschen der ältesten E-Mails  
 Im folgenden Beispiel werden E-Mail-Nachrichten im Datenbank-E-Mail-Protokoll gelöscht, die vor dem Datum `October 9, 2005` gesendet wurden.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>C. Löschen aller E-Mails eines bestimmten Typs  
 Im folgenden Beispiel werden alle fehlerhaften E-Mails im Datenbank-E-Mail-Protokoll gelöscht.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [Erstellen eines Auftrags des SQL Server-Agents zum Archivieren von Datenbank-E-Mail-Nachrichten und Ereignisprotokollen](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
