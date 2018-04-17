---
title: Sp_help_fulltext_columns_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 22417190de19fd801a991c0cc6425311230d8ca6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpfulltextcolumnscursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwendet einen Cursor, um eine Liste der Spalten zurückzugeben, die für die Volltextindizierung angegeben wurden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) stattdessen die Katalogsicht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@cursor_return =**] *@cursor_variable* AUSGABE  
 Bezeichnet die Ausgabevariable vom Typ **cursor**. Bei dem Cursor handelt es sich um einen schreibgeschützten, bildlauffähigen, dynamischen Cursor.  
  
 [ **@table_name =**] **'***table_name***'**  
 Der aus einem oder zwei Teilen bestehende Name der Tabelle, für die Informationen zum Volltextindex angefordert werden. *table_name* ist vom Datentyp **nvarchar(517)**. Der Standardwert ist NULL. Wenn *table_name* ausgelassen wird, werden die Volltextindex-Spalteninformationen für jede volltextindizierte Tabelle abgerufen.  
  
 [  **@column_name =**] **"***Column_name***"**  
 Der Name der Spalte, für die Informationen zum Volltextindex gewünscht werden. *column_name* ist vom Datentyp **sysname** . Der Standardwert ist NULL. Wenn *column_name* ausgelassen wird oder den Wert NULL aufweist, werden die Volltextspalteninformationen für jede volltextindizierte Spalte für *table_name*zurückgegeben. Wenn *table_name* ebenfalls ausgelassen wird oder den Wert NULL aufweist, werden die Volltextindex-Spalteninformationen für jede volltextindizierte Spalte aller Tabellen in der Datenbank zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Tabellenbesitzer. Der Name des Datenbankbenutzers, der die Tabelle erstellt hat.|  
|**TABLE_ID**|**int**|ID der Tabelle.|  
|**TABLE_NAME**|**sysname**|Tabellenname.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|Spalte in einer volltextindizierten Tabelle, die zum Indizieren angegeben ist.|  
|**FULLTEXT_COLID**|**int**|Spalten-ID der volltextindizierten Spalte.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Spalte in einer volltextindizierten Tabelle, die den Dokumenttyp der volltextindizierten Spalte angibt. Dieser Wert kann nur angewendet werden, wenn die volltextindizierte Spalte eine **varbinary(max)** - oder **image** -Spalte ist.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|Die Spalten-ID der Dokumenttypspalte. Dieser Wert kann nur angewendet werden, wenn die volltextindizierte Spalte eine **varbinary(max)** - oder **image** -Spalte ist.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Sprache, die für die Volltextsuche der Spalte verwendet wird.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen werden standardmäßig der **public** -Rolle erteilt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zu den Spalten zurückgegeben, die in allen Tabellen der Datenbank für die Volltextindizierung angegeben wurden.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
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
 [COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
