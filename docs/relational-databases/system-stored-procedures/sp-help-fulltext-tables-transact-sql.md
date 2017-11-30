---
title: Sp_help_fulltext_tables (Transact-SQL) | Microsoft Docs
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
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 587fb2495e065d00a9031c198704af6ede6e80d5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpfulltexttables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste der Tabellen zurück, die für die Volltextindizierung registriert sind.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung **fulltext_indexes** stattdessen die Katalogsicht. Weitere Informationen finden Sie unter [fulltext_indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@fulltext_catalog_name=**] **"***Fulltext_catalog_name***"**  
 Der Name des Volltextkatalogs. *fulltext_catalog_name* ist vom Datentyp **sysname**. Der Standardwert ist NULL. Wenn *Fulltext_catalog_name* fehlt oder ist NULL, alle indizierte Volltext-Tabellen der Datenbank zugeordnet werden zurückgegeben. Wenn *Fulltext_catalog_name* angegeben ist, aber *Table_name* ausgelassen wird oder den Wert NULL aufweist, wird die Volltextindex-Informationen für alle indizierten Volltexttabelle diesem Katalog zugeordnet abgerufen. Wenn beide *Fulltext_catalog_name* und *Table_name* angegeben ist, wird eine Zeile zurückgegeben, wenn *Table_name* zugeordnet ist *Fulltext_catalog_name*; Andernfalls wird ein Fehler ausgelöst.  
  
 [  **@table_name=**] **"***Table_name***"**  
 Der aus einem oder zwei Teilen bestehende Tabellenname, für den die Volltextmetadaten angefordert werden. *table_name* ist vom Datentyp **nvarchar(517)**. Der Standardwert ist NULL. Wenn nur *Table_name* angegeben wird, nur die Zeile, die relevant für *Table_name* zurückgegeben wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Tabellenbesitzer. Der Name des Datenbankbenutzers, der die Tabelle erstellt hat.|  
|**TABELLENNAME**|**sysname**|Tabellenname.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|Index, der die UNIQUE-Einschränkung auf die Spalte anwendet, die als die Spalte für den eindeutigen Schlüssel angegeben ist.|  
|**FULLTEXT_KEY_COLID**|**int**|Spalten-ID des durch FULLTEXT_KEY_NAME identifizierten eindeutigen Index.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|Gibt an, ob die für die Volltextindizierung markierten Spalten in dieser Tabelle bei Abfragen einbezogen werden sollen:<br /><br /> 0 = Inaktiv<br /><br /> 1 = Aktiv|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|Volltextkatalog, in dem sich die Volltextindexdaten der Tabelle befinden.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen werden standardmäßig der **public** -Rolle erteilt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Namen der volltextindizierten Tabellen zurückgegeben, die dem `Cat_Desc`-Volltextkatalog zugeordnet sind.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Sp_fulltext_table &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [Sp_help_fulltext_tables_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
