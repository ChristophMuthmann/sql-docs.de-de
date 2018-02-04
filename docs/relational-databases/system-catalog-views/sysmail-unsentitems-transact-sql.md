---
title: Sysmail_unsentitems (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3a05add3c6c490a0b45e664389e6a49c59959d1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Datenbank-Mail-Nachricht mit der **unsent** oder **Wiederholung** Status. Nachrichten mit dem Status unsent oder retrying werden in der E-Mail-Warteschlange aufbewahrt und können jederzeit gesendet werden. Nachrichten können die **nicht gesendeten** Status aus den folgenden Gründen:  
  
-   Eine neue Nachricht wurde erstellt, und obwohl sich die Nachricht in der E-Mail-Warteschlange befindet, bearbeitet die Datenbank-E-Mail zunächst andere Nachrichten und hat diese Nachricht noch nicht erreicht.  
  
-   Das externe Datenbank-E-Mail-Programm wird nicht ausgeführt, und es werden keine E-Mails gesendet.  
  
 Nachrichten können die **Wiederholung** Status aus den folgenden Gründen:  
  
-   Die Datenbank-E-Mail hat versucht, die E-Mail zu senden, aber der SMTP-Mailserver war nicht erreichbar. Die Datenbank-E-Mail versucht weiterhin, die Nachricht zu senden, wobei sie andere Datenbank-E-Mail-Konten verwendet, die dem Profil, von dem aus die Nachricht gesendet wurde, zugeordnet sind. Wenn keine Konten die e-Mail-Nachrichten senden können, Database Mail wartet die angegebene Zeit für die **Wiederholungsverzögerung für das Konto** Parameter, und versuchen Sie die Nachricht erneut zu senden. Datenbank-Mail verwendet die **Wiederholungsversuche** Parameter, um zu bestimmen, wie oft versucht, die Nachricht zu senden. Aufbewahren von Nachrichten **Wiederholung** Status so lange wie Database Mail versucht, die Nachricht zu senden.  
  
 Verwenden Sie diese Sicht, um anzuzeigen, wie viele Nachrichten darauf warten, gesendet zu werden, und seit wann diese sich in der E-Mail-Warteschlange befinden. Normalerweise ist die Anzahl der **unsent** werden Nachrichten mit niedriger. Führen Sie unter normalen Betriebsbedingungen einen Vergleichstest durch, um eine für Ihre Betriebsabläufe angemessene Anzahl von Nachrichten in der Nachrichtenwarteschlange zu ermitteln.  
  
 Um alle von Database Mail verarbeiteten Nachrichten anzuzeigen, verwenden [Sysmail_allitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Um nur Nachrichten mit dem Status failed anzuzeigen, verwenden [Sysmail_faileditems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Um nur Nachrichten anzuzeigen, die gesendet wurden, verwenden Sie [Sysmail_sentitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Der Bezeichner des E-Mail-Elements in der E-Mail-Warteschlange.|  
|**profile_id**|**int**|Der Bezeichner des Profils, das zum Übermitteln der Nachricht verwendet wurde.|  
|**recipients**|**varchar(max)**|Die E-Mail-Adressen der Nachrichtenempfänger.|  
|**copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten.|  
|**blind_copy_recipients**|**varchar(max)**|Die E-Mail-Adressen derer, die Kopien der Nachricht erhalten, deren Namen jedoch nicht im Nachrichtenkopf angezeigt werden.|  
|**subject**|**nvarchar(510)**|Die Betreffzeile der Nachricht.|  
|**body**|**varchar(max)**|Der Textkörper der Nachricht.|  
|**body_format**|**varchar(20)**|Das Textkörperformat der Nachricht. Die möglichen Werte sind **TEXT** und **HTML**.|  
|**importance**|**varchar(6)**|Die **Wichtigkeit** -Parameter der Nachricht.|  
|**sensitivity**|**varchar(12)**|Die **Empfindlichkeit** -Parameter der Nachricht.|  
|**file_attachments**|**varchar(max)**|Eine durch Semikolons getrennte Liste der Dateinamen, die an die E-Mail-Nachricht angehängt wurden.|  
|**attachment_encoding**|**varchar(20)**|Der Typ der E-Mail-Anlage.|  
|**query**|**varchar(max)**|Die Abfrage, die vom E-Mail-Programm ausgeführt wurde.|  
|**execute_query_database**|**sysname**|Der Datenbankkontext, in dem das E-Mail-Programm die Abfrage ausgeführt hat.|  
|**attach_query_result_as_file**|**bit**|Bei einem Wert von 0 wurden die Abfrageergebnisse hinter dem Inhalt des Textkörpers in den Textkörper der E-Mail-Nachricht eingeschlossen. Bei einem Wert von 1 wurden die Ergebnisse als Anlage zurückgegeben.|  
|**query_result_header**|**bit**|Bei einem Wert von 1 enthielten die Abfrageergebnisse Spaltenheader. Bei einem Wert von 0 enthielten die Abfrageergebnisse keine Spaltenheader.|  
|**query_result_width**|**int**|Die **Query_result_width** -Parameter der Nachricht.|  
|**query_result_separator**|**char(1)**|Das Zeichen, das zum Trennen der Spalten in der Abfrageausgabe verwendet wird.|  
|**exclude_query_output**|**bit**|Die **Exclude_query_output** -Parameter der Nachricht. Weitere Informationen finden Sie unter [Sp_send_dbmail &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|Die **Append_query_error** -Parameter der Nachricht. 0 zeigt an, dass die Datenbank-E-Mail die Nachricht nicht senden soll, wenn die Abfrage einen Fehler enthält.|  
|**send_request_date**|**datetime**|Das Datum und die Uhrzeit, an dem bzw. zu der die Nachricht in der E-Mail-Warteschlange platziert wurde.|  
|**send_request_user**|**sysname**|Der Benutzer, der die Nachricht übermittelt hat. Dies ist der Benutzerkontext der Datenbank-Mail-Prozedur nicht die **aus** Feld der Nachricht.|  
|**sent_account_id**|**int**|Der Bezeichner des Datenbank-E-Mail-Kontos, das zum Senden der Nachricht verwendet wird. Für diese Sicht immer NULL.|  
|**sent_status**|**varchar(8)**|Werden **unsent** Wenn Database Mail nicht, zum Senden der e-Mail versucht hat. Werden **Wiederholung** Wenn Database Mail die Nachricht konnte nicht gesendet, aber ist es erneut zu versuchen.|  
|**sent_date**|**datetime**|Das Datum und die Uhrzeit, an dem bzw. zu der die Datenbank-E-Mail zuletzt versucht hat, die E-Mail zu senden. Hat die Datenbank-E-Mail nicht versucht, die Nachricht zu senden, lautet der Wert NULL.|  
|**last_mod_date**|**datetime**|Das Datum und die Uhrzeit der letzten Änderung der Zeile.|  
|**last_mod_user**|**sysname**|Der Benutzer, der die Zeile zuletzt geändert hat.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, kann diese Sicht Ihnen helfen, die Ursache des Problems zu identifizieren, da sie anzeigt, wie viele Nachrichten darauf warten, gesendet zu werden, und seit wann diese Nachrichten warten. Werden keine Nachrichten gesendet, wird das externe Datenbank-E-Mail-Programm möglicherweise nicht ausgeführt, oder die Datenbank-E-Mail kann aufgrund eines Netzwerkproblems die SMTP-Server nicht erreichen. Wenn viele der ungesendeten Nachrichten dieselbe **Profile_id**, möglicherweise ein Problem mit dem SMTP-Server. Sie sollten eventuell dem Profil zusätzliche Konten hinzufügen. Wenn Nachrichten gesendet werden, aber Nachrichten werden zu viel Zeit in der Warteschlange verbringt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise mehr Ressourcen für das Volume von Nachrichten zu verarbeiten, Sie benötigen.  
  
## <a name="permissions"></a>Berechtigungen  
 Gewährt **Sysadmin** -Serverrolle sysadmin und **DatabaseMailUserRole** -Datenbankrolle. Beim Ausführen von einem Mitglied der **Sysadmin** festen Serverrolle in dieser Ansicht werden alle **unsent** oder **und wiederholen Sie dann** Nachrichten. Alle anderen Benutzer nur finden Sie unter der **unsent** oder **und wiederholen Sie dann** ihnen übermittelten Nachrichten.  
  
  
