---
title: "NEBEN dem Wert für (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aab8020fa04b978d7ec1b657fe0a1084123dfb48
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Generiert eine Sequenznummer aus dem angegebenen Sequenzobjekt.  
  
 Eine detaillierte Erläuterung der Erstellung und Verwendung von Sequenzen, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md). Verwendung [Sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) generiert einen Bereich von Sequenznummern reservieren.  
  
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
 Bestimmt die Reihenfolge, in der der Sequenzwert den Zeilen in einer Partition zugewiesen wird. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt mit dem Typ der Sequenz eine Nummer zurück.  
  
## <a name="remarks"></a>Hinweise  
 Die **NEXT VALUE FOR** Funktion kann in gespeicherten Prozeduren und Triggern verwendet werden.  
  
 Wenn die **NEXT VALUE FOR** -Funktion in einer Abfrage oder standardeinschränkung verwendet wird, wenn das gleiche Sequenzobjekt mehr als einmal verwendet wird, oder wenn das gleiche Sequenzobjekt sowohl in der Anweisung, die die Werte angibt und in einer standardeinschränkung verwendet wird ausgeführt wird, wird der gleiche Wert für alle Spalten verweisen auf die gleiche Sequenz innerhalb einer Zeile im Resultset zurückgegeben.  
  
 Die **NEXT VALUE FOR** Funktion nicht deterministisch ist, und wird nur in Kontexten zulässig, wobei die Anzahl der generierten Sequenzwerte klar definiert ist. Nachfolgend finden Sie eine Definition der Anzahl der Werte, die für das jeweilige Sequenzobjekt, auf das verwiesen wird, in einer Anweisung verwendet werden:  
  
-   **Wählen Sie** -für jedes Sequenzobjekt, auf die verwiesen wird, wird ein neuer Wert pro Zeile im Resultset der Anweisung einmal generiert.  
  
-   **FÜGEN SIE** ... **Werte** -für jedes Sequenzobjekt, auf die verwiesen wird, wird ein neuer Wert für jede eingefügte Zeile in der Anweisung einmal generiert.  
  
-   **UPDATE** -für jedes Sequenzobjekt, auf die verwiesen wird, wird ein neuer Wert generiert, für jede Zeile, die von der Anweisung aktualisiert wird.  
  
-   Verfahrensanweisungen (z. B. **DECLARE**, **festgelegt**usw.)-für jedes Sequenzobjekt, auf die verwiesen wird, wird ein neuer Wert für jede Anweisung generiert.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die **NEXT VALUE FOR** Funktion kann nicht in den folgenden Situationen verwendet werden:  
  
-   Bei Datenbanken im schreibgeschützten Modus  
  
-   Bei Argumenten für eine Tabellenwertfunktion  
  
-   Bei Argumenten für eine Aggregatfunktion  
  
-   Bei Unterabfragen einschließlich allgemeiner Tabellenausdrücke und abgeleiteter Tabellen  
  
-   Bei Sichten, in benutzerdefinierten Funktionen oder in berechneten Spalten  
  
-   In einer Anweisung mit der **DISTINCT**, **UNION**, **UNION ALL**, **EXCEPT** oder **INTERSECT** Operator.  
  
-   In einer Anweisung mit der **ORDER BY** Klausel, wenn **NEXT VALUE FOR** ... **ÜBER** (**ORDER BY** ...) dient.  
  
-   In den folgenden Klauseln: **FETCH**, **über**, **Ausgabe**, **ON**, **PIVOT**,  **UNPIVOT**, **GRUPPIEREN nach**, **HAVING**, **berechnen**, **COMPUTE BY**, oder **FOR XML-**.  
  
-   In bedingten Ausdrücken mit **Fall**, **auswählen**, **COALESCE**, **IIF**, **ISNULL**, oder  **NULLIF**.  
  
-   In einem **Werte** -Klausel, die nicht Teil einer **einfügen** Anweisung.  
  
-   Bei der Definition einer CHECK-Einschränkung  
  
