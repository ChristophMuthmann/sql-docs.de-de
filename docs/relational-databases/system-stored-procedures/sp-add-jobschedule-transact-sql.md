---
title: Sp_add_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3b2680a591628811fb9617077700d05981ece2a2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="spaddjobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Zeitplan für einen Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id=** ] *Job_id*  
 Die ID des Auftrags, dem der Zeitplan hinzugefügt wird. *Job_id* ist **"uniqueidentifier"**, hat keinen Standardwert.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags, dem der Zeitplan hinzugefügt wird. *Job_name* ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@name=** ] **"***Namen***"**  
 Name des Zeitplans. *Namen* ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert.  
  
 [  **@enabled=** ] *Enabled_flag*  
 Gibt den aktuellen Status des Zeitplans an. *Enabled_flag* ist **"tinyint"**, hat den Standardwert **1** (aktiviert). Wenn **0**, der Zeitplan ist nicht aktiviert. Wenn der Zeitplan deaktiviert ist, wird der Auftrag nicht ausgeführt.  
  
 [  **@freq_type=** ] *Frequency_type*  
 Ein Wert, der angibt, wann der Auftrag ausgeführt werden soll. *Frequency_type* ist **Int**, hat den Standardwert **0**, und kann einen der folgenden Werte:  
  
|value|Description|  
|-----------|-----------------|  
|**1**|Einmal|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ zum *Frequency_interval.*|  
|**64**|Ausführen, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst gestartet wird.|  
|**128**|Ausführen, wenn sich der Computer im Leerlauf befindet.|  
  
 [  **@freq_interval=** ] *Frequency_interval*  
 Der Tag, an dem der Auftrag ausgeführt wird. *Frequency_interval* ist **Int**, hat den Standardwert 0 (null) und hängt vom Wert der *Frequency_type* wie in der folgenden Tabelle aufgeführt:  
  
|value|Wirkung|  
|-----------|------------|  
|**1** (einmal)|*Frequency_interval* wird nicht verwendet.|  
|**4** (täglich)|Jede *Frequency_interval* Tage.|  
|**8** (wöchentlich)|*Frequency_interval* kann einen oder mehrere der folgenden (zusammen mit einer logischen OR-Operator):<br /><br /> 1 = Sonntag<br /><br /> 2 = Montag<br /><br /> 4 = Dienstag<br /><br /> 8 = Mittwoch<br /><br /> 16 = Donnerstag<br /><br /> 32 = Freitag<br /><br /> 64 = Samstag|  
|**16** (monatlich)|Auf der *Frequency_interval* Tag des Monats.|  
|**32** (mit relativem Monatsintervall)|*Frequency_interval* ist eines der folgenden:<br /><br /> 1 = Sonntag<br /><br /> 2 = Montag<br /><br /> 3 = Dienstag<br /><br /> 4 = Mittwoch<br /><br /> 5 = Donnerstag<br /><br /> 6 = Freitag<br /><br /> 7 = Samstag<br /><br /> 8 = Tag<br /><br /> 9 = Arbeitstag<br /><br /> 10 = Wochenendtag|  
|**64** (wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst gestartet wird)|*Frequency_interval* wird nicht verwendet.|  
|**128**|*Frequency_interval* wird nicht verwendet.|  
  
 [  **@freq_subday_type=** ] *Frequency_subday_type*  
 Gibt die Einheiten für *Frequency_subday_interval*. *Frequency_subday_type* ist **Int**, hat keinen Standardwert und kann die folgenden Werte sind möglich:  
  
|value|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**0 x 1**|Zum angegebenen Zeitpunkt|  
|**0 x 4**|Minuten|  
|**0 x 8**|Stunden|  
  
 [  **@freq_subday_interval=** ] *Frequency_subday_interval*  
 Anzahl der *Frequency_subday_type* -Perioden zwischen den einzelnen Ausführungen des Auftrags auftreten. *Frequency_subday_interval* ist **Int**, hat den Standardwert 0.  
  
 [  **@freq_relative_interval=** ] *Frequency_relative_interval*  
 Weitere definiert die *Frequency_interval* Wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall).  
  
 *Frequency_relative_interval* ist **Int**, hat keinen Standardwert und kann die folgenden Werte sind möglich:  
  
