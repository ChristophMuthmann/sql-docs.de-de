---
title: Sp_addpublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 59fcdcebd8c8397de2669491d4ea18cb38cfc853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Momentaufnahme- oder Transaktionsveröffentlichung. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung, die erstellt werden soll. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert. Dieser Name muss innerhalb der Datenbank eindeutig sein.  
  
 [  **@taskid=**] *Taskid*  
 Nur für Abwärtskompatibilität unterstützt. Verwenden Sie [Sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
 [  **@restricted=**] **"***eingeschränkte***"**  
 Nur für Abwärtskompatibilität unterstützt. Verwenden Sie *Default_access*.  
  
 [  **@sync_method=**] *"Sync_method ***"**  
 Der Synchronisierungsmodus. *Sync_method* ist **vom Datentyp nvarchar(13)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**native**|Erstellt eine Massenkopierprogramm-Ausgabe aller Tabellen im einheitlichen Modus. *Für Oracle-Verlegern nicht unterstützt*.|  
|**character**|Erstellt eine Massenkopierprogramm-Ausgabe aller Tabellen im Zeichenmodus. *Für einen Oracle-Verleger* **Zeichen** *gilt nur für die momentaufnahmereplikation*.|  
|**gleichzeitige**|Erzeugt eine Massenkopierprogramm-Ausgabe aller Tabellen im einheitlichen Modus, sperrt jedoch die Tabellen während der Erstellung der Momentaufnahme nicht. Wird nur für Transaktionsveröffentlichungen unterstützt. *Für Oracle-Verlegern nicht unterstützt*.|  
|**' concurrent_c '**|Erzeugt eine Massenkopierprogramm-Ausgabe aller Tabellen im Zeichenmodus, sperrt jedoch die Tabellen während der Erstellung der Momentaufnahme nicht. Wird nur für Transaktionsveröffentlichungen unterstützt.|  
|**Datenbank-Momentaufnahme**|Erstellt aus einer Datenbankmomentaufnahme eine Massenkopierprogramm-Ausgabe aller Tabellen im einheitlichen Modus. Datenbank-Momentaufnahmen stehen nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**Zeichensatz der Datenbank-Momentaufnahme**|Erstellt aus einer Datenbankmomentaufnahme eine Massenkopierprogramm-Ausgabe aller Tabellen im Zeichenmodus. Datenbank-Momentaufnahmen stehen nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (Standard)|Standardmäßig **native** für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber. Für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber, der Standardwert ist **Zeichen** Wenn der Wert der *Repl_freq* ist **Momentaufnahme** und **Concurrent_c** in allen anderen Fällen.|  
  
 [  **@repl_freq=**] **"***Repl_freq***"**  
 Ist der Typ der Häufigkeit der Replikation, *Repl_freq* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**fortlaufende** (Standard)|Der Verleger stellt die Ausgabe aller protokollbasierten Transaktionen bereit. Für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber, dies erfordert, dass *Sync_method* festgelegt werden, um **Concurrent_c**.|  
|**Momentaufnahme**|Der Verleger gibt nur geplante Synchronisierungsereignisse aus. Für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber, dies erfordert, dass *Sync_method* festgelegt werden, um **Zeichen**.|  
  
 [  **@description=**] **"***Beschreibung***"**  
 Eine optionale Beschreibung für die Veröffentlichung. *Beschreibung* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@status=**] **"***Status***"**  
 Gibt an, ob Veröffentlichungsdaten verfügbar sind. *Status* ist **nvarchar(8)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Aktive**|Die Veröffentlichungsdaten sind für Abonnenten sofort verfügbar.|  
