---
title: Sp_helptracertokenhistory (Transact-SQL) | Microsoft Docs
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
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c6ecccbb6c545fe9a4da6f50b2bdc6100dad57a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt detaillierte Latenzzeitinformationen für die angegebenen Überwachungstoken zurück, wobei für jeden Abonnenten eine Zeile zurückgegeben wird. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, in die das Überwachungstoken eingefügt wurde. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@tracer_id=** ] *Tracer_id*  
 Die ID des Überwachungstokens in das [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) Tabelle für die Verlaufsinformationen zurückgegeben. *Tracer_id* ist **Int**, hat keinen Standardwert.  
  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter sollte nur angegeben werden, für nicht -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.  
  
 [  **@publisher_db=** ] **"***Publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird ignoriert, wenn die gespeicherte Prozedur auf dem Verleger ausgeführt wird.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|Anzahl der Sekunden zwischen dem Commit des Überwachungstokendatensatzes auf dem Verleger und dem Commit des Datensatzes auf dem Verteiler|  
|**subscriber**|**sysname**|Name des Abonnenten, der das Überwachungstoken empfing|  
|**subscriber_db**|**sysname**|Name der Abonnementdatenbank, in die der Überwachungstokendatensatz eingefügt wurde|  
|**subscriber_latency**|**bigint**|Anzahl der Sekunden zwischen dem Commit des Überwachungstokendatensatzes auf dem Verteiler und dem Commit des Datensatzes auf dem Abonnenten|  
|**overall_latency**|**bigint**|Anzahl der Sekunden zwischen dem Commit des Überwachungstokendatensatzes auf dem Verleger und dem Commit des Datensatzes auf dem Abonnenten|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helptracertokenhistory** wird bei der Transaktionsreplikation verwendet.  
  
 Führen Sie [Sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) abrufen eine Liste von Überwachungstoken für die Veröffentlichung.  
  
 Der Wert NULL im Resultset bedeutet, dass keine Latenzzeitstatistik berechnet werden kann. Dies liegt daran, dass das Überwachungstoken nicht auf dem Verteiler oder einem der Abonnenten empfangen wurde.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle in der Veröffentlichungsdatenbank oder **Db_owner** festen oder  **Replmonitor** Rollen in der Verteilungsdatenbank können ausführen **Sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Siehe auch  
 [Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
