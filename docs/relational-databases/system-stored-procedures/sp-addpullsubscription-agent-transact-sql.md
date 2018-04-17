---
title: Sp_addpullsubscription_agent (Transact-SQL) | Microsoft Docs
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
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca6f7bda4d6d9e0387dcbd98a09040be4d0a0d0a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
 
  Fügt einer Transaktionsveröffentlichung einen neuen geplanten Agent-Auftrag hinzu, mit dem ein Pullabonnement synchronisiert wird. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]          , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
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
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher_db=**] **"*** Publisher_db"*  
 Der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. *Publisher_db* wird von Oracle-Verlegern ignoriert.  
  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten.  
  
 [  **@subscriber_db=**] **"***Subscriber_db***"**  
 Ist der Name der Abonnementdatenbank. *Subscriber_db* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten.  
  
 [  **@subscriber_security_mode=**] *Subscriber_security_mode*  
 Der Sicherheitsmodus, der beim Synchronisieren zum Herstellen der Verbindung mit einem Abonnenten verwendet wird. *Subscriber_security_mode* ist **"Int",** hat den Standardwert NULL. **0** gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. **1** gibt die Windows-Authentifizierung.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten. Der Verteilungs-Agent stellt eine Verbindung mit dem lokalen Abonnenten immer mithilfe der Windows-Authentifizierung her. Wenn ein anderer Wert als NULL oder **1** angegeben ist für diesen Parameter wird eine Warnmeldung zurückgegeben.  
  
 [  **@subscriber_login =**] **"***Subscriber_login***"**  
 Ist der Anmeldename des Abonnenten verwenden, wenn beim Synchronisieren mit einem Abonnenten herstellen der Verbindung an. *Subscriber_login* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten. Wird für diesen Parameter ein Wert angegeben, wird eine Warnmeldung zurückgegeben, der Wert jedoch ignoriert.  
  
 [  **@subscriber_password=**] **"***Subscriber_password***"**  
 Das Kennwort des Abonnenten. *Subscriber_password* ist erforderlich, wenn *Subscriber_security_mode* festgelegt ist, um **0**. *Subscriber_password* ist **Sysname**, hat den Standardwert NULL. Bei Verwendung eines Abonnentenkennworts wird dieses automatisch verschlüsselt.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird aus Gründen der Abwärtskompatibilität von Skripts beibehalten. Wird für diesen Parameter ein Wert angegeben, wird eine Warnmeldung zurückgegeben, der Wert jedoch ignoriert.  
  
 [  **@distributor=**] **"***Verteiler***"**  
 Entspricht dem Namen des Verteilers. *Verteiler* ist **Sysname**, hat den Standardwert der Wert von *Publisher*.  
  
 [  **@distribution_db=**] **"***Distribution_db***"**  
 Ist der Name der Verteilungsdatenbank. *Distribution_db* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@distributor_security_mode=**] *Distributor_security_mode*  
 Der Sicherheitsmodus, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verteiler verwendet wird. *Distributor_security_mode* ist **Int**, hat den Standardwert **1**. **0** gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. **1** gibt die Windows-Authentifizierung.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] **"***Distributor_login***"**  
 Der Verteileranmeldename, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verteiler verwendet wird. *Distributor_login* ist erforderlich, wenn *Distributor_security_mode* festgelegt ist, um **0**. *Distributor_login* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@distributor_password =**] **"***Distributor_password***"**  
 Das Verteilerkennwort. *Distributor_password* ist erforderlich, wenn *Distributor_security_mode* festgelegt ist, um **0**. *Distributor_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein leeres Kennwort. Verwenden Sie ein sicheres Kennwort. Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
 [  **@optional_command_line=**] **"***Standardwert***"**  
 Eine optionale Befehlszeile des Verteilungs-Agents. Beispielsweise **- DefinitionFile** C:\Distdef.txt oder **- CommitBatchSize** 10. *Der Standardwert* ist **nvarchar(4000)**, Standardwert ist eine leere Zeichenfolge.  
  
 [  **@frequency_type=**] *Frequency_type*  
 Die Häufigkeit für die Zeitplanung des Verteilungs-Agents. *Frequency_type* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2** (Standardwert)|Bedarfsgesteuert|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ|  
