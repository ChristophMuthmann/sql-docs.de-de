---
title: Sp_describe_cursor_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fe882cf908e4ae227a486b68c54d34376164455
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdescribecursorcolumns-transact-sql"></a>sp_describe_cursor_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Meldet die Attribute der Spalten im Resultset eines Servercursors.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>Argumente  
 [ @cursor_return=] *Output_cursor_variable* Ausgabe  
 Der Name einer deklarierten Cursorvariablen zum Empfangen der Cursorausgabe. *Output_cursor_variable* ist **Cursor**und hat keinen Standardwert und muss vor dem Aufruf von Sp_describe_cursor_columns keinem Cursor zugeordnet sein. Bei dem zurückgegebenen Cursor handelt es sich um einen scrollfähigen, dynamischen, schreibgeschützten Cursor.  
  
 [ @cursor_source=] {N'local "| N'global "| N'variable'}  
 Gibt an, ob der Cursor, für den der Bericht erstellt wird, mithilfe des Namens eines lokalen Cursors, eines globalen Cursors oder einer Cursorvariablen angegeben wird. Der Parameter ist **nvarchar(30)**.  
  
 [ @cursor_identity=] N'*Local_cursor_name*"  
 Der Name eines mit einer DECLARE CURSOR-Anweisung erstellten Cursors, der entweder das LOCAL-Schlüsselwort aufweist oder standardmäßig auf LOCAL festgelegt ist. *Local_cursor_name* ist **vom Datentyp nvarchar(128)**.  
  
 [ @cursor_identity=] N'*Global_cursor_name*"  
 Der Name eines mit einer DECLARE CURSOR-Anweisung erstellten Cursors, der entweder das GLOBAL-Schlüsselwort aufweist oder standardmäßig auf GLOBAL festgelegt ist. *Global_cursor_name* ist **vom Datentyp nvarchar(128)**.  
  
 *Global_cursor_name* kann auch der Name eines API-Servercursors, die von einer ODBC-Anwendung geöffnet ist, und klicken Sie dann durch Aufrufen von SQLSetCursorName namens sein.  
  
 [ @cursor_identity=] N'*Input_cursor_variable*"  
 Der Name einer Cursorvariablen, die mit einem geöffneten Cursor verknüpft ist. *Input_cursor_variable* ist **vom Datentyp nvarchar(128)**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="cursors-returned"></a>Zurückgegebene Cursor  
 Sp_describe_cursor_columns kapselt den Bericht als eine [!INCLUDE[tsql](../../includes/tsql-md.md)] **Cursor** output-Parameter. Dies ermöglicht, dass [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batches, gespeicherte Prozeduren und Trigger die Ausgabe zeilenweise verwenden können. Dies bedeutet auch, dass die Prozedur direkt über Datenbank-API-Funktionen aufgerufen werden kann. Die **Cursor** -Ausgabeparameter muss an eine Programmvariable gebunden sein, aber die Datenbank-APIs unterstützen die Bindung nicht **Cursor** Parametern oder Variablen.  
  
 In der folgenden Tabelle wird das Format des mit sp_describe_cursor_columns zurückgegebenen Cursors dargestellt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|column_name|**Sysname** (NULL zulassen)|Der Name, der der Resultsetspalte zugewiesen ist. Die Spalte weist den Wert NULL auf, wenn die Spalte ohne zugehörige AS-Klausel angegeben wurde.|  
|ordinal_position|**int**|Die relative Position der Spalte in Bezug auf die äußerst linke Spalte im Resultset. Die erste Spalte befindet sich an Position 0.|  
|column_characteristics_flags|**int**|Eine Bitmaske zum Anzeigen der Informationen, die in DBCOLUMNFLAGS in OLE DB gespeichert sind. Dies kann eine oder eine Kombination der folgenden Optionen sein:<br /><br /> 1 = Lesezeichen<br /><br /> 2 = Feste Länge<br /><br /> 4 = NULL zulassen<br /><br /> 8 = Zeilenversionsverwaltung<br /><br /> 16 = Aktualisierbare Spalte (wird für voraussichtliche Spalten eines Cursors festgelegt, der keine FOR UPDATE-Klausel aufweist. Wenn eine solche Spalte vorhanden ist, ist pro Cursor nur eine einzige zulässig).<br /><br /> Wenn Bitwerte kombiniert werden, gelten die Merkmale der kombinierten Bitwerte. Beispielsweise hat die Spalte mit dem Bitwert 6 eine feste Länge (2) und lässt NULL-Werte zu (4).|  
|column_size|**int**|Die maximal mögliche Größe von Werten in dieser Spalte.|  
|data_type_sql|**smallint**|Eine Zahl, die dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp der Spalte angibt.|  
|column_precision|**tinyint**|Maximale Genauigkeit der Spalte gemäß der *bPrecision* -Wert in OLE DB.|  
|column_scale|**tinyint**|Anzahl der Ziffern rechts vom Dezimaltrennzeichen für die **numerischen** oder **decimal** Datentypen gemäß der *bScale* -Wert in OLE DB.|  
|order_position|**int**|Wenn die Spalte bei der Sortierung des Resultsets berücksichtigt wird, bezeichnet dies die Position der Spalte im Sortierschlüssel relativ zur Spalte ganz links.|  
|order_direction|**varchar(1)**(NULL zulassen)|A = Die Spalte befindet sich im Sortierschlüssel, und die Sortierung ist aufsteigend.<br /><br /> D = Die Spalte befindet sich im Sortierschlüssel, und die Sortierung ist absteigend.<br /><br /> NULL = Die Spalte wird nicht bei der Sortierung berücksichtigt.|  
|hidden_column|**smallint**|0 = Diese Spalte wird in der Auswahlliste angezeigt.<br /><br /> 1 = Zur künftigen Verwendung reserviert.|  
|columnid|**int**|Die Spalten-ID der Basisspalte. Wenn die Resultsetspalte mit einem Ausdruck erstellt wurde, weist columnid den Wert -1 auf.|  
|objectid|**int**|Die Objekt-ID des Objekts oder der Basistabelle, das bzw. die die Spalte bereitstellt. Wenn die Resultsetspalte mit einem Ausdruck erstellt wurde, weist objectid den Wert -1 auf.|  
|dbid|**int**|Die ID der Datenbank mit der Basistabelle, die die Spalte bereitstellt. Wenn die Resultsetspalte mit einem Ausdruck erstellt wurde, weist dbid den Wert -1 auf.|  
|dbname|**sysname**<br /><br /> (NULL zulassen)|Der Name der Datenbank mit der Basistabelle, die die Spalte bereitstellt. Wenn die Resultsetspalte mit einem Ausdruck erstellt wurde, weist dbname den Wert NULL auf.|  
  
## <a name="remarks"></a>Hinweise  
 sp_describe_cursor_columns beschreibt die Attribute der Spalten im Resultset eines Servercursors, wie z.B. den Namen und den Datentyp der einzelnen Cursor. Mit sp_describe_cursor zeigen Sie eine Beschreibung der globalen Attribute des Servercursors an. Mit sp_describe_cursor_tables zeigen Sie an, auf welche Basistabellen der Cursor verweist. Mit sp_cursor_list erhalten Sie einen Bericht der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor, die für die Verbindung sichtbar sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein globaler Cursor geöffnet und mithilfe von `sp_describe_cursor_columns` ein Bericht der im Cursor verwendeten Spalten erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Cursor](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [Sp_describe_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [Sp_cursor_list &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [Sp_describe_cursor_tables &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
