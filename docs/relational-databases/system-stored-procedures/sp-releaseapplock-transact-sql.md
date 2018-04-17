---
title: Sp_releaseapplock (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 503bfd0c13054852aeab822e3ec93d56a04bb4c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 Der Besitzer der Sperre. Dabei handelt es sich um den Wert von *lock_owner* beim Anfordern der Sperre. *lock_owner* ist vom Datentyp **nvarchar(32)**. Der Wert kann **Transaction** (Standard) oder **Session** sein. Wenn die *Lock_owner* Wert **Transaktion**, von Standard oder explizit angegeben wurde, Sp_getapplock muss aus ausgeführt werden innerhalb einer Transaktions.  
  
 [ @DbPrincipal=] '*Database_principal*"  
 Der Benutzer, die Rolle oder die Anwendungsrolle mit Berechtigungen für ein Objekt in einer Datenbank. Um eine Funktion erfolgreich aufzurufen, muss die aufrufende Funktion Mitglied einer der folgenden festen Datenbankrollen sein: *database_principal*, „dbo“ oder „db_owner“. Der Standardwert ist public.  
  
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
 [APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  
