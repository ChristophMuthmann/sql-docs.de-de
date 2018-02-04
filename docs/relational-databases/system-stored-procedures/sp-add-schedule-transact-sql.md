---
title: Sp_add_schedule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: df04306671a8e2a0f0ded0fc7482e56955102a83
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spaddschedule-transact-sql"></a>sp_add_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt einen Zeitplan an, der von einer beliebigen Anzahl von Aufträgen verwendet werden kann.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]  
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 Der Name des Zeitplans. *Schedule_name*ist **Sysname**, hat keinen Standardwert.  
  
 [ **@enabled =** ] *enabled*  
 Gibt den aktuellen Status des Zeitplans an. *aktiviert*ist **"tinyint"**, hat den Standardwert **1** (aktiviert). Wenn **0**, der Zeitplan ist nicht aktiviert. Wenn der Zeitplan nicht aktiviert ist, werden über diesen Zeitplan keine Aufträge ausgeführt.  
  
 [ **@freq_type =** ] *freq_type*  
 Ein Wert, der angibt, wann ein Auftrag ausgeführt werden soll. *Freq_type*ist **Int**, hat den Standardwert **0**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ zum *Freq_interval*|  
|**64**|Ausführen beim Start des SQLServerAgent-Diensts|  
|**128**|Ausführen, wenn sich der Computer im Leerlauf befindet|  
  
 [ **@freq_interval =** ] *freq_interval*  
 Die Tage, an denen ein Auftrag ausgeführt wird. *Freq_interval* ist **Int**, hat den Standardwert **1**, und hängt vom Wert der *Freq_type*.  
  
|Wert des *Freq_type*|Auswirkung auf *Freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (einmal)|*Freq_interval* wird nicht verwendet.|  
|**4** (täglich)|Jede *Freq_interval* Tage.|  
|**8** (wöchentlich)|*Freq_interval* kann einen oder mehrere der folgenden (zusammen mit einer logischen OR-Operator):<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **4** = Dienstag<br /><br /> **8** = Mittwoch<br /><br /> **16** = Donnerstag<br /><br /> **32** = Freitag<br /><br /> **64** = Samstag|  
|**16** (monatlich)|Auf der *Freq_interval* Tag des Monats.|  
|**32** (mit relativem Monatsintervall)|*Freq_interval* ist eines der folgenden:<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **3** = Dienstag<br /><br /> **4** = Mittwoch<br /><br /> **5** = Donnerstag<br /><br /> **6** = Freitag<br /><br /> **7** = Samstag<br /><br /> **8** = Tag<br /><br /> **9** = Arbeitstag<br /><br /> **10** = Wochenendtag|  
|**64** (wenn der SQLServerAgent-Dienst startet)|*Freq_interval* wird nicht verwendet.|  
|**128**|*Freq_interval* wird nicht verwendet.|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 Gibt die Einheiten für *Freq_subday_interval*. *Freq_subday_type*ist **Int**, hat den Standardwert **0**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**0x1**|Zum angegebenen Zeitpunkt|  
|**0x2**|Sekunden|  
|**0x4**|Minuten|  
|**0x8**|Stunden|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 Die Anzahl der *Freq_subday_type* -Perioden zwischen den einzelnen Ausführungen eines Auftrags auftreten. *Freq_subday_interval*ist **Int**, hat den Standardwert **0**. Hinweis: Das Intervall sollte nicht länger als 10 Sekunden sein. *Freq_subday_interval* wird in diesen Fällen ignoriert, in denen *Freq_subday_type* gleich **1**.  
  
 [ **@freq_relative_interval =** ] *freq_relative_interval*  
 Ein Einzelvorgang des *Freq_interval* in jedem Monat, wenn *Freq_interval* beträgt 32 (monatlich, relativ). *Freq_relative_interval*ist **Int**, hat den Standardwert **0**, und kann einen der folgenden Werte sein. *Freq_relative_interval* wird in diesen Fällen ignoriert, in denen *Freq_type* stimmt nicht mit 32.  
  
