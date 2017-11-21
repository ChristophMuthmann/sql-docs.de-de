---
title: ENABLE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
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
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb2fba080ea3c51e5c29456b2166eeea6274f8a3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aktiviert einen DML-, DDL- oder LOGON-Trigger.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem der Trigger gehört. *Schema_name* kann für DDL- oder Logon-Trigger angegeben werden.  
  
 *Form trigger_name*  
 Der Name des Triggers, der aktiviert werden soll.  
  
 ALL  
 Gibt an, dass alle im Bereich der ON-Klausel definierten Trigger aktiviert sind.  
  
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
 Durch das Aktivieren eines Triggers wird dieser nicht neu erstellt. Ein deaktivierter Trigger ist weiterhin als Objekt in der aktuellen Datenbank vorhanden, wird jedoch nicht ausgelöst. Durch das Aktivieren eines Triggers wird dieser ausgelöst, wenn eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ausgeführt wird, für die er ursprünglich programmiert wurde. Trigger werden mithilfe von deaktiviert [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md). Für Tabellen definierte DML-Trigger kann auch deaktiviert oder aktiviert werden, mithilfe von [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Aktivieren eines DML-Triggers benötigt der Benutzer mindestens die ALTER-Berechtigung für die Tabelle oder Sicht, in der der Trigger erstellt wurde.  
  
 Zum Aktivieren eines DDL-Triggers mit Serverbereich (ON ALL SERVER) oder eines LOGON-Triggers benötigt der Benutzer die CONTROL SERVER-Berechtigung auf dem Server. Zum Aktivieren eines DDL-Triggers mit Datenbankbereich (ON DATABASE) benötigt der Benutzer mindestens die ALTER ANY DATABASE DDL TRIGGER-Berechtigung in der aktuellen Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. Aktivieren eines DML-Triggers für eine Tabelle  
 Das folgende Beispiel deaktiviert Trigger `uAddress` , die für die Tabelle erstellt wurde `Address` in der AdventureWorks-Datenbank und anschließend aktiviert.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. Aktivieren eines DDL-Triggers  
 Das folgende Beispiel erstellt einen DDL-Trigger `safety` mit Datenbankbereich, und klicken Sie dann deaktivieren und aktiviert.  
  
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
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. Aktivieren aller Trigger, die mit dem gleichen Bereich definiert wurden  
 Im folgenden Beispiel werden alle DDL-Trigger aktiviert, die im Serverbereich erstellt wurden.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

