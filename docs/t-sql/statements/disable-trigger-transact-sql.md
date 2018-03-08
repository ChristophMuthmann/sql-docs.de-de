---
title: DISABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 69398e740c4ae5ca49c93b1f70d7c02a0d3fbf42
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
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
 Der Name des Schemas, zu dem der Trigger gehört. *Schema_name* kann für DDL- oder Logon-Trigger angegeben werden.  
  
 *Form trigger_name*  
 Der Name des Triggers, der deaktiviert werden soll.  
  
 ALL  
 Gibt an, dass alle im Bereich der ON-Klausel definierten Trigger deaktiviert sind.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt Trigger in Datenbanken, die für die Mergereplikation veröffentlicht werden. Die Angabe von ALL in veröffentlichten Datenbanken deaktiviert diese Trigger, wodurch die Replikation unterbrochen wird. Überprüfen Sie, dass die aktuelle Datenbank nicht für die Mergereplikation veröffentlicht ist, bevor Sie ALL angeben.  
  
 *object_name*  
 Der Name der Tabelle oder Sicht, die auf dem der DML-trigger *Form Trigger_name* zur Ausführung erstellt wurde.  
  
 DATABASE  
 Für einen DDL-Trigger gibt an, dass *Form Trigger_name* erstellt oder zum Ausführen von mit Datenbankbereich geändert wurde.  
  
 ALL SERVER  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Für einen DDL-Trigger gibt an, dass *Form Trigger_name* erstellt oder zum Ausführen von mit einem Serverbereich geändert wurde. ALL SERVER gilt auch für LOGON-Trigger.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="remarks"></a>Hinweise  
 Trigger werden beim Erstellen standardmäßig aktiviert. Durch das Deaktivieren wird ein Trigger nicht gelöscht. Der Trigger ist weiterhin als Objekt in der aktuellen Datenbank vorhanden. Allerdings der Trigger wird nicht ausgelöst, wenn ein [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen für die er programmiert wurde ausgeführt. Trigger können erneut aktiviert werden, mithilfe von [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md). Für Tabellen definierte DML-Trigger kann auch deaktiviert oder aktiviert werden, mithilfe von [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 Das Ändern des Triggers mithilfe der **ALTER TRIGGER** -Anweisung aktiviert den Trigger.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Deaktivieren eines DML-Triggers muss ein Benutzer mindestens die ALTER-Berechtigung für die Tabelle oder Sicht haben, für die der Trigger erstellt wurde.  
  
 Zum Deaktivieren eines DDL-Triggers mit Serverbereich (ON ALL SERVER) oder eines LOGON-Triggers benötigt der Benutzer die CONTROL SERVER-Berechtigung auf dem Server. Um einen DDL-Trigger mit Datenbankbereich (ON DATABASE) zu deaktivieren, muss der Benutzer mindestens die ALTER ANY DATABASE DDL TRIGGER-Berechtigung für die aktuelle Datenbank haben.  
  
## <a name="examples"></a>Beispiele  
In den folgenden Beispielen werden in der AdventureWorks2012-Datenbank beschrieben.
  
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
  
## <a name="see-also"></a>Siehe auch  
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
