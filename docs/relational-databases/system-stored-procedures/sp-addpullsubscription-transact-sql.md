---
title: Sp_addpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ffbadd078651118e48977bbd46b45cbf96fd6cc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt ein Pullabonnement einer Momentaufnahmen- oder Transaktionsveröffentlichung hinzu. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Datenbank ausgeführt, für die das Pullabonnement erstellt werden soll.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. *Publisher_db* wird von Oracle-Verlegern ignoriert.  
  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@independent_agent=**] **"***Independent_agent***"**  
 Gibt an, ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist. *Independent_agent* ist **nvarchar(5)**, Standardwert ist "true". Wenn **"true"**, ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist. Wenn **"false"**, es ist ein Verteilungs-Agent für jedes Verlegerdatenbank und Abonnentendatenbank-Paar. *Independent_agent* ist eine Eigenschaft der Veröffentlichung und muss denselben Wert haben hier, wie er auf dem Verleger übereinstimmt.  
  
 [  **@subscription_type=**] **"***Subscription_type***"**  
 Ist der Typ des Abonnements. *Subscription_type* ist **vom Datentyp nvarchar(9)**, hat den Standardwert **anonyme**. Geben Sie einen Wert von **Pull** für *Subscription_type*, es sei denn, Sie ein Abonnement erstellen, ohne das Abonnement auf dem Verleger zu registrieren möchten. Sie müssen in diesem Fall geben Sie den Wert **anonyme**. Dies ist notwendig für Fälle, in denen Sie können nicht erstellt werden, ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] während der abonnementkonfiguration Verbindung mit dem Verleger.  
  
 [  **@description=**] **"***Beschreibung***"**  
 Ist die Beschreibung der Veröffentlichung. *Beschreibung* ist **nvarchar(100)**, hat den Standardwert NULL.  
  
 [  **@update_mode=**] **"***Update_mode***"**  
 Der Updatetyp. *Update_mode* ist **nvarchar(30)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Schreibgeschützt** (Standard)|Das Abonnement ist schreibgeschützt. Änderungen am Abonnenten werden nicht an den Verleger zurückgesendet. Sollte verwendet werden, wenn Updates nicht auf dem Abonnenten vorgenommen werden.|  
|**Synctran**|Aktiviert die Unterstützung für das sofortige Aktualisieren von Abonnements.|  
|**in der Warteschlange tran**|Aktiviert das verzögerte Aktualisieren über eine Warteschlange für das Abonnement. Daten können auf dem Abonnenten geändert werden; die Änderungen werden in einer Warteschlange gespeichert und an den Verleger weitergegeben.|  
|**Failover**|Aktiviert das sofortige Aktualisieren für das Abonnement, wobei als Failover das verzögerte Aktualisieren über eine Warteschlange verwendet wird. Daten können auf dem Abonnenten geändert werden; die Änderungen werden sofort an den Verleger weitergegeben. Wenn der Verleger und der Abonnent nicht verbunden sind, können Datenänderungen auf dem Abonnenten in einer Warteschlange gespeichert werden, bis Abonnent und Verleger erneut verbunden sind.|  
|**in der Warteschlange failover**|Ermöglicht das Abonnement als Update über eine Warteschlange, mit der Möglichkeit des Wechsels zum sofortigen Updatemodus. Daten können auf dem Abonnenten geändert und in einer Warteschlange gespeichert werden, bis eine Verbindung zwischen dem Abonnenten und dem Verleger hergestellt wird. Wenn eine kontinuierliche Verbindung hergestellt wird, kann der Updatemodus in den sofortigen Updatemodus geändert werden. *Für Oracle-Verlegern nicht unterstützt*.|  
  
 [  **@immediate_sync =**] *Immediate_sync*  
 Ist an, ob die Synchronisierungsdateien erstellt oder neu erstellt jedes Mal, wenn der Momentaufnahme-Agent ausgeführt wird. *Immediate_sync* ist **Bit** hat den Standardwert 1, und muss festgelegt werden, um den gleichen Wert wie *Immediate_sync* in **Sp_addpublication**. *Immediate_sync* ist eine Eigenschaft der Veröffentlichung und muss denselben Wert haben hier, wie er auf dem Verleger übereinstimmt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addpullsubscription** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
> [!IMPORTANT]  
>  Bei Abonnements mit verzögertem Update über eine Warteschlange verwenden Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für Verbindungen mit Abonnenten. Geben Sie für die Verbindung zu den einzelnen Abonnenten jeweils ein anderes Konto an. Beim Erstellen eines Pullabonnements, das verzögerte Updates über eine Warteschlange unterstützt, legt die Replikation immer die Verwendung der Windows-Authentifizierung für die Verbindung fest (für Pullabonnements kann die Replikation nicht auf Metadaten beim Abonnenten zugreifen, die für die Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung erforderlich sind). In diesem Fall sollten Sie ausführen [Sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) so ändern Sie die zu verwendende Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung nach dem Konfigurieren des Abonnements.  
  
 Wenn die [MSreplication_subscriptions &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) Tabelle ist nicht vorhanden, auf dem Abonnenten **Sp_addpullsubscription** wird erstellt. Sie fügt außerdem eine Zeile an die [MSreplication_subscriptions &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) Tabelle. Bei Pullabonnements müssen Sie [Sp_addsubscription &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) zuerst auf dem Verleger aufgerufen werden soll.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addpullsubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create an Updatable Subscription to a Transactional Publication](../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [Sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [Sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
