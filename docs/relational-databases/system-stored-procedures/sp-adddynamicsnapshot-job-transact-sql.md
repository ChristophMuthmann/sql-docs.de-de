---
title: Sp_adddynamicsnapshot_job (Transact-SQL) | Microsoft Docs
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
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6590dad37937cb5b937ac49e541e2264a266de8d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Agentauftrag, der eine Momentaufnahme gefilterter Daten für eine Veröffentlichung mit parametrisierten Zeilenfiltern generiert. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt. Ein Administrator kann diese gespeicherte Prozedur verwenden, um manuell Aufträge für Momentaufnahmen gefilterter Daten für Abonnenten zu erstellen.  
  
> [!NOTE]  
>  Damit ein Auftrag für eine Momentaufnahme gefilterter Daten erstellt werden kann, muss bereits ein Auftrag für eine Standardmomentaufnahme für die Veröffentlichung vorhanden sein.  
  
 Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung, der der Auftrag für die Momentaufnahme gefilterter Daten hinzugefügt wird. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@suser_sname**=] **"***Suser_sname***"**  
 Ist der verwendete Wert beim Erstellen einer Momentaufnahme gefilterter Daten für ein Abonnement, durch den Wert des gefiltert wird die [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion beim Abonnenten. *SUSER_SNAME* ist **Sysname**, hat keinen Standardwert. *SUSER_SNAME* sollte NULL sein, wenn diese Funktion nicht verwendet wird, um die Veröffentlichung dynamisch zu filtern.  
  
 [ **@host_name**=] **"***Host_name***"**  
 Ist der verwendete Wert beim Erstellen einer Momentaufnahme gefilterter Daten für ein Abonnement, durch den Wert des gefiltert wird die [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) -Funktion beim Abonnenten. *HOST_NAME* ist **Sysname**, hat keinen Standardwert. *HOST_NAME* sollte NULL sein, wenn diese Funktion nicht verwendet wird, um die Veröffentlichung dynamisch zu filtern.  
  
 [ **@dynamic_snapshot_jobname**=] **"***Dynamic_snapshot_jobname***"**  
 Der Name des erstellten Auftrags für eine Momentaufnahme gefilterter Daten. *Dynamic_snapshot_jobname* ist **Sysname**, mit dem Standardwert NULL und ist ein optionaler OUTPUT-Parameter. Wenn angegeben, *Dynamic_snapshot_jobname* muss in einem eindeutigen Auftrag auf dem Verteiler aufgelöst werden. Wird das Argument nicht angegeben, wird automatisch ein Auftragsname generiert und im Resultset zurückgegeben, wo der Name folgendermaßen erstellt wird:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  Wenn Sie den Namen des Auftrags für eine dynamische Momentaufnahme generieren, können Sie den Namen des Auftrags für eine Standardmomentaufnahme abschneiden.  
  
 [ **@dynamic_snapshot_jobid**=] **"***Dynamic_snapshot_jobid***"**  
 Ein Bezeichner des erstellten Auftrags für die Momentaufnahme gefilterter Daten. *Dynamic_snapshot_jobid* ist **"uniqueidentifier"**, mit dem Standardwert NULL und ist ein optionaler OUTPUT-Parameter.  
  
 [  **@frequency_type=**] *Frequency_type*  
 Die Häufigkeit, mit der der Auftrag für die Momentaufnahme gefilterter Daten geplant werden soll. *Frequency_type* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Bedarfsgesteuert|  
|**4** (Standard)|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ|  
|**64**|Autostart|  
|**128**|Wiederholt|  
  
 [  **@frequency_interval =** ] *Frequency_interval*  
 Der Zeitraum (in Tagen) der Ausführung des Auftrags für die Momentaufnahme gefilterter Daten. *Frequency_interval* ist **Int**, hat den Standardwert 1, und hängt vom Wert der *Frequency_type*.  
  
|Wert des *Frequency_type*|Auswirkung auf *Frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*Frequency_interval* wird nicht verwendet.|  
|**4** (Standard)|Jede *Frequency_interval* Tagen, bei der Standard ist täglich.|  
|**8**|*Frequency_interval* kann einen oder mehrere der folgenden (zusammen mit einem [ &#124; &#40;bitweises OR&#41; &#40;Transact-SQL&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md) logischer Operator):<br /><br /> **1** = Sonntag &#124; **2** = Montag &#124; **4** = Dienstag &#124; **8** = Mittwoch &#124; **16** = Donnerstag &#124; **32** = Freitag &#124; **64** = Samstag|  
|**16**|Auf der *Frequency_interval* Tag des Monats.|  
|**32**|*Frequency_interval* ist eines der folgenden:<br /><br /> **1** = Sonntag &#124; **2** = Montag &#124; **3** = Dienstag &#124; **4** = Mittwoch &#124; **5** = Donnerstag &#124; **6** = Freitag &#124; **7** = Samstag &#124; **8** = Tag &#124; **9** = Arbeitstag &#124; **10** = Wochenendtag|  
|**64**|*Frequency_interval* wird nicht verwendet.|  
|**128**|*Frequency_interval* wird nicht verwendet.|  
  
 [  **@frequency_subday=**] *Frequency_subday*  
 Gibt die Einheiten für *Frequency_subday_interval*. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Zweimal|  
|**4** (Standard)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *Frequency_subday_interval*  
 Die Anzahl der *Frequency_subday* Punkte, die zwischen den einzelnen Ausführungen des Auftrags auftreten. *Frequency_subday_interval* ist **Int**, hat den Standardwert 5.  
  
 [  **@frequency_relative_interval=**] *Frequency_relative_interval*  
 Das Auftreten des Auftrags für eine Momentaufnahme gefilterter Daten in jedem Monat. Dieser Parameter wird verwendet, wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall). *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**1** (Standard)|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 [  **@frequency_recurrence_factor=**] *Frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert 0.  
  
 [  **@active_start_date=**] *Active_start_date*  
 Das Datum, an dem der Auftrag für die Momentaufnahme gefilterter Daten zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_date=**] *Active_end_date*  
 Das Datum, ab dem der Auftrag für die Momentaufnahme gefilterter Daten nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_time_of_day=**] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Auftrag für die Momentaufnahme gefilterter Daten zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_time_of_day=**] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Auftrag für die Momentaufnahme gefilterter Daten nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifiziert den Auftrag für die Momentaufnahme gefilterter Daten in der [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) -Systemtabelle.|  
|**dynamic_snapshot_jobname**|**sysname**|Name des Auftrags für eine Momentaufnahme gefilterter Daten.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifizierung der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag auf dem Verteiler.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_adddynamicsnapshot_job** wird bei der Mergereplikation für Veröffentlichungen mit parametrisierten Filtern verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_adddynamicsnapshot_job**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [ausgeführt werden kann &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [Sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
