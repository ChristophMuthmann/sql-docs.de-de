---
title: Sysmail_allitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26eb86ab6228c4b9e1439993c94a0cac15f6b880
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailallitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Nachricht, die von der Datenbank-E-Mail verarbeitet wurde. Verwenden Sie diese Sicht, wenn Sie den Status aller Nachrichten anzeigen möchten.  
  
 Um nur Nachrichten mit dem Status failed anzuzeigen, verwenden [Sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Um nur ungesendete Nachrichten anzuzeigen, verwenden [Sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Um nur Nachrichten anzuzeigen, die gesendet wurden, verwenden Sie [Sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Der Bezeichner des E-Mail-Elements in der E-Mail-Warteschlange.|  
|**profile_id**|**int**|Der Bezeichner des Profils, das zum Senden der Nachricht verwendet wurde.|  
|**Empfänger**|**varchar(max)**|Die E-Mail-Adressen der Nachrichtenempfänger.|  
|**copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten.|  
|**blind_copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten, deren Namen jedoch nicht im Nachrichtenkopf angezeigt werden.|  
|**Betreff**|**nvarchar(510)**|Die Betreffzeile der Nachricht.|  
|**body**|**varchar(max)**|Der Textkörper der Nachricht.|  
|**body_format**|**varchar(20)**|Das Textkörperformat der Nachricht. Mögliche Werte sind TEXT und HTML.|  
|**Bedeutung**|**varchar(6)**|Die **Wichtigkeit** -Parameter der Nachricht.|  
|**Sensitivität**|**varchar(12)**|Die **Empfindlichkeit** -Parameter der Nachricht.|  
|**file_attachments**|**varchar(max)**|Eine durch Semikolons getrennte Liste der Dateinamen, die an die E-Mail-Nachricht angehängt wurden.|  
|**attachment_encoding**|**varchar(20)**|Der Typ der E-Mail-Anlage.|  
|**query**|**varchar(max)**|Die Abfrage, die vom E-Mail-Programm ausgeführt wurde.|  
|**execute_query_database**|**sysname**|Der Datenbankkontext, in dem das E-Mail-Programm die Abfrage ausgeführt hat.|  
|**attach_query_result_as_file**|**bit**|Bei einem Wert von 0 wurden die Abfrageergebnisse hinter dem Inhalt des Textkörpers in den Textkörper der E-Mail-Nachricht eingeschlossen. Bei einem Wert von 1 wurden die Ergebnisse als Anlage zurückgegeben.|  
|**query_result_header**|**bit**|Bei einem Wert von 1 enthielten die Abfrageergebnisse Spaltenheader. Bei einem Wert von 0 enthielten die Abfrageergebnisse keine Spaltenheader.|  
|**query_result_width**|**int**|Die **Query_result_width** -Parameter der Nachricht.|  
|**query_result_separator**|**char(1)**|Das Zeichen, das zum Trennen der Spalten in der Abfrageausgabe verwendet wird.|  
|**exclude_query_output**|**bit**|Die **Exclude_query_output** -Parameter der Nachricht. Weitere Informationen finden Sie unter [Sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|Die **Append_query_error** -Parameter der Nachricht. 0 zeigt an, dass die Datenbank-E-Mail die Nachricht nicht senden soll, wenn die Abfrage einen Fehler enthält.|  
|**send_request_date**|**datetime**|Das Datum und die Uhrzeit, an dem bzw. zu der die Nachricht in der E-Mail-Warteschlange platziert wurde.|  
|**send_request_user**|**sysname**|Der Benutzer, der die Nachricht übermittelt hat. Hierbei handelt es sich um den Benutzerkontext der Datenbank-E-Mail-Prozedur, nicht um das Von-Feld der Nachricht.|  
|**sent_account_id**|**int**|Der Bezeichner des Datenbank-E-Mail-Kontos, das zum Senden der Nachricht verwendet wird.|  
|**sent_status**|**varchar(8)**|Der Status der E-Mail. Folgende Werte sind möglich:<br /><br /> **gesendete** -die e-Mail wurde gesendet.<br /><br /> **nicht gesendete** -Database Mail versucht weiterhin, die Nachricht zu senden.<br /><br /> **Erneuter Versuch** -Database Mail die Nachricht konnte nicht gesendet, aber versucht, erneut zu senden.<br /><br /> **Fehler bei** -Database Mail konnte die Nachricht zu senden.|  
|**sent_date**|**datetime**|Das Datum und die Uhrzeit, an dem bzw. zu der die Nachricht gesendet wurde.|  
|**last_mod_date**|**datetime**|Das Datum und die Uhrzeit der letzten Änderung der Zeile.|  
|**last_mod_user**|**sysname**|Der Benutzer, der die Zeile zuletzt geändert hat.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Sysmail_allitems** Sicht, um den Status aller Nachrichten anzuzeigen, die von Database Mail verarbeitet werden. Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, kann diese Sicht Ihnen helfen, die Ursache des Problems zu identifizieren, da sie die Attribute der gesendeten Nachrichten im Vergleich zu den Attributen der ungesendeten Nachrichten anzeigt.  
  
 Die Systemtabellen, die von dieser Sicht verfügbar gemacht werden, enthalten alle Nachrichten, und kann dazu führen, dass die **Msdb** Datenbank vergrößert werden. Löschen Sie alte Nachrichten regelmäßig aus der Sicht, um die Größe der Tabellen zu reduzieren. Weitere Informationen finden Sie unter [erstellen einen SQL Server-Agentauftrag Archiv Datenbank e-Mail-Nachrichten und Ereignisprotokollen](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Gewährt **Sysadmin** -Serverrolle sysadmin und **DatabaseMailUserRole** -Datenbankrolle. Beim Ausführen von einem Mitglied der **Sysadmin** festen Serverrolle, die in dieser Ansicht werden alle Nachrichten. Für alle anderen Benutzer werden nur die von ihnen übermittelten Nachrichten angezeigt.  
  
  
