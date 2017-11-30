---
title: Sp_helpstats (Transact-SQL) | Microsoft Docs
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
- sp_helpstats
- sp_helpstats_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45d6df772da027568b1fbd7593e404f291246bb4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt statistische Informationen zu Spalten und Indizes der angegebenen Tabelle zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]Um Informationen zu Statistiken abzurufen, Fragen den [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) und [stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) Katalogsichten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@objname=**] **"***Object_name***"**  
 Gibt die Tabelle an, in der Statistikinformationen bereitgestellt werden sollen. *Object_name* ist **nvarchar(520)** und darf nicht null sein. Es kann ein ein- oder zweiteiliger Name angegeben werden.  
  
 [  **@results=**] **"***Wert***"**  
 Gibt an, wie viele Informationen bereitgestellt werden. Gültige Einträge sind **alle** und **STATS**. **ALLE** listet Statistiken für alle Indizes und Spalten mit Statistiken erstellt wurden; **STATS** Listet nur Statistiken, die nicht mit einem Index zugeordnet. *Wert* ist **nvarchar(5)** hat den Standardwert STATS.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 In der folgenden Tabelle werden die Spalten des Resultsets beschrieben:  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**statistics_name**|Der Name der Statistik. Gibt **Sysname** darf nicht null sein.|  
|**statistics_keys**|Die Schlüssel, auf denen die Statistik basiert. Gibt **nvarchar(2078)** und darf nicht null sein.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie DBCC SHOW_STATISTICS, um detaillierte statistische Informationen zu einem bestimmten Index oder einer bestimmten Statistik anzuzeigen. Weitere Informationen finden Sie unter [DBCC SHOW_STATISTICS &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) und [Sp_helpindex &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Durch Ausführen von `sp_createstats` werden einspaltige Statistiken für alle in Frage kommenden Spalten aller Benutzertabellen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank erstellt. Anschließend wird `sp_helpstats` ausgeführt, um die für die `Customer`-Tabelle erstellten Statistiken zu ermitteln.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
