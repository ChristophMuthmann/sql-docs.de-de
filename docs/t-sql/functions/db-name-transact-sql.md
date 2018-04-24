---
title: DB_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f9a0898e617c5bc5b4680ce839e3ffa9ef15132
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
**nvarchar(128)**
  
## <a name="permissions"></a>Berechtigungen  
Wenn der Aufrufer von **DB_NAME** nicht der Besitzer der Datenbank und die Datenbank keine **master**- oder **tempdb**-Datenbank ist, ist zum Anzeigen der entsprechenden Zeile mindestens die Berechtigung ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene bzw. die Berechtigung CREATE DATABASE für die **master**-Datenbank erforderlich. Die Datenbank, mit der der Aufrufer eine Verbindung hergestellt hat, kann immer in **sys.databases**angezeigt werden.
  
> [!IMPORTANT]  
>  Standardmäßig verfügt die öffentliche Rolle über die Berechtigung VIEW ANY DATABASE, sodass alle Anmeldenamen auf Datenbankinformationen zugreifen können. Um zu verhindern, dass ein bestimmter Anmeldename eine Datenbank ermitteln kann, widerrufen Sie die VIEW ANY DATABASE-Berechtigung „Öffentlich“ über die REVOKE-Anweisung, oder Verweigern Sie die VIEW ANY DATABASE-Berechtigung für einzelne Anmeldenamen über die DENY-Anweisung.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-return-the-current-database-name"></a>C. Zurückgeben des aktuellen Datenbanknamens  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Zurückgeben des Namens einer Datenbank unter Verwendung der Datenbank-ID  
Das folgende Beispiel gibt den Datenbanknamen für die database_id für jede Datenbank zurück.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Siehe auch
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen (Transact-SQL))](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

