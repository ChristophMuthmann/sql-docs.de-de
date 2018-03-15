---
title: NEXT VALUE FOR (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a4e6ca2ce4c89e1e608d9762d1562a78f7908c23
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Generiert eine Sequenznummer aus dem angegebenen Sequenzobjekt.  
  
 Eine umfassende Erläuterung der Erstellung und Verwendung von Sequenzen finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md). Mit [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) können Sie einen Bereich von Sequenznummern reservieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank mit dem Sequenzobjekt.  
  
 *schema_name*  
 Der Name des Schemas mit dem Sequenzobjekt.  
  
 *sequence_name*  
 Der Name des Sequenzobjekts, von dem die Nummer generiert wird.  
  
 *over_order_by_clause*  
 Bestimmt die Reihenfolge, in der der Sequenzwert den Zeilen in einer Partition zugewiesen wird. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt mit dem Typ der Sequenz eine Nummer zurück.  
  
## <a name="remarks"></a>Remarks  
 Die **NEXT VALUE FOR**-Funktion kann in gespeicherten Prozeduren und Triggern verwendet werden.  
  
 Wird bei Verwendung der **NEXT VALUE FOR**-Funktion in einer Abfrage oder Standardeinschränkung das gleiche Sequenzobjekt mehr als einmal verwendet oder das gleiche Sequenzobjekt sowohl in der Anweisung, die die Werte angibt, als auch in einer ausgeführten Standardeinschränkung verwendet, wird der gleiche Wert für alle Spalten zurückgegeben, die in einer Zeile im Resultset auf die gleiche Sequenz verweisen.  
  
 Die **NEXT VALUE FOR**-Funktion ist nicht deterministisch und nur in Kontexten zulässig, in denen die Anzahl der generierten Sequenzwerte exakt definiert ist. Nachfolgend finden Sie eine Definition der Anzahl der Werte, die für das jeweilige Sequenzobjekt, auf das verwiesen wird, in einer Anweisung verwendet werden:  
  
-   **SELECT**: Für jedes Sequenzobjekt, auf das verwiesen wird, wird im Ergebnis der Anweisung einmal pro Zeile ein neuer Wert generiert.  
  
-   **INSERT** … **VALUES**: Für jedes Sequenzobjekt, auf das verwiesen wird, wird in der Anweisung einmal pro eingefügte Zeile ein neuer Wert generiert.  
  
-   **UPDATE**: Für jedes Sequenzobjekt, auf das verwiesen wird, wird ein neuer Wert für jede Zeile generiert, die von der Anweisung aktualisiert wird.  
  
-   Verfahrensanweisungen (beispielsweise **DECLARE**, **SET**, usw.): Für jedes Sequenzobjekt, auf das verwiesen wird, wird eine neuer Wert für jede Anweisung generiert.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die **NEXT VALUE FOR**-Funktion kann in den folgenden Situationen nicht verwendet werden:  
  
-   Bei Datenbanken im schreibgeschützten Modus  
  
-   Bei Argumenten für eine Tabellenwertfunktion  
  
-   Bei Argumenten für eine Aggregatfunktion  
  
-   Bei Unterabfragen einschließlich allgemeiner Tabellenausdrücke und abgeleiteter Tabellen  
  
-   Bei Sichten, in benutzerdefinierten Funktionen oder in berechneten Spalten  
  
-   Bei Anweisungen, die den Operator **DISTINCT**, **UNION**, **UNION ALL**, **EXCEPT** oder **INTERSECT** verwenden.  
  
-   Bei Anweisungen, die die **ORDER BY**-Klausel verwenden, außer wenn **NEXT VALUE FOR** … **OVER** (**ORDER BY** …) verwendet wird.  
  
-   Bei den folgenden Klauseln: **FETCH**, **OVER**, **OUTPUT**, **ON**, **PIVOT**, **UNPIVOT**, **GROUP BY**, **HAVING**, **COMPUTE**, **COMPUTE BY** oder **FOR XML**.  
  
-   Bei bedingten Ausdrücken mit **CASE**, **CHOOSE**, **COALESCE**, **IIF**, **ISNULL** oder **NULLIF**.  
  
-   Bei einer **VALUES**-Klausel, die nicht Teil einer **INSERT**-Anweisung ist.  
  
-   Bei der Definition einer CHECK-Einschränkung  
  
-   Bei der Definition einer Regel oder eines Standardobjekts. (Die Verwendung in einer Standardeinschränkung ist möglich.)  
  
-   Als Standard in einem benutzerdefinierten Tabellentyp.  
  
-   In einer Anweisung mit **TOP**, **OFFSET** oder wenn die **ROWCOUNT**-Option festgelegt ist.  
  
