---
title: Db_id (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 30d34b3509517d18559d4fbb0aa02a92e6d6cfe8
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Datenbank-ID zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>Argumente  
"*Database_name*"  
Der Datenbankname, der verwendet wird, um die entsprechende Datenbank-ID zurückzugeben. *database_name* ist **sysname** Wenn *Database_name* wird weggelassen wird, wird die aktuelle Datenbank-ID zurückgegeben.
  
## <a name="return-types"></a>Rückgabetypen
**int**
  
## <a name="permissions"></a>Berechtigungen  
Wenn der Aufrufer **DB_ID** ist nicht der Besitzer der Datenbank und die Datenbank ist nicht **master** oder **Tempdb**, mindestens die Berechtigung zum Anzeigen der entsprechenden Zeile erforderlich ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene-Berechtigung oder die CREATE DATABASE-Berechtigung in den **master** Datenbank. Die Datenbank, mit der der Aufrufer eine Verbindung hergestellt hat, kann immer in **sys.databases**angezeigt werden.
  
> [!IMPORTANT]  
>  Standardmäßig verfügt die public-Rolle die VIEW ANY DATABASE-Berechtigung, alle Anmeldungen, die Datenbankinformationen finden Sie unter. Um eine Anmeldung über die Möglichkeit zur Erkennung von einer Datenbank zu blockieren, Aufheben der VIEW ANY DATABASE-Berechtigung aus öffentlichen oder für einzelne Anmeldenamen die VIEW ANY DATABASE-Berechtigung zu verweigern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. Zurückgeben der Datenbank-ID der aktuellen Datenbank  
Im folgenden Beispiel wird die Datenbank-ID der aktuellen Datenbank zurückgegeben.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. Zurückgeben der Datenbank-ID einer angegebenen Datenbank  
Das folgende Beispiel gibt die ID des dem [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank.
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. Angeben des Werts eines Systemfunktionsparameters mithilfe von DB_ID  
Im folgenden Beispiel wird `DB_ID` zum Zurückgeben der Datenbank-ID, der die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank in der Systemfunktion `sys.dm_db_index_operational_stats`. Der erste Parameter dieser Funktion ist eine Datenbank-ID.
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. Gibt die ID der aktuellen Datenbank  
Im folgenden Beispiel wird die Datenbank-ID der aktuellen Datenbank zurückgegeben.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. Die ID einer benannten Datenbank zurück.  
Im folgende Beispiel gibt die Datenbank-ID von der AdventureWorksDW2012-Datenbank zurück.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>Siehe auch
[Db_name &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
[Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  


