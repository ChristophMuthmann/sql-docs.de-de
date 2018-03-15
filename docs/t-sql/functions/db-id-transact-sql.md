---
title: DB_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 152e471cf63efa09b0fc6dcb65acd28a191699b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Datenbank-ID zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>Argumente  
'*database_name*'  
Der Datenbankname, der verwendet wird, um die entsprechende Datenbank-ID zurückzugeben. *database_name* ist **sysname** Wenn *database_name* nicht angegeben ist, wird die aktuelle Datenbank-ID zurückgegeben.
  
## <a name="return-types"></a>Rückgabetypen
**int**
  
## <a name="permissions"></a>Berechtigungen  
Wenn der Aufrufer von **DB_ID** nicht der Besitzer der Datenbank und die Datenbank keine **master**- oder **tempdb**-Datenbank ist, ist zum Anzeigen der entsprechenden Zeile mindestens die Berechtigung ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene bzw. die Berechtigung CREATE DATABASE für die **master**-Datenbank erforderlich. Die Datenbank, mit der der Aufrufer eine Verbindung hergestellt hat, kann immer in **sys.databases**angezeigt werden.
  
> [!IMPORTANT]  
>  Standardmäßig verfügt die öffentliche Rolle über die Berechtigung VIEW ANY DATABASE, sodass alle Anmeldenamen auf Datenbankinformationen zugreifen können. Um zu verhindern, dass ein bestimmter Anmeldename eine Datenbank ermitteln kann, widerrufen Sie die VIEW ANY DATABASE-Berechtigung „Öffentlich“ über die REVOKE-Anweisung, oder Verweigern Sie die VIEW ANY DATABASE-Berechtigung für einzelne Anmeldenamen über die DENY-Anweisung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. Zurückgeben der Datenbank-ID der aktuellen Datenbank  
Im folgenden Beispiel wird die Datenbank-ID der aktuellen Datenbank zurückgegeben.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. Zurückgeben der Datenbank-ID einer angegebenen Datenbank  
Im folgenden Beispiel wird die Datenbank-ID der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zurückgegeben.
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. Angeben des Werts eines Systemfunktionsparameters mithilfe von DB_ID  
Im folgenden Beispiel wird mithilfe von `DB_ID` die Datenbank-ID der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank in der Systemfunktion `sys.dm_db_index_operational_stats` zurückgegeben. Der erste Parameter dieser Funktion ist eine Datenbank-ID.
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. Rückgabe der ID der aktuellen Datenbank  
Im folgenden Beispiel wird die Datenbank-ID der aktuellen Datenbank zurückgegeben.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. Zurückgeben der ID der benannten Datenbank.  
Im folgenden Beispiel wird die Datenbank-ID der AdventureWorksDW2012-Datenbank zurückgegeben.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>Siehe auch
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen (Transact-SQL))](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

