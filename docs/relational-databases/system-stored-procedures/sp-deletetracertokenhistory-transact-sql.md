---
title: Sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
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
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25f264f72042b6d26b3ebc5c677bc9ed4a981751
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt Überwachungstoken-Datensätze aus der [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) und [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) Systemtabellen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_deletetracertokenhistory [ @publication = ] 'publication'   
    [ , [ @tracer_id = ] tracer_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, in die das Überwachungstoken eingefügt wurde. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@tracer_id=** ] *Tracer_id*  
 Die ID des zu löschenden Überwachungstokens. *Tracer_id* ist **Int**, hat den Standardwert NULL. Wenn **null**, und klicken Sie dann alle Überwachungstoken, die zur Veröffentlichung gehörenden gelöscht werden.  
  
 [  **@cutoff_date=** ] *Cutoff_date*  
 Gibt das Umstellungsdatum an, sodass alle vor diesem Datum in die Veröffentlichung eingefügten Überwachungstoken entfernt werden. *Cutoff_date* ist "DateTime" hat den Standardwert NULL.  
  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter sollte nur angegeben werden, für nicht -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.  
  
 [  **@publisher_db=** ] **"***Publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird ignoriert, wenn die gespeicherte Prozedur auf dem Verleger ausgeführt wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_deletetracertokenhistory** wird bei der Transaktionsreplikation verwendet.  
  
 Beim Ausführen von **Sp_deletetracertokenhistory**, können Sie nur eine der angeben *Tracer_id* oder *Cutoff_date*. Wenn Sie beide Parameter angeben, wird eine Fehlermeldung angezeigt.  
  
 Wenn Sie nicht ausgeführt werden **Sp_deletetracertokenhistory** um Überwachungstoken-Metadaten zu entfernen, werden die Informationen entfernt, wenn die regelmäßig verlaufscleanups.  
  
 Überwachungstoken-IDs können bestimmt werden, indem Sie ausführen [Sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) oder durch Abfragen der [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) -Systemtabelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle in der Veröffentlichungsdatenbank oder **Db_owner** festen oder  **Replmonitor** Rollen in der Verteilungsdatenbank können ausführen **Sp_deletetracertokenhistory**.  
  
## <a name="see-also"></a>Siehe auch  
 [Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