|value|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 *Frequency_relative_interval* zeigt das Auftreten des Intervalls. Z. B. wenn *Frequency_relative_interval* festgelegt ist, um **2**, *Frequency_type* festgelegt ist, um **32**, und *Frequency_ Intervall* festgelegt ist, um **3**, kommt es, der geplante Auftrag am zweiten Dienstag jedes Monats.  
  
 [  **@freq_recurrence_factor=** ] *Frequency_recurrence_factor*  
 Die Anzahl der Wochen oder Monate zwischen den geplanten Ausführungen des Auftrags. *Frequency_recurrence_factor* wird nur verwendet, wenn *Frequency_type* festgelegt ist, um **8**, **16**, oder **32**. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert 0.  
  
 [  **@active_start_date=** ] *Active_start_date*  
 Das Datum, an dem Ausführung des Auftrags beginnen kann. *Active_start_date* ist **Int**, hat keinen Standardwert. Das Datum wird das Format YYYYMMDD. Wenn *Active_start_date* festgelegt ist, muss das Datum größer oder gleich 19900101 sein.  
  
 Überprüfen Sie nach dem Erstellen des Zeitplans, ob das Startdatum korrekt ist. Weitere Informationen finden Sie im Abschnitt "Planen von Startdaten" in [erstellen und Zuweisen von Zeitplänen zu Aufträgen](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5).  
  
 [  **@active_end_date=** ] *Active_end_date*  
 Das Datum, an dem die Ausführung des Auftrags beendet werden kann. *Active_end_date* ist **Int**, hat keinen Standardwert. Das Datum wird das Format YYYYMMDD.  
  
 [  **@active_start_time=** ] *Active_start_time*  
 Uhrzeit an einem beliebigen Tag zwischen *Active_start_date* und *Active_end_date* auftragsausführung beginnen. *Active_start_time* ist **Int**, hat keinen Standardwert. Die Zeit wird als HHMMSS im 24-Stunden-Format formatiert.  
  
 [  **@active_end_time=***Active_end_time*  
 Uhrzeit an einem beliebigen Tag zwischen *Active_start_date* und *Active_end_date* auf die Ausführung eines Auftrags beendet. *Active_end_time* ist **Int**, hat keinen Standardwert. Die Zeit wird als HHMMSS im 24-Stunden-Format formatiert.  
  
 [  **@schedule_id=***Schedule_id***Ausgabe**  
 Die Zeitplan-ID, die dem Zeitplan zugewiesen wird, wenn er erfolgreich erstellt wird. *Schedule_id* ist eine Ausgabevariable vom Typ **Int**, hat keinen Standardwert.  
  
 [  **@schedule_uid** =] *Schedule_uid***Ausgabe**  
 Ein eindeutiger Bezeichner für den Zeitplan. *Schedule_uid* ist eine Variable des Typs **"uniqueidentifier"**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Hinweise  
 Auftragszeitpläne können jetzt unabhängig von Aufträgen verwaltet werden. Um einen Zeitplan einen Auftrag hinzuzufügen, verwenden Sie **Sp_add_schedule** um den Zeitplan zu erstellen und **Sp_attach_schedule** den Zeitplan einem Auftrag angefügt.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
 
 ## <a name="example"></a>Beispiel
 Im folgende Beispiel weist einen Auftragszeitplan `SaturdayReports` die wird jeden Samstag um 2:00 Uhr ausgeführt.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Zuweisen von Zeitplänen zu Aufträgen](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [Planen eines Auftrags](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [Erstellen Sie einen Zeitplan](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Sp_add_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Sp_update_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Sp_delete_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Sp_help_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
