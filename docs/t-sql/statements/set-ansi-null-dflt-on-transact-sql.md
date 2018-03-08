---
title: SET ANSI_NULL_DFLT_ON (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ANSI_NULL_DFLT_ON
- ANSI_NULL_DFLT_ON_TSQL
- SET ANSI_NULL_DFLT_ON
- SET_ANSI_NULL_DFLT_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULL_DFLT_ON statement
- ANSI_NULL_DFLT_ON option
- default nullability
- null values [SQL Server], overriding
- overriding default nullability
ms.assetid: 8c925924-a466-4c8b-aeb2-7e0d341f32db
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82532accfe14729a0e3ccbfa7bd3f1b55d2aaa01
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansinulldflton-transact-sql"></a>SET ANSI_NULL_DFLT_ON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert das Verhalten der Sitzung, um die standardmäßige NULL-Zulässigkeit neuer Spalten überschreiben bei der **' ANSI null Default '** option für die Datenbank **"false"**. Weitere Informationen zum Festlegen des Werts für **' ANSI null Default '**, finden Sie unter [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Syntax

```
-- Syntax for SQL Server and Azure SQL Database

SET ANSI_NULL_DFLT_ON {ON | OFF}
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_NULL_DFLT_ON ON
```

## <a name="remarks"></a>Hinweise  
 Diese Einstellung betrifft die NULL-Zulässigkeit für neue Spalten nur, wenn die NULL-Zulässigkeit der Spalte nicht in den CREATE TABLE- und ALTER TABLE-Anweisungen angegeben wurde. Wenn für SET ANSI_NULL_DFLT_ON der Wert ON festgelegt ist und wenn mit den Anweisungen ALTER TABLE und CREATE TABLE neue Spalten erstellt werden, lassen diese standardmäßig NULL-Werte zu, falls der NULL-Zulässigkeitsstatus der Spalte nicht explizit angegeben ist. SET ANSI_NULL_DFLT_ON hat keine Auswirkung auf Spalten, die mit einer expliziten Angabe von NULL oder NOT NULL erstellt wurden.  
  
 Für SET ANSI_NULL_DFLT_OFF und SET ANSI_NULL_DFLT_ON kann nicht gleichzeitig ON festgelegt werden. Wird eine der beiden Optionen aktiviert (ON), so wird die andere deaktiviert (OFF). Daher entweder ANSI_NULL_DFLT_OFF oder ANSI_NULL_DFLT_ON ON festgelegt werden, oder OFF festgelegt sein können. Wenn eine der beiden Optionen auf ON festgelegt ist, tritt die entsprechende Einstellung (SET ANSI_NULL_DFLT_OFF oder SET ANSI_NULL_DFLT_ON) in Kraft. Beide Optionen OFF festgelegt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet den Wert der **Is_ansi_null_default_on** Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 Am zuverlässigsten arbeiten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skripts, die in Datenbanken mit unterschiedlichen Einstellungen der NULL-Zulässigkeit verwendet werden, wenn in CREATE TABLE- und ALTER TABLE-Anweisungen NULL oder NOT NULL angegeben wird.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULL_DFLT_ON automatisch auf ON festgelegt wird, wenn eine Verbindung herstellen. Der Standardwert für SET ANSI_NULL_DFLT_ON für Verbindungen von DB-Library-Anwendungen ist OFF.  
  
 Ist SET ANSI_DEFAULTS auf ON festgelegt, so ist SET ANSI_NULL_DFLT_ON aktiviert.  
  
 Die Einstellung von SET ANSI_NULL_DFLT_ON wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Die Einstellung von SET ANSI_NULL_DFLT_ON gilt nicht, wenn Tabellen mit der SELECT INTO-Anweisung erstellt werden.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @ANSI_NULL_DFLT_ON VARCHAR(3) = 'OFF';  
IF ( (1024 & @@OPTIONS) = 1024 ) SET @ANSI_NULL_DFLT_ON = 'ON';  
SELECT @ANSI_NULL_DFLT_ON AS ANSI_NULL_DFLT_ON;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Auswirkungen der `SET ANSI_NULL_DFLT_ON` beiden Einstellungen für die **' ANSI null Default '** -Datenbankoption.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- The code from this point on demonstrates that SET ANSI_NULL_DFLT_ON  
-- has an effect when the 'ANSI null default' for the database is false.  
-- Set the 'ANSI null default' database option to false by executing  
-- ALTER DATABASE.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT OFF;  
GO  
-- Create table t1.  
CREATE TABLE t1 (a TINYINT) ;  
GO   
-- NULL INSERT should fail.  
INSERT INTO t1 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to ON and create table t2.  
SET ANSI_NULL_DFLT_ON ON;  
GO  
CREATE TABLE t2 (a TINYINT);  
GO   
-- NULL insert should succeed.  
INSERT INTO t2 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to OFF and create table t3.  
SET ANSI_NULL_DFLT_ON OFF;  
GO  
CREATE TABLE t3 (a TINYINT);  
GO  
-- NULL insert should fail.  
INSERT INTO t3 (a) VALUES (NULL);  
GO  
  
-- The code from this point on demonstrates that SET ANSI_NULL_DFLT_ON   
-- has no effect when the 'ANSI null default' for the database is true.  
-- Set the 'ANSI null default' database option to true.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON  
GO  
  
-- Create table t4.  
CREATE TABLE t4 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t4 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to ON and create table t5.  
SET ANSI_NULL_DFLT_ON ON;  
GO  
CREATE TABLE t5 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t5 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to OFF and create table t6.  
SET ANSI_NULL_DFLT_ON OFF;  
GO  
CREATE TABLE t6 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t6 (a) VALUES (NULL);  
GO  
  
-- Set the 'ANSI null default' database option to false.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON;  
GO  
  
-- Drop tables t1 through t6.  
DROP TABLE t1,t2,t3,t4,t5,t6;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SET ANSI_NULL_DFLT_OFF &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)  
  
  
