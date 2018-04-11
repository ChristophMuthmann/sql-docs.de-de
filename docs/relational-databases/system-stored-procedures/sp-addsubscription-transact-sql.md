---
title: Sp_addsubscription (Transact-SQL) | Microsoft Docs
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords:
- sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 860f2f99457344167af9035d0a9ccc21eebc2577
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einer Veröffentlichung ein Abonnement hinzu und legt den Status des Abonnenten fest. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
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
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @publication=] '*publication*'  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [ @article=] '*article*'  
 Der Name des Artikels, für den die Veröffentlichung abonniert wird. *Artikel* ist **Sysname**, hat den Standardwert all. Wird all angegeben, wird allen Artikeln dieser Veröffentlichung ein Abonnement hinzugefügt. Nur die Werte all oder NULL werden für Oracle-Verleger unterstützt.  
  
 [ @subscriber=] '*subscriber*'  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @destination_db=] '*destination_db*'  
 Der Name der Zieldatenbank, in der die replizierten Daten gespeichert werden sollen. *Destination_db* ist **Sysname**, hat den Standardwert NULL. Wenn der Wert NULL, *Destination_db* auf den Namen der Veröffentlichungsdatenbank festgelegt ist. Für Oracle-Verleger *Destination_db* muss angegeben werden. Geben Sie den Wert (Standardziel) für einen nicht - SQL Server-Abonnenten für *Destination_db*.  
  
 [ @sync_type=] '*sync_type*'  
 Der Synchronisierungstyp des Abonnements. *Sync_type* ist **nvarchar(255)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|none|Der Abonnent besitzt bereits das Schema und die Ausgangsdaten für veröffentlichte Tabellen.<br /><br /> Hinweis: Diese Option ist veraltet. Verwenden Sie stattdessen replication support only.|  
|automatic (Standard)|Das Schema und die Ausgangsdaten für veröffentlichte Tabellen werden zuerst an den Abonnenten übertragen.|  
|replication support only|Stellt auf dem Abonnenten das automatische Generieren von benutzerdefinierten gespeicherten Prozeduren für Artikel und Trigger bereit, die ggf. das Aktualisieren von Abonnements unterstützen. Setzt voraus, dass der Abonnent bereits über das Schema und die Anfangsdaten für veröffentlichte Tabellen verfügt. Stellen Sie beim Konfigurieren einer Peer-zu-Peer-Transaktionsreplikationstopologie sicher, dass die Daten in allen Knoten der Topologie identisch sind. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).<br /><br /> *Für Abonnements von nicht - SQL Server-Veröffentlichungen unterstützt nicht.*|  
|initialize with backup|Das Schema und die Ausgangsdaten für veröffentlichte Tabellen werden von einer Sicherung der Veröffentlichungsdatenbank abgerufen. Es wird davon ausgegangen, dass der Abonnent über Zugriff auf eine Sicherung der Veröffentlichungsdatenbank verfügt. Der Speicherort des Typs Sicherung und Medien für die Sicherung werden angegeben, indem *Backupdevicename* und *Backupdevicetype*. Wenn Sie diese Option verwenden, muss eine Peer-zu-Peer-Transaktionsreplikationstopologie während der Konfiguration nicht deaktiviert werden.<br /><br /> *Für Abonnements von nicht - SQL Server-Veröffentlichungen unterstützt nicht.*|  
|initialize from lsn|Wird verwendet, wenn Sie einer Peer-zu-Peer-Transaktionsreplikationstopologie einen Knoten hinzufügen. Wird mit @subscriptionlsn verwendet, um sicherzustellen, dass alle relevanten Transaktionen auf den neuen Knoten repliziert werden. Setzt voraus, dass der Abonnent bereits über das Schema und die Anfangsdaten für veröffentlichte Tabellen verfügt. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
> [!NOTE]  
>  Systemtabellen und Daten werden immer übertragen.  
  
 [ @status=] '*status*'  
 Der Abonnementstatus. *Status* ist **Sysname**, hat den Standardwert NULL. Wenn dieser Parameter nicht explizit festgelegt wird, wird er von der Replikation automatisch auf einen der folgenden Werte festgelegt.  
  
