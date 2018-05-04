---
title: Sp_addsynctriggers (Transact-SQL) | Microsoft Docs
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
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 711126c199480bd1d8ef836b9b587f51db8e4552
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt auf dem Abonnenten Trigger, die mit allen Typen aktualisierbarer Abonnements verwendet werden können (sofortiges Aktualisieren, verzögertes Aktualisieren über eine Warteschlange, sofortiges Aktualisieren mit verzögertem Aktualisieren über eine Warteschlange als Failover). Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Die [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) Prozedur sollte verwendet werden, anstelle von **Sp_addsynctrigger**. [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) generiert ein Skript, enthält die **Sp_addsynctrigger** aufrufen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@sub_table=**] **"***Sub_table***"**  
 Entspricht dem Namen der Abonnententabelle. *Sub_table* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@sub_table_owner=**] **"***Sub_table_owner***"**  
 Entspricht dem Namen des Eigentümers der Abonnententabelle. *Sub_table_owner* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher=**] **'***publisher***'**  
 Entspricht dem Namen des Verlegerservers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Verlegerdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert. Mit NULL wird die aktuelle Datenbank verwendet.  
  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@ins_proc=**] **"***Ins_proc***"**  
 Entspricht dem Namen der gespeicherten Prozedur, die synchrone Transaktionseinfügungen auf Verlegerebene unterstützt. *Ins_proc* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@upd_proc=**] **"***Upd_proc***"**  
 Entspricht dem Namen der gespeicherten Prozedur, die synchrone Transaktionsupdates auf Verlegerebene unterstützt. *Ins_proc* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@del_proc=**] **"***Del_proc***"**  
 Entspricht dem Namen der gespeicherten Prozedur, die synchrone Transaktionslöschungen auf Verlegerebene unterstützt. *Ins_proc* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@cftproc =** ] **"***Cftproc***"**  
 Entspricht dem Namen der automatisch generierten Prozedur, die von Veröffentlichungen verwendet wird, die eine verzögerte Aktualisierung ermöglichen. *Cftproc* ist **Sysname**, hat keinen Standardwert. Für Veröffentlichungen mit sofortigem Update ist dieser Wert NULL. Dieser Parameter wird auf Veröffentlichungen angewendet, die verzögerte Updates über eine Warteschlange ermöglichen (verzögertes Update über eine Warteschlange bzw. sofortiges Update mit verzögertem Update über eine Warteschlange als Failover).  
  
 [  **@proc_owner =** ] **"***Proc_owner***"**  
 Gibt das Benutzerkonto auf Verlegerebene an, unter dem alle automatisch generierten gespeicherten Prozeduren zum Aktualisieren von Veröffentlichungen (verzögert und/oder unmittelbar) erstellt wurden. *Proc_owner* ist **Sysname** hat keinen Standardwert.  
  
 [  **@identity_col=**] **"***Identity_col***"**  
 Entspricht dem Namen der Identitätsspalte auf Verlegerebene. *Identity_col* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@ts_col=**] **"***Timestamp_col***"**  
 Der Name des der **Zeitstempel** Spalte auf dem Verleger. *Timestamp_col* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@filter_clause=**] **"***Filter_clause***"**  
 Eine Einschränkungsklausel (WHERE), die einen horizontalen Filter definiert. Wenn Sie die Einschränkungsklausel eingeben, lassen Sie das Schlüsselwort, in denen. *Filter_clause*ist **nvarchar(4000)**, hat den Standardwert NULL.  
  
 [  **@primary_key_bitmap =**] **"***Primary_key_bitmap***"**  
 Entspricht einer Bitmap der Primärschlüsselspalten in der Tabelle. *Primary_key_bitmap* ist **varbinary(4000)**, hat keinen Standardwert.  
  
 [  **@identity_support =** ] *Identity_support*  
 Aktiviert und deaktiviert die automatische Behandlung von Identitätsbereichen im Fall der verzögerten Aktualisierung. *Identity_support* ist ein **Bit**, hat den Standardwert **0**. **0** bedeutet, dass keine identitätsbereichsunterstützung vorhanden ist, dass im Bereich Unterstützung **1** ermöglicht die automatische Behandlung des Identitätsbereichs.  
  
 [  **@independent_agent =** ] *Independent_agent*  
 Gibt an, ob es einen einzelnen Verteilungs-Agent (einen unabhängigen Agent) für diese Veröffentlichung oder einen Verteilungs-Agent pro Paar aus Veröffentlichungsdatenbank und Abonnementdatenbank (einen freigegebenen Agent) gibt. Dieser Wert reflektiert den Wert der independent_agent-Eigenschaft von der auf Verlegerebene definierten Veröffentlichung. *Independent_agent* ist vom Datentyp bit mit dem Standardwert **0**. Wenn **0**, der Agent ist ein freigegebener Agent. Wenn **1**, der Agent ist ein unabhängiger Agent.  
  
 [  **@distributor =** ] **"***Verteiler***"**  
 Entspricht dem Namen des Verteilers. *Verteiler* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@pubversion**=] *Pubversion*  
 Gibt die Version des Verlegers an. *Pubversion* ist **Int**, hat den Standardwert 1. **1** darauf hin, dass die verlegerversion [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Servicepack 2 oder früher; **2** darauf hin, dass der Verleger [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 3 (SP3) oder höher. *Pubversion* muss explizit festgelegt werden, um **2** Wenn die Verleger-Version ist [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] SP3 oder höher.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addsynctriggers** wird vom Verteilungs-Agent als Teil der abonnementinitialisierung verwendet. Diese gespeicherte Prozedur wird normalerweise nicht von Benutzern ausgeführt, kann jedoch hilfreich sein, wenn der Benutzer manuell ein nosync-Abonnement einrichten muss.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addsynctriggers**.  
  
## <a name="see-also"></a>Siehe auch  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
