---
title: DISABLE TRIGGER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: eaffa8b51daea942631e5f6d18609d2f12d98717
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Deaktiviert einen Trigger.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem der Trigger gehört. *schema_name* kann für DDL- oder LOGON-Trigger nicht angegeben werden.  
  
 *trigger_name*  
 Der Name des Triggers, der deaktiviert werden soll.  
  
 ALL  
 Gibt an, dass alle im Bereich der ON-Klausel definierten Trigger deaktiviert sind.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt Trigger in Datenbanken, die für die Mergereplikation veröffentlicht werden. Die Angabe von ALL in veröffentlichten Datenbanken deaktiviert diese Trigger, wodurch die Replikation unterbrochen wird. Überprüfen Sie, dass die aktuelle Datenbank nicht für die Mergereplikation veröffentlicht ist, bevor Sie ALL angeben.  
  
 *object_name*  
 Der Name der Tabelle oder Sicht, in der der DML-Trigger *trigger_name* zur Ausführung erstellt wurde.  
  
 DATABASE  
 Für einen DDL-Trigger wird dadurch angegeben, dass *trigger_name* zur Ausführung mit dem Datenbankbereich erstellt oder geändert wurde.  
  
 ALL SERVER  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Für einen DDL-Trigger wird hiermit angegeben, dass *trigger_name* zur Ausführung mit dem Serverbereich erstellt oder geändert wurde. ALL SERVER gilt auch für LOGON-Trigger.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="remarks"></a>Remarks  
 Trigger werden beim Erstellen standardmäßig aktiviert. Durch das Deaktivieren wird ein Trigger nicht gelöscht. Der Trigger ist weiterhin als Objekt in der aktuellen Datenbank vorhanden. Der Trigger wird jedoch bei der Ausführung von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausgelöst, für die er programmiert wurde. Trigger können mithilfe von [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md) erneut aktiviert werden. Für Tabellen definierte DML-Trigger können auch mithilfe von [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) deaktiviert oder aktiviert werden.  
  
 Das Ändern des Triggers durch Verwendung der **ALTER TRIGGER**-Anweisung aktiviert den Trigger.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Deaktivieren eines DML-Triggers muss ein Benutzer mindestens die ALTER-Berechtigung für die Tabelle oder Sicht haben, für die der Trigger erstellt wurde.  
  
 Zum Deaktivieren eines DDL-Triggers mit Serverbereich (ON ALL SERVER) oder eines LOGON-Triggers benötigt der Benutzer die CONTROL SERVER-Berechtigung auf dem Server. Um einen DDL-Trigger mit Datenbankbereich (ON DATABASE) zu deaktivieren, muss der Benutzer mindestens die ALTER ANY DATABASE DDL TRIGGER-Berechtigung für die aktuelle Datenbank haben.  
  
## <a name="examples"></a>Beispiele  
Die folgenden Beispiele werden in der AdventureWorks2012-Datenbank beschrieben.
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>A. Deaktivieren eines DML-Triggers für eine Tabelle  
 Im folgenden Beispiel wird der Trigger `uAddress` deaktiviert, der für die `Address`-Tabelle erstellt wurde.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>B. Deaktivieren eines DDL-Triggers  
 Im folgenden Beispiel wird der DDL-Trigger `safety` mit Datenbankbereich erstellt und anschließend deaktiviert.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. Deaktivieren aller Trigger, die mit dem gleichen Bereich definiert wurden  
 Im folgenden Beispiel werden alle DDL-Trigger deaktiviert, die im Serverbereich erstellt wurden.  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
