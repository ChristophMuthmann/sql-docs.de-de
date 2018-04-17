---
title: Sysmail_mailattachments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f6a196b41a9fe768023969637841d20d7a843b8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Anlage, die an die Datenbank-E-Mail übermittelt wurde. Verwenden Sie diese Sicht, wenn Sie Informationen zu Datenbank-E-Mail-Anlagen benötigen. Überprüfen Sie alle Use Database Mail verarbeiteten E-mails [Sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|Der Bezeichner für die Anlage.|  
|**mailitem_id**|**int**|Der Bezeichner für das E-Mail-Element, das die Anlage enthält.|  
|**Dateiname**|**nvarchar(520)**|Der Dateiname der Anlage. Wenn **Attach_query_result** 1 und **Query_attachment_filename** NULL ist, Database Mail erstellt einen beliebigen Dateinamen.|  
|**filesize**|**int**|Die Größe der Anlage in Bytes.|  
|**attachment**|**varbinary(max)**|Der Inhalt der Anlage.|  
|**last_mod_date**|**datetime**|Das Datum und die Uhrzeit der letzten Änderung der Zeile.|  
|**last_mod_user**|**sysname**|Der Benutzer, der die Zeile zuletzt geändert hat.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, können Sie diese Sicht verwenden, um die Eigenschaften der Anlagen anzuzeigen.  
  
 In den Systemtabellen gespeicherte Anlagen können bewirken, dass die **Msdb** Datenbank vergrößert werden. Verwendung **Sysmail_delete_mailitems_sp** e-Mail-Elemente und deren zugeordneten Anlagen zu löschen. Weitere Informationen finden Sie unter [erstellen einen SQL Server-Agentauftrag Archiv Datenbank e-Mail-Nachrichten und Ereignisprotokollen](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erteilt die **Sysadmin** -Serverrolle und die **DatabaseMailUserRole** -Datenbankrolle. Beim Ausführen von einem Mitglied der **Sysadmin** festen Serverrolle, die in dieser Ansicht werden alle Anlagen. Für alle anderen Benutzer werden nur die von ihnen übermittelten Anlagen angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
