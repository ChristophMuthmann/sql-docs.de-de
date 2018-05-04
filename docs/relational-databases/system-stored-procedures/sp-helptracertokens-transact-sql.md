---
title: Sp_helptracertokens (Transact-SQL) | Microsoft Docs
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
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2636da813e83e0efe3efdef7a283ad1ee48293a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Überwachungstoken zurück, das in eine Veröffentlichung eingefügt wurde, um Latenzzeiten zu bestimmen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, in die Überwachungstoken eingefügt wurden. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter sollte nur angegeben werden, für nicht -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.  
  
 [  **@publisher_db=** ] **"***Publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird ignoriert, wenn die gespeicherte Prozedur auf dem Verleger ausgeführt wird.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifiziert einen Überwachungstoken-Datensatz.|  
|**publisher_commit**|**datetime**|Das Datum und die Uhrzeit für den Commit des Tokendatensatzes auf dem Verleger in der Veröffentlichungsdatenbank.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helptracertokens** wird bei der Transaktionsreplikation verwendet.  
  
 **Sp_helptracertokens** wird verwendet, um Überwachungstoken-IDs abgerufen Ausführung [Sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle in der Veröffentlichungsdatenbank oder **Db_owner** festen oder  **Replmonitor** Rollen in der Verteilungsdatenbank können ausführen **Sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Siehe auch  
 [Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