|**Inaktive** (Standard)|Die Veröffentlichungsdaten sind für Abonnenten zunächst nicht verfügbar, wenn die Veröffentlichung erstellt wird (die Abonnierung ist möglich, aber die Abonnements werden nicht verarbeitet).|  
  
 *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@independent_agent=**] **"***Independent_agent***"**  
 Gibt an, ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist. *Independent_agent* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"true"**, ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist. Wenn **"false"**, die Veröffentlichung verwendet einen freigegebenen Verteilungs-Agent, und jedes Verlegerdatenbank und Abonnentendatenbank-Paar besitzt einen einzelnen, freigegebenen Agent.  
  
 [  **@immediate_sync=**] **"***immediate_sync***"**  
 Gibt an, ob die Synchronisierungsdateien für die Veröffentlichung bei jeder Ausführung des Momentaufnahme-Agents neu erstellt werden. *immediate_sync* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"true"**, die Synchronisierungsdateien erstellt oder neu erstellt jedes Mal der Momentaufnahme-Agent ausgeführt wird. Abonnenten können die Synchronisierungsdateien sofort abrufen, wenn der Momentaufnahme-Agent vor dem Erstellen des Abonnements abgeschlossen wurde. Neue Abonnements rufen die neuesten Synchronisierungsdateien ab, die von der letzten Ausführung des Momentaufnahmeagents generiert wurden. *Independent_agent* muss **"true"** für *immediate_sync* werden **"true"**. Wenn **"false"**, die Synchronisierungsdateien nur erstellt, wenn neue Abonnements vorhanden sind. Rufen Sie [Sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) für jedes Abonnement, wenn Sie einen neuen Artikel zu einer vorhandenen Veröffentlichung inkrementell hinzufügen. Abonnenten können die Synchronisierungsdateien nach dem Einrichten des Abonnements erst empfangen, wenn die Momentaufnahme-Agents gestartet und abgeschlossen wurden.  
  
 [  **@enabled_for_internet=**] **"***Enabled_for_internet***"**  
 Gibt an, ob die Veröffentlichung für das Internet aktiviert ist, und bestimmt, ob die Momentaufnahmedateien per FTP (File Transfer Protocol) an einen Abonnenten übertragen werden können. *Enabled_for_internet* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"true"**, die Synchronisierungsdateien für die Veröffentlichung werden im Verzeichnis C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp ablegen. Der Benutzer muss das FTP-Verzeichnis erstellen.  
  
 [  **@allow_push=**] **"***Allow_push***"**  
 Gibt an, ob für die angegebene Veröffentlichung Pushabonnements erstellt werden können. *Allow_push* ist **nvarchar(5)**, hat den Standardwert "true", womit Pushabonnements für die Veröffentlichung zulässig.  
  
 [  **@allow_pull=**] **"***Allow_pull***"**  
 Gibt an, ob für die angegebene Veröffentlichung Pullabonnements erstellt werden können. *Allow_pull* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"false"**, Pullabonnements sind für die Veröffentlichung nicht zulässig.  
  
 [  **@allow_anonymous=**] **"***Allow_anonymous***"**  
 Gibt an, ob für die angegebene Veröffentlichung anonyme Abonnements erstellt werden können. *Allow_anonymous* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"true"**, *immediate_sync* muss ebenfalls festgelegt werden, um **"true"**. Wenn **"false"**, anonyme Abonnements sind für die Veröffentlichung nicht zulässig.  
  
 [  **@allow_sync_tran=**] **"***Allow_sync_tran***"**  
 Gibt an, ob Abonnements mit sofortigem Update für die Veröffentlichung zulässig sind. *Allow_sync_tran* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** ist *für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@autogen_sync_procs=**] **"***Autogen_sync_procs***"**  
 Gibt an, ob die synchronisierende gespeicherte Prozedur für Abonnements mit Update beim Verleger generiert wird. *Autogen_sync_procs* ist **nvarchar(5)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**true**|Wird automatisch festgelegt, wenn das Aktualisieren von Abonnements aktiviert ist.|  
|**false**|Wird automatisch für Oracle-Verleger festgelegt oder wenn das Aktualisieren von Abonnements nicht aktiviert ist.|  
|NULL (Standard)|Standardmäßig **"true"** Wenn aktualisierbare Abonnements aktiviert ist, und um **"false"** bei aktualisierbaren Abonnements nicht aktiviert.|  
  
