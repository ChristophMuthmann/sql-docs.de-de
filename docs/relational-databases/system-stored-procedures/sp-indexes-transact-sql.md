---
title: Sp_indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs: TSQL
helpviewer_keywords: sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95f4a19a1d4d08ec1ac2b80ec3000d19371eac26
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spindexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Indexinformationen für die angegebene Remotetabelle zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @table_server=] '*Table_server*"  
 Der Name eines Verbindungsservers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, und für den Tabelleninformationen angefordert werden. *Table_server* ist **Sysname**, hat keinen Standardwert.  
  
 [ @table_name=] '*Table_name*"  
 Der Name der Remotetabelle, für die Indexinformationen bereitzustellen sind. *TABLE_NAME* ist **Sysname**, hat den Standardwert NULL. Wenn der Wert NULL festgelegt ist, werden alle Tabellen in der angegebenen Datenbank zurückgegeben.  
  
 [ @table_schema=] '*Table_schema*"  
 Gibt das Tabellenschema an. In der Umgebung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht dies dem Tabellenbesitzer. *TABLE_SCHEMA* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @table_catalog=] '*TABLE_NAME*"  
 Der Name der Datenbank, in der *Table_name* befindet. *TABLE_NAME* ist **Sysname**, hat den Standardwert NULL. Wenn der Wert NULL, *TABLE_NAME* standardmäßig **master**.  
  
 [ @index_name=] '*Index_name*"  
 Der Name des Indexes, für den Informationen angefordert werden. *Index* ist **Sysname**, hat den Standardwert NULL.  
  
 [ @is_unique=] '*Is_unique*"  
 Der Typ des Indexes, für den Informationen zurückgegeben werden sollen. *Is_unique* ist **Bit**, hat den Standardwert NULL und kann einen der folgenden Werte.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|1|Gibt Informationen zu eindeutigen Indizes zurück.|  
|0|Gibt Informationen zu Indizes zurück, die nicht eindeutig sind.|  
|NULL|Gibt Informationen zu allen Indizes zurück.|  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|Der Name der Datenbank, in der die angegebene Tabelle gespeichert ist.|  
|TABLE_SCHEM|**sysname**|Das Schema für die Tabelle.|  
|TABLE_NAME|**sysname**|Der Name der Remotetabelle.|  
|NON_UNIQUE|**smallint**|Gibt an, ob der Index eindeutig oder nicht eindeutig ist:<br /><br /> 0 = Eindeutig<br /><br /> 1 = Nicht eindeutig|  
|INDEX_QUALIFER|**sysname**|Der Name des Indexbesitzers. Verschiedene DBMS-Produkte ermöglichen neben dem Tabellenbesitzer auch anderen Benutzern das Erstellen von Indizes. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese Spalte ist immer identisch **TABLE_NAME**.|  
|INDEX_NAME|**sysname**|Der Name des Indexes.|  
|TYPE|**smallint**|Typ des Index:<br /><br /> 0 = Statistiken für eine Tabelle<br /><br /> 1 = In einem Cluster gruppiert<br /><br /> 2 = Hash<br /><br /> 3 = Sonstige|  
|ORDINAL_POSITION|**int**|Die Ordnungsposition der Spalte im Index. Die erste Spalte im Index hat den Wert 1. Diese Spalte gibt immer einen Wert zurück.|  
|COLUMN_NAME|**sysname**|Der Name der Spalte; wird für jede Spalte von TABLE_NAME zurückgegeben.|  
|ASC_OR_DESC|**varchar**|Die Sortierreihenfolge:<br /><br /> A = Aufsteigend<br /><br /> D = Absteigend<br /><br /> NULL = Nicht zutreffend<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt immer A zurück.|  
|CARDINALITY|**int**|Die Anzahl der Zeilen in der Tabelle oder der eindeutigen Werte im Index.|  
|PAGES|**int**|Die Anzahl der Seiten, die zum Speichern des Indexes oder der Tabelle benötigt werden.|  
|FILTER_CONDITION|**Nvarchar (**4000**)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt keinen Wert zurück.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt alle Indexinformationen aus der Tabelle `Employees` der `AdventureWorks2012`-Datenbank auf dem Verbindungsserver `Seattle1` zurück.  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verteilte Abfragen, gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Sp_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Sp_column_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Sp_foreignkeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Sp_tables_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Sp_table_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
