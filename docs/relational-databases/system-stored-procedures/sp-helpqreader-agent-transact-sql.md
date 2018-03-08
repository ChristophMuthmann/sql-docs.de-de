---
title: Sp_helpqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords: sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50492a76e742459e7b883f9887026d0ce63d1eb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpqreaderagent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Eigenschaften des Warteschlangenlese-Agents zurück. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank oder auf dem Verleger für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@frompublisher=** ] *Frompublisher*  
 Gibt an, ob die gespeicherte Prozedur auf dem Verleger oder auf dem Verteiler aufgerufen wird. *Frompublisher* bit und hat den Standardwert 0. **1** bedeutet, dass die gespeicherte Prozedur vom Verleger aufgerufen wird und **0** bedeutet, dass die gespeicherte Prozedur vom Verteiler aufgerufen wird.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Die ID des Agents.|  
|**name**|**nvarchar(100)**|Der Name des Agents.|  
|**job_id**|**uniqueidentifier**|Eindeutige ID des Agentauftrags.|  
|**job_login**|**nvarchar(512)**|Ist das Windows-Konto unter dem der Verteilungs-Agent ausgeführt wird, der zurückgegeben wird, im Format *Domäne*\\*Benutzername*.|  
|**job_password**|**sysname**|Aus Sicherheitsgründen Wert  **\* \* \* \* \* \* \* \* \* \***  ist immer zurückgegeben.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpqreader_agent** wird bei der Transaktionsreplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn der Wert der *Frompublisher* ist **1**, nur Mitglieder der der **Sysadmin** auf dem Verleger oder Mitglieder der festen Serverrolle die **Db_owner**festen Datenbankrolle "" für die Veröffentlichungsdatenbank kann ausführen **Sp_helpqreader_agent**. Andernfalls nur Mitglieder der der **Sysadmin** auf dem Verteiler oder Mitglieder der festen Serverrolle die **Db_owner** festen Datenbankrolle "" für die Verteilungsdatenbank führen kann **Sp_helpqreader_ Agent**.  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
