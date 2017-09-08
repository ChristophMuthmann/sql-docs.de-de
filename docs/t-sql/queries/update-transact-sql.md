---
title: UPDATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE_TSQL
- UPDATE
dev_langs:
- TSQL
helpviewer_keywords:
- DML [SQL Server], UPDATE statement
- data updates [SQL Server], UPDATE statement
- updating data [SQL Server]
- TOP clause, UPDATE
- OUTPUT clause
- large value data types
- data manipulation language [SQL Server], UPDATE statement
- user-defined types [SQL Server], modifying
- INSTEAD OF triggers
- modifying data [SQL Server], UPDATE statement
- data modifications [SQL Server], UPDATE statement
- large data, modifying
- .WRITE clause
- table modifications [SQL Server], UPDATE statement
- UDTs [SQL Server], modifying
- UPDATE statement [SQL Server], about UPDATE statement
- LOB data [SQL Server], modifying
- modifying LOB data
- UPDATE statement [SQL Server]
- FROM clause, UPDATE statement
- WHERE clause, UPDATE statement
ms.assetid: 40e63302-0c68-4593-af3e-6d190181fee7
caps.latest.revision: 91
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 42506702b06f57923d18e3986a29f8036d26d7eb
ms.contentlocale: de-de
ms.lasthandoff: 09/06/2017

