---
title: Sp_helppeerresponses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d429769ece609f17a1ffacc80f818a20ca285947
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt alle Antworten auf einen bestimmten Status von einem Beteiligten an einer Peer-zu-Peer-Replikationstopologie, in dem die Anforderung, durch das Ausführen initiiert wurde empfangene [Sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) in einer beliebigen veröffentlichten Datenbank in der Topologie. Diese gespeicherte Prozedur wird für die Veröffentlichungsdatenbank auf einem Verleger ausgeführt, der an der Peer-zu-Peer-Replikationstopologie beteiligt ist. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@request_id**=] *Request_id*  
 Die ID einer bestimmten Statusanforderung. *Request_id* ist **Int**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|ID der Statusanforderung.|  
|**Peer**|**sysname**|Der Name des Peers, der die Antwort generiert hat.|  
|**peer_db**|**sysname**|Der Datenbankname auf dem Peer, der die Antwort generiert hat.|  
|**received_date**|**datetime**|Datum und Uhrzeit, zu dem der Anforderer die vom Peer gesendete Antwort erhalten hat.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helppeerresponses** wird in der Peer-zu-Peer-Transaktionsreplikation verwendet.  
  
 **Sp_helppeerresponses** Prozedur wird verwendet, wenn das Wiederherstellen einer Datenbank in einer Peer-zu-Peer-Topologie veröffentlicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_helppeerresponses**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [Sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