-   Bei der Definition einer Regel oder eines Standardobjekts. (Die Verwendung in einer Standardeinschränkung ist möglich.)  
  
-   Als Standard in einem benutzerdefinierten Tabellentyp.  
  
-   In einer Anweisung mit **oben**, **OFFSET**, oder wenn die **ROWCOUNT** Option festgelegt ist.  
  
-   In der **, in dem** -Klausel einer Anweisung.  
  
-   In einem **MERGE** Anweisung. (Ausnahme: Wenn die **NEXT VALUE FOR** Funktion in Default-Einschränkung in der Zieltabelle verwendet wird und Standard wird verwendet, der **erstellen** -Anweisung die **MERGE** Anweisung.)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>Verwenden eines Sequenzobjekts in einer Standardeinschränkung  
 Bei Verwendung der **NEXT VALUE FOR** Funktion in Default-Einschränkung, gelten die folgenden Regeln:  
  
-   Standardeinschränkungen in mehreren Tabellen können auf ein einzelnes Sequenzobjekt verweisen.  
  
-   Die Tabelle und das Sequenzobjekt müssen sich in der gleichen Datenbank befinden.  
  
-   Der Benutzer, der die Standardeinschränkung hinzufügt, muss über die REFERENCES-Berechtigung für das Sequenzobjekt verfügen.  
  
-   Ein Sequenzobjekt, auf das von einer Standardeinschränkung verwiesen wird, kann nicht gelöscht werden, bevor nicht die Standardeinschränkung gelöscht wurde.  
  
-   Wenn mehrere Standardeinschränkungen das gleiche Sequenzobjekt verwenden, oder wenn das gleiche Sequenzobjekt sowohl in der Anweisung verwendet wird, die die Werte angibt, als auch in einer Standardeinschränkung, die ausgeführt wird, wird die gleiche Sequenznummer für alle Spalten in einer Zeile zurückgegeben.  
  
-   Verweise auf die **NEXT VALUE FOR** -Funktion in Default-Einschränkung kann nicht angegeben werden. die **über** Klausel.  
  
-   Ein Sequenzobjekt, auf das in einer Standardeinschränkung verwiesen wird, kann geändert werden.  
  
-   Im Fall von ein `INSERT … SELECT` oder `INSERT … EXEC` Anweisung, in denen die Einfügen von Daten stammen aus einer Abfrage mit, einer **ORDER BY** -Klausel, die die Rückgabewerte von der **NEXT VALUE FOR** Funktion generiert in der Reihenfolge gemäß der **ORDER BY** Klausel.  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>Verwenden eines Sequenzobjekts mit einer OVER ORDER BY-Klausel  
 Die **NEXT VALUE FOR** Funktion unterstützt das Generieren von sortierten Sequenzwerten durch Anwenden der **über** -Klausel, um die **NEXT VALUE FOR** aufrufen. Mithilfe der **über** -Klausel garantiert dem Benutzer, dass die zurückgegebenen Werte, in der Größenordnung von generiert werden der **über** -Klausel **Reihenfolge B**Y-Unterklausel. Die folgenden zusätzlichen Regeln gelten bei Verwendung der **NEXT VALUE FOR** -Funktion mit dem **über** Klausel:  
  
-   Mehrere Aufrufe der **NEXT VALUE FOR** -Funktion denselben Sequenz-Generator in einer einzelnen Anweisung alle die gleiche verwenden muss **über** -Klauseldefinition.  
  
-   Mehrere Aufrufe der **NEXT VALUE FOR** Funktion, dass der Verweis unterschiedliche Sequenz-Generatoren in einer einzelnen Anweisung verschiedene sind können **über** -klauseldefinitionen.  
  
-   Ein **über** Klausel angewendet, um die **NEXT VALUE FOR** -Funktion nicht unterstützt die **PARTITION BY** Sub-Klausel.  
  
-   Wenn alle Aufrufe der **NEXT VALUE FOR** -Funktion in einer **wählen** -Anweisung gibt die **über** -Klausel, ein **ORDER BY** -Klausel kann verwendet werden, die **wählen** Anweisung.  
  