-   In der **WHERE**-Klausel einer Anweisung.  
  
-   In einer **MERGE**-Anweisung. (Ausnahme: Wenn die **NEXT VALUE FOR**-Funktion in einer Standardeinschränkung in der Zieltabelle und in der **CREATE**-Anweisung der **MERGE**-Anweisung der Standardwert verwendet wird.)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>Verwenden eines Sequenzobjekts in einer Standardeinschränkung  
 Wenn Sie die **NEXT VALUE FOR**-Funktion in einer Standardeinschränkung verwenden, gelten die folgenden Regeln:  
  
-   Standardeinschränkungen in mehreren Tabellen können auf ein einzelnes Sequenzobjekt verweisen.  
  
-   Die Tabelle und das Sequenzobjekt müssen sich in der gleichen Datenbank befinden.  
  
-   Der Benutzer, der die Standardeinschränkung hinzufügt, muss über die REFERENCES-Berechtigung für das Sequenzobjekt verfügen.  
  
-   Ein Sequenzobjekt, auf das von einer Standardeinschränkung verwiesen wird, kann nicht gelöscht werden, bevor nicht die Standardeinschränkung gelöscht wurde.  
  
-   Wenn mehrere Standardeinschränkungen das gleiche Sequenzobjekt verwenden, oder wenn das gleiche Sequenzobjekt sowohl in der Anweisung verwendet wird, die die Werte angibt, als auch in einer Standardeinschränkung, die ausgeführt wird, wird die gleiche Sequenznummer für alle Spalten in einer Zeile zurückgegeben.  
  
-   Verweise auf die **NEXT VALUE FOR**-Funktion in einer Standardeinschränkung können keine **OVER**-Klausel angeben.  
  
-   Ein Sequenzobjekt, auf das in einer Standardeinschränkung verwiesen wird, kann geändert werden.  
  
-   Bei einer `INSERT … SELECT`- oder `INSERT … EXEC`-Anweisung, bei der die eingefügten Daten aus einer Abfrage mit einer **ORDER BY**-Klausel stammen, werden die von der **NEXT VALUE FOR**-Funktion zurückgegebenen Werte in der von der **ORDER BY**-Klausel angegebenen Reihenfolge generiert.  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>Verwenden eines Sequenzobjekts mit einer OVER ORDER BY-Klausel  
 Die **NEXT VALUE FOR**-Funktion unterstützt das Generieren von sortierten Sequenzwerten durch Verwenden der **OVER**-Klausel für den **NEXT VALUE FOR**-Aufruf. Die Verwendung der **OVER**-Klausel garantiert dem Benutzer, dass die zurückgegebenen Werte in der Reihenfolge generiert werden, die von der **ORDER BY**-Unterklausel der **OVER**-Klausel festgelegt wird. Die Verwendung der **NEXT VALUE FOR**-Funktion mit der **OVER**-Klausel unterliegt folgenden zusätzlichen Regeln:  
  
-   Mehrere Aufrufe der **NEXT VALUE FOR**-Funktion für den gleichen Sequenzgenerator in einer einzelnen Anweisung müssen jeweils die gleiche **OVER**-Klauseldefinition verwenden.  
  
-   Mehrere Aufrufe der **NEXT VALUE FOR**-Funktion, die auf unterschiedliche Sequenzgeneratoren in einer einzelnen Anweisung verweisen, können verschiedene **OVER**-Klauseldefinitionen aufweisen.  
  
-   Eine **OVER**-Klausel, die auf die **NEXT VALUE FOR**-Funktion angewendet wird, unterstützt keine **PARTITION BY**-Unterklausel.  
  
-   Wenn alle Aufrufe der **NEXT VALUE FOR**-Funktion in einer **SELECT**-Anweisung die **OVER**-Klausel angeben, kann eine **ORDER BY**-Klausel in der **SELECT**-Anweisung verwendet werden.  
  
-   Die **OVER**-Klausel kann mit der **NEXT VALUE FOR**-Funktion in einer **SELECT**-Anweisung oder in einer `INSERT … SELECT …`-Anweisung verwendet werden. Das Verwenden der **OVER**-Klausel mit der **NEXT VALUE FOR**-Funktion ist in **UPDATE**- oder **MERGE**-Anweisungen nicht zulässig.  
  
-   Wenn ein anderer Prozess zur gleichen Zeit auf das Sequenzobjekt zugreift, weisen die zurückgegebenen Zahlen möglicherweise Lücken auf.  
  
