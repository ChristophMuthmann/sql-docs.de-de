---
title: Sp_browsereplcmds (Transact-SQL) | Microsoft Docs
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
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8341d233f84a2c9fb2d5b3c7df2495118a2b2f5c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird als Diagnosetool verwendet und gibt ein Resultset mit einer lesbaren Version der replizierten Befehle zurück, die in der Verteilungsdatenbank gespeichert sind. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@xact_seqno_start =**] **"***Xact_seqno_start***"**  
 Gibt die niedrigste genaue Sequenznummer an, die zurückgegeben werden soll. *Xact_seqno_start* ist **nchar(22)**, hat den Standardwert 0 x 00000000000000000000.  
  
 [  **@xact_seqno_end =**] **"***Xact_seqno_end***"**  
 Gibt die höchste genaue Sequenznummer an, die zurückgegeben werden soll. *Xact_seqno_end* ist **nchar(22)**, hat den Standardwert 0xffffffffffffffffffff.  
  
 [  **@originator_id =**] **"***Originator_id***"**  
 Gibt an, ob Befehle mit dem angegebenen *Originator_id* werden zurückgegeben. *Originator_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@publisher_database_id =**] **"***Publisher_database_id***"**  
 Gibt an, ob Befehle mit dem angegebenen *Publisher_database_id* werden zurückgegeben. *Publisher_database_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@article_id =**] **"***Article_id***"**  
 Gibt an, ob Befehle mit dem angegebenen *Article_id* werden zurückgegeben. *Article_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@command_id =**] *Command_id*  
 Ist der Speicherort des Befehls in [MSrepl_commands &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) decodiert werden. *Command_id* ist **Int**, hat den Standardwert NULL. Wenn angegeben, alle anderen Parameter müssen angegeben werden außerdem und *Xact_seqno_start*muss identisch mit *Xact_seqno_end*.  
  
 [  **@agent_id =**] *agent_id-Wert*  
 Gibt an, dass nur Befehle für einen bestimmten Replikations-Agent zurückgegeben werden. *Agent_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@compatibility_level =**] *Compatibility_level*  
 Ist die Version des [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem die *Compatibility_level* ist **Int**, hat den Standardwert 9000000.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Sequenznummer des Befehls.|  
|**originator_srvname**|**sysname**|Server, von dem die Transaktion stammt|  
|**originator_db**|**sysname**|Datenbank, von der die Transaktion stammt|  
|**article_id**|**int**|ID des Artikels.|  
|**type**|**int**|Der Typ des Befehls.|  
|**verbleiben**|**bit**|Zeigt an, ob dies ein Teilbefehl ist.|  
|**Hashkey**|**int**|Nur interne Verwendung.|  
|**originator_publication_id**|**int**|ID der Veröffentlichung, von der die Transaktion stammt|  
|**originator_db_version**|**int**|Version der Datenbank, von der die Transaktion stammt|  
|**originator_lsn**|**varbinary(16)**|Identifiziert die Protokollfolgenummer (LSN, Log Sequence Number) für den Befehl in der ursprünglichen Veröffentlichung Peer-zu-Peer-Transaktionsreplikation verwendet.|  
|**Befehl**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl.|  
|**command_id**|**int**|ID des Befehls in [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Lange Befehle können auf mehrere Zeilen des Resultsets aufgeteilt werden.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_browsereplcmds** wird bei der Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** -Serverrolle oder Mitglied der **Db_owner** oder **Replmonitor** festen Datenbankrollen für die Verteilungsdatenbank können Ausführen**Sp_browsereplcmds**.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
