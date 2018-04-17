---
title: Sp_unregistercustomresolver (Transact-SQL) | Microsoft Docs
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
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8da6d1040171f3da5269962dd75e265e4486143
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spunregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt die Registrierung eines zuvor registrierten Geschäftslogikmoduls auf. Geschäftslogik kann in Form einer COM-Komponente oder einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Assembly vorliegen. Diese gespeicherte Prozedur wird auf dem Verteiler ausgeführt, auf dem die benutzerdefinierte Geschäftslogik registriert wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@article_resolver =** ] **"***Article_resolver***"**  
 Gibt den Namen der benutzerdefinierten Geschäftslogik an, deren Registrierung aufgehoben wird. *Article_resolver* ist **nvarchar(255)**, hat keinen Standardwert. Wenn es sich bei der zu entfernenden Geschäftslogik um eine COM-Komponente handelt, ist dieser Parameter der Anzeigename der Komponente. Handelt es sich bei der Geschäftslogik um eine .NET Framework-Assembly, ist dieser Parameter der Name der Assembly.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_unregistercustomresolver** wird bei der Mergereplikation verwendet.  
  
 Verwendung [Sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) auf jedem Server in der Replikationstopologie, um die Liste der registrierten benutzerdefinierten geschäftslogikmodule oder COM-Konfliktlöser verfügbar zur Topologie zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_unregistercustomresolver**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [Sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