|**64**|Autostart|  
|**128**|Wiederholt|  
  
> [!NOTE]  
>  Angeben des Werts **64** bewirkt, dass der Verteilungs-Agent im fortlaufenden Modus ausgeführt. Dies entspricht dem Festlegen der **-Continuous** Parameter für den Agent. Weitere Informationen finden Sie unter [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
 [  **@frequency_interval=**] *Frequency_interval*  
 Ist der Wert der Häufigkeit festgelegt, die durch Anwenden *Frequency_type*. *Frequency_interval* ist **Int**, hat den Standardwert 1.  
  
 [  **@frequency_relative_interval=**] *Frequency_relative_interval*  
 Das Datum des Verteilungs-Agents. Dieser Parameter wird verwendet, wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall). *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**1** (Standard)|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 [  **@frequency_recurrence_factor=**] *Frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert **1**.  
  
 [  **@frequency_subday=**] *Frequency_subday*  
 Die Häufigkeit für die erneute geplante Ausführung während des definierten Zeitraums. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**1** (Standard)|Einmal|  
|**2**|Zweimal|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *Frequency_subday_interval*  
 Das Intervall für *Frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert **1**.  
  
 [  **@active_start_time_of_day=**] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Verteilungs-Agent zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert **0**.  
  
 [  **@active_end_time_of_day=**] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Verteilungs-Agent nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert **0**.  
  
 [  **@active_start_date=**] *Active_start_date*  
 Das Datum, an dem der Verteilungs-Agent zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert **0**.  
  
 [  **@active_end_date=**] *Active_end_date*  
 Das Datum, ab dem der Verteilungs-Agent nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert **0**.  
  
 [  **@distribution_jobid =**] *Distribution_jobid *** Ausgabe**  
 Die ID des Verteilungs-Agents für diesen Auftrag. *Distribution_jobid* ist **binary(16)**, hat den Standardwert NULL, und es ist ein OUTPUT-Parameter.  
  
 [  **@encrypted_distributor_password=**] *Encrypted_distributor_password*  
 Festlegen von *Encrypted_distributor_password* wird nicht mehr unterstützt. Beim Festlegen dieser **Bit** Parameter **1** führt zu einem Fehler.  
  
 [  **@enabled_for_syncmgr=**] **"***Enabled_for_syncmgr***"**  
 Gibt an, ob das Abonnement über synchronisiert werden kann [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronisierungs-Manager. *Enabled_for_syncmgr* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"false"**, das Abonnement ist nicht mit der Synchronisierungsverwaltung registriert. Wenn **"true"**, das Abonnement mit der Synchronisierungsverwaltung registriert und kann synchronisiert werden, ohne zu starten [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address=**] **"***Ftp_address***"**  
 Nur aus Gründen der Abwärtskompatibilität beibehalten  
  
 [  **@ftp_port=**] *Ftp_port*  
 Nur aus Gründen der Abwärtskompatibilität beibehalten  
  
 [  **@ftp_login=**] **"***Ftp_login***"**  
 Nur aus Gründen der Abwärtskompatibilität beibehalten  
  
 [  **@ftp_password=**] **"***Ftp_password***"**  
 Nur aus Gründen der Abwärtskompatibilität beibehalten  
  
 [  **@alt_snapshot_folder=** ] **"*** Alternate_snapshot_folder"*  
 Gibt den Speicherort des anderen Ordners für die Momentaufnahme an. *Alternate_snapshot_folder* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [ **@working_directory**=] **"***Working_director***"**  
 Der Name des Arbeitsverzeichnisses, das zum Speichern von Daten- und Schemadateien für die Veröffentlichung verwendet wird. *Working_directory* ist **nvarchar(255)**, hat den Standardwert NULL. Dieser Name sollte im UNC-Format angegeben werden.  
  
 [ **@use_ftp**=] **"***Use_ftp***"**  
 Gibt anstelle des normalen Protokolls FTP an, um Momentaufnahmen abzurufen. *Use_ftp* ist **nvarchar(5)**, hat den Standardwert "false".  
  
 [ **@publication_type**=] *Publication_type*  
 Gibt den Replikationstyp der Veröffentlichung an. *Publication_type* ist ein **"tinyint"** hat den Standardwert **0**. Wenn **0**, Veröffentlichung ist ein Transaktionstyp. Wenn **1**, handelt es sich Momentaufnahme. Wenn **2**, handelt es sich zusammenführen.  
  
 [ **@dts_package_name**=] **"***Dts_package_name***"**  
 Gibt den Namen des DTS-Pakets an. *Dts_package_name* ist ein **Sysname** hat den Standardwert NULL. Zum Angeben eines Pakets mit dem Namen `DTSPub_Package` wird beispielsweise der `@dts_package_name = N'DTSPub_Package'`-Parameter verwendet.  
  
 [ **@dts_package_password**=] **"***Dts_package_password***"**  
 Gibt gegebenenfalls das Kennwort des Pakets an. *Dts_package_password* ist **Sysname** hat den Standardwert NULL, d. h. es ist kein Kennwort für das Paket.  
  
> [!NOTE]  
>  Sie müssen ein Kennwort angeben, wenn *Dts_package_name* angegeben ist.  
  
 [ **@dts_package_location**=] **"***Dts_package_location***"**  
 Gibt den Paketspeicherort an. *Dts_package_location* ist ein **nvarchar(12)**, hat den Standardwert **Abonnenten**. Der Speicherort des Pakets kann **Verteiler** oder **Abonnenten**.  
  
 [ **@reserved**=] **"***reservierte***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@offloadagent**=] '*Remote_agent_activation*"  
 > [!NOTE]  
>  Die Aktivierung des Remote-Agents wurde als veraltet markiert und wird nicht mehr unterstützt. Dieser Parameter wird nur zur Aufrechterhaltung der Abwärtskompatibilität von Skripts unterstützt. Festlegen von *Remote_agent_activation* auf einen anderen Wert als **"false"** wird ein Fehler generiert.  
  
 [ **@offloadserver**=] '*Remote_agent_server_name*"  
 > [!NOTE]  
>  Die Aktivierung des Remote-Agents wurde als veraltet markiert und wird nicht mehr unterstützt. Dieser Parameter wird nur zur Aufrechterhaltung der Abwärtskompatibilität von Skripts unterstützt. Festlegen von *Remote_agent_server_name* auf einen beliebigen Wert ungleich NULL wird ein Fehler generiert.  
  
 [ **@job_name**=] '*Job_name*"  
 Der Name eines vorhandenen Agentauftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird nur angegeben, wenn das Abonnement mithilfe eines vorhandenen Auftrags statt mit einem neu erstellten Auftrag (Standard) synchronisiert wird. Wenn Sie nicht Mitglied der sind die **Sysadmin** festen Serverrolle, müssen Sie angeben *Job_login* und *Job_password* beim Angeben von *Job_name*.  
  
 [ **@job_login**=] **"***Job_login***"**  
 Der Anmeldename für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_login* ist **nvarchar(257)**, hat keinen Standardwert. Dieses Windows-Konto wird immer für Agent-Verbindungen mit dem Abonnenten verwendet.  
  
 [ **@job_password**=] **"***Job_password***"**  
 Das Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_password* ist **Sysname**, hat keinen Standardwert.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addpullsubscription_agent** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addpullsubscription_agent**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [Sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [Sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
