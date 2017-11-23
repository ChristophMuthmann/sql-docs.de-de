---
title: Sp_helpsubscription (Transact-SQL) | Microsoft Docs
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
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords: sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201a7c412fbf01ca2600d3c9dc233eadfa33710b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpsubscription-transact-sql"></a>sp_helpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Abonnementinformationen bezüglich einer bestimmten Veröffentlichung, eines Artikels, eines Abonnenten oder einer Gruppe von Abonnements auf. Diese gespeicherte Prozedur wird auf einem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =** ] **"***Veröffentlichung***"**  
 Der Name der zugeordneten Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert  **%** , dem alle Abonnementinformationen für diesen Server zurückgegeben.  
  
 [  **@article=** ] **"***Artikel***"**  
 Der Name des Artikels. *Artikel* ist **Sysname**, hat den Standardwert  **%** , dem alle Abonnementinformationen für die ausgewählten Veröffentlichungen und Abonnenten zurückgegeben. Wenn **alle**, nur ein Eintrag für das vollständige Abonnement für eine Veröffentlichung zurückgegeben.  
  
 [  **@subscriber=** ] **"***Abonnenten***"**  
 Der Name des Abonnenten, für den Abonnementinformationen abgerufen werden sollen. *Abonnenten* ist **Sysname**, hat den Standardwert  **%** , dem alle Abonnementinformationen für die ausgewählten Veröffentlichungen und Artikel zurückgegeben.  
  
 [  **@destination_db=** ] **"***Destination_db***"**  
 Der Name der Zieldatenbank. *Destination_db* ist **Sysname**, hat den Standardwert  **%** .  
  
 [  **@found=** ] **"***gefunden***"**Ausgabe  
 Ein Flag zur Angabe zurückgegebener Zeilen. *gefunden*ist **Int** und ein OUTPUT-Parameter mit dem Standardwert 23456.  
  
 **1** gibt an, die Veröffentlichung gefunden wurde.  
  
 **0** gibt an, die Veröffentlichung wurde nicht gefunden.  
  
 [  **@publisher** =] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, und der Standardwert ist der Name des aktuellen Servers.  
  
> [!NOTE]  
>  *Publisher* sollte nicht angegeben werden, außer wenn es sich um einen Oracle-Verleger ist.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**subscriber**|**sysname**|Der Name des Abonnenten.|  
|**Veröffentlichung**|**sysname**|Name der Veröffentlichung.|  
|**Artikel**|**sysname**|Der Name des Artikels.|  
|**Zieldatenbank**|**sysname**|Name der Zieldatenbank, in der replizierte Daten gespeichert werden.|  
|**Abonnementstatus**|**tinyint**|Abonnementstatus:<br /><br /> **0** = inaktiv<br /><br /> **1** = abonniert<br /><br /> **2** = aktiv|  
|**Synchronisierungstyp**|**tinyint**|Synchronisierungsart des Abonnements:<br /><br /> **1** = automatisch<br /><br /> **2** = keine|  
|**Abonnementtyp**|**int**|Typ des Abonnements:<br /><br /> **0** = Push<br /><br /> **1** = Pullabonnement<br /><br /> **2** = anonym|  
|**vollständiges Abonnement**|**bit**|Gibt an, ob alle Artikel in der Veröffentlichung abonniert werden:<br /><br /> **0** = Nein<br /><br /> **1** = Ja|  
|**Abonnementname**|**nvarchar(255)**|Name des Abonnements.|  
|**Updatemodus**|**int**|**0** = schreibgeschützt<br /><br /> **1** = Abonnement mit sofortigem Update|  
|**Verteilungsauftrags-id**|**Binary(16)**|Auftrags-ID des Verteilungs-Agents.|  
|**loopback_detection**|**bit**|Bestimmt, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet:<br /><br /> **0** = sendet zurück.<br /><br /> **1** tut = sendet nicht zurück.<br /><br /> Wird bei der bidirektionalen Transaktionsreplikation verwendet. Weitere Informationen finden Sie unter [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|**offload_enabled**|**bit**|Gibt an, ob festgelegt wurde, dass die Ausführung eines ausgelagerten Replikations-Agents auf dem Abonnenten ausgeführt wird.<br /><br /> Wenn **0**, Agent auf dem Verleger ausgeführt wird.<br /><br /> Wenn **1**, Agent auf dem Abonnenten ausgeführt wird.|  
|**offload_server**|**sysname**|Name des Servers, der für die Aktivierung des Remote-Agents aktiviert ist. Wenn der Wert NULL ist, klicken Sie dann der aktuelle offload_server [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) Tabelle verwendet wird.|  
|**dts_package_name**|**sysname**|Gibt den Namen des DTS-Pakets (Data Transformation Services) an.|  
|**dts_package_location**|**int**|Speicherort des DTS-Pakets, wenn dem Abonnement eines zugewiesen wurde. Wenn ein Paket, ein Wert vorhanden ist **0** gibt den Speicherort des Pakets auf die **Verteiler**. Der Wert **1** gibt an, die **Abonnenten**.|  
|**subscriber_security_mode**|**smallint**|Der Sicherheitsmodus des Abonnenten, auf dem **1** Windows-Authentifizierung und **0** bedeutet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**subscriber_login**|**sysname**|Der Anmeldename auf dem Abonnenten.|  
|**subscriber_password**||Das tatsächliche Abonnentenkennwort wird nie zurückgegeben. Das Ergebnis ist maskiert, indem eine "**\*\*\*\*\*\***" Zeichenfolge.|  
|**job_login**|**sysname**|Name des Windows-Kontos, unter dem der Verteilungs-Agent ausgeführt wird.|  
|**job_password**||Das tatsächliche Auftragskennwort wird nie zurückgegeben. Das Ergebnis ist maskiert, indem eine "**\*\*\*\*\*\***" Zeichenfolge.|  
|**distrib_agent_name**|**nvarchar(100)**|Name des Agentauftrags, der das Abonnement synchronisiert.|  
|**subscriber_type kann**|**tinyint**|Typ des Abonnenten. Folgende Werte sind möglich:<br /><br /> **0** = SQL Server-Abonnent<br /><br /> **1** = ODBC-Datenquellenserver<br /><br /> **2** = Microsoft JET-Datenbank (veraltet)<br /><br /> **3** = OLE DB-Anbieter|  
|**subscriber_provider**|**sysname**|Eindeutiger Programmbezeichner (PROGID, Programmatic Identifier), mit dem der OLE DB-Anbieter für die Nicht-SQL Server-Datenquelle registriert wird.|  
|**subscriber_datasource**|**nvarchar(4000)**|Name der Datenquelle im vom OLE DB-Anbieter unterstützten Format.|  
|**subscriber_providerstring**|**nvarchar(4000)**|Für den OLE DB-Anbieter spezifische Verbindungszeichenfolge, die die Datenquelle identifiziert.|  
|**subscriber_location**|**nvarchar(4000)**|Speicherort der Datenbank im vom OLE DB-Anbieter unterstützten Format.|  
|**subscriber_catalog**|**sysname**|Katalog, die beim Herstellen einer Verbindung mit dem OLE DB-Anbieter verwendet werden.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpsubscription** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen erhält standardmäßig die **public** -Rolle. Benutzern werden nur Informationen für Abonnements zurückgegeben, die sie erstellt haben. Informationen zu allen Abonnements ist auf Mitglieder der zurückgegebenen der **Sysadmin** auf dem Verleger oder Mitglieder der festen Serverrolle die **Db_owner** festen Datenbankrolle "" für die Veröffentlichungsdatenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Sp_changesubstatus &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [Sp_dropsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