> [!NOTE]  
>  Der vom Benutzer angegebene Wert für *Autogen_sync_procs*wird überschrieben werden, abhängig von den Werten für angegebene *Allow_queued_tran* und *Allow_sync_tran*.  
  
 [  **@retention=**] *Aufbewahrung*  
 Die Beibehaltungsdauer (in Stunden) für die Abonnementaktivität. *Aufbewahrung* ist **Int**, Standardwert ist 336 Stunden. Wenn ein Abonnement im Beibehaltungszeitraum nicht aktiv ist, läuft es ab und wird entfernt. Der Wert kann größer als die maximale Beibehaltungsdauer der vom Verleger verwendeten Verteilungsdatenbank sein. Wenn **0**, laufen bekannte Abonnements der Veröffentlichung nie abläuft, und der Verteilungscleanup-Agent für abgelaufene Abonnements entfernt werden.  
  
 [  **@allow_queued_tran=** ] **"***Allow_queued_updating***"**  
 Aktiviert oder deaktiviert das Hinzufügen von Änderungen beim Abonnenten zu Warteschlangen, bis sie beim Verleger angewendet werden können. *Allow_queued_updating* ist **nvarchar(5)** hat den Standardwert "false". Wenn **"false"**, Änderungen auf dem Abonnenten werden nicht in die Warteschlange eingereiht. **"true"** ist *für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@snapshot_in_defaultfolder=** ] **"***Snapshot_in_default_folder***"**  
 Gibt an, ob Momentaufnahmedateien im Standardordner gespeichert werden. *Snapshot_in_default_folder* ist **nvarchar(5)** hat den Standardwert "true". Wenn **"true"**, momentaufnahmedateien im Standardordner gefunden werden können. Wenn **"false"**, sind momentaufnahmedateien im alternativen vom angegebenen Speicherort gespeichert *Alternate_snapshot_folder*. Alternative Speicherorte können sich auf einem anderen Server, auf einem Netzlaufwerk oder auf Wechselmedien befinden (z. B. auf CD-ROM oder auf einem Wechseldatenträger). Momentaufnahmedateien können auch auf einer FTP-Site gespeichert werden, um zu einem späteren Zeitpunkt vom Abonnenten abgerufen zu werden. Beachten Sie, dass dieser Parameter kann "true" sein und dennoch fehlgeschlagene einen Speicherort der **@alt_snapshot_folder** Parameter. Diese Kombination gibt an, dass die Momentaufnahmedateien sowohl im Standardpfad als auch im alternativen Pfad gespeichert werden.  
  
 [  **@alt_snapshot_folder=** ] **"***Alternate_snapshot_folder***"**  
 Gibt den Speicherort des anderen Ordners für die Momentaufnahme an. *Alternate_snapshot_folder* ist **nvarchar(255)** hat den Standardwert NULL.  
  
 [  **@pre_snapshot_script=** ] **"***Pre_snapshot_script***"**  
 Gibt einen Zeiger auf eine **.sql** Dateispeicherort. *Pre_snapshot_script* ist **nvarchar(255),** hat den Standardwert NULL. Der Verteilungs-Agent führt das vor der Momentaufnahme ausgeführte Skript vor allen Skripts für replizierte Objekte aus, wenn die Momentaufnahme bei einem Abonnenten angewendet wird. Das Skript wird beim Herstellen der Verbindung mit der Abonnementdatenbank in dem vom Verteilungs-Agent verwendeten Sicherheitskontext ausgeführt.  
  
 [  **@post_snapshot_script=** ] **"***Post_snapshot_script***"**  
 Gibt einen Zeiger auf eine **.sql** Dateispeicherort. *Post_snapshot_script* ist **nvarchar(255)**, hat den Standardwert NULL. Der Verteilungs-Agent führt das nach der Momentaufnahme ausgeführte Skript aus, nachdem alle anderen Skripts für replizierte Objekte und Daten während der Erstsynchronisierung angewendet wurden. Das Skript wird beim Herstellen der Verbindung mit der Abonnementdatenbank in dem vom Verteilungs-Agent verwendeten Sicherheitskontext ausgeführt.  
  
 [  **@compress_snapshot=** ] **"***Compress_snapshot***"**  
 Gibt an, dass die Momentaufnahme, die geschrieben wird die **@alt_snapshot_folder** Speicherort ist in komprimiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. *Compress_snapshot* ist **nvarchar(5)**, hat den Standardwert "false". **"false"** gibt an, dass die Momentaufnahme nicht komprimiert wird. **"true"** gibt an, dass die Momentaufnahme komprimiert wird. Momentaufnahmedateien, die größer als 2 Gigabyte (GB) sind, können nicht komprimiert werden. Komprimierte Momentaufnahmedateien werden an dem Speicherort dekomprimiert, an dem der Verteilungs-Agent ausgeführt wird. Pullabonnements werden normalerweise mit komprimierten Momentaufnahmen verwendet, sodass die Dateien auf dem Abonnenten dekomprimiert werden. Die Momentaufnahme im Standardordner kann nicht komprimiert werden.  
  
 [  **@ftp_address =** ] **"***Ftp_address***"**  
 Die Netzwerkadresse des FTP-Diensts für den Verteiler. *Ftp_address* ist **Sysname**, hat den Standardwert NULL. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien für den Verteilungs-Agent oder Merge-Agent eines Abonnenten zum Abholen gespeichert sind. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, kann jede Veröffentlichung einen anderen haben *Ftp_address*. Die Veröffentlichung muss die Weitergabe von Momentaufnahmen über FTP unterstützen.  
  
 [  **@ftp_port=** ] *Ftp_port*  
 Die Anschlussnummer des FTP-Diensts für den Verteiler. *Ftp_port* ist **Int**, hat den Standardwert 21. Gibt an, wo die veröffentlichungsmomentaufnahmedateien für den Verteilungs-Agent oder Merge-Agent eines Abonnenten zum Abholen befinden. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, jede Veröffentlichung kann einen eigenen besitzen *Ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **"***Ftp_subdirectory***"**  
 Gibt an, wo die Momentaufnahmedateien für den Verteilungs-Agent oder Merge-Agent eines Abonnenten zum Abholen verfügbar sind, wenn die Veröffentlichung das Weitergeben von Momentaufnahmen mithilfe von FTP unterstützt. *Ftp_subdirectory* ist **nvarchar(255)**, hat den Standardwert NULL. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, jede Veröffentlichung kann einen eigenen besitzen *ftp_subdirectory* oder festlegen, dass keine Unterverzeichnisse mit einem Nullwert.  
  
 [  **@ftp_login =** ] **"***Ftp_login***"**  
 Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird. *Ftp_login* ist **Sysname**, hat den Standardwert Anonymous.  
  
 [  **@ftp_password =** ] **"***Ftp_password***"**  
 Das Benutzerkennwort, mit dem eine Verbindung zum FTP-Dienst hergestellt wird. *Ftp_password* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@allow_dts =** ] **"***allow_dts nicht***"**  
 Gibt an, dass die Veröffentlichung Datentransformationen zulässt. Beim Erstellen eines Abonnements können Sie ein DTS-Paket angeben. *Allow_transformable_subscriptions* ist **nvarchar(5)** hat den Standardwert "false", lässt keine DTS-Transformationen. Wenn *allow_dts nicht* ist "true" *Sync_method* muss festgelegt werden, entweder **Zeichen** oder **Concurrent_c**.  
  
 **"true"** ist *für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@allow_subscription_copy =** ] **"***Allow_subscription_copy***"**  
 Aktiviert oder deaktiviert die Option zum Kopieren der Abonnementdatenbanken, die diese Veröffentlichung abonniert haben. *Allow_subscription_copy* ist**nvarchar(5)**, hat den Standardwert "false".  
  
 [  **@conflict_policy =** ] **"***Conflict_policy***"**  
 Gibt die Richtlinie zur Konfliktlösung an, die für die Option zur verzögerten Aktualisierung über eine Warteschlange verwendet wird. *Conflict_policy* ist **nvarchar(100)** hat den Standardwert NULL und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Pub wins**|Der Verleger gewinnt den Konflikt.|  
