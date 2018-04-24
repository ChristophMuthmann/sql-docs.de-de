---
title: MERGE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
caps.latest.revision: 76
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab3800d6cded8d8221d411ac2fdcbb75cba628df
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Führt Einfüge-, Update- oder Löschvorgänge in einer Zieltabelle anhand der Ergebnisse eines Joins mit einer Quelltabelle aus. Sie können z.&nbsp;B. zwei Tabellen synchronisieren, indem Sie Zeilen in einer Tabelle anhand von Unterschieden, die in der anderen Tabelle gefunden wurden, einfügen, aktualisieren oder löschen.  
  
 **Leistungstipp:** Das für die MERGE-Anweisung beschriebene bedingte Verhalten funktioniert am besten, wenn die beiden Tabellen eine komplexe Mischung von übereinstimmenden Eigenschaften haben. Beispielsweise das Einfügen einer Zeile, wenn keine vorhanden ist, oder das Aktualisieren der Zeile, wenn sie übereinstimmt. Wenn Sie eine Tabelle einfach nur basierend auf den Zeilen einer anderen Tabelle aktualisieren, können Sie mit den grundlegenden INSERT-, UPDATE- und DELETE-Anweisungen eine bessere Leistung oder mehr Skalierbarkeit erzielen. Zum Beispiel:  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ WITH <common_table_expression> [,...n] ]  
MERGE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>   
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]      
;  
  
<target_table> ::=  
{   
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]   
        [ WITH ( table_hint [ [ , ]...n ] ) ]   
  | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>   
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]   
  | <joined_table>   
  | <pivoted_table>   
  | <unpivoted_table>   
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]   
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]   
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '< contains_search_condition >' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery ) }   
  
