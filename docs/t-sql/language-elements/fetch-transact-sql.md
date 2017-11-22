---
title: Abrufen von Daten (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FETCH
- FETCH_TSQL
dev_langs: TSQL
helpviewer_keywords:
- FETCH statement
- cursors [SQL Server], fetching
- Transact-SQL cursors, fetching and scrolling
- retrieving rows
- fetching [SQL Server]
- SCROLL option
- row fetching [SQL Server]
ms.assetid: 5d68dac2-f91b-4342-bb4e-209ee132665f
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ccf0fc44e9be488c7c07cdb159270056bba0adc6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="fetch-transact-sql"></a>FETCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ruft eine bestimmte Zeile aus einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor ab.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FETCH   
          [ [ NEXT | PRIOR | FIRST | LAST   
                    | ABSOLUTE { n | @nvar }   
                    | RELATIVE { n | @nvar }   
               ]   
               FROM   
          ]   
{ { [ GLOBAL ] cursor_name } | @cursor_variable_name }   
[ INTO @variable_name [ ,...n ] ]   
```  
  
## <a name="arguments"></a>Argumente  
 NEXT  
 Gibt die auf die aktuelle Zeile folgende Zeile zurück und macht diese zur aktuellen Zeile. Ist FETCH NEXT der erste Datenabruf vom Cursor, wird die erste Zeile im Resultset zurückgegeben. NEXT ist die Standardoption für Datenabruf vom Cursor.  
  
 PRIOR  
 Gibt die der aktuellen Zeile vorangehende Zeile zurück und macht diese zur aktuellen Zeile. Ist FETCH PRIOR der erste Datenabruf vom Cursor, wird keine Zeile zurückgegeben, und die Cursorposition verbleibt vor der ersten Zeile.  
  
 FIRST  
 Gibt die erste Zeile im Cursor zurück und macht sie zur aktuellen Zeile.  
  
 LAST  
 Gibt die letzte Zeile im Cursor zurück und macht sie zur aktuellen Zeile.  
  
 ABSOLUTE {  *n* | @*Nvar*}  
 Wenn  *n*  oder @*Nvar* positive Zahl ist, wird die Zeile zurückgegeben  *n*  ausgehend vom Anfang des Cursors-te. der zurückgegebenen Zeile der aktuelle Zeile. Wenn  *n*  oder @*Nvar* ist ein negativer Wert ist, wird die Zeile  *n*  vor dem Ende des Cursors-te. der zurückgegebenen Zeile der aktuelle Zeile. Wenn  *n*  oder @*Nvar* gleich 0 ist, werden keine Zeilen zurückgegeben. *n*muss eine ganzzahlige Konstante und @*Nvar* muss **"smallint"**, **"tinyint"**, oder **Int**.  
  
 RELATIVE {  *n* | @*Nvar*}  
 Wenn  *n*  oder @*Nvar* positive Zahl ist, wird die Zeile zurückgegeben  *n*  der aktuellen Zeile-te. der zurückgegebenen Zeile der aktuelle Zeile. Wenn  *n*  oder @*Nvar* ist ein negativer Wert ist, wird die Zeile  *n*  Zeilen vor der aktuellen Zeile und macht der zurückgegebenen Zeile der aktuelle Zeile. Wenn  *n*  oder @*Nvar* gleich 0 ist, wird die aktuelle Zeile zurückgegeben. Wenn Sie mit FETCH RELATIVE angegeben wird  *n*  oder @*Nvar* 0 oder auf der ersten Datenabruf vom Cursor negative Zahl festgelegt, werden keine Zeilen zurückgegeben. *n*muss eine ganzzahlige Konstante und @*Nvar* muss **"smallint"**, **"tinyint"**, oder **Int**.  
  
 GLOBAL  
 Gibt an, dass *Cursor_name* auf einen globalen Cursor verweist.  
  
 *Cursorname*  
 Der Name des geöffneten Cursors, von dem der Abruf erfolgen soll. Wenn sowohl ein globaler als auch ein lokaler Cursor mit vorhanden *Cursor_name* als Buchstabenfolge, *Cursor_name* auf den globalen Cursor, wenn GLOBAL angegeben ist und auf den lokalen Cursor GLOBAL nicht angegeben ist.  
  
 @*cursor_variable_name*  
 Der Name einer Cursorvariablen, die sich auf den geöffneten Cursor bezieht, von dem der Abruf erfolgen soll.  
  
 INTO @*Variable_name*[,... *n*]  
 Ermöglicht die Zuweisung von Daten aus den Spalten, die durch einen Abruf zurückgegeben werden, an lokale Variablen. Jeder Variablen in der Liste wird (von links nach rechts) die entsprechende Spalte im Cursorresultset zugeordnet. Die Datentypen aller Variablen müssen mit dem Datentyp der entsprechenden Resultsetspalte übereinstimmen oder implizit in diesen Datentyp konvertiert werden können. Die Anzahl von Variablen muss mit der Anzahl von Spalten in der SELECT-Liste des Cursors übereinstimmen.  
  
## <a name="remarks"></a>Hinweise  
 Wird SCROLL in der ISO-Anweisung DECLARE CURSOR nicht angegeben, wird lediglich die FETCH-Option NEXT unterstützt. Wird SCROLL in der ISO-Anweisung DECLARE CURSOR angegeben, werden alle FETCH-Optionen unterstützt.  
  
 Wenn die DECLARE CURSOR-Erweiterungen von [!INCLUDE[tsql](../../includes/tsql-md.md)] verwendet werden, gelten folgende Regeln:  
  
-   Falls entweder FORWARD_ONLY oder FAST_FORWARD angegeben wird, wird lediglich die FETCH-Option NEXT unterstützt.  
  
-   Wenn keine der Optionen DYNAMIC, FORWARD_ONLY oder FAST_FORWARD, aber eine der Optionen KEYSET, STATIC oder SCROLL angegeben ist, werden alle FETCH-Optionen unterstützt.  
  
-   DYNAMIC SCROLL-Cursor unterstützen alle FETCH-Optionen außer ABSOLUTE.  
  
 Der @@FETCH_STATUS -Funktion meldet den Status der letzten FETCH-Anweisung. Die gleichen Informationen werden in der fetch_status-Spalte des Cursors gespeichert, der von sp_describe_cursor zurückgegeben wird. Mit diesen Statusinformationen kann die Gültigkeit von Daten einer vorangehenden FETCH-Anweisung überprüft werden, bevor diese Daten weiterverarbeitet werden. Weitere Informationen finden Sie unter [@@FETCH_STATUS &#40; Transact-SQL &#41; ](../../t-sql/functions/fetch-status-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 FETCH-Berechtigungen erhalten standardmäßig alle gültigen Benutzer.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-fetch-in-a-simple-cursor"></a>A. Verwenden von FETCH in einem einfachen Cursor  
 Im folgenden Beispiel wird ein einfacher Cursor für die Zeilen in der `Person.Person`-Tabelle deklariert, die einen Nachnamen enthalten, der mit `B` beginnt. Mit `FETCH NEXT` wird Zeile für Zeile eingelesen. Die `FETCH`-Anweisungen geben den Wert für die in `DECLARE CURSOR` angegebene Spalte als einzeiliges Resultset zurück.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch.  
FETCH NEXT FROM contact_cursor;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="b-using-fetch-to-store-values-in-variables"></a>B. Verwenden von FETCH, um Werte in Variablen zu speichern  
 Das folgende Beispiel ähnelt Beispiel A. Allerdings wird hier die Ausgabe der `FETCH`-Anweisungen in lokalen Variablen gespeichert und nicht direkt an den Client zurückgegeben. Die `PRINT`-Anweisung fasst die Variablen zu einer einzelnen Zeichenfolge zusammen und gibt sie an den Client zurück.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare the variables to store the values returned by FETCH.  
DECLARE @LastName varchar(50), @FirstName varchar(50);  
  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch and store the values in variables.  
-- Note: The variables are in the same order as the columns  
-- in the SELECT statement.   
  
FETCH NEXT FROM contact_cursor  
INTO @LastName, @FirstName;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
  
   -- Concatenate and display the current values in the variables.  
   PRINT 'Contact Name: ' + @FirstName + ' ' +  @LastName  
  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor  
   INTO @LastName, @FirstName;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="c-declaring-a-scroll-cursor-and-using-the-other-fetch-options"></a>C. Deklarieren eines SCROLL-Cursors und Verwenden der übrigen FETCH-Optionen  
 Im folgenden Beispiel wird ein `SCROLL`-Cursor erstellt, damit alle Möglichkeiten für das Durchführen eines Bildlaufs mit den Optionen `LAST`, `PRIOR`, `RELATIVE` und `ABSOLUTE` genutzt werden können.  
  
```  
USE AdventureWorks2012;  
GO  
-- Execute the SELECT statement alone to show the   
-- full result set that is used by the cursor.  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
-- Declare the cursor.  
DECLARE contact_cursor SCROLL CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Fetch the last row in the cursor.  
FETCH LAST FROM contact_cursor;  
  
-- Fetch the row immediately prior to the current row in the cursor.  
FETCH PRIOR FROM contact_cursor;  
  
-- Fetch the second row in the cursor.  
FETCH ABSOLUTE 2 FROM contact_cursor;  
  
-- Fetch the row that is three rows after the current row.  
FETCH RELATIVE 3 FROM contact_cursor;  
  
-- Fetch the row that is two rows prior to the current row.  
FETCH RELATIVE -2 FROM contact_cursor;  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Schließen &#40; Transact-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Aufheben der ZUORDNUNG &#40; Transact-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [OPEN &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
