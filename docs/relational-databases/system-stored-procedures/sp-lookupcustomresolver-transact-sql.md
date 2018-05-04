---
title: Sp_lookupcustomresolver (Transact-SQL) | Microsoft Docs
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
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 65770490b7a04efed2a4d7e70a2863fe45d5d453
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Informationen zu einem Geschäftslogikhandler oder den Wert des Klassenbezeichners (CLSID, Class Identifier) einer COM-basierten Komponente für benutzerdefinierte Konfliktlöser zurück, die auf dem Verteiler registriert sind. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@article_resolver =** ] **"***Article_resolver***"**  
 Gibt den Namen der benutzerdefinierten Geschäftslogik an, deren Registrierung aufgehoben wird. *Article_resolver* ist **nvarchar(255)**, hat keinen Standardwert. Wenn die Geschäftslogik, die entfernt wird, eine COM-Komponente ist, ist dieser Parameter der angezeigte Name der Komponente. Wenn die Geschäftslogik eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Assembly ist, ist dieser Parameter der Name der Assembly.  
  
 [ **@resolver_clsid**=] **"***Resolver_clsid***"** Ausgabe  
 Der CLSID-Wert des COM-Objekts, das den Namen der benutzerdefinierten Geschäftslogik an, die im angegebenen zugeordnet ist die *Article_resolver* Parameter. *Resolver_clsid* ist **nvarchar(50)**, hat den Standardwert NULL.  
  
 [  **@is_dotnet_assembly=** ] **"***Is_dotnet_assembly***"** Ausgabe  
 Gibt den Typ der benutzerdefinierten Geschäftslogik an, die registriert wird. *Is_dotnet_assembly* ist **Bit**, hat den Standardwert 0. **1** gibt an, dass die benutzerdefinierte Geschäftslogik, die registriert eine Geschäftslogikhandler-Assembly; **0** gibt an, dass es sich um eine COM-Komponente ist.  
  
 [  **@dotnet_assembly_name=** ] **"***Dotnet_assembly_name***"** Ausgabe  
 Der Name der Assembly, die den Geschäftslogikhandler implementiert. *Dotnet_assembly_name* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@dotnet_class_name=** ] **"***Dotnet_class_name***"** Ausgabe  
 Der Name der Klasse, die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> überschreibt, um den Geschäftslogikhandler zu implementieren *Dotnet_class_name* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL. Verwenden Sie diesen Parameter, wenn die gespeicherte Prozedur nicht vom Verleger aufgerufen wird. Wenn keine Angabe erfolgt, wird davon ausgegangen, dass der lokale Server der Verleger ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_lookupcustomresolver** wird bei der Mergereplikation verwendet.  
  
 **Sp_lookupcustomresolver** gibt einen Nullwert für *Resolver_clsid* Wenn die Komponente ist nicht registriert auf dem Verteiler ein Wert von "00000000-0000-0000-0000-000000000000"haben, wenn die Registrierung zu gehört ein .NET Framework-Assembly, die als Geschäftslogikhandler registriert werden.  
  
 **Sp_lookupcustomresolver** wird aufgerufen, indem [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [Sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) zur Überprüfung des angegebenen *Article_resolver*.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Db_owner** festen Datenbankrolle "" für die Veröffentlichungsdatenbank kann ausführen **Sp_lookupcustomresolver**.  
  
## <a name="see-also"></a>Siehe auch  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Ausführen der Geschäftslogik während der Mergesynchronisierung](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Angeben eines Mergeartikelkonfliktlösers](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [Sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
