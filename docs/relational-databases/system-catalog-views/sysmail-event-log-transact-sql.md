---
title: Sysmail_event_log (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aadbf36412f02f9a785d078d6fa949fcbeabc5f7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Windows- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Meldung, die vom Datenbank-E-Mail-System zurückgegeben wird. (Meldung bezieht sich in diesem Kontext z. B. auf eine Fehlermeldung, nicht auf eine E-Mail-Nachricht.) Konfigurieren der **Protokolliergrad** Parameter mithilfe der **Systemparameter konfigurieren** Dialogfeld Database Mail Konfigurations-Assistenten oder die [Sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)gespeicherte Prozedur, um zu bestimmen, welche Meldungen zurückgegeben werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|Der Bezeichner von Elementen im Protokoll.|  
|**event_type**|**varchar(11)**|Die Art der Mitteilung, die in das Protokoll eingefügt wird. Mögliche Werte sind Fehler, Warnungen, Informationsmeldungen, Erfolgsmeldungen und zusätzliche interne Meldungen.|  
|**log_date**|**datetime**|Das Datum und die Uhrzeit des Protokolleintrags.|  
|**Beschreibung**|**nvarchar(max)**|Der Text der aufgezeichneten Meldung.|  
|**process_id**|**int**|Die Prozess-ID des externen Datenbank-E-Mail-Programms. Diese ändert sich normalerweise mit jedem Start des externen Datenbank-E-Mail-Programms.|  
|**mailitem_id**|**int**|Der Bezeichner des E-Mail-Elements in der E-Mail-Warteschlange. Bezieht sich die Meldung nicht auf ein bestimmtes E-Mail-Element, lautet der Wert NULL.|  
|**account_id**|**int**|Die **account_id** des Kontos, das dem Ereignis zugeordnet ist. Ist die Meldung keinem bestimmten E-Mail-Element zugeordnet, lautet der Wert NULL.|  
|**last_mod_date**|**datetime**|Das Datum und die Uhrzeit der letzten Änderung der Zeile.|  
|**last_mod_user**|**sysname**|Der Benutzer, der die Zeile zuletzt geändert hat. Bei E-Mails handelt es sich dabei um den Absender der E-Mail. Bei Meldungen, die vom externen Datenbank-E-Mail-Programm generiert wurden, handelt es sich um den Benutzerkontext des Programms.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, suchen Sie in der **sysmail_event_log** -Sicht nach Ereignissen, die sich auf E-Mail-Fehler beziehen. Einige Meldungen, z. B. Fehler des externen Datenbank-E-Mail-Programms, sind nicht bestimmten E-Mails zugeordnet. Um nach Fehlern zu suchen, die mit bestimmten E-Mails im Zusammenhang stehen, suchen Sie in der **sysmail_faileditems** -Sicht nach der **mailitem_id** der fehlgeschlagenen E-Mail, und durchsuchen Sie **sysmail_event_log** dann nach Meldungen, die sich auf diese **mailitem_id**beziehen. Wenn **sp_send_dbmail**einen Fehler zurückgibt, wird die E-Mail nicht an das Datenbank-E-Mail-System übermittelt, und der Fehler wird nicht in dieser Sicht angezeigt.  
  
 Falls einzelne Kontoübermittlungsversuche fehlschlagen, bewahrt die Datenbank-E-Mail die Fehlermeldungen während der Wiederholungsversuche auf, bis die Übermittlung des E-Mail-Elements entweder erfolgreich durchgeführt wird oder fehlschlägt. Im Fall eines Erfolgs werden die gesammelten Fehler als separate Warnungen, einschließlich der **account_id**, protokolliert. Dies kann dazu führen, dass Warnungen angezeigt werden, obwohl die E-Mail gesendet wurde. Im Fall eines Übermittlungsfehlers werden alle vorherigen Warnungen als eine Fehlermeldung protokolliert, ohne die **account_id**, da bei allen Konten ein Fehler aufgetreten ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Sie müssen ein Mitglied der festen Serverrolle **sysadmin** oder der Datenbankrolle **DatabaseMailUserRole** sein, um auf diese Sicht zugreifen zu können. Mitglieder von **DatabaseMailUserRole** , die nicht Mitglieder der Rolle **sysadmin** sind, können nur Ereignisse für E-Mails anzeigen, die sie selbst übermitteln.  
  
## <a name="see-also"></a>Siehe auch  
 [Sysmail_faileditems &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Externes Datenbank-E-Mail-Programm](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
