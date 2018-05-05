---
title: Sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2c31883e19d688dd7158ece061144ae7d44ccf30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Agentauftrag, der die Momentaufnahme für ein Abonnement einer Veröffentlichung mit einem parametrisierten Zeilenfilter generiert. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication =** ] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 Der Name des Momentaufnahmeauftrags, der geändert wird. *Dynamic_snapshot_jobname*ist **Sysname**, Standardwert N '% s'. Wenn *Dynamic_snapshot_jobid* wird angegeben, muss den Standardwert für *Dynamic_snapshot_jobname*.  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 Die ID des Momentaufnahmeauftrags, der geändert wird. *Dynamic_snapshot_jobid* ist **"uniqueidentifier"**, mit dem Standardwert NULL. Wenn *Dynamic_snapshot_jobname*wird angegeben, muss den Standardwert für *Dynamic_snapshot_jobid*.  
  
 [  **@frequency_type =** ] *Frequency_type*  
 Die Häufigkeit für die Zeitplanung des Agents. *Frequency_type* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Bedarfsgesteuert|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ|  
|**64**|Autostart|  
|**128**|Wiederholt|  
|NULL (Standard)||  
  
 [  **@frequency_interval =** ] *Frequency_interval*  
 Die Tage, an denen der Agent ausgeführt wird. *Frequency_interval* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Sonntag|  
|**2**|Montag|  
|**3**|Dienstag|  
|**4**|Mittwoch|  
|**5**|Donnerstag|  
|**6**|Freitag|  
|**7**|Samstag|  
|**8**|Day|  
|**9**|Wochentage|  
|**10**|Wochenendtage|  
|NULL (Standard)||  
  
 [  **@frequency_subday =** ] *Frequency_subday*  
 Die Häufigkeit für die erneute geplante Ausführung während des definierten Zeitraums. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Zweimal|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (Standard)||  
  
 [  **@frequency_subday_interval =** ] *Frequency_subday_interval*  
 Das Intervall für *Frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_relative_interval =** ] *Frequency_relative_interval*  
 Das Datum, an dem der Merge-Agent ausgeführt wird. Dieser Parameter wird verwendet, wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall). *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
|NULL (Standard)||  
  
 [  **@frequency_recurrence_factor =** ] *Frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert NULL.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Das Datum, an dem der Merge-Agent zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert NULL.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Das Datum, ab dem der Merge-Agent nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_time_of_day =** ] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Merge-Agent zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_time_of_day =** ] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Merge-Agent nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@job_login=** ] **"***Job_login***"**  
 Das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Momentaufnahme-Agent ausgeführt wird, wenn mit einem parametrisierten Zeilenfilter die Momentaufnahme für ein Abonnement generiert wird. *Job_login* ist **nvarchar(257)**, hat den Standardwert NULL.  
  
 [  **@job_password=** ] **"***Job_password***"**  
 Das Kennwort für das Windows-Konto, unter dem der Momentaufnahme-Agent ausgeführt wird, wenn mit einem parametrisierten Zeilenfilter die Momentaufnahme für ein Abonnement generiert wird. *Job_password* ist **nvarchar(257)**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changedynamicsnapshot_job** wird bei der Mergereplikation für Veröffentlichungen mit parametrisierten Zeilenfiltern verwendet.  
  
 Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
