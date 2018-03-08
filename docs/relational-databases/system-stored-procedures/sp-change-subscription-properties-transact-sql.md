---
title: Sp_change_subscription_properties (Transact-SQL) | Microsoft Docs
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
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords: sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fe61cfc2088b75e2ab1af2c457073ad723dd7f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert Informationen für Pullabonnements. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=**] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher_db=**] **"***Publisher_db***"**  
 Der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Die Eigenschaft, die geändert werden soll. *Eigenschaft* ist **Sysname**.  
  
 [  **@value=**] **"***Wert***"**  
 Ist der neue Wert der Eigenschaft. *Wert* ist **nvarchar(1000)**, hat keinen Standardwert.  
  
 [  **@publication_type =** ] *Publication_type*  
 Gibt den Replikationstyp der Veröffentlichung an. *Publication_type* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Veröffentlichungstyp|  
|-----------|----------------------|  
|**0**|Transaktion|  
|**1**|Momentaufnahme|  
|**2**|Merge|  
|NULL (Standard)|Die Replikation bestimmt den Veröffentlichungstyp. Da die gespeicherte Prozedur mehrere Tabellen durchsuchen muss, ist diese Option langsamer, als wenn der genaue Veröffentlichungstyp angegeben wird.|  
  
 Diese Tabelle beschreibt die Eigenschaften von Artikeln und die Werte für diese Eigenschaften.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Gibt den Speicherort des anderen Ordners für die Momentaufnahme an. Wenn NULL festgelegt ist, werden die Momentaufnahmedateien aus dem vom Verleger angegebenen Standardspeicherort übernommen.|  
|**distrib_job_login**||Anmeldename für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**distrib_job_password**||Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**distributor_login**||Verteilerbenutzername.|  
|**distributor_password**||Verteilerkennwort.|  
|**distributor_security_mode**|**1**|Verwendet die Windows-Authentifizierung beim Herstellen der Verbindung mit dem Verteiler.|  
||**0**|Verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung beim Herstellen der Verbindung mit dem Verteiler.|  
|**dts_package_name**||Gibt den Namen des SQL Server 2000 DTS-Pakets (Data Transformation Services) an. Dieser Wert kann nur bei einer Transaktions- oder Momentaufnahmeveröffentlichung angegeben werden.|  
|**dts_package_password**||Gibt das Kennwort für das Paket an. *Dts_package_password* ist **Sysname** hat den Standardwert NULL, der gibt an, dass die Kennworteigenschaft bleiben unverändert.<br /><br /> Hinweis: Ein DTS-Paket muss ein Kennwort verfügen.<br /><br /> Dieser Wert kann nur bei einer Transaktions- oder Momentaufnahmeveröffentlichung angegeben werden.|  
|**dts_package_location**||Der Speicherort, in dem das DTS-Paket gespeichert ist. Dieser Wert kann nur bei einer Transaktions- oder Momentaufnahmeveröffentlichung angegeben werden.|  
|**dynamic_snapshot_location**||Gibt den Pfad zum Ordner an, in dem die Momentaufnahmedateien gespeichert werden. Dieser Wert kann nur bei einer Mergeveröffentlichung angegeben werden.|  
|**ftp_address**||Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_login**||Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_password**||Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**ftp_port**||Nur aus Gründen der Abwärtskompatibilität beibehalten|  
|**Hostname**||Hostname, der beim Herstellen der Verbindung mit dem Verleger verwendet wird.|  
|**sich**||Der Anmeldename, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_password**||Das vom Merge-Agent verwendete Kennwort für die Herstellung einer Verbindung mit dem Webserver, der die Websynchronisierung hostet, wobei die Verbindung über die Standardauthentifizierung erfolgt.|  
|**internet_security_mode**|**1**|Verwendet für die Websynchronisierung die integrierte Windows-Authentifizierung. Wir empfehlen, bei der Websynchronisierung die Standardauthentifizierung zu verwenden. Weitere Informationen finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Verwendet für die Websynchronisierung die Standardauthentifizierung.<br /><br /> Hinweis: Die websynchronisierung erfordert einer SSL-Verbindungs mit dem Webserver.|  
|**internet_timeout**||Zeit in Sekunden, bevor eine Anforderung für eine Websynchronisierung abläuft.|  
|**internet_url**||URL, die den Speicherort der replikationsüberwachung für die websynchronisierung darstellt.|  
|**merge_job_login**||Anmeldename für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**merge_job_password**||Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**publisher_login**||Der Benutzername des Verlegers. Ändern von *Publisher_login* wird nur für Abonnements von mergeveröffentlichungen unterstützt.|  
|**publisher_password**||Das Kennwort des Verlegers. Ändern von *Publisher_password* wird nur für Abonnements von mergeveröffentlichungen unterstützt.|  
|**publisher_security_mode**|**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Verleger. Ändern von *Publisher_security_mode* wird nur für Abonnements von mergeveröffentlichungen unterstützt.|  
||**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Verleger.|  
|**use_ftp**|**true**|Verwendet FTP anstelle des regulären Protokolls zum Abrufen von Momentaufnahmen.|  
||**false**|Verwendet das reguläre Protokoll zum Abrufen von Momentaufnahmen.|  
|**use_web_sync**|**true**|Aktiviert die Websynchronisierung.|  
||**false**|Deaktiviert die Websynchronisierung.|  
|**working_directory**||Name des Arbeitsverzeichnisses für die temporäre Speicherung von Daten und Schemadateien für die Veröffentlichung, wenn für das Übertragen von Momentaufnahmedateien FTP (File Transfer Protocol) verwendet wird.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_change_subscription_properties** wird für alle Replikationstypen verwendet.  
  
 **Sp_change_subscription_properties** für Pullabonnements verwendet wird.  
  
 Für Oracle-Verleger den Wert der *Publisher_db* wird ignoriert, da Oracle nur eine Datenbank pro Serverinstanz zulässt.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Sp_addmergepullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Sp_addmergepullsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [Sp_addpullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [Sp_addpullsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
