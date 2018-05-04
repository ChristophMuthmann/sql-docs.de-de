---
title: Sp_changemergepullsubscription (Transact-SQL) | Microsoft Docs
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
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 31e745e3ab75ae237a440db10c05b3ed4cd7d29e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften des Mergepullabonnements. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert %.  
  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher*ist **Sysname**, hat den Standardwert %.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db*ist **Sysname**, hat den Standardwert %.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Der Name der zu ändernden Eigenschaft. *Eigenschaft* ist **Sysname**, und kann einen der Werte in der Tabelle.  
  
 [  **@value=**] **"***Wert***"**  
 Ist der neue Wert für die angegebene Eigenschaft. *Wert*ist **nvarchar(255)**, und kann einen der Werte in der Tabelle.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Der Speicherort, in der momentaufnahmeordner gespeichert ist, wenn der Speicherort am Standardspeicherort außer oder darüber liegt.|  
|**description**||Die Beschreibung dieses Mergepullabonnements.|  
|**Verteiler**||Name des Verteilers.|  
|**distributor_login**||Die Anmelde-ID, die auf dem Verteiler für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet wird.|  
|**distributor_password**||Für auf dem Verteiler verwendete Kennwort (verschlüsselt) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**distributor_security_mode**|**1**|Verwendet die Windows-Authentifizierung beim Herstellen der Verbindung mit dem Verteiler.|  
||**0**|Verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung beim Herstellen der Verbindung mit dem Verteiler.|  
|**dynamic_snapshot_location**||Pfad zu dem Ordner, in dem die Momentaufnahmedateien gespeichert sind.|  
|**ftp_address**||Nur aus Gründen der Abwärtskompatibilität verfügbar. Ist die Netzwerkadresse des Protokolls FTP (File Transfer)-Diensts für den Verteiler.|  
|**ftp_login**||Nur aus Gründen der Abwärtskompatibilität verfügbar. Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**ftp_password**||Nur aus Gründen der Abwärtskompatibilität verfügbar. Das Benutzerkennwort, mit dem eine Verbindung zum FTP-Dienst hergestellt wird.|  
|**ftp_port**||Nur aus Gründen der Abwärtskompatibilität verfügbar. Die Anschlussnummer des FTP-Diensts für den Verteiler.|  
|**Hostname**||Gibt einen Wert für HOST_NAME() an, wenn diese Funktion in der WHERE-Klausel eines Joinfilters oder einer logischen Datensatzbeziehung verwendet wird.|  
|**sich**||Der Anmeldename, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_password**||Das Kennwort für den Anmeldenamen, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_security_mode**|**1**|Verwendet die Windows-Authentifizierung, wenn eine Verbindung mit dem Webserver hergestellt wird, der die Websynchronisierung hostet.|  
||**0**|Verwendet die Standardauthentifizierung, wenn eine Verbindung mit dem Webserver hergestellt wird, der die Websynchronisierung hostet.|  
|**internet_timeout**||Zeit in Sekunden, bevor eine Anforderung für eine Websynchronisierung abläuft.|  
|**internet_url**||URL, die den Speicherort der replikationsüberwachung für die websynchronisierung darstellt.|  
|**merge_job_login**||Anmeldename für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**merge_job_password**||Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**priority**||Verfügbar nur für Abwärtskompatibilität; Führen Sie [Sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) auf dem Verleger stattdessen zum Ändern der Priorität eines Abonnements.|  
|**publisher_login**||Auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendete Anmelde-ID.|  
|**publisher_password**||Das Kennwort (verschlüsselt), das auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet wird.|  
|**publisher_security_mode**|**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Verleger.|  
||**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Verleger.|  
||**2**|Synchronisierungstrigger verwenden einen statischen **Sysservers** -Eintrag für Remoteprozeduraufruf (RPC) und auf dem Verleger muss definiert werden, der **Sysservers** -Tabelle als Remoteserver oder Verbindungsserver.|  
|**sync_type**|**Automatisch**|Das Schema und die Ausgangsdaten für veröffentlichte Tabellen werden zuerst an den Abonnenten übertragen.|  
||**Keine**|Der Abonnent verfügt bereits über das Schema und die Ausgangsdaten für veröffentlichte Tabellen; Systemtabellen und Daten werden immer übertragen.|  
|**use_ftp**|**true**|FTP wird anstelle des normalen Protokolls zum Abrufen von Momentaufnahmen verwendet.|  
||**false**|Das normale Protokoll wird zum Abrufen von Momentaufnahmen verwendet.|  
|**use_web_sync**|**true**|Das Abonnement kann über HTTP synchronisiert werden.|  
||**false**|Das Abonnement kann über HTTP nicht synchronisiert werden.|  
|**use_interactive_resolver**|**true**|Der interaktive Konfliktlöser wird während der Konfliktlösung verwendet.|  
||**false**|Der interaktive Konfliktlöser wird nicht verwendet.|  
|**working_directory**||Der vollqualifizierte Pfad zum Verzeichnis, in das die Momentaufnahmedateien mithilfe von FTP übertragen werden, wenn diese Option angegeben ist.|  
|NULL (Standard)||Gibt die Liste der unterstützten Werte für *Eigenschaft*.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changemergepullsubscription** wird bei der Mergereplikation verwendet.  
  
 Der aktuelle Server und die aktuelle Datenbank werden als Abonnent und Abonnentendatenbank angenommen.  
  
 Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changemergepullsubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
