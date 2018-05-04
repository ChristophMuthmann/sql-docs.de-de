---
title: Sp_changesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
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
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 47ce4c99261b7b7fd5ee7b3af4636d5ced5cf4f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Momentaufnahme- oder Transaktionspushabonnements bzw. eines Pullabonnements, das an einem verzögerten Update über eine Warteschlange beteiligt ist. Verwenden Sie zum Ändern der Eigenschaften aller anderen Typen von Pullabonnements [Sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md). **Sp_changesubscription** auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt wird.  
  
> [!IMPORTANT]  
>  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication**=] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die geändert werden soll. *Veröffentlichung*ist **Sysname**, hat keinen Standardwert  
  
 [ **@article** =] **"***Artikel***"**  
 Der Name des zu ändernden Artikels. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@subscriber** =] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@destination_db** =] **"***Destination_db***"**  
 Ist der Name der Abonnementdatenbank. *Destination_db* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Die Eigenschaft, die für das angegebene Abonnement geändert werden soll. *Eigenschaft* ist **nvarchar(30)**, und kann einen der Werte in der Tabelle.  
  
 [  **@value=**] **"***Wert***"**  
 Der neue Wert für den angegebenen *Eigenschaft*. *Wert* ist **nvarchar(4000)**, und kann einen der Werte in der Tabelle.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Anmeldename für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**distrib_job_password**||Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**subscriber_catalog**||Katalog, die beim Herstellen einer Verbindung mit dem OLE DB-Anbieter verwendet werden. Diese Eigenschaft ist nur gültig für nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.|  
|**subscriber_datasource**||Name der Datenquelle im vom OLE DB-Anbieter unterstützten Format. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_location**||Speicherort der Datenbank im vom OLE DB-Anbieter unterstützten Format. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_login**||Anmeldename auf dem Abonnenten.|  
|**subscriber_password**||Sicheres Kennwort für den angegebenen Anmeldenamen.|  
|**subscriber_security_mode**|**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Abonnenten.|  
||**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Abonnenten.|  
|**subscriber_provider**||Eindeutiger Programmbezeichner (PROGID, Programmatic Identifier), mit dem der OLE DB-Anbieter für die Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle registriert wird. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriber_providerstring**||Für den OLE DB-Anbieter spezifische Verbindungszeichenfolge, die die Datenquelle identifiziert. *Diese Eigenschaft ist nur gültig für nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Abonnenten.*|  
|**subscriptionstreams**||Die pro Verteilungs-Agent zulässige Anzahl von Verbindungen, um Batches von Änderungen parallel auf einen Abonnenten anzuwenden. Ein Wertebereich von **1** auf **64** direkteinplanung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber. Diese Eigenschaft muss **0** für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten, Oracle-Verleger oder Peer-zu-Peer-Abonnements.|  
|**subscriber_type kann**|**1**|ODBC-Datenquellenserver|  
||**3**|OLE DB-Anbieter|  
|**memory_optimized**|**bit**|Gibt an, dass das Abonnement von speicheroptimierten Tabellen unterstützt. *Memory_optimized* ist **Bit**, bei denen 1 gleich true (das Abonnement unterstützt von speicheroptimierten Tabellen).|  
  
 [  **@publisher =** ] **"***Publisher***"**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht angegeben werden, für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changesubscription** wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 **Sp_changesubscription** können nur zum Ändern der Eigenschaften von Pushabonnements oder Pullabonnements beteiligten verzögerte Aktualisieren der Transaktionsreplikation verwendet werden. Verwenden Sie zum Ändern der Eigenschaften aller anderen Typen von Pullabonnements [Sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md).  
  
 Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changesubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
