---
title: Legen Sie @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a92fa424de70d1ba9cccf437a2de49ab8432ba1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-localvariable-transact-sql"></a>Legen Sie @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt die angegebene lokale Variable, die zuvor erstellt haben, mit der DECLARE @*Local_variable* -Anweisung mit dem angegebenen Wert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET @local_variable {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
  
```  
  
## <a name="arguments"></a>Argumente  
 **@***Local_variable*  
 Der Name einer Variablen eines beliebigen Typs außer **Cursor**, **Text**, **Ntext**, **Image**, oder **Tabelle**. Variablennamen müssen mit einem at-Zeichen beginnen (**@**). Variablennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *Eigenschaftsname*  
 Eigenschaft eines benutzerdefinierten Typs.  
  
 *Feldname*  
 Öffentliches Feld eines benutzerdefinierten Typs.  
  
 *udt_name*  
 Der Name eines benutzerdefinierten CLR-Typs (Common Language Runtime).  
  
 { **.** | **::** }  
 Gibt eine Methode für einen benutzerdefinierten CLR-Typ an. Verwenden Sie z. B. für eine Instanzmethode (nicht statisch) einen Punkt (**.**). Verwenden Sie für eine statische Methode zwei Doppelpunkte (**::**). Zum Aufrufen einer Methode, Eigenschaft oder eines Felds eines CLR-benutzerdefinierten Typs müssen Sie über die EXECUTE-Berechtigung für den Typ verfügen.  
  
 *keine Variablenargumentlisten verwenden* **(** *Argument* [ **,**... *n* ] **)**  
 Eine Methode eines benutzerdefinierten Typs, der ein oder mehrere Argumente übergeben werden, um den Status einer Instanz eines Typs zu ändern. Statische Methoden müssen öffentlich sein.  
  
 **@***SQLCLR_local_variable*  
 Eine Variable, deren Typ sich in einer Assembly befindet. Weitere Informationen finden Sie unter [Common Language Runtime &#40;CLR&#41; Programmierkonzepte für die Integration](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 *mutator_method*  
 Ist eine Methode in der Assembly, die den Status des Objekts ändern kann. SQLMethodAttribute.IsMutator wird für diese Methode angewendet.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Verbundzuweisungsoperator:  
  
 += Addition und Zuweisung  
  
 = Subtraktion und Zuweisung  
  
 * = Multiplikation und Zuweisung  
  
 / = Division und Zuweisung  
  
 % = Modulo und Zuweisung  
  
 &=              Bitweises AND und Zuweisung  
  
 ^ = Bitweises XOR und Zuweisung  
  
 | = Bitweises OR und Zuweisung  
  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *cursor_variable*  
 Ist der Name einer Cursorvariablen. Falls die Zielcursorvariable zuvor auf einen anderen Cursor verwiesen hat, wird dieser Verweis entfernt.  
  
 *Cursorname*  
 Der Name eines Cursors, der mit der DECLARE CURSOR-Anweisung deklariert wurde.  
  
 CURSOR  
 Gibt an, dass die SET-Anweisung eine Cursordeklaration enthält.  
  
 SCROLL  
 Gibt an, dass der Cursor alle FETCH-Optionen unterstützt (FIRST, LAST, NEXT, PRIOR, RELATIVE und ABSOLUTE). Es kann nur eine der beiden Optionen SCROLL oder FAST_FORWARD angegeben werden.  
  
 FORWARD_ONLY  
 Gibt an, dass der Cursor nur die Option FETCH NEXT unterstützt. Der Cursor kann nur in einer Richtung abgerufen werden, von der ersten zur letzten Zeile. Wenn FORWARD_ONLY ohne die Schlüsselwörter STATIC, KEYSET oder DYNAMIC angegeben wird, wird der Cursor mit der Option DYNAMIC implementiert. Wenn weder FORWARD_ONLY noch SCROLL angegeben wird, wird standardmäßig FORWARD_ONLY verwendet, es sei denn, die Schlüsselwörter STATIC, KEYSET oder DYNAMIC werden angegeben. STATIC-, KEYSET- und DYNAMIC-Cursor werden standardmäßig auf SCROLL festgelegt.  
  
 STATIC  
 Definiert einen Cursor, der eine temporäre Kopie der von ihm zu verwendenden Daten erzeugt. Sämtliche Anforderungen an den Cursor werden von dieser temporären Tabelle in tempdb beantwortet; daher werden Änderungen, die an den Basistabellen vorgenommen werden, nicht in den Daten wiedergegeben, die durch Abrufoperationen an diesem Cursor zurückgegeben wurden. Darüber hinaus lässt dieser Cursor keine Änderungen zu.  
  
 KEYSET  
 Gibt an, dass im Cursor die Mitgliedschaft und Reihenfolge der Zeilen fest ist, wenn der Cursor geöffnet wird. Die Menge der Schlüssel, die die Zeilen eindeutig identifizieren, wird in der Keysettable in ' tempdb ' integriert. Änderungen an Nichtschlüsselwerten in den Basistabellen, die vom Cursorbesitzer oder durch Ausführen eines Commits von anderen Benutzern vorgenommen wurden, werden sichtbar, wenn der Cursorbesitzer im Cursor einen Bildlauf durchführt. Von anderen Benutzern vorgenommene Einfügungen sind nicht sichtbar, und Einfügevorgänge können nicht über einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor durchgeführt werden.  
  
 Wenn eine Zeile gelöscht wird, gibt ein Versuch zum Abrufen der Zeile ein @@FETCH_STATUS -2. Updates von Schlüsselwerten von außerhalb des Cursors sind vergleichbar mit dem Löschen der alten Zeile, gefolgt von einem Einfügen der neuen Zeile. Die Zeile mit den neuen Werten ist nicht sichtbar, und versucht, die Zeile mit den alten Werten abzurufen Zurückgeben einer @@FETCH_STATUS -2. Die neuen Werte sind sichtbar, wenn die Aktualisierung über den Cursor durch Angeben der WHERE CURRENT OF-Klausel durchgeführt wird.  
  
 DYNAMIC  
 Definiert einen Cursor, der alle in den Zeilen vorgenommenen Datenänderungen in seinem Resultset widerspiegelt, wenn der Cursorbesitzer im Cursor einen Bildlauf durchführt. Datenwerte, Reihenfolge und Mitgliedschaft der Zeilen können sich bei jedem Abrufvorgang ändern. Die Abrufoptionen FETCH RELATIVE und FETCH ABSOLUTE werden mit dynamischen Cursorn nicht unterstützt.  
  
 FAST_FORWARD  
 Gibt einen FORWARD_ONLY-, READ_ONLY-Cursor mit aktivierter Optimierung an. FAST_FORWARD kann angegeben werden, wenn auch SCROLL angegeben ist.  
  
 READ_ONLY  
 Verhindert, dass Updates über diesen Cursor erfolgen. Auf den Cursor kann nicht in einer WHERE CURRENT OF-Klausel in einer UPDATE- oder DELETE-Anweisung verwiesen werden. Diese Option überschreibt die Standardeinstellung, nach der ein Cursor aktualisiert werden kann.  
  
 SCROLL LOCKS  
 Gibt an, dass positionierte Updates oder Löschungen durch den Cursor garantiert erfolgreich sind. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sperrt die Zeilen, während sie in den Cursor eingelesen werden, um ihre Verfügbarkeit für spätere Änderungen sicherzustellen. Es kann nur eine der beiden Optionen SCROLL_LOCKS oder FAST_FORWARD angegeben werden.  
  
 OPTIMISTIC  
 Gibt an, dass positionierte Updates oder Löschungen durch den Cursor nicht erfolgreich sind, wenn die Zeile seit dem letzten Einlesen in den Cursor aktualisiert wurde. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sperrt keine Zeilen, während sie in den Cursor eingelesen werden. Stattdessen wird durch Vergleiche von timestamp-Spaltenwerten oder durch einen Prüfsummenwert, wenn die Tabelle keine timestamp-Spalte aufweist, bestimmt, ob die Zeile nach dem Einlesen in den Cursor geändert wurde. Wurde die Zeile geändert, so schlägt der versuchte positionierte Update- oder Löschvorgang fehl. Es kann nur eine der beiden Optionen OPTIMISTIC oder FAST_FORWARD angegeben werden.  
  
 TYPE_WARNING  
 Gibt an, dass dem Client eine Warnmeldung gesendet wird, wenn der Cursor vom angeforderten Typ in einen anderen Typ implizit konvertiert wird.  
  
 FÜR *Select_statement*  
 Eine standardmäßige SELECT-Anweisung, die das Resultset des Cursors definiert. Die Schlüsselwörter FOR BROWSE und INTO sind nicht zulässig, in der *Select_statement* der Deklaration eines Cursors.  
  
 Wenn DISTINCT, UNION, GROUP BY- oder HAVING verwendet werden, oder ein Aggregatausdruck, in enthalten ist der *Select_list*, wird der Cursor als STATIC erstellt werden.  
  
 Wenn keine der zugrunde liegenden Tabellen einen eindeutigen Index besitzt und ein SCROLL-Cursor von ISO oder ein KEYSET-Cursor von [!INCLUDE[tsql](../../includes/tsql-md.md)] angefordert wird, liegt automatisch ein STATIC-Cursor vor.  
  
 Wenn *Select_statement* enthält eine ORDER BY-Klausel in der die Spalten keine eindeutigen Zeilenbezeichner sind, ein DYNAMISCHER Cursor wird konvertiert in einen Keysetcursor oder in einen statischen Cursor, wenn ein KEYSET-Cursor nicht geöffnet werden kann. Ebenso wird mit einem Cursor verfahren, der mithilfe der ISO-Syntax, jedoch ohne das STATIC-Schlüsselwort, definiert wurde.  
  
 READ ONLY  
 Verhindert, dass Updates über diesen Cursor erfolgen. Auf den Cursor kann nicht in einer WHERE CURRENT OF-Klausel in einer UPDATE- oder DELETE-Anweisung verwiesen werden. Diese Option überschreibt die Standardeinstellung, nach der ein Cursor aktualisiert werden kann. Dieses Schlüsselwort unterscheidet sich vom vorherigen READ_ONLY durch das Leerzeichen zwischen READ und ONLY anstelle eines Unterstriches.  
  
 UPDATE [OF *Column_name*[ **,**... *n* ] ]  
 Definiert aktualisierbare Spalten innerhalb des Cursors. Wenn OF *Column_name* [**,**...  *n* ] angegeben wird, können nur in die aufgelisteten Spalten geändert werden. Falls keine Liste angegeben wird, können alle Spalten aktualisiert werden, es sei denn, der Cursor wurde mit der Option READ ONLY definiert.  
  
## <a name="remarks"></a>Hinweise  
 Nach dem Deklarieren einer Variablen wird diese auf NULL initialisiert. Verwenden Sie die SET-Anweisung, um einer deklarierten Variablen einen anderen Wert als NULL zuzuweisen. Die SET-Anweisung, die der Variablen einen Wert zuweist, gibt einen einzelnen Wert zurück. Wenn Sie mehrere Variablen initialisieren, verwenden Sie eine separate SET-Anweisung für jede lokale Variable.  
  
 Variablen können nur in Ausdrücken verwendet werden, nicht anstelle von Objektnamen oder Schlüsselwörtern. Um dynamische [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zu erstellen, verwenden Sie EXECUTE.  
  
 Die Syntaxregeln für SET  **@**  *Cursor_variable* schließen nicht die Schlüsselwörter LOCAL und GLOBAL. Wenn der Satz  **@**  *Cursor_variable* = CURSOR...-Syntax verwendet wird, wird der Cursor je nach der Einstellung der Datenbankoption Default to lokalen Cursor als GLOBAL oder LOCAL erstellt.  
  
 Cursorvariablen sind stets lokal, selbst wenn sie auf einen globalen Cursor verweisen. Wenn eine Cursorvariable auf einen globalen Cursor verweist, besitzt der Cursor einen globalen und einen lokalen Verweis. Weitere Informationen finden Sie unter Beispiel C.  
  
 Weitere Informationen finden Sie unter [DECLARE CURSOR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 Der Verbundzuweisungsoperator kann stets verwendet werden, wenn auf der rechten Seite des Operators eine Zuweisung mit einem Ausdruck steht, z. B. Variablen, und SET in einer UPDATE-, SELECT- oder RECEIVE-Anweisung vorhanden ist.  
  
 Verwenden Sie keine Variable in einer SELECT-Anweisung, um Werte zu verketten (d. h., um Aggregatwerte zu berechnen). Dies kann zu unerwarteten Abfrageergebnissen führen. Dies liegt daran, dass nicht gewährleistet ist, dass alle Ausdrücke in der SELECT-Liste (einschließlich Zuweisungen) für jede Ausgabezeile exakt einmal ausgeführt werden. Weitere Informationen finden Sie unter [diesem KB-Artikel](http://support.microsoft.com/kb/287515).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle. Alle Benutzer können SET  **@**  *Local_variable*.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>A. Drucken des Werts einer Variablen, die mit SET initialisiert wurde  
 Das folgende Beispiel erstellt die `@myvar` Variable, legt einen Zeichenfolgenwert in die Variable ab und gibt den Wert der die `@myvar` Variable.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>B. Verwenden einer lokalen Variablen, der ein Wert mit SET zugewiesen wurde, in einer SELECT-Anweisung  
 Im folgenden Beispiel wird eine lokale Variable namens `@state` erstellt, die dann in einer `SELECT`-Anweisung verwendet wird, um die Vor- und Nachnamen aller Mitarbeiter zu suchen, die im US-Bundesstaat `Oregon` ansässig sind.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @state char(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. Verwenden einer Verbundzuweisung für eine lokale Variable  
 Mit den beiden folgenden Beispielen wird das gleiche Ergebnis erzielt. Es wird jeweils eine lokale Variable namens `@NewBalance` erstellt, diese wird mit 10 multipliziert, und der neue Wert der lokalen Variablen wird in einer `SELECT`-Anweisung angezeigt. Im zweiten Beispiel wird ein Verbundzuweisungsoperator verwendet.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. Verwenden von SET mit einem globalen Cursor  
 Im folgenden Beispiel wird eine lokale Variable erstellt und anschließend für die Cursorvariable der globale Cursorname festgelegt.  
  
```  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. Definieren eines Cursors mit SET  
 Dieses Beispiel verwendet die `SET`-Anweisung, um einen Cursor zu definieren.  
  