|Wert|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 [ **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 Die Anzahl der Wochen oder Monate zwischen der geplanten Ausführung eines Auftrags. *freq_recurrence_factor* is used only if *freq_type* is **8**, **16**, or **32**. *Freq_recurrence_factor*ist **Int**, hat den Standardwert **0**.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Das Datum, an dem die Ausführung eines Auftrags beginnen kann. *Active_start_date*ist **Int**, hat den Standardwert NULL, womit des heutigen Datums. Das Datum wird das Format YYYYMMDD. Wenn *Active_start_date* ist nicht NULL ist, muss das Datum größer oder gleich 19900101 sein.  
  
 Überprüfen Sie nach dem Erstellen des Zeitplans, ob das Startdatum korrekt ist. Weitere Informationen finden Sie im Abschnitt "Planen von Startdaten" in [erstellen und Zuweisen von Zeitplänen zu Aufträgen](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5).  
  
 Bei wöchentlichen oder monatlichen Zeitplänen wird vom Agent nicht berücksichtigt, ob active_start_date in der Vergangenheit liegt, und das aktuelle Datum verwendet. Beim Erstellen eines SQL-Agentzeitplans mithilfe von sp_add_schedule kann der active_start_date-Parameter angegeben werden, der das Startdatum der Auftragsausführung darstellt. Wenn der Zeitplantyp "Wöchentlich" oder "Monatlich" lautet und der active_start_date-Parameter auf ein Datum in der Vergangenheit festgelegt ist, werden der active_start_date-Parameter ignoriert und das aktuelle Datum für active_start_date verwendet.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Das Datum, an dem die Ausführung eines Auftrags beendet werden kann. *Active_end_date*ist **Int**, hat den Standardwert **99991231**, womit der 31. Dezember 9999 angegeben. Im Format JJJJMMTT.  
  
 [ **@active_start_time =** ] *active_start_time*  
 Die Zeit an einem beliebigen Tag zwischen *Active_start_date* und *Active_end_date* die Ausführung eines Auftrags beginnen soll. *Active_start_time*ist **Int**, hat den Standardwert **000000**, womit 00:00:00 Uhr im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
 [ **@active_end_time =** ] *active_end_time*  
 Die Zeit an einem beliebigen Tag zwischen *Active_start_date* und *Active_end_date* zu der die Ausführung eines Auftrags. *Active_end_time*ist **Int**, hat den Standardwert **235959**, womit 23:59:59 Uhr im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
 [  **@owner_login_name** =] **"***Owner_login_name***"**  
 Der Name des Serverprinzipals, der Besitzer des Zeitplans ist. *Owner_login_name* ist **Sysname**, hat den Standardwert NULL, gibt an, dass der Zeitplan im Besitz des Erstellers ist.  
  
 [ **@schedule_uid**= ] *schedule_uid***OUTPUT**  
 Ein eindeutiger Bezeichner für den Zeitplan. *Schedule_uid* ist eine Variable des Typs **"uniqueidentifier"**.  
  
 [ **@schedule_id**= ] *schedule_id***OUTPUT**  
 Ein Bezeichner für den Zeitplan. *Schedule_id* ist eine Variable des Typs **Int**.  
  
 [ **@originating_server**= ] *server_name*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-schedule"></a>A. Erstellen eines Zeitplans  
 Im folgenden Beispiel wird ein Zeitplan mit dem Namen `RunOnce` erstellt. Der Zeitplan wird einmal um `23:30` Uhr an dem Tag ausgeführt, an dem der Zeitplan erstellt wird.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>B. Erstellen eines Zeitplans und Zuweisen des Zeitplans zu mehreren Aufträgen  
 Im folgenden Beispiel wird ein Zeitplan mit dem Namen `NightlyJobs` erstellt. Aufträge, die diesen Zeitplan verwenden, werden jeden Tag zur Serveruhrzeit `01:00` Uhr ausgeführt. Im Beispiel wird der Zeitplan den Aufträgen `BackupDatabase` und `RunReports` angefügt.  
  
> [!NOTE]  
>  Bei diesem Beispiel wird davon ausgegangen, dass die Aufträge `BackupDatabase` und `RunReports` bereits vorhanden sind.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Zuweisen von Zeitplänen zu Aufträgen](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [Planen eines Auftrags](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [Erstellen Sie einen Zeitplan](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