|Wert|Description|  
|-----------|-----------------|  
|active|Das Abonnement wird initialisiert und ist bereit, Änderungen anzunehmen. Diese Option wird festgelegt, wenn der Wert der *Sync_type* ist "none, Initialize mit Backup oder Replication Support only".|  
|subscribed|Das Abonnement muss initialisiert werden. Diese Option wird festgelegt, wenn der Wert der *Sync_type* erfolgt automatisch.|  
  
 [ @subscription_type=] '*subscription_type*'  
 Ist der Typ des Abonnements. *Subscription_type* ist **nvarchar(4)**, hat den Standardwert Push. Mögliche Werte sind push und pull. Der Verteilungs-Agents von Pushabonnements befinden, auf dem Verteiler und die Verteilungs-Agents von Pullabonnements befinden, auf dem Abonnenten. *Subscription_type* können Pull sein, um ein benanntes Pullabonnement zu erstellen, mit dem Verleger bekannt ist. Weitere Informationen finden Sie unter [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md).  
  
> [!NOTE]  
>  Für anonyme Abonnements ist diese gespeicherte Prozedur nicht erforderlich.  
  
 [ @update_mode=] '*update_mode*'  
 Ist der Typ des Updates. *Update_mode* ist **nvarchar(30)**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|read only (Standard)|Das Abonnement ist schreibgeschützt. Änderungen am Abonnenten werden nicht an den Verleger gesendet.|  