## <a name="metadata"></a>Metadaten  
 Fragen Sie die [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)-Katalogsicht ab, um Informationen zu Sequenzen zu erhalten.  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die **UPDATE**-Berechtigung für das Sequenzobjekt oder das Schema der Sequenz. Ein Beispiel für das Gewähren der Berechtigung finden Sie weiter unten in diesem Thema in Beispiel F.  
  
### <a name="ownership-chaining"></a>Besitzverkettung  
 Sequenzobjekte unterstützen die Besitzverkettung. Wenn das Sequenzobjekt über den gleichen Besitzer wie die aufrufende gespeicherte Prozedur, der aufrufende Trigger oder die aufrufende Tabelle (mit einem Sequenzobjekt als Standardeinschränkung) verfügt, ist keine Überprüfung der Berechtigung für das Sequenzobjekt erforderlich. Wenn das Sequenzobjekt nicht im Besitz des gleichen Benutzers wie die aufrufende gespeicherte Prozedur, der aufrufende gespeicherte Trigger oder die aufrufende gespeicherte Tabelle ist, muss die Berechtigung für das Sequenzobjekt überprüft werden.  
  
 Wenn die **NEXT VALUE FOR**-Funktion als Standardwert in einer Tabelle verwendet wird, benötigen Benutzer eine **INSERT**-Berechtigung für die Tabelle sowie eine **UPDATE**-Berechtigung für das Sequenzobjekt, um Daten mithilfe der Standardeinstellung hinzuzufügen.  
  
-   Wenn die Standardeinschränkung den gleichen Besitzer wie das Sequenzobjekt hat, sind beim Aufrufen der Standardeinschränkung keine Berechtigungen für das Sequenzobjekt erforderlich.  
  
-   Wenn die Standardeinschränkung und das Sequenzobjekt nicht dem gleichen Benutzer gehören, sind Berechtigungen für das Sequenzobjekt auch beim Aufrufen der Standardeinschränkung erforderlich.  
  
### <a name="audit"></a>Überwachen von  
 Sie können die **NEXT VALUE FOR**-Funktion überwachen, indem Sie die SCHEMA_OBJECT_ACCESS_GROUP überwachen.  
  
## <a name="examples"></a>Beispiele  
 Beispiele zum Erstellen von Sequenzen und Verwenden der **NEXT VALUE FOR**-Funktion für das Generieren von Sequenznummern finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 In den folgenden Beispielen wird die Sequenz `CountBy1` im Schema `Test` verwendet. Führen Sie die folgende Anweisung aus, um die `Test.CountBy1`-Sequenz zu erstellen. In den Beispielen C und E wird die Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] verwendet; die `CountBy1`-Sequenz wird daher in dieser Datenbank erstellt.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. Verwenden einer Sequenz in einer SELECT-Anweisung  
 Im folgenden Beispiel wird die Sequenz `CountBy1` erstellt, die bei jeder Verwendung um den Wert eins vergrößert wird.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. Festlegen einer Variable auf den nächsten Sequenzwert  
 Im folgenden Beispiel werden drei Möglichkeiten veranschaulicht, eine Variable auf den nächsten Wert einer Sequenznummer festzulegen.  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. Verwenden einer Sequenz mit einer Fensterrangfunktion  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. Verwenden der NEXT VALUE FOR-Funktion in der Definition einer Standardeinschränkung  
 Die Verwendung der **NEXT VALUE FOR**-Funktion in der Definition einer Standardeinschränkung wird unterstützt. Ein Beispiel für die Verwendung der **NEXT VALUE FOR**-Funktion in einer **CREATE TABLE**-Anweisung finden Sie unter Beispiel C [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md). Im folgenden Beispiel wird `ALTER TABLE` verwendet, um eine Sequenz als Standard einer aktuellen Tabelle hinzuzufügen.  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. Verwenden der NEXT VALUE FOR-Funktion in einer INSERT-Anweisung  
 Im folgenden Beispiel wird die Tabelle `TestTable` erstellt, und mit der `NEXT VALUE FOR`-Funktion wird eine Zeile eingefügt.  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. Verwenden der NEXT VALUE FOR-Funktion mit SELECT … INTO  
 Im folgenden Beispiel wird mit der `SELECT … INTO`-Anweisung eine Tabelle namens `Production.NewLocation` erstellt und mit der `NEXT VALUE FOR`-Funktion jede Zeile nummeriert.  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. Erteilen der Berechtigung zum Ausführen von NEXT VALUE FOR  
 Im folgenden Beispiel wird dem Benutzer `AdventureWorks\Larry` die **UPDATE**-Berechtigung zum Ausführen von `NEXT VALUE FOR` mit der `Test.CounterSeq`-Sequenz gewährt.  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
