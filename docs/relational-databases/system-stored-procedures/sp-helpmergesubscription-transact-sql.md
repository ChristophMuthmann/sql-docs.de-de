---
title: Sp_helpmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cb5387d011b3987262415e3a88b5fd8bc65a8e2f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über ein Abonnement (Push und Pull) für eine Mergeveröffentlichung zurück. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Wiederveröffentlichungsabonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert **%**. Die Veröffentlichung muss bereits vorhanden sein und den Regeln für Bezeichner entsprechen. Wenn der Wert NULL oder **%**, Informationen zu allen mergeveröffentlichungen und Mergeabonnements in der aktuellen Datenbank zurückgegeben.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert **%**. Mit NULL oder % werden Informationen zu allen Abonnements einer bestimmten Veröffentlichung zurückgegeben.  
  
 [  **@subscriber_db=**] **"***Subscriber_db***"**  
 Ist der Name der Abonnementdatenbank. *Subscriber_db*ist **Sysname**, hat den Standardwert **%**, womit Informationen zu allen Abonnementdatenbanken zurückgegeben.  
  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. Der Verleger muss ein gültiger Server sein. *Publisher*ist **Sysname**, hat den Standardwert **%**, womit Informationen zu allen Verlegern zurückgegeben.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db*ist **Sysname**, hat den Standardwert **%**, womit Informationen zu allen Verlegerdatenbanken zurückgegeben.  
  
 [  **@subscription_type=**] **"***Subscription_type***"**  
 Ist der Typ des Abonnements. *Subscription_type*ist **nvarchar(15)**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Push** (Standard)|Pushabonnement|  
|**Pull**|Pullabonnement|  
|**both**|Sowohl ein Push- als auch ein Pullabonnement|  
  
 [  **@found=**] **"***gefunden***' Ausgabe**  
 Ein Flag zur Angabe zurückgegebener Zeilen. *gefunden*ist **Int** und ein OUTPUT-Parameter hat den Standardwert NULL. **1** gibt an, die Veröffentlichung gefunden wurde. **0** gibt an, die Veröffentlichung wurde nicht gefunden.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|Name des Abonnements.|  
|**Veröffentlichung**|**sysname**|Name der Veröffentlichung.|  
|**publisher**|**sysname**|Name des Verlegers.|  
|**publisher_db**|**sysname**|Name der Verlegerdatenbank.|  
|**subscriber**|**sysname**|Der Name des Abonnenten.|  
|**subscriber_db**|**sysname**|Name der Abonnementdatenbank.|  
|**status**|**int**|Status des Abonnements:<br /><br /> **0** = alle Aufträge sind starten<br /><br /> **1** = ein oder mehrere Aufträge werden gestartet<br /><br /> **2** = alle Aufträge wurden erfolgreich ausgeführt.<br /><br /> **3** = mindestens ein Auftrag wird ausgeführt.<br /><br /> **4** = alle Aufträge sind geplant und im Leerlauf<br /><br /> **5** = mindestens ein Auftrag versucht, führen Sie nach einem vorherigen Fehler<br /><br /> **6** = mindestens ein Auftrag konnte nicht erfolgreich ausgeführt|  
|**subscriber_type kann**|**int**|Abonnententyp|  
|**subscription_type**|**int**|Typ des Abonnements:<br /><br /> **0** = Push<br /><br /> **1** = Pullabonnement<br /><br /> **2** = beide|  
|**priority**|**float(8)**|Zahl zur Angabe der Priorität für das Abonnement.|  
|**sync_type**|**tinyint**|Synchronisierungsart des Abonnements.|  
|**description**|**nvarchar(255)**|Kurze Beschreibung des Mergeabonnements.|  
|**Der Standardwert**|**Binary(16)**|Auftrags-ID des Merge-Agents.|  
|**full_publication**|**tinyint**|Gibt an, ob das Abonnement für eine vollständige oder gefilterte Veröffentlichung besteht.|  
|**offload_enabled**|**bit**|Gibt an, ob festgelegt wurde, dass die Auslagerungsausführung eines Replikations-Agents auf dem Abonnenten ausgeführt wird. Bei NULL erfolgt die Ausführung auf dem Verleger.|  
|**offload_server**|**sysname**|Name des Servers, auf den der Agent verlagert wird.|  
|**use_interactive_resolver**|**int**|Gibt zurück, ob der interaktive Konfliktlöser während der Konfliktlösung verwendet wird. Wenn **0**, der interaktive Konfliktlöser nicht verwendet wird.|  
|**Hostname**|**sysname**|Bereitgestellte Wert, wenn ein Abonnement, durch den Wert gefiltert wird der [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) Funktion.|  
|**subscriber_security_mode**|**smallint**|Der Sicherheitsmodus des Abonnenten, auf dem **1** Windows-Authentifizierung und **0** bedeutet [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**subscriber_login**|**sysname**|Der Anmeldename auf dem Abonnenten.|  
|**subscriber_password**|**sysname**|Das tatsächliche Abonnentenkennwort wird nie zurückgegeben. Das Ergebnis ist maskiert, indem eine "**\*\*\*\*\*\***" Zeichenfolge.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpmergesubscription** dient bei der Mergereplikation zurückzugebenden Abonnementinformationen, die auf dem Verleger oder dem Wiederveröffentlichungsabonnenten gespeichert.  
  
 Bei anonymen Abonnements weist die *Subscription_type*ist der Wert immer **1** (Pull). Sie müssen jedoch ausführen [Sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) für Informationen zu anonymen Abonnements auf dem Abonnenten.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle oder der veröffentlichungszugriffsliste für die Veröffentlichung, zu dem das Abonnement gehört, kann ausführen **"sp_" Helpmergesubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [Sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [Sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
