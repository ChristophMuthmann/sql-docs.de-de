---
title: Sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords: sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f9accc8ae7ffb64d82fa10c3b60a2f8fec44b8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Agent-Aufträgen zurück, die gefilterte Datenmomentaufnahmen generieren. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert  **%** , Informationen über alle momentaufnahmeaufträge für gefilterten Daten, die mit der angegebenen Zeichenfolge zurückgegeben *Dynamic_ Snapshot_jobid*und *Dynamic_snapshot_jobname*für alle Veröffentlichungen.  
  
 [  **@dynamic_snapshot_jobname =** ] **"***Dynamic_snapshot_jobname***"**  
 Der Name eines Auftrags für eine Momentaufnahme gefilterter Daten. *Dynamic_snapshot_jobname*ist **Sysname**, hat Standardwert  **%** ", womit alle dynamischen Aufträge für eine Veröffentlichung mit dem angegebenen *Dynamic_ Snapshot_jobid*. Wenn beim Erstellen des Auftrags kein expliziter Auftragsname angegeben wurde, hat der Auftragsname folgendes Format:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [  **@dynamic_snapshot_jobid =** ] **"***Dynamic_snapshot_jobid***"**  
 Ein Bezeichner eines Auftrags für eine Momentaufnahme gefilterter Daten. *Dynamic_snapshot_jobid*ist **"uniqueidentifier"**, mit dem Standardwert NULL, womit alle momentaufnahmeaufträge, die mit der angegebenen Zeichenfolge *Dynamic_snapshot_jobname*.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifiziert den Auftrag für eine Momentaufnahme gefilterter Daten.|  
|**job_name**|**sysname**|Name des Auftrags für eine Momentaufnahme gefilterter Daten.|  
|**job_id**|**uniqueidentifier**|Identifiziert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag auf dem Verteiler.|  
|**dynamic_filter_login**|**sysname**|Wert für die Bewertung der [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) Funktion in einem parametrisierten Zeilenfilter für die Veröffentlichung definiert.|  
|**den Wert**|**sysname**|Wert für die Bewertung der [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) Funktion in einem parametrisierten Zeilenfilter für die Veröffentlichung definiert.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Der Pfad zu dem Ordner, aus dem die Momentaufnahmedateien gelesen werden, wenn ein parametrisierter Zeilenfilter verwendet wird.|  
|**frequency_type**|**int**|Die Häufigkeit, mit der der Agent planmäßig ausgeführt wird. Die folgenden Werte sind möglich:<br /><br /> **1** = einmalige Ausführung<br /><br /> **2** = bedarfsgesteuert<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = mit relativem Monatsintervall<br /><br /> **64** = Autostart<br /><br /> **128** = wiederholt|  
|**frequency_interval**|**int**|Die Tage, an denen der Agent ausgeführt wird. Die folgenden Werte sind möglich.<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **3** = Dienstag<br /><br /> **4** = Mittwoch<br /><br /> **5** = Donnerstag<br /><br /> **6** = Freitag<br /><br /> **7** = Samstag<br /><br /> **8** = Tag<br /><br /> **9** = Arbeitstage<br /><br /> **10** = Wochenendtage|  
|**frequency_subday_type**|**int**|Ist der Typ, der definiert, wie oft der Agent ausgeführt wird, wenn *Frequency_type* ist **4** (täglich), und kann einen der folgenden Werte sein.<br /><br /> **1** = zum angegebenen Zeitpunkt<br /><br /> **2** = Sekunden<br /><br /> **4** = Minuten<br /><br /> **8** = Stunden|  
|**frequency_subday_interval**|**int**|Anzahl der Intervalle von *Frequency_subday_type* dar, die zwischen der geplanten Ausführung des Agents auftreten.|  
|**frequency_relative_interval**|**int**|Ist die Woche, die der Agent ausgeführt, in einem bestimmten Monat wird beim *Frequency_type* ist **32** (mit relativem Monatsintervall) und kann einen der folgenden Werte sein.<br /><br /> **1** = erster<br /><br /> **2** = Sekunde<br /><br /> **4** = Dritter<br /><br /> **8** = vierter<br /><br /> **16** = letzter|  
|**frequency_recurrence_factor**|**int**|Anzahl der Wochen oder Monate zwischen der geplanten Ausführung der Momentaufnahme.|  
|**active_start_date**|**int**|Datum, an dem die Ausführung der Momentaufnahme zum ersten Mal geplant ist (Format: YYYYMMDD).|  
|**active_end_date**|**int**|Datum, an dem die Ausführung der Momentaufnahme zum letzten Mal geplant ist (Format: YYYYMMDD).|  
|**active_start_time**|**int**|Uhrzeit, zu der die Ausführung der Momentaufnahme zum ersten Mal geplant ist (Format: HHMMSS).|  
|**active_end_time**|**int**|Uhrzeit, zu der die Ausführung der Momentaufnahme zum letzten Mal geplant ist (Format: HHMMSS).|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdynamicsnapshot_job** wird bei der Mergereplikation verwendet.  
  
 Werden alle Standardparameterwerte verwendet, werden Informationen zu allen Aufträgen für eine Momentaufnahme partitionierter Daten für die gesamte Veröffentlichungsdatenbank zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** feste Datenbankrolle und der veröffentlichungszugriffsliste für die Veröffentlichung können **Sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
