---
title: Sp_getapplock (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_getapplock_TSQL
- sp_getapplock
dev_langs: TSQL
helpviewer_keywords:
- application locks
- sp_getapplock
ms.assetid: e1e85908-9f31-47cf-8af6-88c77e6f24c9
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5c7b65a7330a1b87e7ee81a4f76a715038cd3d6d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spgetapplock-transact-sql"></a>sp_getapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sperrt eine Anwendungsressource.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_getapplock [ @Resource = ] 'resource_name' ,  
     [ @LockMode = ] 'lock_mode'   
     [ , [ @LockOwner = ] 'lock_owner' ]   
     [ , [ @LockTimeout = ] 'value' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @Resource=] '*Resource_name*"  
 Zeichenfolge, die einen Namen zum Identifizieren der Sperrressource angibt. Die Anwendung muss sicherstellen, dass der Ressourcenname eindeutig ist. Der angegebene Name wird intern als Hashwert in einem Wert gespeichert, der im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sperren-Manager gespeichert werden kann. *Resource_name* ist **nvarchar(255)** hat keinen Standardwert. Wenn eine Ressourcenzeichenfolge länger als ist **nvarchar(255)**, wird es abgeschnitten **nvarchar(255)**.  
  
 *Resource_name* binären Vergleich und daher wird Groß-/Kleinschreibung beachtet, unabhängig von den sortierungseinstellungen der aktuellen Datenbank.  
  
> [!NOTE]  
>  Nachdem eine Anwendungssperre eingerichtet wurde, können nur die ersten 32 Zeichen im Nur-Text-Format abgerufen werden. Die übrigen Zeichen werden hashcodiert.  
  
 [ @LockMode=] '*_mode*"  
 Der Sperrmodus, der für eine bestimmte Ressource abgerufen werden soll. *_mode* ist **nvarchar(32)** und hat keinen Standardwert. Der Wert kann eine der folgenden sein: **Shared**, **Update**, **IntentShared**, **IntentExclusive**, oder **exklusive** .  
  
 [ @LockOwner=] '*Lock_owner*"  
 Der Besitzer der Sperre ist die *Lock_owner* Wert, der beim Anfordern der Sperre. *Lock_owner* ist **nvarchar(32)**. Der Wert kann **Transaktion** (Standard) oder **Sitzung**. Wenn die *Lock_owner* Wert **Transaktion**, von Standard oder explizit angegeben wurde, Sp_getapplock muss aus ausgeführt werden innerhalb einer Transaktions.  
  
 [ @LockTimeout=] '*Wert*"  
 Der Wert für das Sperrtimeout in Millisekunden. Der Standardwert ist identisch mit den Rückgabewert von@LOCK_TIMEOUT. Damit bei Sperranforderungen, die nicht sofort erteilt werden können, nicht auf die Sperre gewartet, sondern ein Fehler zurückgegeben wird, geben Sie 0 an.  
  
 [ @DbPrincipal=] '*Database_principal*"  
 Der Benutzer, die Rolle oder die Anwendungsrolle mit Berechtigungen für ein Objekt in einer Datenbank. Der Aufrufer der Funktion muss ein Mitglied sein *Database_principal*, Dbo oder Db_owner festen Datenbankrolle an die Funktion erfolgreich aufzurufen. Der Standardwert ist public.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 \>= 0 (Erfolg) oder < 0 (Fehler)  
  
|Wert|Ergebnis|  
|-----------|------------|  
|0|Die Sperre wurde erfolgreich synchron erteilt.|  
|1|Die Sperre wurde erfolgreich erteilt, nachdem das Aufheben anderer, inkompatibler Sperren abgewartet wurde.|  
|-1|Timeout für die Sperranforderung.|  
|-2|Die Sperranforderung wurde abgebrochen.|  
|-3|Die Sperranforderung wurde als Deadlockopfer gewählt.|  
|-999|Gibt einen Fehler bei Parameterüberprüfung oder einen anderen Aufruffehler an.|  
  
## <a name="remarks"></a>Hinweise  
 Für eine Ressource bestehende Sperren sind der aktuellen Transaktion oder der aktuellen Sitzung zugeordnet. Der aktuellen Transaktion zugeordnete Sperren werden aufgehoben, wenn für die Transaktion ein Commit oder ein Rollback ausgeführt wird. Der aktuellen Sitzung zugeordnete Sperren werden aufgehoben, wenn die Sitzung abgemeldet wird. Wenn der Server aus irgendeinem Grund heruntergefahren wird, werden alle Sperren aufgehoben.  
  
 Die von sp_getapplock erstellte Sperrenressource wird in der aktuellen Datenbank der Sitzung erstellt. Jede Sperrenressource wird durch die kombinierten Werte folgender Elemente identifiziert:  
  
-   Die Datenbank-ID der Datenbank, die die Sperrenressource enthält.  
  
-   Der im @DbPrincipal-Parameter angegebene Datenbankprinzipal.  
  
-   Der im @Resource-Parameter angegebene Name für die Sperre.  
  
 Nur ein Mitglied des im @DbPrincipal-Parameter angegebenen Datenbankprinzipals kann Anwendungssperren einrichten, die diesen Prinzipal angeben. Mitglieder der Rollen dbo und db_owner werden implizit als Mitglieder aller Rollen betrachtet.  
  
 Mit sp_releaseapplock können Sperren explizit aufgehoben werden. Wenn eine Anwendung mehrere Male sp_getapplock für dieselbe Sperrenressource aufruft, muss sp_releaseapplock genauso oft aufgerufen werden, um die Sperre aufzuheben.  
  
 Wenn sp_getapplock mehrere Male für dieselbe Sperrenressource aufgerufen wird, aber eine der Anforderungen einen Sperrmodus angibt, der nicht mit dem vorhandenen Modus übereinstimmt, kommt es in Bezug auf die Ressource zu einer Vereinigung der beiden Sperrmodi. In den meisten Fällen bedeutet dies, dass der Sperrmodus zum Stärkeren der Sperrmodi, d. h. des vorhandenen oder des neu angeforderten, heraufgestuft wird. Der stärkere Sperrmodus wird beibehalten, bis die Sperre endgültig aufgehoben wird, selbst wenn schon vorher Aufrufe zur Aufhebung der Sperre auftreten. In der folgenden Aufrufsequenz bleibt die Ressource im `Exclusive`-Modus und nicht im `Shared`-Modus.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
EXEC @result = sp_releaseapplock @Resource = 'Form1';  
COMMIT TRANSACTION;  
GO  
```  
  
 Ein Deadlock mit einer Anwendungssperre führt keinen Rollback für die Transaktion durch, die die Anwendungssperre angefordert hat. Jeder Rollback, der möglicherweise als Ergebnis des Rückgabewertes benötigt wird, muss manuell ausgeführt werden. Daher wird empfohlen, die Fehlerüberprüfung im Code einzuschließen, sodass bei Rückgabe bestimmter Werte (z. B. -3) ein ROLLBACK TRANSACTION-Vorgang oder eine andere Aktion initiiert wird.  
  
 Beispiel:  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
IF @result = -3  
BEGIN  
    ROLLBACK TRANSACTION;  
END  
ELSE  
BEGIN  
    EXEC @result = sp_releaseapplock @Resource = 'Form1';  
    COMMIT TRANSACTION;  
END;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die aktuelle Datenbank-ID, um die Ressource zu kennzeichnen. Beim Ausführen von sp_getapplock führt dies zu unterschiedlichen Sperren auf unterschiedlichen Ressourcen, selbst wenn identische Parameterwerte auf verschiedenen Datenbanken verwendet werden.  
  
 Verwenden Sie die dynamische Verwaltungssicht sys.dm_tran_locks oder die gespeicherte Systemprozedur sp_lock zum Überprüfen von Sperrinformationen, oder verwenden Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], um Sperren zu überwachen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine freigegebene Sperre, die der aktuellen Transaktion zugeordnet ist, für die `Form1`-Ressource in der `AdventureWorks2012`-Datenbank eingerichtet.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
 Im folgenden Beispiel wird `dbo` als Datenbankprinzipal angegeben.  
  
```  
BEGIN TRAN;  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'AdventureWorks2012',   
     @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [APPLOCK_MODE &#40; Transact-SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40; Transact-SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [Sp_releaseapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)  
  
  
