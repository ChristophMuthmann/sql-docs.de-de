---
title: Sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
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
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d36b7578a9194b8220e1aeb771b47e7ef10bcd0c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Überprüft, ob der aktuelle Host für die Veröffentlichungsdatenbank die Replikation unterstützen kann. Muss von einer Verteilungsdatenbank ausgeführt werden. Diese Prozedur wird aufgerufen, indem **Sp_get_redirected_publisher**.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@original_publisher** =] **"***Original_publisher***"**  
 Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, die die Datenbank ursprünglich veröffentlicht hat. *Original_publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Der Name der zu veröffentlichenden Datenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@redirected_publisher** =] **"***Redirected_publisher***"**  
 Das Ziel der Umleitung angegebenen **Sp_redirect_publisher** für das Verleger-/Datenbankpaar aufgerufen wurde. *Redirected_publisher* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 Wenn kein Eintrag für den Verleger und die Veröffentlichungsdatenbank vorhanden ist **Sp_validate_redirected_publisher** null im Ausgabeparameter zurückgegeben *@redirected_publisher*. Wenn ein Eintrag vorhanden ist, wird er im Ausgabeparameter in Erfolgs- und Fehlerfällen zurückgegeben.  
  
 Bei erfolgreicher Validierung **Sp_validate_redirected_publisher** eine erfolgsanzeige zurück.  
  
 Wenn die Überprüfung fehlschlägt, werden Fehler mit einer Fehlerbeschreibung ausgelöst.  
  
## <a name="permissions"></a>Berechtigungen  
 Aufrufer muss entweder ein Mitglied der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle "" für die Verteilungsdatenbank oder ein Mitglied einer veröffentlichungszugriffsliste für eine definierte Veröffentlichung der Verlegerdatenbank zugeordnet.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [Sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [Sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
