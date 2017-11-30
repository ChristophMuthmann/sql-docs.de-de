---
title: Sp_fulltext_column (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs: TSQL
helpviewer_keywords: sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3b9a0ed0ffc5e748381fa3dd49e3f39d639e332
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spfulltextcolumn-transact-sql"></a>sp_fulltext_column (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Gibt an, ob eine bestimmte Spalte einer Tabelle bei der Volltextindizierung berücksichtigt werden soll.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@tabname=** ] **"***Qualified_table_name***"**  
 Ein ein- oder zweiteiliger Tabellenname. Die Tabelle muss in der aktuellen Datenbank vorhanden sein. Die Tabelle muss über einen Volltextindex verfügen. *qualified_table_name* ist vom Datentyp **nvarchar(517)**und hat keinen Standardwert.  
  
 [  **@colname=** ] **"***Column_name***"**  
 Der Name einer Spalte in *qualified_table_name*. Die Spalte muss eine Zeichen-, eine **varbinary(max)** - oder eine **image** -Spalte sein und darf keine berechnete Spalte sein. *column_name* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann Volltextindizes von Textdaten, die in Spalten vom gespeicherten erstellen **varbinary(max)** oder **Image** -Datentyp. Bilder und Abbildungen werden nicht indiziert.  
  
 [  **@action=** ] **"***Aktion***"**  
 Die Aktion, die ausgeführt werden soll. *action* ist vom Datentyp **varchar(20)**und hat keinen Standardwert. Die folgenden Werte sind möglich:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Hinzufügen**|Fügt dem inaktiven Volltextindex der Tabelle den *column_name* von *qualified_table_name* hinzu. Durch diese Aktion wird die Volltextindizierung für die Spalte aktiviert.|  
|**Löschen**|Entfernt *column_name* aus dem inaktiven Volltextindex von *qualified_table_name* .|  
  
 [  **@language=** ] **"***Language_term***"**  
 Die Sprache der in der Spalte gespeicherten Daten. Eine Liste der in enthaltenen Sprachen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Sys. fulltext_languages &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
> [!NOTE]  
>  Verwenden Sie 'Neutral', wenn eine Spalte Daten in mehreren Sprachen oder in einer nicht unterstützten Sprache enthält. Die Standardsprache wird mithilfe der Konfigurationsoption 'default full-text language' angegeben.  
  
 [  **@type_colname =** ] **"***Type_column_name***"**  
 Der Name einer Spalte in *qualified_table_name* , die den Dokumenttyp von *column_name*enthält. Diese Spalte muss vom Typ **char**, **nchar**, **varchar**oder **nvarchar**sein. Wird nur verwendet, wenn der Datentyp von *column_name* **varbinary(max)** oder **image**ist. *type_column_name* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Volltextindex aktiv ist, wird ggf. das derzeit ausgeführte Auffüllen beendet. Wenn für eine Tabelle mit einem aktiven Volltextindex die Änderungsnachverfolgung aktiviert ist, stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] außerdem sicher, dass der Index aktuell ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet z. B. das aktuelle Auffüllen der Tabelle, löscht den vorhandenen Index und startet einen neuen Auffüllvorgang.  
  
 Wenn die Änderungsprotokollierung aktiviert ist und Spalten zum Volltextindex hinzugefügt oder aus ihm gelöscht werden sollen, wobei der Index beibehalten werden soll, sollte die Tabelle deaktiviert und dann die erforderlichen Spalten hinzugefügt oder gelöscht werden. Bei diesen Aktionen wird der Index eingefroren. Die Tabelle kann später wieder aktiviert werden, wenn das Auffüllen gestartet werden soll.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss ein Mitglied der festen Datenbankrolle **db_ddladmin** oder ein Mitglied der festen Datenbankrolle **db_owner** bzw. der Besitzer der Tabelle sein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `DocumentSummary` -Spalte aus der `Document` -Tabelle dem Volltextindex der Tabelle hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 Im folgenden Beispiel wird vorausgesetzt, dass Sie einen Volltextindex für die `spanishTbl`-Tabelle erstellt haben. Sie können die `spanishCol` -Spalte dem Volltextindex hinzufügen, indem Sie die folgende gespeicherte Prozedur ausführen:  
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 Beim Ausführen der Abfrage:  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 Das Resultset würde auch Zeilen mit anderen Formen von `trabajar` (arbeiten) einschließen, z. B. `trabajo`, `trabajamos`und `trabajan`.  
  
> [!NOTE]  
>  Alle Spalten, die in einer einzelnen Funktionsklausel für eine Volltextabfrage aufgelistet sind, müssen dieselbe Sprache verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Sp_help_fulltext_columns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [Sp_help_fulltext_columns_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [Sp_help_fulltext_tables &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [Sp_help_fulltext_tables_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Volltextsuche und semantische Suche gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