|**Sub reinit**|Erneutes Initialisieren des Abonnements.|  
|**Sub wins**|Der Abonnent gewinnt den Konflikt.|  
|NULL (Standard)|Wenn NULL, und die Veröffentlichung eine momentaufnahmeveröffentlichung handelt, wird die Standardrichtlinie **sub Reinit**. Wenn NULL und die Veröffentlichung keine momentaufnahmeveröffentlichung ist, wird die Standardeinstellung **Pub Wins**.|  
  
 *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@centralized_conflicts =** ] **"***Centralized_conflicts***"**  
 Gibt an, ob Konfliktdatensätze auf dem Verleger gespeichert werden. *Centralized_conflicts* ist **nvarchar(5)**, Standardwert ist "true". Wenn **"true"**, Konfliktdatensätze werden auf dem Verleger gespeichert. Wenn **"false"**, Konfliktdatensätze werden gespeichert, auf dem Verleger und dem Abonnenten, die den Konflikt verursacht hat. *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@conflict_retention =** ] *Conflict_retention*  
 Gibt die Konfliktaufbewahrungsdauer in Tagen an. Der Zeitraum, in dem Konfliktmetadaten für Peer-zu-Peer-Transaktionsreplikation und Abonnements mit verzögertem Update gespeichert werden. *Conflict_retention* ist **Int**, hat den Standardwert von 14. *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@queue_type =** ] **"***Queue_type***"**  
 Gibt an, welcher Wartenschlangentyp verwendet wird. *Warteschlangentyp* ist **nvarchar(10)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**sql**|Verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen.|  