<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }   
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argumente  
 WITH \<common_table_expression>  
 Gibt den temporären Resultset- oder Sichtnamen an, der auch als allgemeiner Tabellenausdruck bezeichnet wird und innerhalb der MERGE-Anweisung definiert ist. Das Resultset wird aus einer einfachen Abfrage abgeleitet. Die MERGE-Anweisung verweist auf dieses Resultset. Weitere Informationen finden Sie unter [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP ( *expression* ) [ PERCENT ]  
 Gibt die Anzahl oder den Prozentsatz der betroffenen Zeilen an. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein. Die Zeilen, auf die im TOP-Ausdruck verwiesen wird, sind nicht auf bestimmte Weise angeordnet. Weitere Informationen finden Sie unter [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 Die TOP-Klausel wird angewendet, nachdem die gesamte Quelltabelle und die gesamte Zieltabelle verknüpft und die nicht für eine der Aktionen INSERT, UPDATE oder DELETE in Frage kommenden verknüpften Zeilen gelöscht wurden. Die TOP-Klausel verringert zudem die Anzahl der verknüpften Zeilen auf den angegebenen Wert, und die INSERT-, UPDATE- oder DELETE-Aktionen werden ungeordnet auf die verbliebenen verknüpften Zeilen angewendet. Dies bedeutet, dass für die Verteilung der Zeilen auf die in den WHEN-Klauseln definierten Aktionen keine bestimmte Reihenfolge gilt. Wenn beispielsweise TOP (10) angegeben wird, sind 10 Zeilen betroffen. Von diesen Zeilen können sieben aktualisiert und drei eingefügt werden, oder eine Zeile kann gelöscht, fünf können aktualisiert und vier eingefügt werden usw.  
  
 Da die MERGE-Anweisung einen vollständigen Tabellenscan der Quell- und der Zieltabelle ausführt, kann die E/A-Leistung beeinträchtigt werden, wenn mit der TOP-Klausel eine große Tabelle durch Erstellen mehrerer Batches geändert wird. In diesem Szenario muss unbedingt sichergestellt werden, dass alle aufeinanderfolgenden Batches auf neue Zeilen ausgerichtet sind.  
  
 *database_name*  
 Der Name der Datenbank, in der sich *target_table* befindet.  
  
 *schema_name*  
 Der Namen des Schemas, zu dem die Tabelle *target_table* gehört.  
  
 *target_table*  
 Die Tabelle oder Sicht, mit der die Datenzeilen aus \<table_source> basierend auf \<clause_search_condition> abgeglichen werden. *target_table* ist das Ziel aller Einfüge-, Update- oder Löschvorgänge, die durch die WHEN-Klauseln der MERGE-Anweisung angegeben werden.  
  
 Wenn *target_table* eine Sicht ist, müssen alle Aktionen für die Tabelle die Bedingungen zum Aktualisieren von Sichten erfüllen. Weitere Informationen finden Sie unter [Modify Data Through a View (Ändern von Daten über eine Sicht)](../../relational-databases/views/modify-data-through-a-view.md).  
  
 *target_table* darf keine Remotetabelle sein. Für *target_table* dürfen keine Regeln definiert sein.  
  
 [ AS ] *table_alias*  
 Ist ein alternativer Name, über den auf eine Tabelle verwiesen wird.  
  
 USING \<table_source>  
 Gibt die Datenquelle an, die basierend auf \<merge_search condition> mit den Datenzeilen in *target_table* abgeglichen wird. Das Ergebnis dieser Zuordnung legt die Aktionen fest, die von den WHEN-Klauseln der MERGE-Anweisung ausgeführt werden. \<table_source> kann eine Remotetabelle oder eine abgeleitete Tabelle sein, die auf Remotetabellen zugreift. 
  
 \<table_source> kann eine abgeleitete Tabelle sein, die mit dem [Tabellenwertkonstruktor](../../t-sql/queries/table-value-constructor-transact-sql.md) von [!INCLUDE[tsql](../../includes/tsql-md.md)] eine Tabelle durch Angeben mehrerer Zeilen erstellt.  
  
 Weitere Informationen zur Syntax und zu den Argumenten dieser Klausel finden Sie unter [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 ON \<merge_search_condition>  
 Gibt die Bedingungen an, unter denen \<table_source> mit *target_table* verknüpft wird, um Übereinstimmungen zu ermitteln. 
  
> [!CAUTION]  
>  Es ist wichtig, dass nur die Spalten aus der Zieltabelle angegeben werden, die für Abgleichszwecke verwendet werden. Geben Sie also Spalten aus der Zieltabelle an, die mit der entsprechenden Spalte der Quelltabelle abgeglichen werden. Versuchen Sie nicht, die Abfrageleistung zu optimieren, indem Sie Zeilen in der Zieltabelle in der ON-Klausel herausfiltern, beispielsweise durch Angabe von `AND NOT target_table.column_x = value`. Dadurch kann es zu unerwarteten und falschen Ergebnissen kommen.  
  
 WHEN MATCHED THEN \<merge_matched>  
 Gibt an, dass alle Zeilen von *target_table*, die mit den von \<table_source> ON \<merge_search_condition> zurückgegebenen Zeilen übereinstimmen und alle zusätzlichen Suchbedingungen erfüllen, gemäß der \<merge_matched>-Klausel aktualisiert oder gelöscht werden.  
  
 Die MERGE-Anweisung kann höchstens über zwei WHEN MATCHED-Klauseln verfügen. Wenn zwei Klauseln angegeben werden, muss die erste Klausel von einer AND \<search_condition>-Klausel begleitet werden. Für jede gegebene Zeile wird die zweite WHEN MATCHED-Klausel nur angewendet, wenn die erste nicht angewendet wurde. Wenn zwei WHEN MATCHED-Klauseln vorhanden sind, muss die eine eine UPDATE-Aktion und die andere eine DELETE-Aktion angeben. Wenn UPDATE in der \<merge_matched>-Klausel angegeben wird und mehr als eine Zeile aus \<table_source> basierend auf \<merge_search_condition> mit einer Zeile in *target_table* übereinstimmt, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück. Die MERGE-Anweisung kann dieselbe Zeile nicht mehrmals aktualisieren oder dieselbe Zeile aktualisieren und löschen.  
  
 WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
 Gibt an, dass für jede Zeile, die von \<table_source> ON \<merge_search_condition> zurückgegeben wird und nicht mit einer Zeile in *target_table* übereinstimmt, aber eine zusätzliche Suchbedingung erfüllt (falls vorhanden), eine Zeile in *target_table* eingefügt wird. Die einzufügenden Werte werden durch die \<merge_not_matched>-Klausel angegeben. Die MERGE-Anweisung kann nur über eine WHEN NOT MATCHED-Klausel verfügen.  
  
 WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
 Gibt an, dass alle Zeilen von *target_table*, die nicht mit den von \<table_source> ON \<merge_search_condition> zurückgegebenen Zeilen übereinstimmen und die alle zusätzlichen Suchbedingungen erfüllen, gemäß der \<merge_matched>-Klausel aktualisiert oder gelöscht werden.  
  
 Die MERGE-Anweisung kann höchstens über zwei WHEN NOT MATCHED BY SOURCE-Klauseln verfügen. Wenn zwei Klauseln angegeben werden, muss die erste Klausel von einer AND \<clause_search_condition>-Klausel begleitet werden. Für jede gegebene Zeile wird die zweite WHEN NOT MATCHED BY SOURCE-Klausel nur angewendet, wenn die erste nicht angewendet wurde. Wenn zwei WHEN NOT MATCHED BY SOURCE-Klauseln vorhanden sind, muss die eine eine UPDATE-Aktion und die andere eine DELETE-Aktion angeben. In \<clause_search_condition> kann nur auf Spalten aus der Zieltabelle verwiesen werden.  
  
 Wenn von \<table_source> keine Zeilen zurückgegeben werden, kann auf Spalten in der Quelltabelle nicht zugegriffen werden. Wenn die in der \<merge_matched>-Klausel angegebene Update- oder Löschaktion auf Spalten in der Quelltabelle verweist, wird der Fehler 207 (Ungültiger Spaltenname) zurückgegeben. Die Klausel `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` kann beispielsweise dazu führen, dass die Anweisung fehlschlägt, da der Zugriff auf `Col1` in der Quelltabelle nicht möglich ist.  
  
 AND \<clause_search_condition>  
 Gibt jede gültige Suchbedingung an. Weitere Informationen finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 \<table_hint_limited>  
 Gibt mindestens einen Tabellenhinweis an, der für jeden durch die MERGE-Anweisung ausgeführten Einfüge-, Update- oder Löschvorgang auf die Zieltabelle angewendet wird. Das WITH-Schlüsselwort und die Klammern sind erforderlich.  
  
 NOLOCK und READUNCOMMITTED sind nicht zulässig. Weitere Informationen zu Tabellenhinweisen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Das Angeben eines TABLOCK-Hinweises für eine Tabelle, die das Ziel einer INSERT-Anweisung ist, hat dieselbe Wirkung wie das Angeben eines TABLOCKX-Hinweises. Auf die Tabelle wird eine exklusive Sperre angewendet. Wenn FORCESEEK angegeben wird, wird der Hinweis auf die implizite Instanz der Zieltabelle angewendet, die mit der Quelltabelle verknüpft ist.  
  
> [!CAUTION]  
>  Wenn READPAST mit WHEN NOT MATCHED [ BY TARGET ] THEN INSERT angegeben wird, kann dies zu INSERT-Operationen führen, die gegen UNIQUE-Beschränkungen verstoßen.  
  
 INDEX ( index_val [ ,...n ] )  
 Gibt den Namen oder die ID eines oder mehrerer Indizes in der Zieltabelle zum Ausführen eines impliziten Joins mit der Quelltabelle an. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<OUTPUT_Clause>  
 Gibt ohne bestimmte Reihenfolge eine Zeile für jede Zeile in *target_table* zurück, die aktualisiert, eingefügt oder gelöscht wird. **$action** kann in der OUTPUT-Klausel angegeben werden. **$action** ist eine Spalte vom Typ **nvarchar(10)**, die einen der drei folgenden Werte für jede Zeile zurückgibt: INSERT, UPDATE oder DELETE. Der zurückgegebene Wert hängt von der für diese Zeile ausgeführten Aktion ab. Weitere Informationen zu den Argumenten dieser Klausel finden Sie unter [OUTPUT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 OPTION ( \<query_hint> [ ,...n ] )  
 Gibt an, dass zum Anpassen der Art und Weise, wie die Anweisung durch das Datenbankmodul verarbeitet wird, Hinweise des Abfrageoptimierers verwendet werden. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 \<merge_matched>  
 Gibt die Update- oder Löschaktion an, die auf alle Zeilen von *target_table* angewendet wird, die nicht mit den von \<table_source> ON \<merge_search_condition> zurückgegebenen Zeilen übereinstimmen, und die alle zusätzlichen Suchbedingungen erfüllen.  
  
 UPDATE SET \<set_clause>  
 Gibt die Liste der Spalten- oder Variablennamen an, die in der Zieltabelle aktualisiert werden sollen, sowie die Werte, mit denen das Update vorgenommen werden soll.  
  
 Weitere Informationen zu den Argumenten dieser Klausel finden Sie unter [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md). Es ist nicht zulässig, eine Variable auf denselben Wert festzulegen wie eine Spalte.  
  
 Delete  
 Gibt an, dass die Zeilen, die mit Zeilen in *target_table* übereinstimmen, gelöscht werden.  
  
 \<merge_not_matched>  
 Gibt die Werte an, die in die Zieltabelle eingefügt werden sollen.  
  
 (*column_list*)  
 Ist eine Liste mit einer oder mehreren Spalten der Zieltabelle, in die Daten eingefügt werden sollen. Spalten müssen als einteiliger Name angegeben werden. Andernfalls schlägt die MERGE-Anweisung fehl. *column_list* muss in Klammern eingeschlossen und durch ein Trennzeichen getrennt werden.  
  
 VALUES ( *values_list*)  
 Eine durch Trennzeichen getrennte Liste mit Konstanten, Variablen oder Ausdrücken, die Werte zum Einfügen in die Zieltabelle zurückgeben. Ausdrücke dürfen keine EXECUTE-Anweisung enthalten.  
  
 DEFAULT VALUES  
 Erzwingt, dass die eingefügte Zeile den für jede Spalte definierten Standardwert enthält.  
  
 Weitere Informationen zu dieser Klausel finden Sie unter [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 \<search condition>  
 Gibt die Suchbedingungen an, die zum Angeben von \<merge_search_condition> oder \<clause_search_condition> verwendet werden. Weitere Informationen zu den Argumenten für diese Klausel finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Mindestens eine der drei MATCHED-Klauseln muss angegeben werden, dies kann jedoch in beliebiger Reihenfolge erfolgen. Eine Variable in derselben MATCHED-Klausel kann nicht mehr als einmal aktualisiert werden.  
  
 Jede Einfüge-, Update- oder Löschaktion, die in der Zieltabelle durch die MERGE-Anweisung angegeben wird, ist durch alle für die Tabelle definierten Beschränkungen eingeschränkt, einschließlich aller kaskadierenden referenziellen Integritätsbeschränkungen. Wenn IGNORE_DUP_KEY für alle eindeutigen Indizes in der Zieltabelle auf ON festgelegt ist, ignoriert MERGE diese Einstellung.  
  
 Die MERGE-Anweisung erfordert ein Semikolon (;) als Abschlusszeichen für die Anweisung. Wenn eine MERGE-Anweisung ohne das Abschlusszeichen ausgeführt wird, wird der Fehler 10713 generiert.  
  
 Bei Verwendung nach MERGE gibt [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md) die Gesamtanzahl der eingefügten, aktualisierten und gelöschten Zeilen an den Client zurück.  
  
 MERGE ist ein vollständig reserviertes Schlüsselwort, wenn der Kompatibilitätsgrad der Datenbank auf 100 oder höher festgelegt ist. Die MERGE-Anweisung ist bei einem Kompatibilitätsgrad von sowohl 90 als auch 100 verfügbar. Bei einem Kompatibilitätsgrad von 90 ist das Schlüsselwort allerdings nicht vollständig reserviert.  
  
 Die **MERGE**-Anweisung sollte nicht zusammen mit dem Replikationstyp „Verzögertes Update über eine Warteschlange“ verwendet werden. **MERGE** und der Trigger für verzögerte Updates über eine Warteschlange sind nicht kompatibel. Ersetzen Sie die **MERGE**-Anweisung durch eine INSERT- oder UPDATE-Anweisung.  
  
## <a name="trigger-implementation"></a>Triggerimplementierung  
 Für jeden Einfüge-, Update- oder Löschvorgang, der in der MERGE-Anweisung angegeben ist, löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle entsprechenden AFTER-Trigger aus, die in der Zieltabelle definiert sind, gewährleistet jedoch nicht, für welche Aktion Trigger zuerst oder zuletzt ausgelöst werden. Trigger, die für dieselbe Aktion definiert sind, halten sich an die von Ihnen angegebene Reihenfolge. Weitere Informationen zum Festlegen der Reihenfolge beim Auslösen von Triggern finden Sie unter [Angeben des ersten und des letzten Triggers](../../relational-databases/triggers/specify-first-and-last-triggers.md).  
  
 Wenn in der Zieltabelle ein aktivierter INSTEAD OF-Trigger für einen Einfüge-, Update- oder Löschvorgang definiert ist, der durch eine MERGE-Anweisung ausgeführt wird, muss sie einen aktivierten INSTEAD OF-Trigger für alle in der MERGE-Anweisung angegebenen Aktionen enthalten.  
  
 Wenn für *target_table* ein INSTEAD OF UPDATE-Trigger oder INSTEAD OF DELETE-Trigger definiert ist, werden die Update- oder Löschvorgänge nicht ausgeführt. Stattdessen werden die Trigger ausgelöst, und die **inserted**- und die **deleted**-Tabelle werden entsprechend aufgefüllt.  
  
 Wenn für *target_table* der INSTEAD OF INSERT-Trigger definiert ist, wird der Einfügevorgang nicht ausgeführt. Stattdessen werden die Trigger ausgelöst, und die **inserted**-Tabelle wird entsprechend aufgefüllt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die SELECT-Berechtigung für die Quelltabelle und die INSERT-, UPDATE- oder DELETE-Berechtigung für die Zieltabelle. Weitere Informationen finden Sie im Abschnitt „Berechtigungen“ in den Artikeln zu [SELECT](../../t-sql/queries/select-transact-sql.md), [INSERT](../../t-sql/statements/insert-transact-sql.md), [UPDATE](../../t-sql/queries/update-transact-sql.md) und [DELETE](../../t-sql/statements/delete-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. Verwenden von MERGE zum Ausführen von INSERT- und UPDATE-Vorgängen für eine Tabelle in einer einzelnen Anweisung  
 Ein verbreitetes Szenario ist das Aktualisieren mindestens einer Spalte in einer Tabelle, wenn eine übereinstimmende Zeile vorhanden ist, oder das Einfügen der Daten als neue Zeile, wenn keine übereinstimmende Zeile vorhanden ist. Dazu werden normalerweise Parameter an eine gespeicherte Prozedur übergeben, die die entsprechende UPDATE-Anweisung und INSERT-Anweisung enthält. Mit der MERGE-Anweisung können Sie beide Tasks in einer einzelnen Anweisung ausführen. Im folgenden Beispiel wird eine gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank dargestellt, die sowohl eine INSERT-Anweisung als auch eine UPDATE-Anweisung enthält. Anschließend wird die Prozedur so geändert, dass sie die entsprechenden Vorgänge mit einer einzelnen MERGE-Anweisung ausführt.  
  
```  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.      
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the 
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values 
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN   
        UPDATE SET Name = source.Name  
WHEN NOT MATCHED THEN  
    INSERT (UnitMeasureCode, Name)  
    VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup   
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. Verwenden von MERGE zum Ausführen von UPDATE- und DELETE-Operationen für eine Tabelle in einer einzelnen Anweisung  
 Im folgenden Beispiel wird die `ProductInventory`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank täglich mit MERGE aktualisiert. Dies erfolgt auf der Grundlage der in der `SalesOrderDetail`-Tabelle verarbeiteten Bestellungen. Die `Quantity`-Spalte der `ProductInventory`-Tabelle wird aktualisiert, indem die Anzahl der täglich aufgegebenen Bestellungen für die einzelnen Produkte in der `SalesOrderDetail`-Tabelle subtrahiert wird. Wenn die Anzahl der Bestellungen für ein Produkt dazu führt, dass der Produktbestand auf oder unter 0 (null) fällt, wird die Zeile für dieses Produkt aus der `ProductInventory`-Tabelle gelöscht.  
  
```  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED   
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,   
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity, 
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. Verwenden von MERGE zum Ausführen von UPDATE- und INSERT-Vorgängen für eine Zieltabelle unter Verwendung einer abgeleiteten Quelltabelle  
 Im folgenden Beispiel wird die `SalesReason`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank durch das Aktualisieren oder Einfügen von Zeilen mithilfe von MERGE geändert. Wenn der Wert von `NewName` in der Quelltabelle einem Wert in der `Name`-Spalte der Zieltabelle entspricht (`SalesReason`), wird die `ReasonType`-Spalte in der Zieltabelle aktualisiert. Wenn der Wert von `NewName` jedoch nicht übereinstimmt, wird die Quellzeile in die Zieltabelle eingefügt. Die Quelltabelle ist eine abgeleitete Tabelle, die mithilfe des [!INCLUDE[tsql](../../includes/tsql-md.md)]-Tabellenwertkonstruktors mehrere Zeilen für die Quelltabelle angibt. Weitere Informationen zum Verwenden des Tabellenwertkonstruktors in einer abgeleiteten Tabelle finden Sie unter [Table Value Constructor &#40;Transact-SQL&#41; (Tabellenwertkonstruktor &#40;Transact-SQL&#41;)](../../t-sql/queries/table-value-constructor-transact-sql.md). Im Beispiel wird auch gezeigt, wie die Ergebnisse der OUTPUT-Klausel in einer Tabellenvariablen gespeichert werden. Es wird erläutert, wie die Ergebnisse der MERGE-Anweisung zusammengefasst werden, indem ein einfacher SELECT-Vorgang ausgeführt wird, der die Anzahl an eingefügten und aktualisierten Zeilen zurückgibt.  
  
```  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), 
              ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. Einfügen der Ergebnisse der MERGE-Anweisung in eine andere Tabelle  
 Im folgenden Beispiel werden aus der OUTPUT-Klausel einer MERGE-Anweisung zurückgegebene Daten erfasst und in eine andere Tabelle eingefügt. Die MERGE-Anweisung aktualisiert die `Quantity`-Spalte der `ProductInventory`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank täglich auf der Grundlage der Bestellungen, die in der `SalesOrderDetail`-Tabelle verarbeitet werden. In diesem Beispiel werden die aktualisierten Zeilen erfasst und in eine andere Tabelle eingefügt, in der Bestandsänderungen nachverfolgt werden.  
  
```  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty   
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)   
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0   
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0   
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID, 
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty) 
 WHERE Action = 'UPDATE';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [OUTPUT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [MERGE in Integration Services-Paketen](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Table Value Constructor &#40;Transact-SQL&#41; (Tabellenwertkonstruktor &#40;Transact-SQL&#41;)](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  