|sync tran|Aktiviert die Unterstützung für das sofortige Aktualisieren von Abonnements. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|queued tran|Aktiviert das verzögerte Aktualisieren über eine Warteschlange für das Abonnement. Daten können auf dem Abonnenten geändert werden; die Änderungen werden in einer Warteschlange gespeichert und an den Verleger weitergegeben. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|failover|Aktiviert das sofortige Aktualisieren für das Abonnement, wobei als Failover das verzögerte Aktualisieren über eine Warteschlange verwendet wird. Daten können auf dem Abonnenten geändert werden; die Änderungen werden sofort an den Verleger weitergegeben. Wenn der Verleger und der Abonnent nicht verbunden sind, kann der Updatemodus geändert werden, damit Datenänderungen auf dem Abonnenten in einer Warteschlange gespeichert werden, bis Abonnent und Verleger erneut verbunden sind. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|queued failover|Ermöglicht das Abonnement als Update über eine Warteschlange, mit der Möglichkeit des Wechsels zum sofortigen Updatemodus. Daten können auf dem Abonnenten geändert und in einer Warteschlange gespeichert werden, bis eine Verbindung zwischen dem Abonnenten und dem Verleger hergestellt wird. Wenn eine kontinuierliche Verbindung hergestellt wird, kann der Updatemodus in den sofortigen Updatemodus geändert werden. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
  
 Beachten Sie, dass die Werte Synctran und queued Tran nicht zulässig sind, wenn die abonnierte Veröffentlichung DTS zulässt.  
  
 [ @loopback_detection=] '*loopback_detection*'  
 Gibt an, ob der Verteilungs-Agent Transaktionen, die vom Abonnenten stammen, zurück an den Abonnenten sendet. *Loopback_detection* ist **nvarchar(5)**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|true|Der Verteilungs-Agent sendet Transaktionen des Abonnenten nicht an den Abonnenten zurück. Wird bei der bidirektionalen Transaktionsreplikation verwendet. Weitere Informationen finden Sie unter [Bidirektionale Transaktionsreplikation](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|false|Der Verteilungs-Agent sendet Transaktionen des Abonnenten an den Abonnenten zurück.|  
|NULL (Standard)|Wird für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten automatisch auf true und für einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten auf false festgelegt.|  
  
 [ @frequency_type=] *frequency_type*  
 Die Häufigkeit für die Zeitplanung des Verteilungstasks. *Frequency_type* ist "Int", und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|1|Einmal|  
|2|Bedarfsgesteuert|  
|4|Täglich|  
|8|Wöchentlicher Zeitplan|  
|16|Monatlicher Zeitplan|  
|32|Monatlich, relativ|  
|64 (Standard)|Autostart|  
|128|Wiederholt|  
  
 [ @frequency_interval=] *frequency_interval*  
 Ist der Wert der Häufigkeit festgelegt, die durch Anwenden *Frequency_type*. *Frequency_interval* ist **Int**, hat den Standardwert NULL.  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 Das Datum des Verteilungs-Agents. Dieser Parameter wird verwendet, wenn *Frequency_type* auf 32 (monatlich, relativ) festgelegt wird. *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|1|Erster|  
|2|Zweimal|  
|4|Dritter|  
|8|Vierter|  
|16|Letzter|  
|NULL (Standard)||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 Wird von verwendete Wiederholungsfaktor *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert NULL.  
  
 [ @frequency_subday=] *frequency_subday*  
 Die Häufigkeit (in Minuten) für die erneute geplante Ausführung während des definierten Zeitraums. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|1|Einmal|  
|2|Zweimal|  
|4|Minute|  
|8|Hour|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 Das Intervall für *Frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert NULL.  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 Die Tageszeit, zu der der Verteilungs-Agent zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 Die Tageszeit, ab der der Verteilungs-Agent nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [ @active_start_date=] *active_start_date*  
 Das Datum, an dem der Verteilungs-Agent zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert NULL.  
  
 [ @active_end_date=] *active_end_date*  
 Das Datum, ab dem der Verteilungs-Agent nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date* ist **Int**, hat den Standardwert NULL.  
  
 [ @optional_command_line=] '*optional_command_line*'  
 Die optional auszuführende Befehlszeile. *Der Standardwert* ist **nvarchar(4000)**, hat den Standardwert NULL.  
  
 [ @reserved=] '*reserved*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 Gibt an, ob das Abonnement über synchronisiert werden kann [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronisierungsverwaltung von Windows. *Enabled_for_syncmgr* ist **nvarchar(5)**, hat den Standardwert "false". Mit FALSE wird das Abonnement nicht bei der Windows-Synchronisierungsverwaltung registriert. Mit TRUE wird das Abonnement bei der Windows-Synchronisierungsverwaltung registriert und kann synchronisiert werden, ohne [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zu starten. Diese Option wird für Oracle-Verleger nicht unterstützt.  
  
 [ @offloadagent=] '*Remote_agent_activation*"  
 Gibt an, dass eine Remoteaktivierung der Momentaufnahme möglich ist. *Remote_agent_activation* ist **Bit** hat den Standardwert 0.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird nur noch bereitgestellt, um Abwärtskompatibilität von Skripts sicherzustellen.  
  
 [ @offloadserver= ] '*remote_agent_server_name*'  
 Gibt den Netzwerknamen des Servers an, der für die Remoteaktivierung verwendet werden soll. *Remote_agent_server_name*ist **Sysname**, hat den Standardwert NULL.  
  
 [ @dts_package_name= ] '*dts_package_name*'  
 Gibt den Namen des DTS-Pakets (Data Transformation Services) an. *Dts_package_name* ist ein **Sysname** hat den Standardwert NULL. Um z. B. ein Paket namens DTSPub_Package anzugeben, wird der Parameter `@dts_package_name = N'DTSPub_Package'` verwendet. Dieser Parameter ist für Pushabonnements verfügbar. Verwenden Sie sp_addpullsubscription_agent, um einem Pullabonnement DTS-Paketinformationen hinzuzufügen.  
  
 [ @dts_package_password= ] '*dts_package_password*'  
 Gibt gegebenenfalls das Kennwort des Pakets an. *Dts_package_password* ist **Sysname** hat den Standardwert NULL.  
  
> [!NOTE]  
>  Sie müssen ein Kennwort angeben, wenn *Dts_package_name* angegeben ist.  
  
 [ @dts_package_location=] '*Dts_package_location*"  
 Gibt den Paketspeicherort an. *Dts_package_location* ist ein **nvarchar(12)**, hat den Standardwert des VERTEILERS. Der Speicherort des Pakets kann distributor oder subscriber sein.  
  
 [ @distribution_job_name= ] '*distribution_job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher= ] '*publisher*'  
 Gibt einen nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht angegeben werden, für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 [ @backupdevicetype= ] '*backupdevicetype*'  
 Gibt den Sicherungsmedientyp an, der beim Initialisieren eines Abonnenten von einer Sicherung verwendet wird. *Backupdevicetype* ist **nvarchar(20)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|logical (Standard)|Das Sicherungsmedium ist ein logisches Medium.|  
|disk|Das Sicherungsmedium ist ein Laufwerk.|  
|tape|Das Sicherungsmedium ist ein Bandlaufwerk.|  
  
 *Backupdevicetype* wird nur verwendet, wenn *Sync_method*auf Initialize_with_backup festgelegt ist.  
  
 [ @backupdevicename= ] '*backupdevicename*'  
 Gibt den Namen des Sicherungsmediums an, das beim Initialisieren eines Abonnenten von einer Sicherung verwendet wird. *Backupdevicename* ist **nvarchar(1000)**, hat den Standardwert NULL.  
  
 [ @mediapassword= ] '*mediapassword*'  
 Gibt ein Kennwort für den Mediensatz an, falls beim Formatieren des Mediums ein Kennwort festgelegt wurde. *MEDIAPASSWORD* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password= ] '*password*'  
 Gibt ein Kennwort für die Sicherung an, falls beim Erstellen der Sicherung ein Kennwort festgelegt wurde. *Kennwort*ist **Sysname**, hat den Standardwert NULL.  
  
 [ @fileidhint= ] *fileidhint*  
 Identifiziert einen Ordnungswert des wiederherzustellenden Sicherungssatzes. *Fileidhint* ist **Int**, hat den Standardwert NULL.  
  
 [ @unload= ] *unload*  
 Gibt an, ob ein Datensicherungsmedium nach Abschluss der Initialisierung von der Sicherung entladen werden soll. *Entladen* ist **Bit**, hat den Standardwert 1. 1 gibt an, dass das Band entladen werden soll. *Entladen* wird nur verwendet, wenn *Backupdevicetype* Band ist.  
  
 [ @subscriptionlsn= ] *subscriptionlsn*  
 Gibt die Protokollfolgenummer (LSN, Log Sequence Number) an, bei der ein Abonnement beginnen soll, Änderungen an einen Knoten in einer Peer-zu-Peer-Transaktionsreplikationstopologie zu übermitteln. Verwendet eine @sync_type Wert Initialize from Lsn, um sicherzustellen, dass alle relevanten Transaktionen auf einem neuen Knoten repliziert werden. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [ @subscriptionstreams= ] *subscriptionstreams*  
 Die Anzahl zulässiger Verbindungen pro Verteilungs-Agent, um Änderungsbatches parallel auf einen Abonnenten anzuwenden, während viele Transaktionsmerkmale beibehalten werden, die bei Verwendung eines einzigen Threads vorhanden sind. *Subscriptionstreams* ist **"tinyint"**, hat den Standardwert NULL. Mögliche Werte zwischen 1 und 64 werden unterstützt. Dieser Parameter wird für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten, Oracle-Verleger oder Peer-zu-Peer-Abonnements nicht unterstützt. Bei Verwendung von subscriptionstreams werden der msreplication_subscriptions-Tabelle zusätzliche Zeilen (eine pro Datenstrom) hinzugefügt, wobei die agent_id auf NULL festgelegt ist.  
  
