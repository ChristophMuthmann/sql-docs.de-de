---
title: Sp_foreignkeys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 248113fe68932f385203b067d77afad506fabbdf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Fremdschlüssel zurück, die auf Primärschlüssel in der Tabelle auf dem Verbindungsserver verweisen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@table_server =** ] **"***Table_server***"**  
 Der Name des Verbindungsservers, für den Tabelleninformationen zurückgegeben werden sollen. *Table_server* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@pktab_name =** ] **"***Pktab_name***"**  
 Der Name der Tabelle mit einem Primärschlüssel. *Pktab_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@pktab_schema =** ] **"***Pktab_schema***"**  
 Der Name des Schemas mit einem Primärschlüssel. *Pktab_schema*ist **Sysname**, hat den Standardwert NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält dies den Namen des Besitzers.  
  
 [  **@pktab_catalog =** ] **"***Pktab_catalog***"**  
 Der Name des Katalogs mit einem Primärschlüssel. *Pktab_catalog*ist **Sysname**, hat den Standardwert NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält dies den Namen der Datenbank.  
  
 [  **@fktab_name =** ] **"***Fktab_name***"**  
 Der Name der Tabelle mit einem Fremdschlüssel. *Fktab_name*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@fktab_schema =** ] **"***Fktab_schema***"**  
 Der Name des Schemas mit einem Fremdschlüssel. *Fktab_schema*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@fktab_catalog =** ] **"***Fktab_catalog***"**  
 Der Name des Katalogs mit einem Fremdschlüssel. *Fktab_catalog*ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Katalog***.** *Schema***.** *Tabelle*), die im Resultset dargestellt wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|Katalog für die Tabelle, in der sich der Primärschlüssel befindet|  
|**PKTABLE_SCHEM**|**sysname**|Schema für die Tabelle, in der sich der Primärschlüssel befindet|  
|**PKTABLE_NAME**|**sysname**|Name der Tabelle (mit dem Primärschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|**PKCOLUMN_NAME**|**sysname**|Namen der Primärschlüsselspalte oder der Spalten, für jede Spalte von der **TABLE_NAME** zurückgegeben. Dieses Feld gibt immer einen Wert zurück.|  
|**FKTABLE_CAT**|**sysname**|Katalog für die Tabelle, in der sich der Fremdschlüssel befindet|  
|**FKTABLE_SCHEM**|**sysname**|Schema für die Tabelle, in der sich der Fremdschlüssel befindet|  
|**FKTABLE_NAME**|**sysname**|Der Name der Tabelle (mit einem Fremdschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|**FKCOLUMN_NAME**|**sysname**|Name des der Fremdschlüsselspalten für jede Spalte von TABLE_NAME zurückgegeben. Dieses Feld gibt immer einen Wert zurück.|  
|**KEY_SEQ**|**smallint**|Die Sequenznummer der Spalte in einem mehrspaltigen Primärschlüssel. Dieses Feld gibt immer einen Wert zurück.|  
|**UPDATE_RULE**|**smallint**|Die Aktion, die für den Fremdschlüssel ausgeführt wird, wenn es sich bei dem SQL-Vorgang um ein Update handelt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt 0, 1 oder 2 für diese Spalten zurück:<br /><br /> 0=CASCADE; kaskadierende Änderungen am Fremdschlüssel.<br /><br /> 1=NO ACTION; keine Änderungen, wenn der Fremdschlüssel vorhanden ist.<br /><br /> 2=SET_NULL; Fremdschlüssel auf NULL festlegen.|  
|**DELETE_RULE**|**smallint**|Die Aktion, die für den Fremdschlüssel ausgeführt wird, wenn es sich bei dem SQL-Vorgang um eine Löschung handelt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt 0, 1 oder 2 für diese Spalten zurück:<br /><br /> 0=CASCADE; kaskadierende Änderungen am Fremdschlüssel.<br /><br /> 1=NO ACTION; keine Änderungen, wenn der Fremdschlüssel vorhanden ist.<br /><br /> 2=SET_NULL; Fremdschlüssel auf NULL festlegen.|  
|**FK_NAME**|**sysname**|Der Fremdschlüsselbezeichner. Ist NULL, wenn er auf die Datenquelle nicht anwendbar ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt den Namen der FOREIGN KEY-Einschränkung zurück.|  
|**PK_NAME**|**sysname**|Der Primärschlüsselbezeichner. Ist NULL, wenn er auf die Datenquelle nicht anwendbar ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt den Namen der PRIMARY KEY-Einschränkung zurück.|  
|**DEFERRABILITY**|**smallint**|Gibt an, ob die Einschränkungsüberprüfung verzögert werden kann.|  
  
 Im Resultset geben die Spalten FK_NAME und PK_NAME immer NULL zurück.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_foreignkeys** FOREIGN_KEYS-Rowsets für Abfragen der **IDBSchemaRowset** -Schnittstelle des OLE DB-Anbieters, der entspricht *Table_server*. Die *Table_name*, *Table_schema*, *"TABLE_CATALOG"*, und *Spalte* Parameter übergeben werden, auf diese Schnittstelle, um die Zeilen einzuschränken zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Fremdschlüsselinformationen zur `Department`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank auf dem Verbindungsserver `Seattle1` zurück.  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Sp_column_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [Sp_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Sp_primarykeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [Sp_tables_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Sp_table_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