|NULL (Standard)|Standardmäßig **Sql**, dadurch wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen.|  
  
> [!NOTE]  
>  Unterstützung für die Verwendung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing wurde eingestellt. Angeben des Werts **Msmq** führt zu einer Warnung, und legen Replikation automatisch den Wert auf **Sql**.  
  
 *Für Oracle-Verlegern nicht unterstützt*.  
  
 [  **@add_to_active_directory =** ] **"*** hinzufügen**_**To_active_directory ***"**  
 Dieser Parameter wurde als veraltet markiert und wird nur zum Sicherstellen der Abwärtskompatibilität von Skripts unterstützt. Für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory ist das Hinzufügen von Veröffentlichungsinformationen nicht länger möglich.  
  
 [  **@logreader_job_name =** ] **"***Logreader_agent_name***"**  
 Der Name eines vorhandenen Agentauftrags. *Logreader_agent_name* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird nur angegeben, wenn der Protokolllese-Agent einen vorhandenen Auftrag verwendet, anstatt dass ein neuer Auftrag erstellt wird.  
  
 [  **@qreader_job_name =** ] **"***Queue_reader_agent_name***"**  
 Der Name eines vorhandenen Agentauftrags. *Queue_reader_agent_name* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird nur angegeben, wenn der Warteschlangenlese-Agent einen vorhandenen Auftrag verwendet, anstatt dass ein neuer Auftrag erstellt wird.  
  
 [  **@publisher =** ] **"***Publisher***"**  
 Gibt einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, beim Hinzufügen einer Veröffentlichung auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 [  **@allow_initialize_from_backup =** ] **"***Allow_initialize_from_backup***"**  
 Gibt an, ob Abonnenten ein Abonnement für diese Veröffentlichung über eine Sicherung anstelle einer Anfangsmomentaufnahme initialisieren können. *Allow_initialize_from_backup* ist **nvarchar(5)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**true**|Aktiviert die Initialisierung aus einer Sicherung.|  
|**false**|Deaktiviert die Initialisierung aus einer Sicherung.|  
|NULL (Standard)|Standardmäßig **"true"** für eine Veröffentlichung in einer Peer-zu-Peer-Replikationstopologie und **"false"** für alle anderen Veröffentlichungen.|  
  
 Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
> [!WARNING]  
>  Um fehlende Abonnentendaten zu vermeiden, wenn Sie **sp_addpublication** mit `@allow_initialize_from_backup = N'true'`verwenden, sollten Sie immer `@immediate_sync = N'true'`verwenden.  
  
 [  **@replicate_ddl =** ] *Replicate_ddl*  
 Gibt an, ob für die Veröffentlichung die Schemareplikation unterstützt wird. *Replicate_ddl* ist **Int**, hat den Standardwert **1** für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber und **0** für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber. **1** gibt an, dass die Anweisungen des Data Definition Language (DDL) wird auf dem Verleger ausgeführte repliziert werden, und **0** gibt an, dass die DDL-Anweisungen nicht repliziert werden. *Schemareplikation wird für Oracle-Verlegern nicht unterstützt.* Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Die *@replicate_ddl* Parameter wird berücksichtigt, wenn eine DDL-Anweisung eine Spalte hinzugefügt. Die *@replicate_ddl* Parameter wird ignoriert, wenn eine DDL-Anweisung ändert oder eine Spalte aus den folgenden Gründen löscht.  
  