> [!NOTE]  
>  subscriptionstreams [!INCLUDE[tsql](../../includes/tsql-md.md)]kann nicht für Artikel verwendet werden, die für die Übermittlung von  konfiguriert sind. Um subscriptionstreams zu verwenden, konfigurieren Sie Artikel stattdessen für die Übermittlung von Aufrufen gespeicherter Prozeduren.  
  
 [ @subscriber_type=] *subscriber_type*  
 Der Typ des Abonnenten. *subscriber_type kann* ist **"tinyint"**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|0 (Standard)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten|  
|1|ODBC-Datenquellenserver|  
|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet-Datenbank|  
|3|OLE DB-Anbieter|  
  
 [ @memory_optimized=] *memory_optimized*  
 Gibt an, dass das Abonnement von speicheroptimierten Tabellen unterstützt. *Memory_optimized* ist **Bit**, bei denen 1 gleich true (das Abonnement unterstützt von speicheroptimierten Tabellen).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_addsubscription wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn sp_addsubscription von einem Mitglied der festen Serverrolle sysadmin ausgeführt wird, um ein Pushabonnement zu erstellen, wird der Auftrag des Verteilungs-Agents implizit erstellt und unter dem Konto des SQL Server-Agent-Diensts ausgeführt. Es wird empfohlen, Sie führen [Sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) und geben Sie die Anmeldeinformationen eines anderen, Agent-spezifischen Windows-Kontos für @job_login und @job_password. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 sp_addsubscription hindert ODBC- und OLE DB-Abonnenten am Zugriff auf folgende Veröffentlichungen:  
  
