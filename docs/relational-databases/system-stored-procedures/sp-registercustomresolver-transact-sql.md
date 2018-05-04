---
title: Sp_registercustomresolver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7ed693b83e3266390fb3ee245e1681b6350ed51c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spregistercustomresolver-transact-sql"></a>sp_registercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registriert einen Geschäftslogikhandler oder einen COM-basierten benutzerdefinierten Konfliktlöser, der während der Synchronisierung der Mergereplikation aufgerufen werden kann. Diese gespeicherte Prozedur wird auf dem Verteiler ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@article_resolver =** ] **"***Article_resolver***"**  
 Gibt den Anzeigenamen für die benutzerdefinierte Geschäftslogik an, die registriert wird. *Article_resolver* ist **nvarchar(255)**, hat keinen Standardwert.  
  
 [  **@resolver_clsid=** ] **"***Resolver_clsid***"**  
 Gibt den CLSID-Wert des COM-Objekts an, das registriert wird. Benutzerdefinierte Geschäftslogik *Resolver_clsid* ist **nvarchar(50)**, hat den Standardwert NULL. Dieser Parameter muss auf eine gültige CLSID oder auf NULL festgelegt werden, wenn Sie eine Assembly für einen Geschäftslogikhandler registrieren.  
  
 [  **@is_dotnet_assembly=** ] **"***Is_dotnet_assembly***"**  
 Gibt den Typ der benutzerdefinierten Geschäftslogik an, die registriert wird. *Is_dotnet_assembly* ist **nvarchar(50)**, hat den Standardwert "false". **"true"** gibt an, dass die benutzerdefinierte Geschäftslogik, die registriert eine Geschäftslogikhandler-Assembly; **"false"** gibt an, dass es sich um eine COM-Komponente ist.  
  
 [  **@dotnet_assembly_name=** ] **"***Dotnet_assembly_name***"**  
 Der Name der Assembly, die den Geschäftslogikhandler implementiert. *Dotnet_assembly_name* ist **nvarchar(255)**, hat den Standardwert NULL. Sie müssen den vollständigen Pfad zur Assembly angeben, falls sie nicht im gleichen Verzeichnis wie die ausführbare Datei für den Merge-Agent, im gleichen Verzeichnis wie die Anwendung, mit der der Merge-Agent synchron gestartet wird, oder im globalen Assemblycache (GAC) bereitgestellt wird.  
  
 [  **@dotnet_class_name=** ] **"***Dotnet_class_name***"**  
 Der Name der Klasse, die <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> überschreibt, um den Geschäftslogikhandler zu implementieren Der Name muss angegeben werden, in der Form **Namespace.Classname**. *Dotnet_class_name* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_registercustomresolver** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_registercustomresolver**.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [Sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [Sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
