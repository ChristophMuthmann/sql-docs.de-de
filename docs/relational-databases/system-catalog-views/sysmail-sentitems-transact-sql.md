---
title: Sysmail_sentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sysmail_sentitems_TSQL
- sysmail_sentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_sentitems database mail view
ms.assetid: 16eb2a44-cebb-4cec-93ac-e2498c39989f
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f65f33de438152843839853d9e53dff9154f7ae7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailsentitems-transact-sql"></a>sysmail_sentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Nachricht, die von der Datenbank-E-Mail gesendet wurde. Verwendung **Sysmail_sentitems** Wenn anzuzeigen, welche Nachrichten erfolgreich gesendet wurden werden sollen.  
  
 Um alle von Database Mail verarbeiteten Nachrichten anzuzeigen, verwenden [Sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Um nur Nachrichten mit dem Status failed anzuzeigen, verwenden [Sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Finden nicht nur gesendet, oder verwenden Sie die Nachrichten, und wiederholen Sie dann [Sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Um e-Mail-Anlagen anzuzeigen, verwenden [Sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Der Bezeichner des E-Mail-Elements in der E-Mail-Warteschlange.|  
|**profile_id**|**int**|Der Bezeichner des Profils, das zum Senden der Nachricht verwendet wurde.|  
|**Empfänger**|**varchar(max)**|Die E-Mail-Adressen der Nachrichtenempfänger.|  
|**copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten.|  
|**blind_copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten, deren Namen jedoch nicht im Nachrichtenkopf angezeigt werden.|  
|**Betreff**|**nvarchar(510)**|Die Betreffzeile der Nachricht.|  
|**body**|**varchar(max)**|Der Textkörper der Nachricht.|  
|**body_format**|**varchar(20)**|Das Textkörperformat der Nachricht. Die möglichen Werte sind **TEXT** und **HTML**.|  
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
|**send_request_user**|**sysname**|Der Benutzer, der die Nachricht gesendet hat. Hierbei handelt es sich um den Benutzerkontext der Datenbank-E-Mail-Prozedur, nicht um das Von-Feld der Nachricht.|  
|**sent_account_id**|**int**|Der Bezeichner des Datenbank-E-Mail-Kontos, das zum Senden der Nachricht verwendet wird.|  
|**sent_status**|**varchar(8)**|Der Status der E-Mail. Immer **gesendet** für diese Ansicht.|  
|**sent_date**|**datetime**|Das Datum und die Uhrzeit, an dem bzw. zu der die Nachricht gesendet wurde.|  
|**last_mod_date**|**datetime**|Das Datum und die Uhrzeit der letzten Änderung der Zeile.|  
|**last_mod_user**|**sysname**|Der Benutzer, der die Zeile zuletzt geändert hat.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, kann diese Sicht Ihnen helfen, die Ursache des Problems zu identifizieren, da sie die Attribute der Nachrichten anzeigt, die erfolgreich gesendet wurden. Die Datenbank-E-Mail markiert Nachrichten als gesendet, wenn sie erfolgreich an einen SMTP-Mailserver übermittelt wurden. E-Mails werden normalerweise innerhalb weniger Minuten empfangen, können sich jedoch aufgrund von Problemen mit dem SMTP-Server verzögern. Die Datenbank-E-Mail markiert die Nachricht als gesendet, wenn sie vom SMTP-Mailserver akzeptiert wurde. E-Mail-Fehler, die auf dem SMTP-Mailserver auftreten, z. B. eine unzustellbare Empfänger-E-Mail-Adresse, werden nicht an die Datenbank-E-Mail zurückgegeben. Diese E-Mails werden als gesendet markiert, obwohl sie nicht übermittelt wurden. Diese Art von Problem müssen Sie auf dem SMTP-Server behandeln. Darüber hinaus sendet der SMTP-Mailserver möglicherweise eine Benachrichtigung, dass die Nachricht nicht zugestellt werden konnte, an die Antwort-E-Mail-Adresse für ein Datenbank-E-Mail-Konto.  
  
## <a name="permissions"></a>Berechtigungen  
 Gewährt **Sysadmin** -Serverrolle sysadmin und **Databasemailuserrole** -Datenbankrolle. Beim Ausführen von einem Mitglied der **Sysadmin** festen Serverrolle, die in dieser Ansicht werden alle gesendeten Nachrichten an. Für alle anderen Benutzer werden nur die von ihnen gesendeten Nachrichten angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Messagingobjekte für Datenbank-E-Mail](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
  
