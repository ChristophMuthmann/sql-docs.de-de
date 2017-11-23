---
title: APPLOCK_MODE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs: TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6b5c0a0879580e5c1e084259b61ff206d49c896
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Sperrmodus zurück, der vom Besitzer der Sperre für eine bestimmte Anwendungsressource aufrechterhalten wird. APPLOCK_MODE ist eine Anwendungssperrfunktion, die für die aktuelle Datenbank gilt. Die Datenbank umfasst den Bereich der Anwendungssperren.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumente  
"*Database_principal*"  
Der Benutzer, die Rolle oder die Anwendungsrolle, dem bzw. der Berechtigungen für Objekte in einer Datenbank erteilt werden können. Der Aufrufer der Funktion muss ein Mitglied sein *Database_principal*, Dbo oder Db_owner festen Datenbankrolle um die Funktion erfolgreich aufzurufen.
  
"*Resource_name*"  
Der Name einer Sperrressource, der von der Clientanwendung angegeben wird. Die Anwendung muss sicherstellen, dass der Ressourcenname eindeutig ist. Der angegebene Name wird intern als Hashwert in einem Wert gespeichert, der im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperren-Manager gespeichert werden kann. *Resource_name*ist **nvarchar(255)** hat keinen Standardwert. *Resource_name* binäre verglichen und Groß-/Kleinschreibung beachtet, unabhängig von den sortierungseinstellungen der aktuellen Datenbank.
  
"*Lock_owner*"  
Der Besitzer der Sperre ist die *Lock_owner* Wert, der beim Anfordern der Sperre. *Lock_owner* ist **nvarchar(32)**, und der Wert kann entweder **Transaktion** (Standard) oder **Sitzung**.
  
## <a name="return-types"></a>Rückgabetypen
**nvarchar(32)**
  
## <a name="return-value"></a>Rückgabewert
Gibt den Sperrmodus zurück, der vom Besitzer der Sperre für eine bestimmte Anwendungsressource aufrechterhalten wird. Für den Sperrmodus sind die folgenden Werte möglich:
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Freigegebene**|**Exclusive**||  
  
*Dieser Sperrmodus ist eine Kombination aus anderen Sperrmodi und kann nicht mithilfe von sp_getapplock explizit aktiviert werden.
  
## <a name="function-properties"></a>Funktionseigenschaften
**Nicht deterministisch**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>Beispiele  
Zwei Benutzer (Benutzer A und Benutzer B) führen in getrennten Sitzungen die folgende Sequenz von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen aus.
  
Benutzer A führt Folgendes aus:
  
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
  
Benutzer B führt dann Folgendes aus:
  
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
  
Benutzer A führt dann Folgendes aus:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
Benutzer B führt dann Folgendes aus:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
Benutzer A und Benutzer B führen dann Folgendes aus:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[APPLOCK_TEST &#40; Transact-SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[Sp_getapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[Sp_releaseapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
