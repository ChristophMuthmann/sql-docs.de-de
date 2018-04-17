---
title: Sp_helpsubscription_properties (Transact-SQL) | Microsoft Docs
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
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78637041673509151652fd1e6d4125c8e41e2aa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft Sicherheitsinformationen aus der [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) Tabelle. Diese gespeicherte Prozedur wird auf dem Abonnenten ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert **%**, Informationen über alle Verleger zurückgegeben.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert **%**, Informationen über alle Verlegerdatenbanken zurückgegeben.  
  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**, womit Informationen zu allen Veröffentlichungen zurückgegeben.  
  
 [  **@publication_type=**] *Publication_type*  
 Ist der Typ der Veröffentlichung. *Publication_type* ist **Int**, hat den Standardwert NULL. Wenn angegeben, *Publication_type* muss eines der folgenden Werte sein:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Transaktionsveröffentlichung|  
|**1**|Momentaufnahmeveröffentlichung|  
|**2**|Mergeveröffentlichung|  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Name des Verlegers.|  
|**publisher_db**|**sysname**|Name der Verlegerdatenbank.|  
|**Veröffentlichung**|**sysname**|Name der Veröffentlichung.|  
|**publication_type**|**int**|Typ der Veröffentlichung:<br /><br /> **0** = transaktionsveröffentlichung<br /><br /> **1** = Momentaufnahme<br /><br /> **2** = Merge|  
|**publisher_login**|**sysname**|Auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendete Anmelde-ID.|  
|**publisher_password**|**nvarchar(524)**|Das Kennwort, das auf dem Verleger für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwendet wird (verschlüsselt).|  
|**publisher_security_mode**|**int**|Auf dem Verleger verwendeter Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**Verteiler**|**sysname**|Name des Verteilers.|  
|**distributor_login**|**sysname**|Verteilerbenutzername.|  
|**distributor_password**|**nvarchar(524)**|Verteilerkennwort (verschlüsselt).|  
|**distributor_security_mode**|**int**|Auf dem Verteiler verwendeter Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**ftp_address**|**sysname**|Nur aus Gründen der Abwärtskompatibilität beibehalten Die Netzwerkadresse des FTP-Dienstes für den Verteiler.|  
|**ftp_port**|**int**|Nur aus Gründen der Abwärtskompatibilität beibehalten Die Nummer des Anschlusses für den FTP-Dienst des Verteilers.|  
|**ftp_login**|**sysname**|Nur aus Gründen der Abwärtskompatibilität beibehalten Der Benutzername, mit dem eine Verbindung mit dem FTP-Dienst hergestellt wird.|  
|**ftp_password**|**nvarchar(524)**|Nur aus Gründen der Abwärtskompatibilität beibehalten Das Benutzerkennwort für die Verbindung mit dem FTP-Dienst verwendet.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Gibt den Speicherort des anderen Ordners für die Momentaufnahme an.|  
|**working_directory**|**nvarchar(255)**|Der Name des Arbeitsverzeichnisses, das zum Speichern der Daten- und Schemadateien verwendet wird.|  
|**use_ftp**|**bit**|Gibt anstelle des normalen Protokolls FTP an, um Momentaufnahmen abzurufen. Wenn **1**, FTP verwendet wird.|  
|**dts_package_name**|**sysame**|Gibt den Namen des DTS-Pakets (Data Transformation Services) an.|  
|**dts_package_password**|**nvarchar(524)**|Gibt gegebenenfalls das Kennwort des Pakets an.|  
|**dts_package_location**|**int**|Der Speicherort, in dem das DTS-Paket gespeichert ist.<br /><br /> **0** = das Paket befindet, auf dem Verteiler.<br /><br /> **1** = das Paket befindet, auf dem Abonnenten.|  
|**offload_agent**|**bit**|Gibt an, ob der Agent remote aktiviert werden kann. Wenn **0**, der Agent nicht remote aktiviert werden.|  
|**offload_server**|**sysname**|Gibt den Netzwerknamen des Servers an, der für die Remoteaktivierung verwendet wird.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Gibt den Pfad zum Ordner an, in dem die Momentaufnahmedateien gespeichert werden.|  
|**use_web_sync**|**bit**|Gibt an, ob das Abonnement über HTTPS synchronisiert werden kann ein Wert von **1** bedeutet, dass dieses Feature aktiviert ist.|  
|**internet_url**|**nvarchar(260)**|URL, die den Speicherort der replikationsüberwachung für die websynchronisierung darstellt.|  
|**sich**|**nvarchar(128)**|Der Anmeldename, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_password**|**nvarchar(524)**|Das Kennwort für den Anmeldenamen, der vom Merge-Agent zum Herstellen einer Verbindung mit dem Webserver verwendet wird, der die Websynchronisierung mithilfe der Standardauthentifizierung hostet.|  
|**internet_security_mode**|**int**|Der verwendete Authentifizierungsmodus beim Herstellen einer Verbindung mit dem Webserver, der die websynchronisierung, wobei der Wert hostet **1** bedeutet, dass Windows-Authentifizierung und den Wert **0** bedeutet, dass die Standardauthentifizierung.|  
|**internet_timeout**|**int**|Zeit in Sekunden, bevor eine Anforderung für eine Websynchronisierung abläuft.|  
|**Hostname**|**nvarchar(128)**|Gibt den Wert für HOST_NAME() an, wenn diese Funktion in der WHERE-Klausel eines parametrisierten Zeilenfilters verwendet wird.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpsubscription_properties** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_helpsubscription_properties**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
