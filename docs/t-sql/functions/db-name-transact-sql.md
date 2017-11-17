---
title: Db_name (Transact-SQL) | Microsoft Docs
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
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5743ccb1374640078a77d84a140e9e5d0fdaef0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt den Datenbanknamen zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumente  
*database_id*  
Die ID der Datenbank, die zurückgegeben werden soll. *database_id* ist vom Datentyp **int**und hat keinen Standardwert. Wenn keine ID angegeben ist, wird der Name der aktuellen Datenbank zurückgegeben.
  
## <a name="return-types"></a>Rückgabetypen
**vom Datentyp nvarchar(128)**
  
## <a name="permissions"></a>Berechtigungen  
Wenn der Aufrufer **DB_NAME** ist nicht der Besitzer der Datenbank und die Datenbank ist nicht **master** oder **Tempdb**, mindestens die Berechtigung zum Anzeigen der entsprechenden Zeile erforderlich ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene-Berechtigung oder die CREATE DATABASE-Berechtigung in den **master** Datenbank. Die Datenbank, mit der der Aufrufer eine Verbindung hergestellt hat, kann immer in **sys.databases**angezeigt werden.
  
> [!IMPORTANT]  
>  Standardmäßig verfügt die public-Rolle die VIEW ANY DATABASE-Berechtigung, alle Anmeldungen, die Datenbankinformationen finden Sie unter. Um eine Anmeldung über die Möglichkeit zur Erkennung von einer Datenbank zu blockieren, Aufheben der VIEW ANY DATABASE-Berechtigung aus öffentlichen oder für einzelne Anmeldenamen die VIEW ANY DATABASE-Berechtigung zu verweigern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-current-database-name"></a>A. Zurückgeben des aktuellen Datenbanknamens  
Das folgende Beispiel gibt den Namen der aktuellen Datenbank zurück.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. Zurückgeben des Datenbanknamens einer angegebenen Datenbank-ID  
Das folgende Beispiel gibt den Datenbanknamen für die Datenbank-ID `3` zurück.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Zurückgeben des aktuellen Datenbanknamens  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Geben Sie den Namen einer Datenbank mit der Datenbank-ID zurück.  
Das folgende Beispiel gibt den Datenbanknamen und Database_id für jede Datenbank zurück.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Siehe auch
[Db_id &#40; Transact-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  


