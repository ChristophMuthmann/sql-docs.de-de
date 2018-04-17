---
title: Sp_helptext (Transact-SQL) | Microsoft Docs
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
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ff9b4c0dd094cbe8e3a3816a1f0a8efd1dc64335
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Zeigt die Definition einer benutzerdefinierten Regel, in der Standardeinstellung unverschlüsselt [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur, benutzerdefinierte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktion, Trigger, berechnete Spalte, CHECK-Einschränkung, Sicht oder Systemobjekt wie z. B. einer gespeicherten Prozedur.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@objname =** ] **'***name***'**  
 Der qualifizierte oder nicht qualifizierte Name eines Objekts mit Schemabereich. Anführungszeichen sind nur dann erforderlich, wenn ein qualifiziertes Objekt angegeben wird. Bei Angabe eines vollqualifizierten Namens, einschließlich eines Datenbanknamens, muss es sich bei dem Datenbanknamen um den Namen der aktuellen Datenbank handeln. Das Objekt muss in der aktuellen Datenbank vorhanden sein. *name* ist vom Datentyp **nvarchar(776)**und hat keinen Standardwert.  
  
 [  **@columnname =** ] **"***Computed_column_name***"**  
 Der Name der berechneten Spalte, für die Definitionsinformationen angezeigt werden sollen. Die Tabelle, welche die Spalte beinhaltet, muss als *name*angegeben werden. *column_name* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Text**|**nvarchar(255)**|Objektdefinition|  
  
## <a name="remarks"></a>Hinweise  
 sp_helptext zeigt die Definition an, die verwendet wird, um ein Objekt in mehreren Zeilen zu erstellen. Jede Zeile umfasst 255 Zeichen von der [!INCLUDE[tsql](../../includes/tsql-md.md)] Definition. Die Definition befindet sich in der **Definition** Spalte in der [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der Rolle **public** . Definitionen von Systemobjekten sind öffentlich sichtbar. Die Definition von Benutzerobjekten ist für den Objektbesitzer sichtbar oder für Berechtigte, die über eine der folgenden Berechtigungen verfügen: ALTER, CONTROL, TAKE OWNERSHIP oder VIEW DEFINITION.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. Anzeigen der Definition eines Triggers  
 Das folgende Beispiel zeigt die Definition des Triggers `dEmployee` in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]Datenbank.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. Anzeigen der Definition einer berechneten Spalte  
 Das folgende Beispiel zeigt die Definition der berechneten Spalte `TotalDue` auf die `SalesOrderHeader` -Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank.  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
