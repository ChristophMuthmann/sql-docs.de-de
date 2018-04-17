---
title: Sp_changesubstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f38f61bdb7fe29846b9776e5b9c89dee6c52feda
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Status eines vorhandenen Abonnenten. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**. Wenn *Veröffentlichung* nicht angegeben ist, werden alle Veröffentlichungen betroffen sind.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des Artikels. Er muss für die Veröffentlichung eindeutig sein. *Artikel* ist **Sysname**, hat den Standardwert **%**. Wenn *Artikel* nicht angegeben ist, wird allen Artikeln betroffen sind.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten, dessen Status geändert werden soll. *Abonnenten* ist **Sysname**, hat den Standardwert **%**. Wenn *Abonnenten* nicht angegeben wird, auf den angegebenen Artikel wird der Status für alle Abonnenten geändert.  
  
 [  **@status =**] **"***Status***"**  
 Wird der Abonnementstatus in der **Syssubscriptions** Tabelle. *Status* ist **Sysname**, hat keinen Standardwert und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Aktive**|Der Abonnent ist synchronisiert und empfängt Daten.|  
|**Inaktive**|Es ist ein Eintrag für einen Abonnenten ohne Abonnement vorhanden.|  
|**abonniert**|Der Abonnent fordert Daten an, ist aber noch nicht synchronisiert.|  
  
 [  **@previous_status=**] **"***Previous_status***"**  
 Der vorherige Status für das Abonnement. *Previous_status* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter können Sie alle Abonnements zu ändern, die aktuell diesen Status, und er ermöglicht damit Gruppenfunktionen für eine bestimmte Gruppe von Abonnements verfügen (z. B. Festlegen aller aktiven Abonnements zurück zum **abonniert**).  
  
 [  **@destination_db=**] **"***Destination_db***"**  
 Der Name der Zieldatenbank. *Destination_db* ist **Sysname**, hat den Standardwert **%**.  
  
 [  **@frequency_type=**] *Frequency_type*  
 Die Häufigkeit für die Zeitplanung des Verteilungstasks. *Frequency_type* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_interval=**] *Frequency_interval*  
 Ist der Wert der Häufigkeit festgelegt, die durch Anwenden *Frequency_type*. *Frequency_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_relative_interval=**] *Frequency_relative_interval*  
 Das Datum des Verteilungstasks. Dieser Parameter wird verwendet, wenn *Frequency_type* auf 32 (monatlich, relativ) festgelegt wird. *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
|NULL (Standard)||  
  
 [  **@frequency_recurrence_factor=**] *Frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_subday=**] *Frequency_subday*  
 Die Häufigkeit (in Minuten) für die erneute geplante Ausführung während des definierten Zeitraums. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Zweimal|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (Standard)||  
  
 [  **@frequency_subday_interval=**] *Frequency_subday_interval*  
 Das Intervall für *Frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_time_of_day=**] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Verteilungstask zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_time_of_day=**] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Verteilungstask nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_date=**] *Active_start_date*  
 Das Datum, an dem der Verteilungstask zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_date=**] *Active_end_date*  
 Das Datum, ab dem der Verteilungstask nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@optional_command_line=**] **"***Standardwert***"**  
 Eine optionale Eingabeaufforderung. *Der Standardwert* ist **nvarchar(4000)**, hat den Standardwert NULL.  
  
 [  **@distribution_jobid=**] *Distribution_jobid*  
 Die Auftrags-ID des Verteilungs-Agents auf dem Verteiler für das Abonnement, wenn der Abonnementstatus von inaktiv auf aktiv geändert wird. In anderen Fällen wird sie nicht definiert. Wenn an einem einzelnen Aufruf dieser gespeicherten Prozedur mehrere Verteilungs-Agents beteiligt sind, ist Ergebnis nicht definiert. *Distribution_jobid* ist **binary(16)**, hat den Standardwert NULL.  
  
 [  **@from_auto_sync=**] *From_auto_sync*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor=**] *Ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent=** ] *Remote_agent_activation*  
 > [!NOTE]  
>  Die Aktivierung des Remote-Agents wurde als veraltet markiert und wird nicht mehr unterstützt. Dieser Parameter wird nur zur Aufrechterhaltung der Abwärtskompatibilität von Skripts unterstützt. Festlegen von *Remote_agent_activation* auf einen anderen Wert als **0** wird ein Fehler generiert.  
  
 [  **@offloadserver=** ] **"***Remote_agent_server_name***"**  
 > [!NOTE]  
>  Die Aktivierung des Remote-Agents wurde als veraltet markiert und wird nicht mehr unterstützt. Dieser Parameter wird nur zur Aufrechterhaltung der Abwärtskompatibilität von Skripts unterstützt. Festlegen von *Remote_agent_server_name* auf einen beliebigen Wert ungleich NULL wird ein Fehler generiert.  
  
 [ **@dts_package_name**=] **"***Dts_package_name***"**  
 Gibt den Namen des DTS-Pakets (Data Transformation Services) an. *Dts_package_name* ist ein **Sysname**, hat den Standardwert NULL. Z. B. für ein Paket mit dem Namen **DTSPub_Package** würden Sie angeben `@dts_package_name = N'DTSPub_Package'`.  
  
 [ **@dts_package_password**=] **"***Dts_package_password***"**  
 Gibt das Kennwort für das Paket an. *Dts_package_password* ist **Sysname** hat den Standardwert NULL, der gibt an, dass die Kennworteigenschaft bleiben unverändert.  
  
> [!NOTE]  
>  Ein DTS-Paket muss über ein Kennwort verfügen.  
  
 [ **@dts_package_location**=] *Dts_package_location*  
 Gibt den Paketspeicherort an. *Dts_package_location* ist ein **Int**, hat den Standardwert **0**. Wenn **0**, der Speicherort des Pakets wird auf dem Verteiler. Wenn **1**, der Speicherort des Pakets wird auf dem Abonnenten. Der Speicherort des Pakets kann **Verteiler** oder **Abonnenten**.  
  
 [ **@skipobjectactivation**=] *Skipobjectactivation*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@distribution_job_name=** ] **"***distribution_job _name***"**  
 Der Name des Verteilungsauftrags. *distribution_job _name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@publisher**=] **"***Publisher***"**  
 Gibt einen nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, beim Ändern von Artikeleigenschaften auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changesubstatus** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 **Sp_changesubstatus** ändert den Status des Abonnenten in der **Syssubscriptions** Tabelle mit den geänderten Status. Falls erforderlich, aktualisiert der Artikelstatus in der **Sysarticles** Tabelle, um die Aktivität bzw. Inaktivität anzuzeigen. Falls erforderlich, es das Replikationsflag ein- oder Ausschalten der **Sysobjects** Tabelle der replizierten Tabelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle **Db_owner** festen Datenbankrolle oder der Ersteller des Abonnements kann ausführen **Sp_changesubstatus**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
