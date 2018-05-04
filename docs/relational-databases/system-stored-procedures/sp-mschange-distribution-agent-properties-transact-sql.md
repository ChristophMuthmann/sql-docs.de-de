---
title: Sp_MSchange_distribution_agent_properties (Transact-SQL) | Microsoft Docs
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
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4134d0fce27f28362cee87c8c039ddb8cdcfaebc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spmschangedistributionagentproperties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Verteilungs-Agent-Auftrags, der ausgeführt wird eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höhere Version Verteiler. Diese gespeicherte Prozedur wird zum Ändern von Eigenschaften verwendet, wenn der Verleger in einer Instanz von [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ausgeführt wird. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher** = ] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher_db=** ] **"***Publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publication =** ] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@subscriber=** ] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@subscriber_db=** ] **"***Subscriber_db***"**  
 Ist der Name der Abonnementdatenbank. *Subscriber_db* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@property =** ] **"***Eigenschaft***"**  
 Der Name der zu ändernden Veröffentlichungseigenschaft. *Eigenschaft* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@value =** ] **"***Wert***"**  
 Der neue Eigenschaftswert. *Wert* ist **nvarchar(524)**, hat den Standardwert NULL.  
  
 Diese Tabelle beschreibt die änderbaren Eigenschaften des Verteilungs-Agent-Auftrags sowie die Einschränkungen für die Werte dieser Eigenschaften.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Anmeldename für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**distrib_job_password**||Kennwort für das Windows-Konto, unter dem der Agentauftrag ausgeführt wird.|  
|**subscriber_catalog**||Katalog, die beim Herstellen einer Verbindung mit dem OLE DB-Anbieter verwendet werden. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_datasource**||Name der Datenquelle im vom OLE DB-Anbieter unterstützten Format. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_location**||Speicherort der Datenbank im vom OLE DB-Anbieter unterstützten Format. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_login**||Anmeldename, der beim Herstellen der Verbindung mit einem Abonnenten zum Synchronisieren des Abonnements verwendet werden soll.|  
|**subscriber_password**||Kennwort des Abonnenten.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||Eindeutiger Programmbezeichner (PROGID, Programmatic Identifier), mit dem der OLE DB-Anbieter für die Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle registriert wird. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_providerstring**||Für den OLE DB-Anbieter spezifische Verbindungszeichenfolge, die die Datenquelle identifiziert. *Diese Eigenschaft gilt nur für nicht - SQL Server-Abonnenten.*|  
|**subscriber_security_mode**|**1**|Windows-Authentifizierung.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.|  
|**subscriber_type kann**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten|  
||**1**|ODBC-Datenquellenserver|  
||**3**|OLE DB-Anbieter|  
|**subscriptionstreams**||Bezeichnet die Anzahl zulässiger Verbindungen pro Verteilungs-Agent, um Änderungsbatches parallel auf einen Abonnenten anzuwenden. *Nicht unterstützt für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten, Oracle-Verleger oder Peer-zu-Peer-Abonnements.*|  
  
> [!NOTE]  
>  Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_MSchange_distribution_agent_properties** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn der Verleger ausgeführt wird, in einer Instanz von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höhere Version, die Sie verwenden sollten [Sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) so ändern Sie Eigenschaften eines Merge-Agent-Auftrags, der ein Pushabonnement synchronisiert, die auf dem Verteiler ausgeführt wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle auf dem Verteiler ausführen kann **Sp_MSchange_distribution_agent_properties**.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [Sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
