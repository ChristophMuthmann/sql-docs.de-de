---
title: Sp_requestpeerresponse (Transact-SQL) | Microsoft Docs
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
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 233189ee46144b4acd6e880f2f5b5875af551ff4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wenn diese Prozedur auf einem Knoten in einer Peer-zu-Peer-Topologie ausgeführt wird, fordert sie von jedem anderen Knoten in der Topologie eine Antwort an. Durch Ausführen dieser Prozedur und Überprüfen der entsprechenden Antworten können Sie sicherstellen, dass alle früheren Befehle an die antwortenden Knoten übermittelt wurden. Diese gespeicherte Prozedur wird auf dem anfordernden Knoten auf jeder Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication**=] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung in einer Peer-zu-Peer-Topologie, für die der Status überprüft wird. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@description**=] **"***Beschreibung***"**  
 Benutzerdefinierte Informationen, mit denen einzelne Statusanforderungen identifiziert werden können. *Beschreibung* ist **nvarchar(4000)**, hat den Standardwert NULL.  
  
 [ **@request_id** =] *Request_id*  
 Gibt die ID der neuen Anforderung zurück. *Request_id* ist **Int** und ist ein OUTPUT-Parameter. Dieser Wert kann verwendet werden, für die Ausführung [Sp_helppeerresponses &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) um alle Antworten auf eine statusanforderung anzuzeigen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_requestpeerresponse** wird in der Peer-zu-Peer-Transaktionsreplikation verwendet.  
  
 **Sp_requestpeerresponse** wird verwendet, um sicherzustellen, dass alle Befehle vor dem Wiederherstellen einer Datenbank in einer Peer-zu-Peer-Topologie veröffentlicht. alle anderen Knoten empfangen wurden. Die Prozedur wird außerdem beim Replizieren von DDL-Änderungen (Data Definition Language) verwendet, die vorgenommen wurden, während ein Knoten offline war. Damit kann abgeschätzt werden, wann diese Änderungen bei den anderen Knoten ankommen.  
  
 **Sp_requestpeerresponse** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_requestpeerresponse**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [Sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
