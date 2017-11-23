---
title: Sp_cursor_list (Transact-SQL) | Microsoft Docs
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
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45b45ac36dad0142475bf82e8dcf49fe52ab7300
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcursorlist-transact-sql"></a>sp_cursor_list (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Meldet die Attribute der Servercursor, die aktuell für die Verbindung geöffnet sind.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @cursor_return=] *Cursor_variable_name*Ausgabe  
 Der Name einer deklarierten Cursorvariablen. *Cursor_variable_name* ist **Cursor**, hat keinen Standardwert. Bei dem Cursor handelt es sich um einen scrollfähigen, dynamischen, schreibgeschützten Cursor.  
  
 [ @cursor_scope=] *Cursor_scope*  
 Gibt die Ebene der Cursor an, die gemeldet werden sollen. *Cursor_scope* ist **Int**, hat keinen Standardwert und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|1|Alle lokalen Cursor melden.|  
|2|Alle globalen Cursor melden.|  
|3|Lokale und globale Cursor melden.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="cursors-returned"></a>Zurückgegebene Cursor  
 sp_cursor_list gibt den Bericht nicht als Resultset, sondern als einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Cursorausgabeparameter zurück. Dadurch können [!INCLUDE[tsql](../../includes/tsql-md.md)] Batches, gespeicherten Prozeduren und Trigger, um die Ausgabe zeilenweise gleichzeitig arbeiten. Dies bedeutet außerdem, dass es nicht möglich ist, die Prozedur direkt über Datenbank-API-Funktionen aufzurufen. Der cursor-Ausgabeparameter muss an eine Programmvariable gebunden sein, aber die Datenbank-APIs unterstützen die Bindung von cursor-Parametern oder -Variablen nicht.  
  
 Dies ist das Format des von sp_cursor_list zurückgegebenen Cursors. Das Format des Cursors ist mit dem von sp_describe_cursor zurückgegebenen Format identisch.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|Der Name, der zum Verweisen auf den Cursor verwendet wird. Wenn der Verweis auf den Cursor über den Namen in einer DECLARE CURSOR-Anweisung angegeben wurde, ist der Verweisname Cursornamen identisch. Wenn der Verweis auf den Cursor über eine Variable erfolgte, ist der Verweisname der Name der Cursorvariablen.|  
|cursor_name|**sysname**|Der Name des Cursors aus einer DECLARE CURSOR-Anweisung. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], wenn der Cursor erstellt wurde, indem eine Cursorvariable auf einen Cursor festgelegt **Cursor_name** gibt den Namen der Cursorvariablen zurück.  In früheren Versionen gibt diese Ausgabespalte einen systemgenerierten Namen zurück.|  
|cursor_scope|**smallint**|1 = LOKAL<br /><br /> 2 = GLOBAL|  
|status|**smallint**|Die gleichen Werte, die von der CURSOR_STATUS-Systemfunktion gemeldet werden:<br /><br /> 1 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geöffnet. Ein statischer, Keyset- oder Insensitivcursor weist mindestens eine Zeile auf. Bei einem dynamischen Cursor weist das Resultset keine oder mehr Zeilen auf.<br /><br /> 0 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geöffnet, weist aber keine Zeilen auf. Dynamische Cursor geben diesen Wert nie zurück.<br /><br /> -1 = Der Cursor, auf den mit dem Cursornamen oder der Variablen verwiesen wird, ist geschlossen.<br /><br /> -2 = Gilt nur für Cursorvariablen. Der Variablen ist kein Cursor zugewiesen. Möglicherweise hat ein OUTPUT-Parameter der Variablen einen Cursor zugewiesen, aber die gespeicherte Prozedur hat den Cursor vor der Rückgabe geschlossen.<br /><br /> -3 = Ein Cursor oder eine Cursorvariable mit dem angegebenen Namen ist nicht vorhanden, oder für die Cursorvariable wurde kein Cursor reserviert.|  
|model|**smallint**|1 = Insensitiv (oder statisch)<br /><br /> 2 = Keyset<br /><br /> 3 = dynamisch<br /><br /> 4 = Schneller Vorwärtscursor|  
|Parallelität (concurrency)|**smallint**|1 = schreibgeschützt<br /><br /> 2 = Scrollsperre<br /><br /> 3 = Vollständig|  
|scrollable|**smallint**|0 = Vorwärts<br /><br /> 1 = Scrollfähig|  
|open_status|**smallint**|0 = Geschlossen<br /><br /> 1 = Geöffnet|  
|cursor_rows|**int**|Die Anzahl von qualifizierenden Zeilen im Resultset. Weitere Informationen finden Sie unter [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|Der Status des letzten Abrufs für diesen Cursor. Weitere Informationen finden Sie unter [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md):<br /><br /> 0 = Abruf erfolgreich.<br /><br /> -1 = Abruf fehlerhaft oder außerhalb des zulässigen Bereichs des Cursors.<br /><br /> -2 = Die angeforderte Zeile fehlt.<br /><br /> -9 = Kein Abruf für Cursor.|  
|column_count|**smallint**|Die Anzahl von Spalten im Resultset des Cursors.|  
|row_count|**smallint**|Die Anzahl von Zeilen, auf die sich der letzte Vorgang für den Cursor auswirkt. Weitere Informationen finden Sie unter [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**smallint**|Der zuletzt ausgeführte Vorgang für den Cursor:<br /><br /> 0 = Für den Cursor wurden keine Vorgänge ausgeführt.<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = EINFÜGEN<br /><br /> 4 = UPDATE<br /><br /> 5 = LÖSCHEN<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|Ein eindeutiger Wert für den Cursor innerhalb des Serverbereichs.|  
  
## <a name="remarks"></a>Hinweise  
 sp_cursor_list erstellt eine Liste der aktuellen Servercursor, die für die Verbindung geöffnet sind, und beschreibt die globalen Cursorattribute, wie z. B. die Scrolloptionen und die Aktualisierbarkeit des Cursors. sp_cursor_list listet die folgenden Cursor auf:  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor.  
  
-   API-Servercursor geöffnet, die von einer ODBC-Anwendung, die dann SQLSetCursorName zum Benennen des Cursors aufgerufen wird.  
  
 Mit sp_describe_cursor_columns zeigen Sie eine Beschreibung der Attribute des vom Cursor zurückgegebenen Resultsets. Mit sp_describe_cursor_tables zeigen Sie an, auf welche Basistabellen der Cursor verweist. Sp_describe_cursor zeigt dieselben Informationen an wie Sp_cursor_list, jedoch nur für den angegebenen Cursor.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen erhält standardmäßig die public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein globaler Cursor geöffnet und mithilfe von `sp_cursor_list` ein Bericht der Cursorattribute erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