---
# <a name="update-transact-sql"></a>UPDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert vorhandene Daten in einer Tabelle oder Sicht in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Beispiele finden Sie unter [Beispiele](#UpdateExamples).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [...n] ]  
UPDATE   
    [ TOP ( expression ) [ PERCENT ] ]   
    { { table_alias | <object> | rowset_function_limited   
         [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
      }  
      | @table_variable      
    }  
    SET  
        { column_name = { expression | DEFAULT | NULL }  
          | { udt_column_name.{ { property_name = expression  
                                | field_name = expression }  
                                | method_name ( argument [ ,...n ] )  
                              }  
          }  
          | column_name { .WRITE ( expression , @Offset , @Length ) }  
          | @variable = expression  
          | @variable = column = expression  
          | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
        } [ ,...n ]   
  
    [ <OUTPUT Clause> ]  
    [ FROM{ <table_source> } [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                  { { [ GLOBAL ] cursor_name }   
                      | cursor_variable_name   
                  }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
    | database_name .[ schema_name ] .   
    | schema_name .  
    ]  
    table_or_view_name}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

UPDATE [ database_name . [ schema_name ] . | schema_name . ] table_name   
SET { column_name = { expression | NULL } } [ ,...n ]  
[ FROM from_clause ]  
[ WHERE <search_condition> ]   
[ OPTION ( LABEL = label_name ) ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 MIT \<Common_table_expression >  
 Gibt den temporären Resultset- oder Sichtnamen an, der auch als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bezeichnet wird und innerhalb der UPDATE-Anweisung definiert ist. Das CTE-Resultset wird aus einer einfachen Abfrage abgeleitet. Die UPDATE-Anweisung verweist auf dieses Resultset.  
  
 Allgemeine Tabellenausdrücke können auch mit den Anweisungen SELECT, INSERT, DELETE und CREATE VIEW verwendet werden. Weitere Informationen finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(** *Ausdruck***)** [PERCENT]  
 Gibt die Anzahl oder den Prozentsatz der Zeilen, die aktualisiert werden. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein.  
  
 Die Zeilen, auf die im TOP-Ausdruck für die Anweisung INSERT, UPDATE oder DELETE verwiesen wird, sind nicht auf bestimmte Weise angeordnet.  
  
 Begrenzen von Klammern *Ausdruck* in TOP sind in INSERT-, Update- und DELETE-Anweisungen erforderlich. Weitere Informationen finden Sie unter [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 *table_alias*  
 Der in der FROM-Klausel angegebene Alias, der die Tabelle oder Sicht darstellt, aus der die Zeilen aktualisiert werden sollen.  
  
 *Servername*  
 Der Name des Servers (mithilfe eines Verbindungsservernamens oder der [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) -Funktion als Servername) auf dem die Tabelle oder Sicht befindet. Wenn *Server_name* angegeben wird, *Database_name* und *Schema_name* erforderlich sind.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehört.  
  
 *Table_or view_name*  
 Der Name der Tabelle oder Sicht, aus der die Zeilen aktualisiert werden sollen. Die Sicht verweist *Table_or_view_name* muss aktualisierbar sein und auf genau eine Basistabelle in der FROM-Klausel der Sicht verweisen. Weitere Informationen zu aktualisierbaren Sichten finden Sie unter [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 Handelt es sich um die [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) Funktion, je nach den Funktionen des Anbieters.  
  
 MIT **(** \<Table_Hint_Limited > **)**  
 Gibt mindestens einen Tabellenhinweis an, der für eine Zieltabelle zulässig ist. Das WITH-Schlüsselwort und die Klammern sind erforderlich. NOLOCK und READUNCOMMITTED sind nicht zulässig. Informationen zu Tabellenhinweisen finden Sie unter [Tabellenhinweise &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 @*table_variable*  
 Gibt eine [Tabelle](../../t-sql/data-types/table-transact-sql.md) -Variable als Tabellenquelle.  
  
 SET  
 Gibt die Liste der zu aktualisierenden Spalten- oder Variablennamen an.  
  
 *Spaltenname*  
 Eine Spalte mit Daten, die geändert werden sollten. *Column_name* muss vorhanden sein, *Table_or View_name*. Identitätsspalten können nicht aktualisiert werden.  
  
 *expression*  
 Eine Variable, ein Literalwert, ein Ausdruck oder eine SELECT-Anweisung als Unterabfrage in Klammern, die bzw. der einen einzelnen Wert zurückgibt. Der Rückgabewert von *Ausdruck* ersetzt den vorhandenen Wert in *Column_name* oder  *@variable* .  
  
> [!NOTE]  
>  Beim Verweisen auf die Unicode-Zeichen-Datentypen **Nchar**, **Nvarchar**, und **Ntext**, "Ausdruck" vorangestellt werden der Großbuchstabe n '. Wenn "N" nicht angegeben wird, konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Zeichenfolge in die Codepage, die der Standardsortierung der Datenbank oder Spalte entspricht. Alle Zeichen, die in der betreffenden Codepage nicht gefunden werden, gehen verloren.  
  
 DEFAULT  
 Gibt an, dass der vorhandene Wert in der Spalte durch den für die Spalte definierten Standardwert ersetzt werden soll. Damit kann auch die Spalte auf NULL geändert werden, wenn diese keinen Standard aufweist und NULL-Werte zulässt.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Verbundzuweisungsoperator:  
 +=                    Addition und Zuweisung  
 -=                     Subtraktion und Zuweisung  
 *=                     Multiplikation und Zuweisung  
 /=                      Division und Zuweisung  
 %=                    Modulo und Zuweisung  
 &=                     Bitweises AND und Zuweisung  
 ^=                     Bitweises XOR und Zuweisung  
 |=                      Bitweises OR und Zuweisung  
  
 *udt_column_name*  
 Eine benutzerdefinierte Spalte.  
  
 *Property_name* | *Feldname*  
 Member einer öffentlichen Eigenschaft oder öffentlicher Daten eines benutzerdefinierten Typs.  
  
 *keine Variablenargumentlisten verwenden* **(** *Argument* [ **,**... *n*] **)**  
 Ist eine nicht statische, öffentliche Mutatormethode von *Udt_column_name* , die ein oder mehrere Argumente annimmt.  
  
 **.** Schreiben **(***Ausdruck***,***@Offset***,** *@Length***)**  
 Gibt an, dass ein Abschnitt des Werts der *Column_name* geändert werden soll. *Ausdruck* ersetzt  *@Length*  Einheiten, beginnend  *@Offset*  von *Column_name*. Nur für Spalten vom **varchar(max)**, **nvarchar(max)**, oder **varbinary(max)** kann mit dieser Klausel angegeben werden. *Column_name* darf nicht NULL sein und darf nicht mit einem Tabellennamen oder Tabellenalias qualifiziert werden.  
  
 *Ausdruck* ist der Wert, der in kopiert *Column_name*. *Ausdruck* ausgewertet werden muss, oder werden implizit umgewandelt werden kann die *Column_name* Typ. Wenn *Ausdruck* ist auf NULL gesetzt,  *@Length*  wird ignoriert, und der Wert im *Column_name* wird abgeschnitten, an der angegebenen  *@Offset* .  
  
 *@Offset*Stellt den Startpunkt im Wert des *Column_name* an dem *Ausdruck* geschrieben wird. *@Offset*ist eine nullbasierte Ordnungsposition, **"bigint"**, und darf keine negative Zahl sein. Wenn  *@Offset*  NULL ist, hängt der Updatevorgang *Ausdruck* am Ende der vorhandenen *Column_name* Wert und  *@Length*  wird ignoriert. Wenn @Offset ist größer als die Länge der *Column_name* Wert, der [!INCLUDE[ssDE](../../includes/ssde-md.md)] gibt einen Fehler zurück. Wenn  *@Offset*  plus  *@Length*  das Ende des zugrunde liegenden Werts in der Spalte überschreitet, wird die Löschung bis zum letzten Zeichen des Werts. Wenn  *@Offset*  zuzüglich LEN (*Ausdruck*) ist größer als die zugrunde liegende deklarierte Größe, wird ein Fehler ausgelöst.  
  
 *@Length*die Länge des Abschnitts in der Spalte, beginnend mit  *@Offset* , d. h. durch ersetzt *Ausdruck*. *@Length*ist **"bigint"** und darf keine negative Zahl sein. Wenn  *@Length*  NULL ist, entfernt der Updatevorgang alle Daten aus  *@Offset*  bis zum Ende der *Column_name* Wert.  
  
 Weitere Informationen finden Sie in den Hinweisen.  
  
 **@***Variable*  
 Ist eine deklarierte Variable, die auf den Rückgabewert von festgelegt ist *Ausdruck*.  
  
 Legen Sie  **@**  *Variable* = *Spalte* = *Ausdruck* legt die Variable auf denselben fest. Wert der Spalte. Dies unterscheidet sich von SET  **@**  *Variable* = *Spalte*, *Spalte*  =  *Ausdruck*, wodurch die Variable auf den Wert vor dem Update der Spalte.  
  
 \<OUTPUT_Clause >  
 Gibt aktualisierte Daten oder Ausdrücke zurück, die darauf als Teil des UPDATE-Vorgangs basieren. Die OUTPUT-Klausel wird nicht in DML-Anweisungen unterstützt, die an Remotetabellen oder -sichten gerichtet sind. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 VON \<Table_source >  
 Gibt an, dass eine Tabelle, Sicht oder abgeleitete Tabelle als Quelle die Kriterien für den Updatevorgang bereitstellen soll. Weitere Informationen finden Sie unter [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 Wenn das Objekt, das aktualisiert wird, mit dem Objekt in der FROM-Klausel identisch ist und nur ein Verweis auf das Objekt in der FROM-Klausel vorhanden ist, kann ein Objektalias angegeben werden. Wenn das Objekt, das aktualisiert wird, mehrmals in der FROM-Klausel vorhanden ist, darf genau ein Verweis auf das Objekt keinen Tabellenalias angeben. Alle anderen Verweise auf das Objekt in der FROM-Klausel müssen einen Objektalias aufweisen.  
  
 Eine Sicht mit einem INSTEAD OF UPDATE-Trigger kann nicht Ziel für eine UPDATE-Anweisung mit einer FROM-Klausel sein.  
  
> [!NOTE]  
>  Jeder Aufruf von OPENDATASOURCE, OPENQUERY oder OPENROWSET in der FROM-Klausel wird einzeln und unabhängig von anderen Aufrufen dieser Funktionen ausgewertet, die als Ziel des Updates verwendet werden, auch wenn für die beiden Aufrufe identische Argumente angegeben werden. Insbesondere haben Filter- oder Joinbedingungen, die auf das Ergebnis eines dieser Aufrufe angewendet werden, keine Auswirkungen auf die Ergebnisse des jeweils anderen.  
  
 WHERE  
 Gibt die Bedingungen an, mit denen die zu aktualisierenden Zeilen eingegrenzt werden. Es gibt zwei Arten von Updates, die vom verwendeten WHERE-Klauseltyp abhängen:  
  
-   Gesuchte Updates legen eine Suchbedingung fest, der die zu löschenden Zeilen entsprechen müssen.  
  
-   Positionierte Updates verwenden die CURRENT OF-Klausel, um einen Cursor anzugeben. Der Updatevorgang wird an der aktuellen Position des Cursors ausgeführt.  
  
\<Search_condition >  
 Bezeichnet die Bedingung, die erfüllt sein muss, damit die Zeilen aktualisiert werden. Die Suchbedingung kann auch die Bedingung sein, auf der ein Join basiert. Es gibt keinen Höchstwert hinsichtlich der Anzahl von Prädikaten in einer Suchbedingung. Weitere Informationen zu Prädikaten und suchbedingungen finden Sie unter [Suchbedingung &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
CURRENT OF  
 Gibt an, dass das Update an der aktuellen Position des angegebenen Cursors ausgeführt wird.  
  
 Ein positioniertes Update, das eine WHERE CURRENT OF-Klausel verwendet, aktualisiert die Einzelzeile an der aktuellen Cursorposition. Dies kann genauer sein als ein gesuchtes Update, das eine WHERE verwendet \<Search_condition >-Klausel, um die zu aktualisierenden Zeilen zu kennzeichnen. Mit einem gesuchten Update werden mehrere Zeilen geändert, wenn eine einzelne Zeile durch die Suchbedingung nicht eindeutig identifiziert wird.  
  
GLOBAL  
 Gibt an, dass *Cursor_name* auf einen globalen Cursor verweist.  
  
*Cursorname*  
 Der Name des geöffneten Cursors, von dem der Abruf erfolgen soll. Wenn sowohl ein globaler als auch ein lokaler Cursor mit dem Namen *Cursor_name* vorhanden ist, dieses Argument bezieht sich auf den globalen Cursor, wenn GLOBAL angegeben; andernfalls ist, bezieht sich auf den lokalen Cursor. Der Cursor muss Updates zulassen.  
  
*cursor_variable_name*  
 Ist der Name einer Cursorvariablen. *Cursor_variable_name* muss auf einen Cursor, der Updates zulässt verweisen.  
  
OPTION **(** \<Query_hint > [ **,**... *n* ] **)**  
 Gibt an, dass mithilfe von Optimierungshinweisen angepasst wird, wie die Anweisung von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verarbeitet wird. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Verwenden der @@ROWCOUNT Funktion zum Zurückgeben der Anzahl der eingefügten Zeilen an die Clientanwendung. Weitere Informationen finden Sie unter [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
 Variablennamen können in UPDATE-Anweisungen verwendet werden, um die betroffenen alten und neuen Werte anzuzeigen. Diese Vorgehensweise sollte aber nur angewendet werden, wenn die UPDATE-Anweisung einen einzelnen Datensatz betrifft. Wenn die UPDATE-Anweisung mehrere Datensätze, um die alten und neuen Werte für die einzelnen Datensätze zurückzugeben betroffen sind, verwenden die [OUTPUT-Klausel](../../t-sql/queries/output-clause-transact-sql.md).  
  
 Gehen Sie beim Angeben der FROM-Klausel zum Bereitstellen der Kriterien für den Updatevorgang vorsichtig vor. Das Ergebnis einer UPDATE-Anweisung ist nicht definiert, wenn sie nicht deterministisch ist. Dies ist der Fall, wenn die UPDATE-Anweisung eine FROM-Klausel enthält, in der nicht für jedes Vorkommen einer zu aktualisierenden Spalte genau ein Wert verfügbar ist. Beispielsweise erfüllen im folgenden Skript der UPDATE-Anweisung beide Zeilen der `Table1`-Tabelle die Bedingungen der FROM-Klausel in der UPDATE-Anweisung. Es ist jedoch nicht definiert, welche Zeile von `Table1` zum Aktualisieren der Zeile in `Table2.` verwendet wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  
UPDATE dbo.Table2   
SET dbo.Table2.ColB = dbo.Table2.ColB + dbo.Table1.ColB  
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA);  
GO  
SELECT ColA, ColB   
FROM dbo.Table2;  
```  
  
 Dasselbe Problem kann auftreten, wenn die Klauseln FROM und WHERE CURRENT OF kombiniert werden. Im folgenden Beispiel erfüllen beide Zeilen der `Table2`-Tabelle die Bedingungen der `FROM`-Klausel in der `UPDATE`-Anweisung. Es ist jedoch nicht definiert, welche Zeile aus `Table2` zum Aktualisieren der Zeile in `Table1` verwendet wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1  
    (c1 int PRIMARY KEY NOT NULL, c2 int NOT NULL);  
GO  
CREATE TABLE dbo.Table2  
    (d1 int PRIMARY KEY NOT NULL, d2 int NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES (1, 10);  
INSERT INTO dbo.Table2 VALUES (1, 20), (2, 30);  
GO  
DECLARE abc CURSOR LOCAL FOR  
    SELECT c1, c2   
    FROM dbo.Table1;  
OPEN abc;  
FETCH abc;  
UPDATE dbo.Table1   
SET c2 = c2 + d2   
FROM dbo.Table2   
WHERE CURRENT OF abc;  
GO  
SELECT c1, c2 FROM dbo.Table1;  
GO  
```  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Die Unterstützung für die Verwendung der READUNCOMMITTED- und NOLOCK-Hinweise in der FROM-Klausel, die sich auf die Zieltabelle einer UPDATE- oder DELETE-Anweisung beziehen, wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Vermeiden Sie die Verwendung dieser Hinweise in diesem Kontext beim Entwickeln neuer Anwendungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden.  
  
## <a name="data-types"></a>Datentypen  
 Alle **Char** und **Nchar** Spalten werden rechts auf die definierte Länge aufgefüllt.  
  
 Wenn ANSI_PADDING auf OFF festgelegt ist, werden alle nachfolgende Leerzeichen aus Daten eingefügt entfernt **Varchar** und **Nvarchar** Spalten gilt nicht für Zeichenfolgen, die nur aus Leerzeichen bestehen. Diese Zeichenfolgen werden auf eine leere Zeichenfolge abgeschnitten. Wenn ANSI_PADDING auf ON festgelegt ist, werden nachfolgende Leerzeichen eingefügt. Der Microsoft SQL Server-ODBC-Treiber und der OLE DB-Provider für SQL Server stellen beim Herstellen einer Verbindung SET ANSI_PADDING automatisch auf ON ein. Diese Einstellung kann in ODBC-Datenquellen oder durch Festlegen von Verbindungsattributen oder Verbindungseigenschaften konfiguriert werden. Weitere Informationen finden Sie unter [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
### <a name="updating-text-ntext-and-image-columns"></a>Aktualisieren der Spalten "text", "ntext" und "image"  
 Ändern einer **Text**, **Ntext**, oder **Image** Spalte mit UPDATE die Spalte initialisiert, einen gültiger Textzeiger zugewiesen und mindestens eine Datenseite zuordnet, es sei denn, die Spalte wird mit NULL aktualisiert.  
  
 Ersetzen oder ändern umfangreicher Blöcke **Text**, **Ntext**, oder **Image** Daten verwenden, die [WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) oder [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) statt der UPDATE-Anweisung.  
  
 Wenn die UPDATE-Anweisung mehr als eine Zeile, beim Aktualisieren der Gruppierungsschlüssel und einen oder mehrere ändern konnte **Text**, **Ntext**, oder **Image** Spalten hat, wird das Teilupdate Diese Spalten als vollständige Ersetzung dieser Werte ausgeführt wird.  
  
> [!IMPORTANT]  
>  Die **Ntext**, **Text**, und **Image** Datentypen werden in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung dieser Datentypen bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden. Verwenden Sie stattdessen [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)und [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) .  
  
### <a name="updating-large-value-data-types"></a>Aktualisieren von Datentypen mit umfangreichen Werten  
 Verwenden der **.** Schreiben (*Ausdruck***,**  *@Offset*  **,***@Length*)-Klausel Ausführen ein teilweisen oder vollständigen Updates der **varchar(max)**, **nvarchar(max)**, und **varbinary(max)** Datentypen. Z. B. ein teilweises Update von einer **varchar(max)** Spalte möglicherweise löschen oder ändern Sie nur die ersten 200 Zeichen der Spalte, während ein vollständiges Update würde löschen oder ändern alle Daten in der Spalte. **.** Schreiben von Updates, die neue Daten eingefügt oder angefügt werden minimal protokolliert, wenn das Wiederherstellungsmodell der Datenbank auf Massenprotokolliert oder einfach festgelegt ist. Die minimale Protokollierung wird nicht verwendet, wenn vorhandene Werte aktualisiert werden. Weitere Informationen finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] konvertiert ein teilweises Update in ein vollständiges Update, wenn die UPDATE-Anweisung eine dieser Aktionen bewirkt:  
-   Ändert eine Schlüsselspalte der partitionierten Sicht oder Tabelle.  
-   Ändert mehr als eine Zeile und aktualisiert außerdem den Schlüssel eines nicht eindeutigen gruppierten Index in einen nicht konstanten Wert.  
  
Sie können keine der **.** WRITE-Klausel zum Aktualisieren einer NULL-Spalte, oder legen Sie den Wert der *Column_name* auf NULL.  
  
*@Offset*und  *@Length*  angegeben sind, in Byte für **Varbinary** und **Varchar** Datentypen und in Zeichen für die **Nvarchar**-Datentyp. Die geeigneten Offsets werden für Doppelbyte-Zeichensatzsortierungen (DBCS, Double-Byte Character Set) berechnet.  
  
Es wird empfohlen, Daten in Blockgrößen einzufügen bzw. zu aktualisieren, die ein Vielfaches von 8.040 Byte sind, um eine optimale Leistung zu erzielen.  
  
Wenn die geänderte Spalte durch die **.** Schreiben Sie die Klausel in einer OUTPUT-Klausel der vollständige Wert der Spalte verwiesen wird entweder das anfangsimage in **gelöscht.** *Column_name* oder das endimage in **eingefügt.** *Column_name*, an die angegebene Spalte in der Tabellenvariablen zurückgegeben. Finden Sie unter folgenden Beispiel R.  
  
Um dieselbe Funktionalität von zu erreichen **.** Mit anderen Zeichen- oder Binärdatentypen zu schreiben, verwenden Sie die [haben Zugriff auf Inhalte &#40; Transact-SQL &#41; ](../../t-sql/functions/stuff-transact-sql.md).  
  
### <a name="updating-user-defined-type-columns"></a>Aktualisieren von Spalten mit benutzerdefiniertem Datentyp  
 Sie können Werte in benutzerdefinierten Spalten auf eine der folgenden Arten aktualisieren:  
  
-   Bereitstellen eines Werts eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyps, sofern der benutzerdefinierte Typ implizite oder explizite Konvertierung von diesem Typ unterstützt. Im folgenden Beispiel wird gezeigt, wie Sie einen Wert in einer Spalte des benutzerdefinierten Typs `Point` durch explizites Konvertieren aus einer Zeichenfolge aktualisieren.  
  
    ```sql  
    UPDATE Cities  
    SET Location = CONVERT(Point, '12.3:46.2')  
    WHERE Name = 'Anchorage';  
    ```  
  
-   Aufrufen einer als Mutator markierten Methode des benutzerdefinierten Typs, um das Update auszuführen. Im folgenden Beispiel wird eine Mutatormethode des Typs `Point` namens `SetXY` aufgerufen. Dadurch wird der Status der Instanz des Typs aktualisiert.  
  
    ```sql  
    UPDATE Cities  
    SET Location.SetXY(23.5, 23.5)  
    WHERE Name = 'Anchorage';  
    ```  
  
    > [!NOTE]  
    >  Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein Fehler zurückgegeben, wenn eine mutator-Methode für einen NULL-Wert von [!INCLUDE[tsql](../../includes/tsql-md.md)] aufgerufen wird oder wenn ein neuer von einer mutator-Methode generierter Wert NULL ist.  
  
-   Ändern des Werts eines Members einer öffentlichen Eigenschaft oder öffentlicher Daten des benutzerdefinierten Typs. Der Ausdruck, der den Wert bereitstellt, muss implizit in den Typ der Eigenschaft konvertierbar sein. Im folgenden Beispiel wird der Wert der `X`-Eigenschaft des benutzerdefinierten Typs `Point` geändert.  
  
    ```sql  
    UPDATE Cities  
    SET Location.X = 23.5  
    WHERE Name = 'Anchorage';  
    ```  
  
     Wenn Sie verschiedene Eigenschaften einer Spalte des gleichen benutzerdefinierten Typs ändern möchten, geben Sie mehrere UPDATE-Anweisungen aus, oder rufen Sie eine Mutatormethode des Typs auf.  
  
### <a name="updating-filestream-data"></a>Aktualisieren von FILESTREAM-Daten  
 Sie können ein FILESTREAM-Feld mithilfe der UPDATE-Anweisung auf einen NULL-Wert, einen leeren Wert oder eine relativ kleine Menge von Inlinedaten aktualisieren. Große Datenmengen lassen sich jedoch mithilfe von Win32-Schnittstellen effizienter in eine Datei streamen. Wenn Sie ein FILESTREAM-Feld aktualisieren, ändern Sie die zugrunde liegenden BLOB-Daten im Dateisystem. Wenn ein FILESTREAM-Feld auf NULL festgelegt wird, werden die dem Feld zugeordneten BLOB-Daten gelöscht. Sie können keine. Write() zum Ausführen von teilupdates an FILESTREAM-Daten. Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn das Update einer Zeile eine Einschränkung oder Regel oder die NULL-Einstellung für die Spalte verletzt bzw. der neue Wert einen inkompatiblen Datentyp hat, wird die Anweisung abgebrochen. Außerdem wird ein Fehler zurückgegeben, und es werden keine Datensätze aktualisiert.  
  
 Wenn in einer UPDATE-Anweisung ein arithmetischer Fehler (Überlauf, Division durch Null oder Definitionsbereichsfehler/Domänenfehler) bei der Auswertung eines Ausdrucks auftritt, wird das Update nicht ausgeführt. Der Rest des Batches wird nicht ausgeführt, und eine Fehlermeldung wird zurückgegeben.  
  
 Wenn das Update mindestens einer Spalte eines gruppierten Index dazu führt, dass die Größe des gruppierten Index und der Zeile den Wert von 8.060 Byte überschreitet, tritt beim Update ein Fehler auf, und es wird eine Fehlermeldung zurückgegeben.  
  
## <a name="interoperability"></a>Interoperabilität  
 UPDATE-Anweisungen sind im Textkörper von benutzerdefinierten Funktionen nur zulässig, wenn es sich bei der Tabelle, die geändert wird, um eine Tabellenvariable handelt.  
  
 Wenn ein INSTEAD-OF-Trigger für UPDATE-Aktionen für eine Tabelle definiert ist, wird der Trigger statt der UPDATE-Anweisung ausgeführt. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen nur AFTER-Trigger für UPDATE-Anweisungen und andere Anweisungen zur Datenänderung. Die FROM-Klausel kann nicht in einer UPDATE-Anweisung angegeben werden, die (direkt oder indirekt) auf eine Sicht verweist, für die ein INSTEAD OF-Trigger definiert wurde. Weitere Informationen zu INSTEAD OF-Trigger finden Sie unter [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die FROM-Klausel kann nicht in einer UPDATE-Anweisung angegeben werden, die, entweder direkt oder indirekt auf eine Sicht verweist, die einen INSTEAD OF-Trigger definiert wurde. Weitere Informationen zu INSTEAD OF-Trigger finden Sie unter [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 Wenn ein allgemeiner Tabellenausdruck (CTE) das Ziel einer UPDATE-Anweisung ist, müssen alle Verweise auf den allgemeinen Tabellenausdruck in der Anweisung übereinstimmen. Wenn dem allgemeinen Tabellenausdruck z. B. ein Alias in der FROM-Klausel zugewiesen wird, muss der Alias für alle weiteren Verweise auf den allgemeinen Tabellenausdruck verwendet werden. Eindeutige Verweise auf allgemeine Tabellenausdrücke sind erforderlich, da ein allgemeiner Tabellenausdruck keine Objekt-ID hat, mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die implizite Beziehung zwischen einem Objekt und seinem Alias erkennt. Ohne diese Beziehung erzeugt der Abfrageplan möglicherweise ein unerwartetes Joinverhalten und unbeabsichtigte Abfrageergebnisse. In den folgenden Beispielen werden richtige und falsche Methoden zum Angeben eines allgemeinen Tabellenausdrucks veranschaulicht, wenn der allgemeine Tabellenausdruck das Zielobjekt des Updatevorgangs ist.  
  
```sql  
USE tempdb;  
GO  
-- UPDATE statement with CTE references that are correctly matched.  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE x -- cte is referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;  
SELECT * FROM @x;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ID     Value  
 ------ -----  
 1      100  
 2      200  
 (2 row(s) affected)  
```  

UPDATE-Anweisung mit CTE-verweisen, die falsch abgeglichen werden.  
```sql  
USE tempdb;  
GO  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE cte   -- cte is not referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;   
SELECT * FROM @x;   
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Value  
------ -----  
1      100  
2      100  
(2 row(s) affected)  
```  

## <a name="locking-behavior"></a>Sperrverhalten  
 Eine UPDATE-Anweisung ruft immer eine exklusive (X) Sperre für die von ihr geänderte Tabelle ab und hält diese Sperre bis zum Abschluss der Transaktion aufrecht. Bei einer exklusiven Sperre können keine anderen Transaktionen Daten ändern. Sie können Tabellenhinweise angeben, um dieses Standardverhalten für die Dauer der UPDATE-Anweisung zu überschreiben, indem Sie eine andere Sperrmethode angeben. Es wird jedoch empfohlen, dass Hinweise nur von erfahrenen Entwicklern und Datenbankadministratoren und nur als letzte Möglichkeit verwendet werden. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="logging-behavior"></a>Protokollierungsverhalten  
 Die UPDATE-Anweisung wird protokolliert; Allerdings teilaktualisierungen von Datentypen mit umfangreichen Werten die **.** Schreiben Sie die Klausel werden minimal protokolliert. Weitere Informationen finden Sie im vorherigen Abschnitt "Datentypen" unter "Aktualisieren von Datentypen mit umfangreichen Werten".  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Für die Zieltabelle sind UPDATE-Berechtigungen erforderlich. SELECT-Berechtigungen müssen auch für die Tabelle aktualisiert werden, wenn die UPDATE-Anweisung eine WHERE-Klausel enthält, oder wenn *Ausdruck* in der SET-Klausel eine Spalte in der Tabelle verwendet.  
  
 Aktualisieren Sie Berechtigungen erhalten standardmäßig Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** und **Db_datawriter** festen Datenbankrollen und der Besitzer der Tabelle. Mitglieder der **Sysadmin**, **Db_owner**, und **Db_securityadmin** Rollen sowie der Tabellenbesitzer können Berechtigungen an andere Benutzer übertragen.  
  
##  <a name="UpdateExamples"></a> Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Grundlegende Syntax](#BasicSyntax)|UPDATE|  
|[Beschränken der Zeilen, die aktualisiert werden](#LimitingValues)|WHERE • TOP • WITH common table expression • WHERE CURRENT OF|  
|[Festlegen von Spaltenwerten](#ColumnValues)|Berechnete Werte • Verbundoperatoren • Standardwerte • Unterabfragen|  
|[Angeben von Zielobjekten keine Standardtabellen sind](#TargetObjects)|Sichten • Tabellenvariablen • Tabellenaliase|  
|[Aktualisieren von Daten basierend auf Daten aus anderen Tabellen](#OtherTables)|FROM|  
|[Aktualisieren von Zeilen in einer Remotetabelle](#RemoteTables)|Verbindungsserver • OPENQUERY • OPENDATASOURCE|  
|[Aktualisieren von LOB-Datentypen](#LOBValues)|. • OPENROWSET SCHREIBEN|  
|[Aktualisieren von benutzerdefinierten Typen](#UDTs)|Benutzerdefinierte Typen|  
|[Überschreiben das Standardverhalten des Abfrageoptimierers mithilfe von Hinweisen](#TableHints)|Tabellenhinweise • Abfragehinweise|  
|[Erfassen der Ergebnisse der UPDATE-Anweisung](#CaptureResults)|OUTPUT-Klausel|  
|[Verwenden von UPDATE in anderen Anweisungen](#Other)|Gespeicherte Prozeduren • TRY…CATCH|  
  
###  <a name="BasicSyntax"></a>Grundlegende Syntax  
 Anhand von Beispielen in diesem Abschnitt wird die grundlegende Funktion der UPDATE-Anweisung mithilfe der mindestens erforderlichen Syntax veranschaulicht.  
  
#### <a name="a-using-a-simple-update-statement"></a>A. Verwenden einer einfachen UPDATE-Anweisung  
 Im folgenden Beispiel wird eine einzelne Spalte für alle Zeilen in der `Person.Address`-Tabelle aktualisiert.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.Address  
SET ModifiedDate = GETDATE();  
```  
  
#### <a name="b-updating-multiple-columns"></a>B. Aktualisieren mehrerer Spalten  
 Im folgenden Beispiel werden die Werte in den Spalten `Bonus`, `CommissionPct` und `SalesQuota` für alle Zeilen in der `SalesPerson`-Tabelle aktualisiert.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET Bonus = 6000, CommissionPct = .10, SalesQuota = NULL;  
GO  
```  
  
###  <a name="LimitingValues"></a>Beschränken der Zeilen, die aktualisiert werden  
 Die Beispiele in diesem Abschnitt veranschaulichen Methoden, mit denen die Anzahl der von der UPDATE-Anweisung betroffenen Zeilen eingegrenzt werden kann.  
  
#### <a name="c-using-the-where-clause"></a>C. Verwenden der WHERE-Klausel  
 Im folgenden Beispiel wird die WHERE-Klausel verwendet, um die zu aktualisierenden Zeilen anzugeben. Die Anweisung aktualisiert den Wert in der Spalte `Color` der Tabelle `Production.Product` für alle Zeilen, die in der Spalte `Color` den vorhandenen Wert "Red" aufweisen und einen Wert in der Spalte `Name` aufweisen, der mit "Road-250" beginnt.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
SET Color = N'Metallic Red'  
WHERE Name LIKE N'Road-250%' AND Color = N'Red';  
GO  
```  
  
#### <a name="d-using-the-top-clause"></a>D. Verwenden der TOP-Klausel  
 In den folgenden Beispielen wird mithilfe der TOP-Klausel die Anzahl der Zeilen beschränkt, die in einer UPDATE-Anweisung geändert werden. Wenn eine TOP (*n*)-Klausel mit UPDATE verwendet wird, erfolgt des Update-Vorgangs auf eine zufällige Auswahl von "*n*" Anzahl der Zeilen. Im folgenden Beispiel wird die `VacationHours`-Spalte um 25 Prozent für 10 zufällige Zeilen in der `Employee`-Tabelle aktualisiert.  
  
```sql  
USE AdventureWorks2012;
GO
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;
GO  
```  
  
 Wenn Sie TOP verwenden müssen, um Updates in einer sinnvollen Abfolge anzuwenden, müssen Sie zusammen mit ORDER BY in einer untergeordneten SELECT-Anweisung verwenden. Mit dem nachfolgenden Beispiel werden die Urlaubsstunden der 10 Mitarbeiter mit dem frühesten Einstellungsdatum aktualisiert.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
#### <a name="e-using-the-with-commontableexpression-clause"></a>E. Verwenden der WITH common_table_expression-Klausel  
 Im folgenden Beispiel wird der `PerAssemnblyQty`-Wert für alle Teile und Komponenten aktualisiert, die direkt oder indirekt zum Erstellen der `ProductAssemblyID 800` verwendet werden. Der allgemeine Tabellenausdruck gibt eine hierarchische Liste mit Teilen, die verwendet werden, direkt zum Erstellen `ProductAssemblyID 800` und Teile, die zum Erstellen dieser Komponenten usw. verwendet werden. Nur die Zeilen, die vom allgemeinen Tabellenausdruck zurückgegeben werden, werden geändert.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
#### <a name="f-using-the-where-current-of-clause"></a>F. Verwenden der WHERE CURRENT OF-Klausel  
 Im folgenden Beispiel wird die WHERE CURRENT OF-Klausel verwendet, um nur die Zeile zu aktualisieren, auf der der Cursor positioniert ist. Wenn ein Cursor auf einem Join basiert, wird nur die Tabelle geändert, die mit `table_name` in der UPDATE-Anweisung angegeben wurde. Andere im Cursor enthaltene Tabellen sind davon nicht betroffen.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
UPDATE HumanResources.EmployeePayHistory  
SET PayFrequency = 2   
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
###  <a name="ColumnValues"></a>Festlegen von Spaltenwerten  
 Die Beispiele in diesem Abschnitt veranschaulichen das Update von Spalten mithilfe von berechneten Werten, Unterabfragen und DEFAULT-Werten.  
  
#### <a name="g-specifying-a-computed-value"></a>G. Angeben eines berechneten Werts  
 In den folgenden Beispielen werden berechnete Werte in einer UPDATE-Anweisung verwendet. In diesem Beispiel wird der Wert in der `ListPrice`-Spalte für alle Zeilen in der `Product`-Tabelle verdoppelt.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
UPDATE Production.Product  
SET ListPrice = ListPrice * 2;  
GO  
```  
  
#### <a name="h-specifying-a-compound-operator"></a>H. Angeben eines Verbundoperators  
 Im folgenden Beispiel wird die `@NewPrice`-Variable verwendet, um den Preis aller roten Fahrräder zu erhöhen, indem zum aktuellen Preis der Wert 10 addiert wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @NewPrice int = 10;  
UPDATE Production.Product  
SET ListPrice += @NewPrice  
WHERE Color = N'Red';  
GO  
```  
  
 Im folgenden Beispiel werden mithilfe des Verbundoperators += die `' - tool malfunction'`-Daten an den vorhandenen Wert in der Spalte `Name` für Zeilen mit einer `ScrapReasonID` zwischen 10 und 12 angefügt.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ScrapReason   
SET Name += ' - tool malfunction'  
WHERE ScrapReasonID BETWEEN 10 and 12;  
```  
  
#### <a name="i-specifying-a-subquery-in-the-set-clause"></a>I. Angeben einer Unterabfrage in der SET-Klausel  
 Im folgenden Beispiel wird mit einer Unterabfrage in der SET-Klausel der Wert bestimmt, der zum Aktualisieren der Spalte verwendet wird. Die Unterabfrage muss nur einen Skalarwert (d. h. einen einzelnen Wert pro Zeile) zurückgeben. In diesem Beispiel wird die Spalte `SalesYTD` in der `SalesPerson`-Tabelle geändert, um die neuesten Verkaufszahlen in der `SalesOrderHeader`-Tabelle wiederzugeben. Die Unterabfrage aggregiert die Umsätze für jeden Vertriebsmitarbeiter in der `UPDATE`-Anweisung.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
#### <a name="j-updating-rows-using-default-values"></a>J. Aktualisieren von Zeilen mit DEFAULT-Werten  
 Im folgenden Beispiel wird die Spalte `CostRate` auf den Standardwert (0.00) für alle Zeilen festgelegt, die über einen `CostRate`-Wert größer als `20.00` verfügen.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Location  
SET CostRate = DEFAULT  
WHERE CostRate > 20.00;  
```  
  
###  <a name="TargetObjects"></a>Angeben von Zielobjekten keine Standardtabellen sind  
 In den Beispielen in diesem Abschnitt wird veranschaulicht, wie Zeilen durch Angeben einer Sicht, eines Tabellenalias oder einer Tabellenvariablen aktualisiert werden.  
  
#### <a name="k-specifying-a-view-as-the-target-object"></a>K. Angeben einer Sicht als Zielobjekt  
 Im folgenden Beispiel werden Zeilen in einer Tabelle aktualisiert, indem eine Sicht als Zielobjekt angegeben wird. Die Sichtdefinition verweist auf mehrere Tabellen, die UPDATE-Anweisung wird jedoch erfolgreich ausgeführt, da sie auf Spalten nur von einer der zugrunde liegenden Tabellen verweist. Die UPDATE-Anweisung würde fehlschlagen, wenn Spalten von beiden Tabellen angegeben wären. Weitere Informationen finden Sie unter [Ändern von Daten über eine Sicht](../../relational-databases/views/modify-data-through-a-view.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.vStateProvinceCountryRegion  
SET CountryRegionName = 'United States of America'  
WHERE CountryRegionName = 'United States';  
```  
  
#### <a name="l-specifying-a-table-alias-as-the-target-object"></a>L. Angeben eines Tabellenalias als Zielobjekt  
 Im folgenden Beispiel werden Zeilen in der Tabelle `Production.ScrapReason` aktualisiert. Der `ScrapReason` in der FROM-Klausel zugewiesene Tabellenalias wird als Zielobjekt in der UPDATE-Klausel angegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE sr  
SET sr.Name += ' - tool malfunction'  
FROM Production.ScrapReason AS sr  
JOIN Production.WorkOrder AS wo   
     ON sr.ScrapReasonID = wo.ScrapReasonID  
     AND wo.ScrappedQty > 300;  
```  
  
#### <a name="m-specifying-a-table-variable-as-the-target-object"></a>M. Angeben einer Tabellenvariablen als Zielobjekt  
 Im folgenden Beispiel werden Zeilen in einer Tabellenvariablen aktualisiert.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
-- Populate the table variable with employee ID values from HumanResources.Employee.  
INSERT INTO @MyTableVar (EmpID)  
    SELECT BusinessEntityID FROM HumanResources.Employee;  
  
-- Update columns in the table variable.  
UPDATE @MyTableVar  
SET NewVacationHours = e.VacationHours + 20,  
    ModifiedDate = GETDATE()  
FROM HumanResources.Employee AS e   
WHERE e.BusinessEntityID = EmpID;  
  
-- Display the results of the UPDATE statement.  
SELECT EmpID, NewVacationHours, ModifiedDate FROM @MyTableVar  
ORDER BY EmpID;  
GO  
```  
  
###  <a name="OtherTables"></a>Aktualisieren von Daten basierend auf Daten aus anderen Tabellen  
 Anhand von Beispielen in diesem Abschnitt werden Methoden zum Aktualisieren von Zeilen auf Grundlage von Informationen in einer anderen Tabelle gezeigt.  
  
#### <a name="n-using-the-update-statement-with-information-from-another-table"></a>N. Verwenden der UPDATE-Anweisung mit Informationen aus einer anderen Tabelle  
 Im folgenden Beispiel wird die `SalesYTD` in der `SalesPerson`-Tabelle geändert, um die neuesten Verkaufszahlen in der `SalesOrderHeader`-Tabelle wiederzugeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD + SubTotal  
FROM Sales.SalesPerson AS sp  
JOIN Sales.SalesOrderHeader AS so  
    ON sp.BusinessEntityID = so.SalesPersonID  
    AND so.OrderDate = (SELECT MAX(OrderDate)  
                        FROM Sales.SalesOrderHeader  
                        WHERE SalesPersonID = sp.BusinessEntityID);  
GO  
```  
  
 Im vorherigen Beispiel wird angenommen, dass nur ein Verkauf für einen angegebenen Verkäufer an einem bestimmten Datum aufgezeichnet wird und Updates aktuell sind. Wenn mehr als ein Verkauf für einen angegebenen Verkäufer am selben Tag gespeichert werden kann, funktioniert das gezeigte Beispiel nicht richtig. Das Beispiel ausgeführt wird, ohne Fehler, aber jeder `SalesYTD` Wert wird mit nur einem Verkauf, unabhängig davon, wie viele Verkäufe an diesem Tag tatsächlich stattgefunden aktualisiert. Die Ursache ist darin zu suchen, dass eine einzelne UPDATE-Anweisung dieselbe Zeile nicht zweimal ändern kann.  
  
 Wenn für einen angegebenen Vertriebsmitarbeiter mehrere Verkäufe pro Tag möglich sind, müssen sämtliche Verkäufe der einzelnen Vertriebsmitarbeiter mithilfe der `UPDATE`-Anweisung aggregiert werden, wie im nachfolgenden Beispiel dargestellt:  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
###  <a name="RemoteTables"></a>Aktualisieren von Zeilen in einer Remotetabelle  
 Beispiele in diesem Abschnitt veranschaulichen, wie Aktualisieren von Zeilen in einer remotezieltabelle mit einem [Verbindungsserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) oder ein [Rowsetfunktion](../../t-sql/functions/rowset-functions-transact-sql.md) auf die Remotetabelle zu verweisen.  
  
#### <a name="o-updating-data-in-a-remote-table-by-using-a-linked-server"></a>O. Aktualisieren von Daten in einer Remotetabelle mithilfe eines Verbindungsservers  
 Im folgenden Beispiel wird eine Tabelle auf einem Remoteserver aktualisiert. Im Beispiel wird zuerst erstellen einen Link zur Remotedatenquelle mithilfe [Sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Der Name des Verbindungsservers (`MyLinkServer`) wird anschließend als Teil des vierteiligen Objektnamens in der Form server.catalog.schema.object angegeben. Beachten Sie, dass Sie einen gültigen Servernamen für `@datasrc` angeben müssen.  
  
```sql  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI10',   
    @datasrc = N'<server name>',  
    @catalog = N'AdventureWorks2012';  
GO  
USE AdventureWorks2012;  
GO  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
UPDATE MyLinkServer.AdventureWorks2012.HumanResources.Department  
SET GroupName = N'Public Relations'  
WHERE DepartmentID = 4;  
```  
  
#### <a name="p-updating-data-in-a-remote-table-by-using-the-openquery-function"></a>P. Aktualisieren von Daten in einer Remotetabelle mithilfe der OPENQUERY-Funktion  
 Im folgende Beispiel wird eine Zeile in einer Remotetabelle aktualisiert, durch Angeben der [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) Rowset-Funktion. Der im vorherigen Beispiel erstellte Name des Verbindungsservers wird hier verwendet.  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
#### <a name="q-updating-data-in-a-remote-table-by-using-the-opendatasource-function"></a>Q. Aktualisieren von Daten in einer Remotetabelle mithilfe der OPENDATASOURCE-Funktion  
 Das folgende Beispiel fügt eine Zeile in eine Remotetabelle durch Angabe der [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) Rowset-Funktion. Geben Sie einen gültigen Servernamen für die Datenquelle mithilfe des Formats *Server_name* oder *Server_name\instance_name*. Sie müssen möglicherweise die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für "Ad Hoc Distributed Queries" konfigurieren. Weitere Informationen finden Sie unter [ad hoc distributed Queries (Serverkonfigurationsoption)](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
###  <a name="LOBValues"></a>Aktualisieren von LOB-Datentypen  
 Anhand von Beispielen in diesem Abschnitt werden Methoden zum Aktualisieren von Werten in Spalten gezeigt, die mit LOB-Datentypen (Large Object) definiert sind.  
  
#### <a name="r-using-update-with-write-to-modify-data-in-an-nvarcharmax-column"></a>R. Verwenden von UPDATE mit .WRITE zum Ändern von Daten in einer nvarchar(max)-Spalte  
 Im folgenden Beispiel wird die. WRITE-Klausel, um einen Teilwert in aktualisieren `DocumentSummary`, wird ein **nvarchar(max)** Spalte in der `Production.Document` Tabelle. Das Wort `components` wird durch das Wort `features` ersetzt. Dazu werden das Ersetzungswort, die Anfangsposition (Offset) des zu ersetzenden Worts in den vorhandenen Daten und die Anzahl von zu ersetzenden Zeichen (Länge) angegeben. Im Beispiel wird auch die OUTPUT-Klausel zurückzugebenden die Anfangs- und endimages der der `DocumentSummary` Spalte die `@MyTableVar` Variable für Tabellenname.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
```  
  
#### <a name="s-using-update-with-write-to-add-and-remove-data-in-an-nvarcharmax-column"></a>S. Verwenden von UPDATE mit .WRITE zum Hinzufügen und Entfernen von Daten in einer nvarchar(max)-Spalte  
 In den folgenden Beispielen hinzufügen und Entfernen von Daten aus einer **nvarchar(max)** Spalte, die einen Wert, der zurzeit auf NULL festgelegt wurde. Da die. WRITE-Klausel kann nicht zum Ändern einer NULL-Spalte verwendet werden, die Spalte zuerst mit temporären Daten aufgefüllt. Anschließend werden diese Daten mithilfe der .WRITE-Klausel durch die richtigen Daten ersetzt. In den zusätzlichen Beispielen werden am Ende des Spaltenwerts Daten angefügt, Daten (durch Abschneiden) aus der Spalte entfernt und schließlich Teildaten aus der Spalte entfernt. Die SELECT-Anweisungen zeigen die Datenänderung an, die von jeder UPDATE-Anweisung generiert wurde.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Replacing NULL value with temporary data.  
UPDATE Production.Document  
SET DocumentSummary = N'Replacing NULL value'  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Replacing temporary data with the correct data. Setting @Length to NULL   
-- truncates all existing data from the @Offset position.  
UPDATE Production.Document  
SET DocumentSummary .WRITE(N'Carefully inspect and maintain the tires and crank arms.',0,NULL)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Appending additional data to the end of the column by setting   
-- @Offset to NULL.  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N' Appending data to the end of the column.', NULL, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing all data from @Offset to the end of the existing value by   
-- setting expression to NULL.   
UPDATE Production.Document  
SET DocumentSummary .WRITE (NULL, 56, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing partial data beginning at position 9 and ending at   
-- position 21.  
UPDATE Production.Document  
SET DocumentSummary .WRITE ('',9, 12)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
```  
  
#### <a name="t-using-update-with-openrowset-to-modify-a-varbinarymax-column"></a>T. Verwenden von UPDATE mit OPENROWSET zum Ändern einer varbinary(max)-Spalte  
 Im folgende Beispiel ersetzt ein vorhandenes Image gespeichert einer **varbinary(max)** Spalte durch ein neues Image. Die [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) -Funktion mit der BULK-Option beim Laden des Bilds in der Spalte verwendet wird. In diesem Beispiel wird angenommen, dass eine Datei namens `Tires.jpg` im angegebenen Dateipfad vorhanden ist.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ProductPhoto  
SET ThumbNailPhoto = (  
    SELECT *  
    FROM OPENROWSET(BULK 'c:Tires.jpg', SINGLE_BLOB) AS x )  
WHERE ProductPhotoID = 1;  
GO  
```  
  
#### <a name="u-using-update-to-modify-filestream-data"></a>U. Verwenden von UPDATE zum Ändern von FILESTREAM-Daten  
 Im folgenden Beispiel wird die UPDATE-Anweisung zum Ändern der Daten in der Dateisystemdatei verwendet. Diese Methode wird nicht zum Streamen von großen Datenmengen in eine Datei empfohlen. Verwenden Sie die entsprechenden Win32-Schnittstellen. Im folgenden Beispiel wird der gesamte Text im Dateidatensatz durch den Text `Xray 1`ersetzt. Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
```sql  
UPDATE Archive.dbo.Records  
SET [Chart] = CAST('Xray 1' as varbinary(max))  
WHERE [SerialNumber] = 2;  
```  
  
###  <a name="UDTs"></a>Aktualisieren von benutzerdefinierten Typen  
 In den folgenden Beispielen werden Werte in Spalten eines CLR-benutzerdefinierten Typs (UDT) geändert. Es werden drei Methoden gezeigt. Weitere Informationen zu benutzerdefinierten Spalten finden Sie unter [benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
#### <a name="v-using-a-system-data-type"></a>V. Verwenden eines Systemdatentyps  
 Sie können einen UDT durch Bereitstellen eines Werts eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyps aktualisieren, sofern der benutzerdefinierte Typ implizite oder explizite Konvertierung von diesem Typ unterstützt. Im folgenden Beispiel wird gezeigt, wie Sie einen Wert in einer Spalte des benutzerdefinierten Typs `Point` durch explizites Konvertieren aus einer Zeichenfolge aktualisieren.  
  
```sql  
UPDATE dbo.Cities  
SET Location = CONVERT(Point, '12.3:46.2')  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="w-invoking-a-method"></a>W. Aufrufen einer Methode  
 Sie können einen UDT durch Aufrufen einer Methode des benutzerdefinierten Typs, die als Mutator markiert ist, aktualisieren, um das Update auszuführen. Im folgenden Beispiel wird eine Mutatormethode des Typs `Point` namens `SetXY` aufgerufen. Dadurch wird der Status der Instanz des Typs aktualisiert.  
  
```sql  
UPDATE dbo.Cities  
SET Location.SetXY(23.5, 23.5)  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="x-modifying-the-value-of-a-property-or-data-member"></a>X. Ändern des Werts einer Eigenschaft oder eines Datenelements  
 Sie können einen UDT durch Ändern des Werts eines Elements einer registrierten Eigenschaft oder öffentlicher Daten des benutzerdefinierten Typs aktualisieren. Der Ausdruck, der den Wert bereitstellt, muss implizit in den Typ der Eigenschaft konvertierbar sein. Im folgenden Beispiel wird der Wert der `X`-Eigenschaft des benutzerdefinierten Typs `Point` geändert.  
  
```sql  
UPDATE dbo.Cities  
SET Location.X = 23.5  
WHERE Name = 'Anchorage';  
```  
  
###  <a name="TableHints"></a>Überschreiben das Standardverhalten des Abfrageoptimierers mithilfe von Hinweisen  
 In den Beispielen in diesem Abschnitt wird gezeigt, wie mit Tabellen- und Abfragehinweisen beim Verarbeiten der UPDATE-Anweisung zeitweise das Standardverhalten des Abfrageoptimierers überschrieben wird.  
  
> [!CAUTION]  
>  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer in der Regel den optimalen Ausführungsplan für eine Abfrage auswählt, wird empfohlen, dass erfahrene Entwickler und Datenbankadministratoren Hinweise nur dann verwenden, wenn alle anderen Möglichkeiten sich als unzureichend erwiesen haben.  
  
#### <a name="y-specifying-a-table-hint"></a>Y. Angeben eines Tabellenhinweises  
 Im folgenden Beispiel wird die [Tabellenhinweis](../../t-sql/queries/hints-transact-sql-table.md) TABLOCK. Dieser Hinweis gibt an, dass eine gemeinsame Sperre für die Tabelle `Production.Product` eingerichtet und bis zum Ende der UPDATE-Anweisung aufrechterhalten wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
#### <a name="z-specifying-a-query-hint"></a>Z. Angeben eines Abfragehinweises  
 Im folgenden Beispiel wird die [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) `OPTIMIZE FOR (@variable)` in der UPDATE-Anweisung. Dieser Hinweis weist den Abfrageoptimierer an, einen bestimmten Wert für eine lokale Variable zu verwenden, wenn die Abfrage kompiliert und optimiert wird. Dieser Wert wird nur während der Abfrageoptimierung verwendet, nicht während der Abfrageausführung.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE Production.uspProductUpdate  
@Product nvarchar(25)  
AS  
SET NOCOUNT ON;  
UPDATE Production.Product  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE @Product  
OPTION (OPTIMIZE FOR (@Product = 'BK-%') );  
GO  
-- Execute the stored procedure   
EXEC Production.uspProductUpdate 'BK-%';  
```  
  
###  <a name="CaptureResults"></a>Erfassen der Ergebnisse der UPDATE-Anweisung  
 Die Beispiele in diesem Abschnitt zeigen, wie die [OUTPUT-Klausel](../../t-sql/queries/output-clause-transact-sql.md) zum Zurückgeben von Informationen aus bzw. Ausdrücke basierend auf an, die für jede Zeile von einer UPDATE-Anweisung betroffen sind. Diese Ergebnisse können an die verarbeitende Anwendung zurückgegeben werden, die sie z. B. für Bestätigungen, Archivierungen und andere Anwendungsanforderungen verwendet.  
  
#### <a name="aa-using-update-with-the-output-clause"></a>AA. Verwenden von UPDATE mit der OUTPUT-Klausel  
 Im folgenden Beispiel wird die Spalte `VacationHours` in der Tabelle `Employee` um 25 Prozent für die ersten 10 Zeilen aktualisiert und außerdem der Wert in der Spalte `ModifiedDate` auf das aktuelle Datum festgelegt. Die `OUTPUT`-Klausel gibt an die `VacationHours`-Tabellenvariable den Wert für `UPDATE` zurück, der vor der Anwendung der `deleted.VacationHours`-Anweisung in der `inserted.VacationHours`-Spalte vorhanden war, und den aktualisierten Wert in der `@MyTableVar`-Spalte.  
  
 Es folgen zwei `SELECT`-Anweisungen, die die Werte in `@MyTableVar` und die Ergebnisse des Updatevorgangs in der `Employee`-Tabelle zurückgeben. Weitere Beispiele zum Verwenden der OUTPUT-Klausel, finden Sie unter [OUTPUT-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
###  <a name="Other"></a>Verwenden von UPDATE in anderen Anweisungen  
 In Beispielen in diesem Abschnitt wird die Verwendung von UPDATE in anderen Anweisungen veranschaulicht.  
  
#### <a name="ab-using-update-in-a-stored-procedure"></a>AB. Verwenden von UPDATE in einer gespeicherten Prozedur  
 Im folgenden Beispiel wird eine UPDATE-Anweisung in einer gespeicherten Prozedur verwendet. Die Prozedur erfordert den Eingabeparameter `@NewHours` und den Ausgabeparameter `@RowCount`. Die `@NewHours` Parameterwert wird in der UPDATE-Anweisung zum Aktualisieren der Spalte verwendet `VacationHours` in der Tabelle `HumanResources.Employee`. Der Ausgabeparameter `@RowCount` wird verwendet, um die Anzahl betroffener Zeilen an eine lokale Variable zurückzugeben. Der CASE-Ausdruck wird in der SET-Klausel verwendet, um den Wert, der für `VacationHours` festgelegt wird, bedingt zu bestimmen. Wenn der Mitarbeiter pro Stunde bezahlt wird (`SalariedFlag` = 0), ist `VacationHours` auf die aktuelle Anzahl der Stunden zuzüglich des Werts festgelegt, der unter `@NewHours` angegeben ist. Andernfalls ist `VacationHours` auf den Wert festgelegt, der unter `@NewHours` angegeben ist.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
#### <a name="ac-using-update-in-a-trycatch-block"></a>STROMVERSORGUNG. Verwenden von UPDATE in einem TRY…CATCH-Block  
 Im folgenden Beispiel wird eine UPDATE-Anweisung in einem... CATCH-Block, um Ausführungsfehler zu behandeln, die während des Updatevorgangs auftreten können.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Intentionally generate a constraint violation error.  
    UPDATE HumanResources.Department  
    SET Name = N'MyNewName'  
    WHERE DepartmentID BETWEEN 1 AND 2;  
END TRY  
BEGIN CATCH  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="ad-using-a-simple-update-statement"></a>AD. Verwenden einer einfachen UPDATE-Anweisung  
 Die folgenden Beispielen wird gezeigt wie alle Zeilen betroffen sein können, wenn eine WHERE-Klausel nicht verwendet wird, geben Sie die Zeile (oder Zeilen) zu aktualisieren.  
  
 In diesem Beispiel aktualisiert die Werte in der `EndDate` und `CurrentFlag` Spalten für alle Zeilen in der `DimEmployee` Tabelle.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET EndDate = '2010-12-31', CurrentFlag='False';  
```  
  
 Sie können für eine UPDATE-Anweisung auch berechnete Werte verwenden. Das folgende Beispiel verdoppelt den Wert in der `ListPrice`-Spalte für alle Zeilen in der `Product`-Tabelle.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET BaseRate = BaseRate * 2;  
```  
  
### <a name="ae-using-the-update-statement-with-a-where-clause"></a>AE. Verwenden der UPDATE-Anweisung mit einer WHERE-Klausel  
 Im folgenden Beispiel wird die WHERE-Klausel verwendet, um die zu aktualisierenden Zeilen anzugeben.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET FirstName = 'Gail'  
WHERE EmployeeKey = 500;  
```  
  
### <a name="af-using-the-update-statement-with-label"></a>AF. Verwenden der UPDATE-Anweisung mit Bezeichnung  
 Im folgenden Beispiel wird die Verwendung einer Bezeichnung für die UPDATE-Anweisung.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimProduct  
SET ProductSubcategoryKey = 2   
WHERE ProductKey = 313  
OPTION (LABEL = N'label1');  
```  
  
### <a name="ag-using-the-update-statement-with-information-from-another-table"></a>AG. Verwenden der UPDATE-Anweisung mit Informationen aus einer anderen Tabelle  
 Dieses Beispiel erstellt eine Tabelle zum Speichern der Gesamtumsatz nach Jahr. Aktualisiert den Gesamtumsatz für das Jahr 2004 durch Ausführen einer SELECT-Anweisung für die FactInternetSales-Tabelle.  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE YearlyTotalSales (  
    YearlySalesAmount money NOT NULL,  
    Year smallint NOT NULL )  
WITH ( DISTRIBUTION = REPLICATE );  
  
INSERT INTO YearlyTotalSales VALUES (0, 2004);  
INSERT INTO YearlyTotalSales VALUES (0, 2005);  
INSERT INTO YearlyTotalSales VALUES (0, 2006);  
  
UPDATE YearlyTotalSales  
SET YearlySalesAmount=  
(SELECT SUM(SalesAmount) FROM FactInternetSales WHERE OrderDateKey >=20040000 AND OrderDateKey < 20050000)  
WHERE Year=2004;  
  
SELECT * FROM YearlyTotalSales;   
```  

### <a name="ah-ansi-join-replacement-for-update-statements"></a>AH. ANSI Join Ersatz für Update-Anweisungen
Sie können möglicherweise, dass Sie ein komplexes Update verfügen, das mehr als zwei Tabellen, die zusammen mit ANSI-Syntax verknüpfen die Update- oder DELETE ausführen verknüpft.  

Stellen Sie sich vor, dass mussten Sie diese Tabelle zu aktualisieren:  

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;  
```

Die ursprüngliche Abfrage könnte etwa so aussehen besprochen haben:  

```
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;  
```

Da [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] unterstützt keine ANSI-in der FROM-Klausel einer UPDATE-Anweisung Joins, die dieser Code kann nicht über kopiert werden, ohne ihn leicht ändern.  

Eine Kombination aus einer CTAS und eines impliziten Joins können Sie diesen Code ersetzen:  

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Text und Image-Funktionen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [WITH Common_table_expression &#40; Transact-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  

