---
title: APPLOCK_TEST (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 463c6e176cec6c0403e85bc75584e6bd890e0668
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Diese Funktion gibt Informationen darüber zurück, ob eine Sperre für eine bestimmte Anwendungsressource und einen angegebenen Sperrenbesitzer erteilt werden kann, ohne die Sperre zu aktivieren. APPLOCK_TEST ist eine Anwendungssperrfunktion, die für die aktuelle Datenbank gilt. Die Datenbank umfasst den Bereich der Anwendungssperren.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumente  
**'** *database_principal* **'**  
Der Benutzer, die Rolle oder die Anwendungsrolle, dem bzw. der Berechtigungen für Objekte in einer Datenbank erteilt werden können. Um eine Funktion erfolgreich aufzurufen, muss der Aufrufer der Funktion Mitglied einer der folgenden festen Datenbankrollen sein: *database_principal*, „dbo“ oder „db_owner“.
  
**'** *resource_name* **'**  
Der Name einer Sperrressource, der von der Clientanwendung angegeben wird. Die Anwendung muss sicherstellen, dass der Ressourcenname eindeutig ist. Der angegebene Name wird intern als Hashwert codiert, der intern im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperren-Manager gespeichert werden kann.  *resource_name* ist vom Datentyp **nvarchar(255)** und besitzt keinen Standardwert. *resource_name* unterliegt dem Binärvergleich. Daher muss die Groß-/Kleinschreibung unabhängig von den Sortierungseinstellungen der aktuellen Datenbank berücksichtigt werden.
  
**'** *lock_mode* **'**  
Der abzurufende Sperrmodus für eine spezifische Ressource. *lock_mode* ist vom Datentyp **nvarchar(32)** und verfügt nicht über einen Standardwert. *lock_mode* kann folgende Werte aufweisen: **Shared**, **Update**, **IntentShared**, **IntentExclusive** und **Exclusive**.
  
**'** *lock_owner* **'**  
Der Besitzer der Sperre. Dabei handelt es sich um den Wert von *lock_owner* beim Anfordern der Sperre. *lock_owner* ist vom Datentyp **nvarchar(32)**. Der Wert kann **Transaktion** (Standard) oder **Sitzung** entsprechen. Wird der Standard oder **Transaction** explizit angegeben, muss APPLOCK_TEST aus einer Transaktion heraus ausgeführt werden.
  
## <a name="return-types"></a>Rückgabetypen
**smallint**
  
## <a name="return-value"></a>Rückgabewert
0 (null), wenn die Sperre dem angegebenen Besitzer nicht erteilt werden kann. Wenn die Sperre erteilt werden kann, wird 1 zurückgegeben.
  
## <a name="function-properties"></a>Funktionseigenschaften
**Nondeterministic**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>Beispiele  
Zwei Benutzer (**Benutzer A** und **Benutzer B**) führen in getrennten Sitzungen die folgende Sequenz von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen aus.
  
**Benutzer A** führt Folgendes aus:
  
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
  
**Benutzer B** führt dann Folgendes aus:
  
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
  
**Benutzer A** führt dann Folgendes aus:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**Benutzer B** führt dann Folgendes aus:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**Benutzer A** und **Benutzer B** führen dann Folgendes aus:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