-   Die **über** -Klausel kann mit der **NEXT VALUE FOR** funktionieren bei Verwendung in einer **wählen** Anweisung oder `INSERT … SELECT …` Anweisung. Verwenden der **über** -Klausel mit der **NEXT VALUE FOR** Funktion ist nicht zulässig **UPDATE** oder **MERGE** Anweisungen.  
  
-   Wenn ein anderer Prozess zur gleichen Zeit auf das Sequenzobjekt zugreift, weisen die zurückgegebenen Zahlen möglicherweise Lücken auf.  
  
## <a name="metadata"></a>Metadaten  
 Weitere Informationen zu Sequenzen, Fragen Sie die [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert **UPDATE** -Berechtigung für das Sequenzobjekt oder das Schema der Sequenz. Ein Beispiel für das Gewähren der Berechtigung finden Sie weiter unten in diesem Thema in Beispiel F.  
  
### <a name="ownership-chaining"></a>Besitzverkettung  
 Sequenzobjekte unterstützen die Besitzverkettung. Wenn das Sequenzobjekt über den gleichen Besitzer wie die aufrufende gespeicherte Prozedur, der aufrufende Trigger oder die aufrufende Tabelle (mit einem Sequenzobjekt als Standardeinschränkung) verfügt, ist keine Überprüfung der Berechtigung für das Sequenzobjekt erforderlich. Wenn das Sequenzobjekt nicht im Besitz des gleichen Benutzers wie die aufrufende gespeicherte Prozedur, der aufrufende gespeicherte Trigger oder die aufrufende gespeicherte Tabelle ist, muss die Berechtigung für das Sequenzobjekt überprüft werden.  
  
 Wenn die **NEXT VALUE FOR** Funktion als Standardwert in einer Tabelle verwendet wird, Benutzer müssen beide **einfügen** Berechtigung für die Tabelle und **UPDATE** -Berechtigung für das Sequenzobjekt , zum Einfügen von Daten unter Verwendung des standardmäßigen.  
  
-   Wenn die Standardeinschränkung den gleichen Besitzer wie das Sequenzobjekt hat, sind beim Aufrufen der Standardeinschränkung keine Berechtigungen für das Sequenzobjekt erforderlich.  
  
-   Wenn die Standardeinschränkung und das Sequenzobjekt nicht dem gleichen Benutzer gehören, sind Berechtigungen für das Sequenzobjekt auch beim Aufrufen der Standardeinschränkung erforderlich.  
  
### <a name="audit"></a>Überwachung  
 So überwachen Sie die **NEXT VALUE FOR** funktionieren, indem Sie die SCHEMA_OBJECT_ACCESS_GROUP überwachen.  
  
## <a name="examples"></a>Beispiele  
 Beispiele für Sequenzen Erstellung und Verwendung der **NEXT VALUE FOR** Funktion zum Generieren von Sequenznummern finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
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
 Mithilfe der **NEXT VALUE FOR** -Funktion in der Definition einer standardeinschränkung wird unterstützt. Ein Beispiel der Verwendung von **NEXT VALUE FOR** in einem **CREATE TABLE** -Anweisung finden Sie unter Beispiel C[Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md). Im folgenden Beispiel wird `ALTER TABLE` verwendet, um eine Sequenz als Standard einer aktuellen Tabelle hinzuzufügen.  
  
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
 Im folgenden Beispiel wird die `SELECT … INTO` Anweisung zum Erstellen einer Tabelle mit dem Namen `Production.NewLocation` und verwendet die `NEXT VALUE FOR` Funktion, um jede Zeile Zahl.  
  
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
 Im folgenden Beispiel wird **UPDATE** Berechtigungen für einen Benutzer mit dem Namen `AdventureWorks\Larry` Berechtigung zum Ausführen von `NEXT VALUE FOR` mithilfe der `Test.CounterSeq` Sequenz.  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