```  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. Zuweisen eines Werts aus einer Abfrage  
 Das folgende Beispiel verwendet eine Abfrage, um einer Variablen einen Wert zuzuweisen.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. Zuweisen eines Werts zu einer benutzerdefinierten Typvariablen durch Ändern einer Eigenschaft des Typs  
 Im folgenden Beispiel wird ein Wert für den benutzerdefinierten Typ `Point` festgelegt, indem der Wert der `X`-Eigenschaft des Typs geändert wird.  
  
```  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. Zuweisen eines Werts zu einer benutzerdefinierten Typvariablen durch Aufrufen einer Methode des Typs  
 Im folgenden Beispiel wird einen Wert für den benutzerdefinierten Typ **zeigen** durch Aufrufen der Methode `SetXY` des Typs.  
  
```  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>I. Erstellen einer Variablen für einen CLR-Typ und Aufrufen einer Mutatormethode  
 Im folgenden Beispiel wird eine Variable für den Typ `Point` erstellt und anschließend eine Mutatormethode in `Point` ausgeführt.  
  
```  
CREATE ASSEMBLY mytest from 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. Drucken des Werts einer Variablen, die mit SET initialisiert wurde  
 Das folgende Beispiel erstellt die `@myvar` Variable, legt einen Zeichenfolgenwert in die Variable ab und gibt den Wert der die `@myvar` Variable.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT top 1 @myvar FROM sys.databases;  
  
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>K. Verwenden einer lokalen Variablen, der ein Wert mit SET zugewiesen wurde, in einer SELECT-Anweisung  
 Das folgende Beispiel erstellt eine lokale Variable namens `@dept` und verwendet diese lokale Variable in einem `SELECT` Anweisung, um die vor- und Nachnamen Namen aller Mitarbeiter zu suchen, die Arbeiten in der `Marketing` Abteilung.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @dept char(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>L. Verwenden einer Verbundzuweisung für eine lokale Variable  
 Mit den beiden folgenden Beispielen wird das gleiche Ergebnis erzielt. Es wird jeweils eine lokale Variable mit dem Namen `@NewBalance` erstellt, diese wird mit `10` multipliziert, und der neue Wert der lokalen Variablen wird in einer `SELECT`-Anweisung angezeigt. Im zweiten Beispiel wird ein Verbundzuweisungsoperator verwendet.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>M. Zuweisen eines Werts aus einer Abfrage  
 Das folgende Beispiel verwendet eine Abfrage, um einer Variablen einen Wert zuzuweisen.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


