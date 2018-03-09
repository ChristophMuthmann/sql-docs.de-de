---
title: Sp_describe_cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38eae1442b8058b6596efd525196f2f76b4b6dce
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Meldet die Attribute eines Servercursors.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
    , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
    , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @cursor_return=] *Output_cursor_variable* Ausgabe  
 Der Name einer deklarierten Cursorvariablen zum Empfangen der Cursorausgabe. *Output_cursor_variable* ist **Cursor**und hat keinen Standardwert und muss vor dem Aufruf von Sp_describe_cursor keinem Cursor zugeordnet sein. Bei dem zurückgegebenen Cursor handelt es sich um einen scrollfähigen, dynamischen, schreibgeschützten Cursor.  
  
 [ @cursor_source=] {N'local "| N'global "| N'variable'}  
 Gibt an, ob der Cursor, für den der Bericht erstellt wird, mithilfe des Namens eines lokalen Cursors, eines globalen Cursors oder einer Cursorvariablen angegeben wird. Der Parameter ist **nvarchar(30)**.  
  
 [ @cursor_identity=] N'*Local_cursor_name*"]  
 Der Name eines mit einer DECLARE CURSOR-Anweisung erstellten Cursors, der entweder das LOCAL-Schlüsselwort aufweist oder standardmäßig auf LOCAL festgelegt ist. *Local_cursor_name* ist **vom Datentyp nvarchar(128)**.  
  
 [ @cursor_identity=] N'*Global_cursor_name*"]  
 Der Name eines mit einer DECLARE CURSOR-Anweisung erstellten Cursors, der entweder das GLOBAL-Schlüsselwort aufweist oder standardmäßig auf GLOBAL festgelegt ist. *Global_cursor_name* ist **vom Datentyp nvarchar(128)**.  
  
 *Global_cursor_name* kann auch der Name eines API-Servercursors, die von einer ODBC-Anwendung geöffnet wird, die dann durch Aufrufen von SQLSetCursorName.  
  
 [ @cursor_identity=] N'*Input_cursor_variable*"]  
 Der Name einer Cursorvariablen, die mit einem geöffneten Cursor verknüpft ist. *Input_cursor_variable* ist **vom Datentyp nvarchar(128)**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="cursors-returned"></a>Zurückgegebene Cursor  
 Sp_describe_cursor kapselt das Resultset in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] **Cursor** output-Parameter. Dies ermöglicht, dass [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batches, gespeicherte Prozeduren und Trigger die Ausgabe zeilenweise verwenden können. Dies bedeutet auch, dass die Prozedur direkt über Datenbank-API-Funktionen aufgerufen werden kann. Die **Cursor** -Ausgabeparameter muss an eine Programmvariable gebunden sein, aber die Datenbank-APIs unterstützen die Bindung nicht **Cursor** Parametern oder Variablen.  
  
 In der folgenden Tabelle wird das Format des Cursors dargestellt, der mithilfe von sp_describe_cursor zurückgegeben wird. Das Format des Cursors ist mit dem mithilfe von sp_cursor_list zurückgegebenen Format identisch.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|Name, der zum Verweisen auf den Cursor verwendet wird. Wenn der Verweis auf den Cursor über den Namen in einer DECLARE CURSOR-Anweisung erfolgte, ist der Name des Verweises mit dem Cursornamen identisch. Wenn der Verweis auf den Cursor über eine Variable erfolgte, ist der Variablenname der Name des Verweises.|  
|cursor_name|**sysname**|Der Name des Cursors aus einer DECLARE CURSOR-Anweisung. Wenn in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Cursor erstellt wurde, indem eine Cursorvariable auf einen Cursor festgelegt wurde, gibt cursor_name den Namen der Cursorvariablen zurück. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt diese Ausgabespalte einen systemgenerierten Namen zurück.|  
|cursor_scope|**tinyint**|1 = LOKAL<br /><br /> 2 = GLOBAL|  
|status|**int**|Einige Werte, die von der CURSOR_STATUS-Systemfunktion gemeldet werden:<br /><br /> 1 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geöffnet. Ein statischer, Keyset- oder Insensitivcursor weist mindestens eine Zeile auf. Bei einem dynamischen Cursor weist das Resultset keine oder mehr Zeilen auf.<br /><br /> 0 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geöffnet, weist aber keine Zeilen auf. Dynamische Cursor geben diesen Wert nie zurück.<br /><br /> -1 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geschlossen.<br /><br /> -2 = Gilt nur für Cursorvariablen. Der Variablen ist kein Cursor zugewiesen. Möglicherweise hat ein OUTPUT-Parameter der Variablen einen Cursor zugewiesen, aber die gespeicherte Prozedur hat den Cursor vor der Rückgabe geschlossen.<br /><br /> -3 = Ein Cursor oder eine Cursorvariable mit dem angegebenen Namen ist nicht vorhanden, oder für die Cursorvariable wurde kein Cursor reserviert.|  
|model|**tinyint**|1 = Insensitiv (oder statisch)<br /><br /> 2 = Keyset<br /><br /> 3 = dynamisch<br /><br /> 4 = Schneller Vorwärtscursor|  
|Parallelität (concurrency)|**tinyint**|1 = schreibgeschützt<br /><br /> 2 = Scrollsperre<br /><br /> 3 = Vollständig|  
|scrollable|**tinyint**|0 = Vorwärts<br /><br /> 1 = Scrollfähig|  
|open_status|**tinyint**|0 = Geschlossen<br /><br /> 1 = Geöffnet|  
|cursor_rows|**decimal(10,0)**|Die Anzahl der kennzeichnenden Zeilen im Resultset. Weitere Informationen finden Sie unter [@@CURSOR_ROWS &#40; Transact-SQL &#41; ](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|Status des letzten Abrufs für diesen Cursor. Weitere Informationen finden Sie unter [@@FETCH_STATUS &#40; Transact-SQL &#41; ](../../t-sql/functions/fetch-status-transact-sql.md).<br /><br /> 0 = Abruf erfolgreich.<br /><br /> -1 = Abruf fehlerhaft oder außerhalb des zulässigen Bereichs des Cursors.<br /><br /> -2 = Die angeforderte Zeile fehlt.<br /><br /> -9 = Kein Abruf für Cursor.|  
|column_count|**smallint**|Anzahl der Spalten im Resultset des Cursors|  
|row_count|**decimal(10,0)**|Anzahl der Zeilen, auf die sich den letzten Vorgang für den Cursor auswirkt. Weitere Informationen finden Sie unter [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**tinyint**|Letzter Vorgang für den Cursor ausgeführt:<br /><br /> 0 = Für den Cursor wurden keine Vorgänge ausgeführt.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = EINFÜGEN<br /><br /> 4 = UPDATE<br /><br /> 5 = LÖSCHEN<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Ein eindeutiger Wert für den Cursor innerhalb des Serverbereichs|  
  
## <a name="remarks"></a>Hinweise  
 sp_describe_cursor beschreibt die für einen Servercursor globalen Attribute, wie z. B. die Optionen zum Durchführen eines Bildlaufs und zum Aktualisieren. Mit sp_describe_cursor_columns zeigen Sie eine Beschreibung der Attribute des vom Cursor zurückgegebenen Resultsets. Mit sp_describe_cursor_tables zeigen Sie an, auf welche Basistabellen der Cursor verweist. Mit sp_cursor_list erhalten Sie einen Bericht der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor, die für die Verbindung sichtbar sind.  
  
 Eine DECLARE CURSOR-Anweisung kann einen Cursortyp anfordern, den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der in DECLARE CURSOR enthaltenen SELECT-Anweisung nicht unterstützen kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konvertiert den Cursor implizit in einen Typ, der mithilfe der SELECT-Anweisung unterstützt werden kann. Wenn TYPE_WARNING in der DECLARE CURSOR-Anweisung angegeben wird, sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Anwendung eine Meldung zu Informationszwecken, dass eine Konvertierung durchgeführt wurde. Sp_describe_cursor kann dann aufgerufen werden, um den Cursortyp zu bestimmen, der implementiert wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein globaler Cursor geöffnet und mithilfe von `sp_describe_cursor` ein Bericht der Cursorattribute erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
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
 [Sp_cursor_list &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [Sp_describe_cursor_columns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [Sp_describe_cursor_tables &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