-   Erstellt wurden, mit dem systemeigenen *Sync_method* im Aufruf [Sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
-   Artikel, die für die Veröffentlichung mit hinzugefügten enthalten die [Sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) gespeicherten Prozedur ein *Pre_creation_cmd* Parameterwert 3 (abschneiden).  
  
-   Fehler beim Festlegen *Update_mode* auf sync Tran.  
  
-   Veröffentlichungen, bei denen ein Artikel für die Verwendung parametrisierter Anweisungen konfiguriert ist.  
  
 Darüber hinaus, wenn eine Veröffentlichung erstellt wurden die *Allow_queued_tran* option Gruppe auf "true" (wodurch Änderungen auf dem Abonnenten queuing, bis sie auf dem Verleger angewendet werden können), die Timestamp-Spalte in einem Artikel als ausgegeben**Zeitstempel**, und Änderungen für die betreffende Spalte an den Abonnenten gesendet werden. Der Abonnent generiert und aktualisiert den Wert der timestamp-Spalte. Für einen ODBC- oder OLE DB-Abonnenten, Sp_addsubscription schlägt fehl, wenn versucht wird, eine Veröffentlichung abonnieren, die hat *Allow_queued_tran* legen Sie auf "true" und die Artikel mit Timestamp-Spalten.  
  
 Wenn ein Abonnement ein DTS-Paket nicht verwendet, kann nicht abonniert für eine Veröffentlichung, die festgelegt wird, um *Allow_transformable_subscriptions*. Wenn die Tabelle der Veröffentlichung für ein DTS-Abonnement und ein Nicht-DTS-Abonnement repliziert werden muss, müssen zwei separate Veröffentlichungen erstellt werden: eine für jeden Abonnementtyp.  
  
 Bei Auswahl der **sync_type** -Optionen *replication support only*, *initialize with backup*oder *initialize from lsn*muss der Protokolllese-Agent ausgeführt werden, nachdem **sp_addsubscription**ausgeführt wurde, damit die festgelegten Skripts in die Verteilungsdatenbank geschrieben werden. Der Protokolllese-Agent muss unter einem Konto ausgeführt werden, das Mitglied der festen Serverrolle **sysadmin** ist. Wenn die **sync_type** -Option auf *Automatic*festgelegt wird, sind keine speziellen Aktionen für den Protokollleser-Agent erforderlich.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle sysadmin oder der festen Datenbankrolle db_owner können sp_addsubscription ausführen. Für Pullabonnements können Benutzer, deren Anmeldename in der Veröffentlichungszugriffsliste eingetragen ist, sp_addsubscription ausführen.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
