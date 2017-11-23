---
title: Sp_deletepeerrequesthistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords: sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9deb92cbdc9eff3e54efb1b37d18abc7bfc01252
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht Verlaufsdaten im Zusammenhang mit einer veröffentlichungsstatusanforderung, darunter den anforderungsverlauf ([MSpeer_request &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) sowie den ([MSpeer_response &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/mspeer-response-transact-sql.md)). Diese gespeicherte Prozedur wird für die Veröffentlichungsdatenbank auf einem Verleger in einer Peer-zu-Peer-Replikationstopologie ausgeführt. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, für die die Statusanforderung ausgeführt wurde. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@request_id=** ] *Request_id*  
 Gibt eine einzelne Statusanforderung an, damit alle Antworten auf diese Anforderung gelöscht werden. *Request_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@cutoff_date=** ] *Cutoff_date*  
 Gibt ein Umstellungsdatum an. Alle Antwortdatensätze mit einem früheren Datum werden gelöscht. *Cutoff_date* ist **"DateTime"**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_deletepeerrequesthistory** wird in einer Peer-zu-Peer-transaktionsreplikationstopologie verwendet. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Beim Ausführen von **Sp_deletepeerrequesthistory**, entweder *Request_id* oder *Cutoff_date* muss angegeben werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_deletepeerrequesthistory**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_helppeerrequests &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [Sp_helppeerresponses &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [Sp_requestpeerresponse &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
