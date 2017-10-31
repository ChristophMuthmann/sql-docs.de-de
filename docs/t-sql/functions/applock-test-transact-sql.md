---
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a272abaccb41653c9b1b0569738b74905e93e5c9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt Informationen darüber zurück, ob eine Sperre für eine bestimmte Anwendungsressource und einen angegebenen Sperrenbesitzer erteilt werden kann, ohne die Sperre zu aktivieren. APPLOCK_TEST ist eine Funktion für Anwendungssperren und wird in der aktuellen Datenbank ausgeführt. Die Datenbank umfasst den Bereich der Anwendungssperren.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumente  
**"** *Database_principal* **"**  
Der Benutzer, die Rolle oder die Anwendungsrolle, dem bzw. der Berechtigungen für Objekte in einer Datenbank erteilt werden können. Der Aufrufer der Funktion muss ein Mitglied sein *Database_principal*, **Dbo**, oder die **Db_owner** festen Datenbankrollen die Funktion erfolgreich aufzurufen.
  
**"** *Resource_name* **"**  
Der Name einer Sperrressource, der von der Clientanwendung angegeben wird. In der Anwendung muss sichergestellt sein, dass die Ressource eindeutig ist. Der angegebene Name wird intern als Hashwert in einem Wert gespeichert, der im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperren-Manager gespeichert werden kann. *Resource_name*ist **nvarchar(255)** hat keinen Standardwert. *Resource_name* Binärvergleich ist und die Groß-/Kleinschreibung beachtet, unabhängig von den sortierungseinstellungen der aktuellen Datenbank.
  
**"** *_mode* **"**  
Der Sperrmodus, der für eine bestimmte Ressource abgerufen werden soll. *_mode* ist **nvarchar(32)** und hat keinen Standardwert. Der Wert kann eine der folgenden sein: **Shared**, **Update**, **IntentShared**, **IntentExclusive**, **exklusive** .
  
**"** *Lock_owner* **"**  
Der Besitzer der Sperre ist die *Lock_owner* Wert, der beim Anfordern der Sperre. *Lock_owner* ist **nvarchar(32)**. Der Wert kann **Transaktion** (Standard) oder **Sitzung**. Wenn Standard oder **Transaktion** explizit angegeben wird, muss APPLOCK_TEST aus innerhalb einer Transaktion ausgeführt werden.
  
## <a name="return-types"></a>Rückgabetypen
**smallint**
  
## <a name="return-value"></a>Rückgabewert
Gibt 0 zurück, wenn die Sperre dem angegebenen Besitzer nicht erteilt werden kann. Wenn die Sperre erteilt werden kann, wird 1 zurückgegeben.
  
## <a name="function-properties"></a>Funktionseigenschaften
**Nicht deterministisch**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel zwei Benutzer (**Benutzer A** und **User B**) führen die folgende Sequenz von in getrennten Sitzungen [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen.
  
**Benutzer A** ausgeführt wird:
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
**Benutzer B** führt dann:
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
**Benutzer A** führt dann:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**Benutzer B** führt dann:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**Benutzer A** und **User B** beide führen:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[APPLOCK_MODE &#40; Transact-SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[Sp_getapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[Sp_releaseapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

