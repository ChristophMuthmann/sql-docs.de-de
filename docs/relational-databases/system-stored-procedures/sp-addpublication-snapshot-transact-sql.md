---
title: Sp_addpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9de7dc82dd63e8ea6b23d9c561a8fd7ea83da435
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt den Momentaufnahme-Agent für die angegebene Veröffentlichung. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
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
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@frequency_type=**] *Frequency_type*  
 Die Häufigkeit für die Ausführung des Momentaufnahme-Agents. *Frequency_type* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal.|  
|**4** (Standard)|Tägliche.|  
|**8**|Wöchentlich|  
|**16**|Monatlich|  
|**32**|Monatlich, relativ zum Häufigkeitsintervall.|  
|**64**|Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent gestartet wird.|  
|**128**|Ausführen, wenn sich der Computer im Leerlauf befindet|  
  
 [  **@frequency_interval=**] *Frequency_interval*  
 Ist der Wert der Häufigkeit festgelegt, die durch Anwenden *Frequency_type*. *Frequency_interval* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert für frequency_type|Auswirkung auf frequency_interval|  
|------------------------------|-----------------------------------|  
|**1**|*Frequency_interval* wird nicht verwendet.|  
|**4** (Standard)|Jede *Frequency_interval* Tagen, bei der Standard ist täglich.|  
|**8**|*Frequency_interval* kann einen oder mehrere der folgenden (zusammen mit einem [&#124; (Bitweises OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) logischer Operator):<br /><br /> **1** = Sonntag &#124;<br /><br /> **2** = Montag &#124;<br /><br /> **4** = Dienstag &#124;<br /><br /> **8** = Mittwoch &#124;<br /><br /> **16** = Donnerstag &#124;<br /><br /> **32** = Freitag &#124;<br /><br /> **64** = Samstag|  
|**16**|Auf der *Frequency_interval* Tag des Monats.|  
|**32**|*Frequency_interval* ist eines der folgenden:<br /><br /> **1** = Sonntag &#124;<br /><br /> **2** = Montag &#124;<br /><br /> **3** = Dienstag &#124;<br /><br /> **4** = Mittwoch &#124;<br /><br /> **5** = Donnerstag &#124;<br /><br /> **6** = Freitag &#124;<br /><br /> **7** = Samstag &#124;<br /><br /> **8** = Tag &#124;<br /><br /> **9** = Arbeitstag &#124;<br /><br /> **10** = Wochenendtag|  
|**64**|*Frequency_interval* wird nicht verwendet.|  
|**128**|*Frequency_interval* wird nicht verwendet.|  
  
 [  **@frequency_subday=**] *Frequency_subday*  
 Ist die Einheit für *Freq_subday_interval*. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Zweimal|  
|**4** (Standard)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *Frequency_subday_interval*  
 Das Intervall für *Frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert von 5, womit alle 5 Minuten.  
  
 [  **@frequency_relative_interval=**] *Frequency_relative_interval*  
 Das Datum, an dem der Momentaufnahme-Agent ausgeführt wird. *Frequency_relative_interval* ist **Int**, hat den Standardwert 1.  
  
 [  **@frequency_recurrence_factor=**] *Frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert 0.  
  
 [  **@active_start_date=**] *Active_start_date*  
 Das Datum, an dem der Momentaufnahme-Agent zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert 0.  
  
 [  **@active_end_date=**] *Active_end_date*  
 Das Datum, ab dem der Momentaufnahme-Agent nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert 99991231, womit der 31. Dezember 9999.  
  
 [  **@active_start_time_of_day=**] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Momentaufnahme-Agent zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert 0.  
  
 [  **@active_end_time_of_day=**] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Momentaufnahme-Agent nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert 235959, womit 23:59:59 Uhr auf dem 24-Stunden-Format an.  
  
 [  **@snapshot_job_name =** ] **"***Snapshot_agent_name***"**  
 Der Name eines vorhandenen Auftrags des Momentaufnahme-Agents, wenn ein vorhandener Auftrag verwendet wird. *Snapshot_agent_name* ist **nvarchar(100)** hat den Standardwert NULL. Dieser Parameter dient der internen Verwendung und sollte beim Erstellen einer neuen Veröffentlichung nicht angegeben werden. Wenn *Snapshot_agent_name* angegeben ist, klicken Sie dann *Job_login* und *Job_password* muss NULL sein.  
  
 [  **@publisher_security_mode** =] *Publisher_security_mode*  
 Der vom Agent beim Herstellen der Verbindung mit dem Verleger verwendete Sicherheitsmodus. *Publisher_security_mode* ist **"smallint"**, hat den Standardwert 1. **0** gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung und **1** gibt die Windows-Authentifizierung. Der Wert **0** muss angegeben werden, für nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login** =] **"***Publisher_login***"**  
 Der Anmeldename, der beim Herstellen der Verbindung mit dem Verleger verwendet wird. *Publisher_login* ist **Sysname**, hat den Standardwert NULL. *Publisher_login* muss angegeben werden, wenn *Publisher_security_mode* ist **0**. Wenn *Publisher_login* ist NULL und *Publisher_security_mode* ist **1**, und klicken Sie dann das Windows-Konto im angegebenen *Job_login* verwendet werden Wenn eine Verbindung mit dem Verleger herstellen.  
  
 [  **@publisher_password** =] **"***Publisher_password***"**  
 Das Kennwort, das beim Herstellen der Verbindung mit dem Verleger verwendet wird. *Publisher_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Speichern Sie keine Authentifizierungsinformationen in Skriptdateien. Es wird empfohlen, Anmeldenamen und Kennwörter zur Laufzeit bereitzustellen, um die Sicherheit zu verbessern.  
  
 [  **@job_login** =] **"***Job_login***"**  
 Der Anmeldename für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_login* ist **nvarchar(257)**, hat den Standardwert NULL. Das Windows-Konto wird stets für Agent-Verbindungen mit dem Verteiler verwendet. Sie müssen diesen Parameter angeben, wenn Sie einen neuen Auftrag des Momentaufnahme-Agents erstellen.  
  
> [!NOTE]  
>  Für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber, diese Angabe muss die gleiche Anmeldung im angegebenen [Sp_adddistpublisher &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
 [  **@job_password** =] **"***Job_password***"**  
 Das Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_password* ist **Sysname**, hat keinen Standardwert. Sie müssen diesen Parameter angeben, wenn Sie einen neuen Auftrag des Momentaufnahme-Agents erstellen.  
  
> [!IMPORTANT]  
>  Speichern Sie keine Authentifizierungsinformationen in Skriptdateien. Es wird empfohlen, Anmeldenamen und Kennwörter zur Laufzeit bereitzustellen, um die Sicherheit zu verbessern.  
  
 [  **@publisher** =] **"***Publisher***"**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, für die Erstellung einer Momentaufnahme-Agent auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addpublication_snapshot** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addpublication_snapshot**.  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [Sp_addpublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Sp_changepublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [Sp_startpublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
