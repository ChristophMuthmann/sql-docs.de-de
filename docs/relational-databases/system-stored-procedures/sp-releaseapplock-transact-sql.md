---
title: Sp_releaseapplock (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb17b39125209ca15214356e84f832e2f8cbc73
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spreleaseapplock-transact-sql"></a>sp_releaseapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Sperre für eine Anwendungsressource frei.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_releaseapplock [ @Resource = ] 'resource_name'   
     [ , [ @LockOwner = ] 'lock_owner' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @Resource=] '*Resource_name*"  
 Der Name einer Sperrressource, der von der Clientanwendung angegeben wird. In der Anwendung muss sichergestellt sein, dass die Ressource eindeutig ist. Der angegebene Name wird intern als Hashwert in einem Wert gespeichert, der im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperren-Manager gespeichert werden kann. *Resource_name* ist **nvarchar(255)** hat keinen Standardwert. *Resource_name* ist Binärvergleich, daher wird Groß-/Kleinschreibung beachtet, unabhängig von den sortierungseinstellungen der aktuellen Datenbank.  
  
 [ @LockOwner=] '*Lock_owner*"  
 Der Besitzer der Sperre ist die *Lock_owner* Wert, der beim Anfordern der Sperre. *Lock_owner* ist **nvarchar(32)**. Der Wert kann **Transaktion** (Standard) oder **Sitzung**. Wenn die *Lock_owner* Wert **Transaktion**, von Standard oder explizit angegeben wurde, Sp_getapplock muss aus ausgeführt werden innerhalb einer Transaktions.  
  
 [ @DbPrincipal=] '*Database_principal*"  
 Der Benutzer, die Rolle oder die Anwendungsrolle mit Berechtigungen für ein Objekt in einer Datenbank. Der Aufrufer der Funktion muss ein Mitglied sein *Database_principal*, Dbo oder Db_owner festen Datenbankrolle um die Funktion erfolgreich aufzurufen. Der Standardwert ist public.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 \>= 0 (Erfolg) oder < 0 (Fehler)  
  
|Wert|Ergebnis|  
|-----------|------------|  
|0|Die Sperre wurde erfolgreich aufgehoben.|  
|-999|Weist auf einen Fehler bei der Parameterüberprüfung oder einen anderen Aufruffehler hin.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Anwendung mehrere Male sp_getapplock für dieselbe Sperrenressource aufruft, muss sp_releaseapplock genauso oft aufgerufen werden, um die Sperre aufzuheben.  
  
 Wenn der Server aus irgendeinem Grund heruntergefahren wird, werden die Sperren aufgehoben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Sperre, die der aktuellen Transaktion zugeordnet ist, für die Ressource `Form1` in der `AdventureWorks2012`-Datenbank aufgehoben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'Form1',   
     @LockMode = 'Shared';  
EXEC sp_releaseapplock @DbPrincipal = 'dbo', @Resource = 'Form1';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [APPLOCK_MODE &#40; Transact-SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40; Transact-SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [Sp_getapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  