-   Wenn eine Spalte gelöscht wird, muss die Sysarticlecolumns aktualisiert werden, um zu verhindern, dass neue DML-Anweisungen die gelöschte Spalte, die der Verteilungs-Agent fehlschlagen würde aufnehmen. Die *@replicate_ddl* Parameter wird ignoriert, da die Replikation immer die schemaänderung replizieren muss.  
  
-   Wenn eine Spalte geändert wird, hat sich möglicherweise der Quelldatentyp oder die NULL-Zulässigkeit geändert. Dies hat zur Folge, dass DML-Anweisungen einen Wert enthalten, der möglicherweise nicht mit der Tabelle beim Abonnenten kompatibel ist. Solche DML-Anweisungen können bewirken, dass der Verteilungs-Agent fehlschlägt. Die *@replicate_ddl* Parameter wird ignoriert, da die Replikation immer die schemaänderung replizieren muss.  
  
-   Wenn eine DDL-Anweisung eine neue Spalte hinzufügt, schließt Sysarticlecolumns nicht die neue Spalte. DML-Anweisungen versuchen nicht, Daten für die neue Spalte zu replizieren. Der Parameter wird berücksichtigt, da sowohl das Replizieren als auch das Nicht-Replizieren der DDL akzeptabel ist.  
  
 [  **@enabled_for_p2p =** ] **"***enabled_for_p2p***"**  
 Ermöglicht die Verwendung der Veröffentlichung in einer Peer-zu-Peer-Replikationstopologie. *enabled_for_p2p* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** gibt an, dass die Veröffentlichung Peer-zu-Peer-Replikation unterstützt. Beim Festlegen von *enabled_for_p2p* auf **"true"**, gelten die folgenden Einschränkungen:  
  
-   *Allow_anonymous* muss **"false"**.  
  
-   *allow_dts nicht* muss **"false"**.  
  
-   *Allow_initialize_from_backup* muss **"true"**.  
  
-   *Allow_queued_tran* muss **"false"**.  
  
-   *Allow_sync_tran* muss **"false"**.  
  
-   *Conflict_policy* muss **"false"**.  
  
-   *Independent_agent* muss **"true"**.  
  
-   *Repl_freq* muss **fortlaufende**.  
  
-   *Replicate_ddl* muss **1**.  
  
 Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [  **@publish_local_changes_only =** ] **"***Publish_local_changes_only***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] **"***Enabled_for_het_sub***"**  
 Aktiviert die Unterstützung von Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten durch die Veröffentlichung. *Enabled_for_het_sub* ist **nvarchar(5)** hat den Standardwert "false". Der Wert **"true"** bedeutet, dass die Veröffentlichung nicht-unterstützt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten. Wenn *Enabled_for_het_sub* ist **"true"**, gelten die folgenden Einschränkungen:  
  
-   *Allow_initialize_from_backup* muss **"false"**.  
  
-   *Allow_push* muss **"true"**.  
  
-   *Allow_queued_tran* muss **"false"**.  
  
-   *Allow_subscription_copy* muss **"false"**.  
  
-   *Allow_sync_tran* muss **"false"**.  
  
-   *Autogen_sync_procs* muss **"false"**.  
  
-   *Conflict_policy* muss NULL sein.  
  
-   *Enabled_for_internet* muss **"false"**.  
  
-   *enabled_for_p2p* muss **"false"**.  
  
-   *Ftp_address* muss NULL sein.  
  
-   *Ftp_subdirectory* muss NULL sein.  
  
-   *Ftp_password* muss NULL sein.  
  
-   *Pre_snapshot_script* muss NULL sein.  
  
