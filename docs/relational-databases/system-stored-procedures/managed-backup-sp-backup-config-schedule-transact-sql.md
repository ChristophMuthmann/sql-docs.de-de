---
title: managed_backup.sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
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
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3ba08667f9eebe37cc5493903b714ee1bf0d67f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Konfiguriert die automatisierte oder benutzerdefinierte Planungsoptionen für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> Argumente  
 @database_name  
 Der Name der Datenbank zum Aktivieren der verwalteten Sicherung in einer bestimmten Datenbank. Wenn der Wert NULL oder *, und klicken Sie dann diese verwaltete Sicherung für alle Datenbanken auf dem Server gilt.  
  
 @scheduling_option  
 Geben Sie "System", für die sicherungsplanung System gesteuert. Geben Sie "Benutzerdefiniert" für einen benutzerdefinierten Zeitplan durch die anderen Paratmeters definiert.  
  
 @full_backup_freq_type  
 Der frequenztyp für die verwaltete Sicherung, die auf "Täglich" oder "Wöchentlich" festgelegt werden können.  
  
 @days_of_week  
 Die Wochentage für die Sicherungen beim @full_backup_freq_type ist auf wöchentlich festgelegt. Geben Sie die vollständige Zeichenfolgennamen wie "Montag".  Sie können auch mehr als einen Tag-Namen, die durch Kommas getrennt angeben. Z. B. "Montag, Mittwoch, Freitag".  
  
 @backup_begin_time  
 Die Startzeit für das Zeitfenster für Sicherungen. Sicherungen werden nicht außerhalb des Zeitfensters, die durch eine Kombination von definiert ist gestartet @backup_begin_time und @backup_duration.  
  
 @backup_duration  
 Die Dauer des Fensters Sicherungszeitpunkt aus. Beachten Sie, dass es gibt keine Garantie, dass Sicherungen während des Zeitfensters durch definierten abgeschlossen werden @backup_begin_time und @backup_duration. Sicherungsvorgänge, die in diesem Zeitfenster gestartet wurden, aber überschreiten die Dauer des Fensters werden nicht abgebrochen werden.  
  
 @log_backup_freq  
 Dies bestimmt die Häufigkeit der Sicherungen des Transaktionsprotokolls. Diese Sicherungen Vorkommen in regelmäßigen Abständen anstatt auf dem Zeitplan für die Datenbank gesichert wird. @log_backup_freqkann in Minuten oder Stunden und 0 ist gültig, womit keine protokollsicherungen. Deaktivieren von Sicherungen nur wäre für Datenbanken mit einem einfachen Wiederherstellungsmodell geeignet.  
  
> [!NOTE]  
>  Wenn das Wiederherstellungsmodell von simple in full geändert wird, müssen Sie die Log_backup_freq von 0 auf einen Wert ungleich 0 (null) neu konfigurieren.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in **Db_backupoperator** -Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen und **EXECUTE** Berechtigungen für **Sp_delete_ Backuphistory** gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
