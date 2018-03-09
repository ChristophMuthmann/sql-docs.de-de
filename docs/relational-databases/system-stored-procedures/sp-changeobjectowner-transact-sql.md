---
title: Sp_changeobjectowner (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00d4fbb90a767294e3d529e6fa5706eecfd841f1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Besitzer eines Objekts in der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  Diese gespeicherte Prozedur funktioniert nur mit den Objekten in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) oder [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) stattdessen. **Sp_changeobjectowner** ändert sowohl das Schema als auch den Besitzer. Aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ändert diese gespeicherte Prozedur nur Objektbesitzer, wenn sowohl der aktuelle Besitzer als auch der neue Besitzer Schemas besitzen, die den gleichen Namen wie die Datenbankbenutzernamen aufweisen.  
  
> [!IMPORTANT]  
>  Dieser gespeicherten Prozedur wurde eine neue Berechtigungsanforderung hinzugefügt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@objname =** ] **"***Objekt***"**  
 Der Name einer vorhandenen Tabelle, Sicht, benutzerdefinierten Funktion oder gespeicherter Prozedur in der aktuellen Datenbank. *Objekt* ist ein **nvarchar(776)**, hat keinen Standardwert. *Objekt* kann qualifiziert werden, mit dem Besitzer des vorhandenen Objekts, in der Form *existing_owner.Object***.** *Objekt* , wenn das Schema und der schemabesitzer den gleichen Namen haben.  
  
 [  **@newowner=**] **"***Besitzer* **"**  
 Der Name des Sicherheitskontos, das den neuen Besitzer des Objekts darstellt. *Besitzer* ist **Sysname**, hat keinen Standardwert. *Besitzer* muss ein gültiger Datenbankbenutzer, eine Serverrolle [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldename oder Windows-Gruppe mit Zugriff auf die aktuelle Datenbank. Wenn es sich beim neuen Besitzer um einen Windows-Benutzer oder eine Windows-Gruppe handelt, für den bzw. die kein entsprechender Datenbankprinzipal vorhanden ist, wird ein Datenbankbenutzer erstellt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changeobjectowner** entfernt alle vorhandene Berechtigungen aus dem Objekt. Sie müssen sämtliche Berechtigungen erneut zuweisen, die Sie nach der Ausführung beibehalten möchten **Sp_changeobjectowner**. Deshalb wird empfohlen, dass Sie bestehende Berechtigungen vor ihrer Ausführung Skript **Sp_changeobjectowner**. Nachdem der Besitz des Objekts geändert wurde, können Sie das Skript verwenden, um die Berechtigungen erneut zuzuweisen. Sie müssen den Objektbesitzer im Berechtigungsskript vor dem Ausführen ändern.  
  
 Wenn Sie den Besitzer eines sicherungsfähigen Elements ändern möchten, verwenden Sie ALTER AUTHORIZATION. Zum Ändern eines Schemas verwenden Sie ALTER SCHEMA.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in den beiden die **Db_ddladmin** festen Datenbankrolle "" und die **Db_securityadmin** feste Datenbankrolle und auch über die CONTROL-Berechtigung für das Objekt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Besitzer der `authors`-Tabelle zu `Corporate\GeorgeW` geändert.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