-   *Post_snapshot_script* muss NULL sein.  
  
-   *Replicate_ddl* muss 0 sein.  
  
-   *Qreader_job_name* muss NULL sein.  
  
-   *Warteschlangentyp* muss NULL sein.  
  
-   *Sync_method* nicht **native** oder **gleichzeitige**.  
  
 Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 [  **@p2p_conflictdetection=** ] **"***p2p_conflictdetection***"**  
 Ermöglicht die Erkennung von Konflikten durch den Verteilungs-Agent, wenn die Veröffentlichung für die Peer-zu-Peer-Replikation aktiviert ist. *p2p_conflictdetection* ist **nvarchar(5)** hat den Standardwert "true". Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 Gibt eine ID für einen Knoten in einer Peer-zu-Peer-Topologie an. *p2p_originator_id* ist **Int**, hat den Standardwert NULL. Diese ID wird für die konflikterkennung verwendet, wenn *p2p_conflictdetection* auf "true" festgelegt ist. Geben Sie eine positive ungleich NULL ID, die in der Topologie noch nie verwendet wurde. Führen Sie eine Liste von IDs, die bereits verwendet wurden, [Sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
 [  **@p2p_continue_onconflict=** ] **"***p2p_continue_onconflict***"**  
 Legt fest, ob der Verteilungs-Agent nach Erkennung eines Konflikts die Verarbeitung von Änderungen fortsetzt. *p2p_continue_onconflict* ist **nvarchar(5)** hat den Standardwert "false".  
  
> [!CAUTION]  
>  Es wird empfohlen, den Standardwert FALSE zu verwenden. Wenn diese Option auf TRUE festgelegt wird, versucht der Verteilungs-Agent, die Datenkonvergenz in der Topologie herbeizuführen, indem die konfliktverursachende Zeile von dem Knoten mit der höchsten Absender-ID angewendet wird. Bei dieser Methode ist keine Konvergenz garantiert. Sie sollten sicherstellen, dass die Topologie nach der Erkennung eines Konflikts konsistent ist. Weitere Informationen finden Sie im Abschnitt "Konfliktbehandlung" unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [  **@allow_partition_switch=** ] **"***Allow_partition_switch***"**  
 Gibt an, ob ALTER TABLE…SWITCH-Anweisungen für die veröffentlichte Datenbank ausgeführt werden können. *Allow_partition_switch* ist **nvarchar(5)** hat den Standardwert "false". Weitere Informationen finden Sie unter [Replicate Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
 [  **@replicate_partition_switch=** ] **"***Replicate_partition_switch***"**  
 Gibt an, ob ALTER TABLE…SWITCH-Anweisungen, die für die veröffentlichte Datenbank ausgeführt werden, auf Abonnenten repliziert werden sollen. *Replicate_partition_switch* ist **nvarchar(5)** hat den Standardwert "false". Diese Option gilt nur, wenn *Allow_partition_switch* auf "true" festgelegt ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addpublication** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn mehrere Veröffentlichungen vorhanden sind, die veröffentlichen, der dasselbe Datenbankobjekt nur Veröffentlichungen mit einer *Replicate_ddl* Wert **1** repliziert, ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION und ALTER TRIGGER-DDL-Anweisungen. Eine ALTER TABLE DROP COLUMN DDL-Anweisung wird hingegen von allen Veröffentlichungen repliziert, die die gelöschte Spalte veröffentlichen.  
  
 Mit aktivierter DDL-Replikation (*Replicate_ddl* = **1**) nicht replizierende-DDL für eine Veröffentlichung ändert, für die Veröffentlichung [Sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) muss zuerst ausgeführt werden, zum Festlegen von *Replicate_ddl* auf **0**. Nachdem die nicht replizierenden DDL-Anweisungen ausgestellt wurden, [Sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) erneut ausgeführt werden können, um die DDL-Replikation wieder aktivieren.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addpublication**. Für Anmeldungen unter Verwendung der Windows-Authentifizierung muss in der Datenbank ein Konto vorhanden sein, das das zugehörige Windows-Benutzerkonto darstellt. Ein Benutzerkonto für eine Windows-Gruppe reicht in diesem Fall nicht aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [Sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [Sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
