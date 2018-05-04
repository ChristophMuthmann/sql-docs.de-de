---
title: Sp_helpmergepullsubscription (Transact-SQL) | Microsoft Docs
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
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 905ead01709a932639f72e874f1246228f2f9c21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Pullabonnements zurück, die auf einem Abonnenten vorhanden sind. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>Argument  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**. Wenn *Veröffentlichung* ist **%**, Informationen zu allen mergeveröffentlichungen und Mergeabonnements in der aktuellen Datenbank zurückgegeben.  
  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher*ist **Sysname**, hat den Standardwert **%**.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db*ist **Sysname**, hat den Standardwert **%**.  
  
 [  **@subscription_type=**] **"***Subscription_type***"**  
 Gibt an, ob Pullabonnements angezeigt werden. *Subscription_type*ist **nvarchar(10)**, hat den Standardwert **'Pull'**. Gültige Werte sind **'Push'**, **'Pull'**, oder **'both'**.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|Name des Abonnements.|  
|**Veröffentlichung**|**sysname**|Name der Veröffentlichung.|  
|**publisher**|**sysname**|Name des Verlegers.|  
|**publisher_db**|**sysname**|Name der Verlegerdatenbank.|  
|**subscriber**|**sysname**|Der Name des Abonnenten.|  
|**subscription_db**|**sysname**|Name der Abonnementdatenbank.|  
|**status**|**int**|Abonnementstatus:<br /><br /> **0** = inaktives Abonnement<br /><br /> **1** = aktives Abonnement<br /><br /> **2** = gelöschtes Abonnement<br /><br /> **3** = getrenntes Abonnement<br /><br /> **4** = angefügtes Abonnement<br /><br /> **5** = Abonnement wurde für die erneute Initialisierung mit Upload markiert<br /><br /> **6** = Fehler bei der das Abonnement Anfügen<br /><br /> **7** = Abonnement aus einer Sicherung wiederhergestellt|  
|**subscriber_type kann**|**int**|Typ des Abonnenten:<br /><br /> **1** = global<br /><br /> **2** = lokal<br /><br /> **3** = anonym|  
|**subscription_type**|**int**|Typ des Abonnements:<br /><br /> **0** = Push<br /><br /> **1** = Pullabonnement<br /><br /> **2** = anonym|  
|**priority**|**float(8)**|Abonnementpriorität. Der Wert muss kleiner als **100,00**.|  
|**sync_type**|**tinyint**|Synchronisierungsart des Abonnements:<br /><br /> **1** = automatisch<br /><br /> **2** = Snapshot wird nicht verwendet.|  
|**description**|**nvarchar(255)**|Kurze Beschreibung des Pullabonnements.|  
|**Der Standardwert**|**Binary(16)**|Auftrags-ID des Merge-Agents.|  
|**enabled_for_syncmgr**|**int**|Zeigt an, ob das Abonnement über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] synchronisiert werden kann.|  
|**last_updated**|**nvarchar(26)**|Zeitpunkt, zu dem der Merge-Agent das Abonnement zuletzt erfolgreich synchronisiert hat.|  
|**publisher_login**|**sysname**|Anmeldename des Verlegers.|  
|**publisher_password**|**sysname**|Kennwort des Verlegers.|  
|**publisher_security_mode**|**int**|Gibt den Sicherheitsmodus des Verlegers an:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**Verteiler**|**sysname**|Name des Verteilers.|  
|**distributor_login**|**sysname**|Anmeldename des Verteilers.|  
|**distributor_password**|**sysname**|Das Verteilerkennwort.|  
|**distributor_security_mode**|**int**|Gibt den Sicherheitsmodus des Verteilers an:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**ftp_address**|**sysname**|Nur aus Gründen der Abwärtskompatibilität verfügbar. Ist die Netzwerkadresse des File Transfer Protocol (FTP) Service, für den Verteiler.|  
|**ftp_port**|**int**|Nur aus Gründen der Abwärtskompatibilität verfügbar. Die Anschlussnummer des FTP-Diensts für den Verteiler.|  
|**ftp_login**|**sysname**|Nur aus Gründen der Abwärtskompatibilität verfügbar. Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**ftp_password**|**sysname**|Nur aus Gründen der Abwärtskompatibilität verfügbar. Das Benutzerkennwort, mit dem eine Verbindung zum FTP-Dienst hergestellt wird.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Der Speicherort des Momentaufnahmeordners, wenn dies nicht der standardmäßige Speicherort ist oder ein zusätzlicher Speicherort zum Standardspeicherort vorhanden ist.|  
|**working_directory**|**nvarchar(255)**|Der vollqualifizierte Pfad zum Verzeichnis, in das die Momentaufnahmedateien mithilfe von FTP übertragen werden, wenn diese Option angegeben ist.|  
|**use_ftp**|**bit**|Das Abonnement abonniert die Veröffentlichung über die konfigurierten Internet- und FTP-Adressierungseigenschaften. Wenn **0**, Abonnement nicht FTP verwendet. Wenn **1**, Abonnement wird mithilfe von FTP.|  
|**offload_agent**|**bit**|Gibt an, ob eine Remotaktivierung und -ausführung der Momentaufnahme möglich ist. Wenn **0**, der Agent kann nicht remote aktiviert werden.|  
|**offload_server**|**sysname**|Name des Servers, der für die Remoteaktivierung verwendet wird.|  
|**use_interactive_resolver**|**int**|Gibt zurück, ob der interaktive Konfliktlöser während der Konfliktlösung verwendet wird. Wenn **0**, der interaktive Konfliktlöser wird nicht verwendet.|  
|**subid**|**uniqueidentifier**|ID des Abonnenten.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Der Pfad zu dem Ordner, in dem die Momentaufnahmedateien gespeichert werden.|  
|**last_sync_status**|**int**|Synchronisierungsstatus:<br /><br /> **1** = wird gestartet<br /><br /> **2** = war erfolgreich<br /><br /> **3** = wird ausgeführt<br /><br /> **4** = im Leerlauf<br /><br /> **5** = Wiederholung nach einem vorherigen Fehler<br /><br /> **6** = Fehler<br /><br /> **7** = Fehler bei Überprüfung<br /><br /> **8** = Überprüfung erfolgreich<br /><br /> **9** = Herunterfahren wurde angefordert|  
|**last_sync_summary**|**sysname**|Beschreibung der letzten Synchronisierungsergebnisse.|  
|**use_web_sync**|**bit**|Gibt an, ob das Abonnement über HTTPS synchronisiert werden kann ein Wert von **1** bedeutet, dass dieses Feature aktiviert ist.|  
|**internet_url**|**nvarchar(260)**|URL, die den Speicherort der replikationsüberwachung für die websynchronisierung darstellt.|  
|**sich**|**nvarchar(128)**|Der Anmeldename, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_password**|**nvarchar(524)**|Das Kennwort für den Anmeldenamen, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_security_mode**|**int**|Der verwendete Authentifizierungsmodus beim Herstellen einer Verbindung mit dem Webserver, der die Websynchronisierung hostet. Der Wert **1** bedeutet, dass Windows-Authentifizierung und den Wert **0** bedeutet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**internet_timeout**|**int**|Zeit in Sekunden, bevor eine Anforderung für eine Websynchronisierung abläuft.|  
|**Hostname**|**nvarchar(128)**|Gibt einen überladenen Wert für [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) Wenn diese Funktion in der WHERE-Klausel eines parametrisierten Zeilenfilters verwendet wird.|  
|**job_login**|**nvarchar(512)**|Ist das Windows-Konto unter dem der Merge-Agent ausgeführt wird, der zurückgegeben wird, im Format *Domäne*\\*Benutzername*.|  
|**job_password**|**sysname**|Aus Sicherheitsgründen den Wert "**\*\*\*\*\*\*\*\*\*\***" ist immer zurückgegeben.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpmergepullsubscription** wird bei der Mergereplikation verwendet. Im Resultset, das Datum im zurückgegebenen **Last_updated** formatiert als *YYYYMMDD ss.fff*.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle "" und die **Db_owner** feste Datenbankrolle können ausführen **Sp_helpmergepullsubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [Sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
