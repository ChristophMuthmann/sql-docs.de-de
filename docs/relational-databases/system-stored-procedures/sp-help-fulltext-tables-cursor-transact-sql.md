---
title: Sp_help_fulltext_tables_cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef0fa0c119c293e085d68124ee44dee378fb99d1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpfulltexttablescursor-transact-sql"></a>sp_help_fulltext_tables_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Verwendet einen Cursor, um eine Liste der Tabellen zurückzugeben, die für die Volltextindizierung registriert sind.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwenden Sie die neue **fulltext_indexes** stattdessen die Katalogsicht. Weitere Informationen finden Sie unter [fulltext_indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@cursor_return=** ]  *@cursor_variable*  AUSGABE  
 Bezeichnet die Ausgabevariable vom Typ **cursor**. Bei dem Cursor handelt es sich um einen schreibgeschützten, bildlauffähigen, dynamischen Cursor.  
  
 [  **@fulltext_catalog_name=** ] **"***Fulltext_catalog_name***"**  
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
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Siehe auch  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Sp_fulltext_table &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [Sp_help_fulltext_tables &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
