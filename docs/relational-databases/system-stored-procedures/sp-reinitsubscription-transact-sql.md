---
title: Sp_reinitsubscription (Transact-SQL) | Microsoft Docs
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
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2be8faabc7645d4f9b93d84fea0977e620a13d46
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Kennzeichnet das Abonnement für die erneute Initialisierung. Diese gespeicherte Prozedur wird auf dem Verleger für Pushabonnements ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert all.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des Artikels. *Artikel* ist **Sysname**, hat den Standardwert all. Für eine sofort aktualisierbare Veröffentlichung *Artikel* muss **alle**ist, andernfalls die gespeicherte Prozedur überspringt die Veröffentlichung und meldet einen Fehler.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@destination_db=**] **"***Destination_db***"**  
 Der Name der Zieldatenbank. *Destination_db* ist **Sysname**, hat den Standardwert all.  
  
 [  **@for_schema_change=**] **"***For_schema_change***"**  
 Gibt an, ob eine Schemaänderung in der Veröffentlichungsdatenbank eine erneute Initialisierung verursacht. *For_schema_change* ist **Bit**, hat den Standardwert 0. Wenn **0**, aktive Abonnements für Veröffentlichungen, die sofortiges Aktualisieren zulassen werden erneut aktiviert werden, solange die gesamte Veröffentlichung, nicht nur einige Artikel darin, erneut initialisiert werden. Die erneute Initialisierung wird demnach als Ergebnis von Schemaänderungen initiiert. Wenn **1**, aktive Abonnements werden nicht erneut aktiviert, bis der Momentaufnahme-Agent ausgeführt wird.  
  
 [  **@publisher=** ] **"***Publisher***"**  
 Gibt einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.  
  
 [  **@ignore_distributor_failure=** ] *Ignore_distributor_failure*  
 Lässt die erneute Initialisierung zu, auch wenn der Verteiler nicht vorhanden oder offline ist. *Ignore_distributor_failure* ist **Bit**, hat den Standardwert 0. Wenn **0**, eine erneute Initialisierung schlägt fehl, wenn der Verteiler nicht vorhanden ist oder offline ist.  
  
 [  **@invalidate_snapshot=** ] *Invalidate_snapshot*  
 Erklärt die vorhandene Veröffentlichungsmomentaufnahme für ungültig. *Invalidate_snapshot* ist **Bit**, hat den Standardwert 0. Wenn **1**, eine neue Momentaufnahme für die Veröffentlichung generiert wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_reinitsubscription** wird bei der Transaktionsreplikation verwendet.  
  
 **Sp_reinitsubscription** wird für die Peer-zu-Peer-Transaktionsreplikation nicht unterstützt.  
  
 Für Abonnements, bei denen die Anfangsmomentaufnahme automatisch angewendet wird und bei denen die Veröffentlichung keine aktualisierbaren Abonnements zulässt, muss der Momentaufnahme-Agent ausgeführt werden, nachdem diese gespeicherte Prozedur ausgeführt wird, sodass Programmdateien für das Schema- und Massenkopieren vorbereitet werden und die Verteilungs-Agents in der Lage sind, die Abonnements neu zu synchronisieren.  
  
 Für Abonnements, bei denen die Anfangsmomentaufnahme automatisch angewendet wird und bei denen die Veröffentlichung aktualisierbare Abonnements zulässt, führt der Verteilungs-Agent eine erneute Synchronisierung für das Abonnement durch, indem die neuesten Programmdateien für das Schema- und Massenkopieren verwendet werden, die zuvor vom Momentaufnahme-Agent erstellt wurden. Der Verteilungs-Agent synchronisiert das Abonnement sofort, nachdem der Benutzer führt **Sp_reinitsubscription**, ist der Verteilungs-Agent nicht Synchronisierung kann auftreten, nachdem die Nachricht Intervall (ausgelastet ist, andernfalls vom Verteilungs-Agent-Befehlszeilenparameter angegeben: **MessageInterval**).  
  
 **Sp_reinitsubscription** wirkt sich nicht auf Abonnements, in denen die anfangsmomentaufnahme manuell angewendet wird.  
  
 Übergeben Sie zur neusynchronisierung anonymer Abonnements einer Veröffentlichung **alle** oder NULL als *Abonnenten*.  
  
 Die Transaktionsreplikation unterstützt die erneute Initialisierung von Abonnements auf Artikelebene. Die Momentaufnahme des Artikels wird während der nächsten Synchronisierung erneut auf den Abonnenten angewendet, nachdem der Artikel für die erneute Initialisierung markiert wurde. Wenn jedoch abhängige Artikel vorhanden sind, die von demselben Abonnenten abonniert werden, kann die erneute Anwendung der Momentaufnahme auf den Artikel möglicherweise einen Fehler erzeugen, wenn in der Veröffentlichung nicht auch abhängige Artikel unter bestimmten Umständen automatisch erneut initialisiert werden:  
  
-   Wenn 'drop' als Vorabbefehl vor der Erstellung des entsprechenden Artikels verwendet wird, werden Artikel für schemagebundene Sichten und schemagebundene gespeicherte Prozeduren für das Basisobjekt des Artikels ebenfalls für die erneute Initialisierung markiert.  
  
-   Wenn die Schemaoption für den Artikel das Erstellen von Skripts für die deklarative referenzielle Integrität der Primärschlüssel einbezieht, werden Artikel, die über Basistabellen mit Fremdschlüsselbeziehungen zu Basistabellen des erneut initialisierten Artikels verfügen, ebenfalls für die erneute Initialisierung markiert.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** , den Mitgliedern der festen Serverrolle die **Db_owner** festen Datenbankrolle oder der Ersteller des Abonnements kann ausführen **Sp_reinitsubscription** .  
  
## <a name="see-also"></a>Siehe auch  
 [Erneutes Initialisieren eines Abonnements](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
