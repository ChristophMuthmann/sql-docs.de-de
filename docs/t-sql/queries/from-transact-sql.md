---
title: AUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: c1abc4a060dd275ba2f8500e88d634a5ba9244ee
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt die Tabellen, Sichten, abgeleiteten Tabellen und verknüpften Tabellen in DELETE-, SELECT- und UPDATE-Anweisungen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] fest. Die FROM-Klausel wird in der SELECT-Anweisung immer benötigt, es sei denn, die Auswahlliste enthält nur Konstanten, Variablen und arithmetische Ausdrücke (keine Spaltennamen).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>Argumente  
\<table_source>  
 Gibt eine Tabelle, Sicht, Tabellenvariable oder abgeleitete Tabelle als Quelle mit oder ohne Alias zum Verwenden in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung an. In einer Anweisung können bis zu 256 Tabellenquellen verwendet werden. Allerdings variiert das Limit in Abhängigkeit vom verfügbaren Arbeitsspeicher und der Komplexität anderer Ausdrücke in der Abfrage. Einzelne Abfragen unterstützen möglicherweise nicht bis zu 256 Tabellenquellen.  
  
> [!NOTE]  
>  Durch eine hohe Anzahl an Tabellen, auf die in einer Abfrage verwiesen wird, kann möglicherweise die Abfrageleistung beeinträchtigt werden. Zusätzliche Faktoren haben außerdem Auswirkungen auf die Kompilierungs- und Optimierungszeit. Dazu gehören das Vorhandensein von Indizes und indizierte Sichten auf jedem \<Table_source > und die Größe der \<Select_list > in der SELECT-Anweisung.  
  
 Die Reihenfolge der Tabellenquellen nach dem FROM-Schlüsselwort hat keinen Einfluss auf das Resultset. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt Fehler zurück, wenn doppelte Namen in der FROM-Klausel angezeigt werden.  
  
 *table_or_view_name*  
 Der Name einer Tabelle oder Sicht.  
  
 Wenn die Tabelle oder Sicht in einer anderen Datenbank auf derselben Instanz von vorhanden ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verwenden Sie einen vollqualifizierten Namen in der Form *Datenbank*. *Schema*. *Object_name*.  
  
 Wenn die Tabelle oder Sicht außerhalb der Instanz von vorhanden ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l, verwenden Sie einen vierteiligen Namen in der Form *Linked_server*. *Katalog*. *Schema*. *Objekt*. Weitere Informationen finden Sie unter [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)erläutert. Ein vierteiliger Name, mit dem Sie erstellt ist, die [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) Funktion als Serverteil des Namens auch zum Angeben der remotequelltabelle verwendet werden kann. Wenn OPENDATASOURCE angegeben wird, *Database_name* und *Schema_name* gelten möglicherweise nicht für alle Datenquellen und unterliegen den Funktionen des OLE DB-Anbieters, der auf das Remoteobjekt zugreift.  
  
 [AS] *table_alias*  
 Ist ein Alias für *Table_source* , entweder zur Vereinfachung oder zur Unterscheidung einer Tabelle oder Sicht in einem selbstjoin oder einer Unterabfrage verwendet werden kann. Ein Alias ist oftmals ein verkürzter Tabellenname, der verwendet wird, um in einem Join auf bestimmte Spalten der beteiligten Tabellen zu verweisen. Falls ein Spaltenname in mehr als einer Tabelle des Joins vorkommt, muss dieser Spaltenname für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch einen Tabellennamen, einen Sichtnamen oder einen Alias gekennzeichnet werden. Falls ein Alias definiert ist, kann der Tabellenname nicht verwendet werden.  
  
 Wenn eine abgeleitete Tabelle, Rowset oder Tabellenwertfunktion oder operatorklausel (z. B. Pivot- oder UNPIVOT) verwendet wird, ist der erforderliche *Table_alias* am Ende der-Klausel wird die verknüpfte Tabellenname für alle Spalten, einschließlich gruppierter Spalten zurückgegeben.  
  
 MIT (\<Table_hint >)  
 Gibt an, dass der Abfrageoptimierer eine Optimierungs- oder Sperrstrategie bei dieser Tabelle und für diese Anweisung verwendet. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 *rowset_function*  

**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Gibt eine der Rowsetfunktionen (z. B. OPENROWSET) an, die ein Objekt zurückgeben, das statt eines Tabellenverweises verwendet werden kann. Weitere Informationen über eine Liste mit Rowsetfunktionen finden Sie unter [Rowset-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 Die Verwendung der OPENROWSET- und OPENQUERY-Funktionen zum Angeben eines Remoteobjekts hängt von den Fähigkeiten des OLE DB-Anbieters ab, der auf das Objekt zugreift.  
  
 *bulk_column_alias*  

**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Ein optionaler Alias, der einen Spaltennamen im Resultset ersetzt. Spaltenaliase sind nur in SELECT-Anweisungen zulässig, die die OPENROWSET-Funktion mit der BULK-Option verwenden. Bei Verwendung von *Bulk_column_alias*, geben Sie einen Alias für jede Tabellenspalte in derselben Reihenfolge wie die Spalten in der Datei.  
  
> [!NOTE]  
>  Dieser Alias überschreibt das NAME-Attribut in den COLUMN-Elementen einer XML-Formatdatei, sofern vorhanden.  
  
 *user_defined_function*  
 Gibt eine Tabellenwertfunktion an.  
  
 OPENXML \<openxml_clause>  

**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Stellt eine Rowsetsicht eines XML-Dokuments bereit. Weitere Informationen finden Sie unter [OPENXML &#40; Transact-SQL &#41; ](../../t-sql/functions/openxml-transact-sql.md).  
  
 *derived_table*  
 Entspricht einer Unterabfrage, die Zeilen von der Datenbank abruft. *Derived_table* als Eingabe für die äußere Abfrage verwendet wird.  
  
 *abgeleitete* *_table* können die [!INCLUDE[tsql](../../includes/tsql-md.md)] tabellenwertkonstruktors mehrere Zeilen angeben. Beispiel: `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`. Weitere Informationen finden Sie unter [Tabellenwertkonstruktor &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 Ein optionaler Alias, der einen Spaltennamen im Resultset der abgeleiteten Tabelle ersetzen soll. Geben Sie für jede Spalte in der Auswahlliste einen Spaltenalias an, und schließen Sie die gesamte Liste der Spaltenaliasnamen in Klammern ein.  
  
 *Table_or_view_name* FOR SYSTEM_TIME \<System_time >  

**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Gibt an, dass eine bestimmte Version der Daten aus der angegebenen temporalen Tabelle und ihre verknüpften System versionierte Verlaufstabelle zurückgegeben wird  
  
\<tablesample_clause>  
 Gibt an, dass Beispieldaten aus der Tabelle zurückgegeben werden. Die Beispieldaten können ungefähr sein. Diese Klausel kann für eine primäre oder verknüpfte Tabelle in einer SELECT-, UPDATE- oder DELETE-Anweisung verwendet werden. TABLESAMPLE kann nicht für Sichten angegeben werden.  
  
> [!NOTE]  
>  Wenn Sie TABLESAMPLE für Datenbanken verwenden, die auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden, wird der Kompatibilitätsgrad der Datenbank auf mindestens 110 festgelegt, und PIVOT ist in einer rekursiven allgemeinen Tabellenausdrucksabfrage (CTE, Common Table Expression) nicht zugelassen. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 SYSTEM  
 Eine von der Implementierung abhängige Stichprobenmethode, die durch ISO-Standards angegeben ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist dies die einzige verfügbare Stichprobenmethode. Sie wird standardmäßig angewendet. SYSTEM wendet eine seitenbasierte Stichprobenmethode an, in der eine zufällige Gruppe von Seiten aus der Tabelle für die Stichprobe ausgewählt wird. Alle Zeilen auf diesen Seiten werden als Stichprobenteilmenge zurückgegeben.  
  
 *sample_number*  
 Ein genauer oder ungefährer konstanter numerischer Ausdruck, der den Prozentanteil oder die Anzahl der Zeilen angibt. Wenn mit PERCENT angegeben *Sample_number* wird implizit konvertiert, um eine **"float"** Wert; andernfalls wird es in konvertiert **"bigint"**. PERCENT ist die Standardeinstellung.  
  
 PERCENT  
 Gibt an, dass eine *Sample_number* Prozent der Zeilen der Tabelle aus der Tabelle abgerufen werden sollen. Wenn PERCENT angegeben wird, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen ungefähren Wert des angegebenen Prozentanteils zurück. Wenn PERCENT angegeben wird die *Sample_number* Ausdruck muss zu einem Wert von 0 bis 100 ausgewertet.  
  
 ROWS  
 Gibt an, dass eine ungefähre *Sample_number* Zeilen abgerufen werden soll. Wenn ROWS angegeben ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ungefähr die angegebene Zeilenanzahl zurück. Wenn ROWS angegeben ist, die *Sample_number* Ausdruck muss auf einen ganzzahligen Wert größer als 0 (null) ausgewertet.  
  
 REPEATABLE  
 Gibt an, dass die ausgewählten Stichprobendaten erneut zurückgegeben werden können. Bei Angabe mit demselben *Repeat_seed* Wert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dieselbe Teilmenge von Zeilen zurück, solange keine Änderungen an den Zeilen in der Tabelle vorgenommen wurden. Bei Angabe mit einem anderen *Repeat_seed* Wert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird wahrscheinlich Return einige andere Stichprobe der Zeilen in der Tabelle. Die folgenden an der Tabelle vorgenommenen Aktionen gelten als Änderungen: Einfügen, Aktualisieren, Löschen, neues Erstellen oder Defragmentieren von Indizes sowie Wiederherstellen oder Anfügen von Datenbanken.  
  
 *repeat_seed*  
 Ist ein konstanter ganzzahliger Ausdruck, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Generieren einer Zufallszahl verwendet wird. *Repeat_seed* ist **"bigint"**. Wenn *Repeat_seed* nicht angegeben ist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist einen Wert, nach dem Zufallsprinzip. Für einen bestimmten *Repeat_seed* Wert, der stichprobenergebnis gilt immer, wenn keine Änderungen auf die Tabelle angewendet wurden. Die *Repeat_seed* Ausdruck muss in eine ganze Zahl größer als 0 (null) ausgewertet.  
  
 \<joined_table>  
 Ein Resultset, das das Produkt von zwei oder mehr Tabellen darstellt. Verwenden Sie für mehrere Joins Klammern, um die natürliche Joinreihenfolge zu ändern.  
  
\<join_type>  
 Gibt den Typ der Joinoperation an.  
  
 **INNERE**  
 Gibt an, dass alle übereinstimmenden Paare von Zeilen zurückgegeben werden. Zeilen, die in den beiden Tabellen nicht übereinstimmen, werden verworfen. Wenn kein Jointyp angegeben wird, ist dies die Standardeinstellung.  
  
 FULL [OUTER]  
 Gibt an, dass eine Zeile aus der linken oder der rechten Tabelle im Resultset aufgeführt werden soll, die die Joinbedingung nicht erfüllt. Die Ausgabespalten der anderen Tabelle werden in diesem Fall auf NULL festgelegt. Dies erfolgt zusätzlich zu allen Zeilen, die von INNER JOIN zurückgegeben werden.  
  
 LEFT [OUTER]  
 Gibt an, dass alle Zeilen der linken Tabelle, die die angegebene Joinbedingung nicht erfüllen, im Resultset enthalten sind. Die Ausgabespalten der anderen Tabelle werden auf NULL gesetzt. Dies erfolgt zusätzlich zu allen Zeilen, die von INNER JOIN zurückgegeben werden.  
  
 RIGHT [OUTER]  
 Gibt an, dass alle Zeilen der rechten Tabelle, die die angegebene Joinbedingung nicht erfüllen, im Resultset enthalten sind. Die Ausgabespalten der anderen Tabelle werden auf NULL gesetzt. Dies erfolgt zusätzlich zu allen Zeilen, die von INNER JOIN zurückgegeben werden.  
  
\<join_hint>  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)], gibt an, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfrage Optimierer verwendet einen Joinhinweis oder Ausführungsalgorithmus pro Join in der FROM-Klausel angegeben. Weitere Informationen finden Sie unter [Join-Abfragehinweise &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 Für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], diese joinhinweise gelten, für innere Joins von zwei verteilungsspalten nicht kompatibel. Sie können die abfrageleistung verbessern, indem Sie den Betrag der datenverschiebung, die bei der Verarbeitung einer Abfrage einschränken. Die zulässige joinhinweise für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] lauten wie folgt:  
  
 REDUZIEREN  
 Reduziert die Anzahl der Zeilen, die für die Tabelle auf der rechten Seite des Joins verschoben werden, um zwei inkompatible Verteilungstabellen kompatibel zu machen. REDUCE-Hinweis wird einen Semi-join-Hinweis auch aufgerufen werden.  
  
 REPLICATE  
 Bewirkt, dass die Werte in die verknüpfte Spalte aus der Tabelle auf der linken Seite des Joins auf allen Knoten repliziert werden sollen. Die Tabelle auf der rechten Seite ist auf die replizierten Version dieser Spalten verknüpft.  
  
 VOM REDISTRIBUTE-HINWEIS  
 Erzwingt, dass zwei Datenquellen werden für Spalten, die in der JOIN-Klausel angegebenen verteilt werden. Für eine verteilte Tabelle [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] führt eine zufällige Verschiebung. Für eine replizierte Tabelle [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] führt eine Kürzung verschieben. Um zu verstehen, Verschieben dieser Typen, finden Sie im Abschnitt "DMS-Abfrage-Plan-Vorgänge" im Thema "Grundlegendes zu Abfragepläne" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Dieser Hinweis kann die Leistung verbessern, wenn der Abfrageplan einen broadcast Verschiebevorgang verwendet, um eine Verteilung inkompatible Join zu beheben.  
  
 JOIN  
 Legt fest, dass die angegebene Joinoperation mit den angegebenen Tabellenquellen oder Sichten durchgeführt werden soll.  
  
 ON \<search_condition>  
 Gibt die Bedingung an, auf der der Join basiert. Als Bedingung können beliebige Prädikate angegeben werden, obwohl häufig Spalten- und Vergleichsoperatoren verwendet werden, z. B.:  
  
```sql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 Wenn in der Bedingung Spalten angegeben werden, müssen die Spalten nicht denselben Namen oder Datentyp aufweisen. Die Datentypen müssen jedoch, wenn sie nicht identisch sind, kompatibel sein oder von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implizit konvertiert werden können. Wenn die Datentypen nicht implizit konvertiert werden können, muss die Bedingung den Datentyp mithilfe der CONVERT-Funktion explizit konvertieren.  
  
 Es kann Prädikate geben, die sich auf nur eine der verknüpften Tabellen beziehen, die in der ON-Klausel angegeben sind. Derartige Prädikate können auch in der WHERE-Klausel der Abfrage stehen. Bei einem inneren Join (INNER JOIN) spielt es keine Rolle, wo diese Prädikate stehen. Bei einem äußeren Join (OUTER JOIN) können derartige Prädikate dagegen zu unterschiedlichen Ergebnissen führen. Dies liegt daran, dass die in der ON-Klausel angegebenen Prädikate vor dem Join auf die Tabelle angewendet werden, während die WHERE-Klausel semantisch auf das Ergebnis des Joins angewendet wird.  
  
 Weitere Informationen zu suchbedingungen und Prädikaten finden Sie unter [Suchbedingung &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 Gibt das Kreuzprodukt zweier Tabellen an. Gibt dieselben Zeilen wie die frühere Joinanweisung (die nicht SQL-92-gemäß ist) ohne WHERE-Klausel zurück.  
  
 *left_table_source* { CROSS | OUTER } APPLY *right_table_source*  
 Gibt an, dass die *Right_table_source* der Apply-Operators wird ausgewertet, für jede Zeile des der *Left_table_source*. Diese Funktion ist nützlich, wenn die *Right_table_source* enthält eine Tabellenwertfunktion, die Spaltenwerte aus der *Left_table_source* als eines ihrer Argumente.  
  
 Mit APPLY muss CROSS oder OUTER angegeben werden. Wenn CROSS angegeben wird, werden keine Zeilen erstellt bei der *Right_table_source* wird ausgewertet, für eine bestimmte Zeile von der *Left_table_source* und gibt ein leeres Resultset zurück.  
  
 Wenn OUTER angegeben wird, wird eine Zeile für jede Zeile der erzeugt der *Left_table_source* , auch wenn die *Right_table_source* für diese Zeile ausgewertet, und gibt ein leeres Resultset zurück.  
  
 Weitere Informationen finden Sie im Abschnitt mit Hinweisen.  
  
 *left_table_source*  
 Eine Tabellenquelle gemäß Definition im vorherigen Argument. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.  
  
 *right_table_source*  
 Eine Tabellenquelle gemäß Definition im vorherigen Argument. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.  
  
 *table_source* PIVOT \<pivot_clause>  
 Gibt an, dass die *Table_source* pivotiert wird basierend auf den *Pivot_column*. *Table_source* ist eine Tabelle oder ein Tabellenausdruck. Die Ausgabe ist eine Tabelle, die alle Spalten der enthält die *Table_source* mit Ausnahme der *Pivot_column* und *Value_column*. Die Spalten der *Table_source*, mit Ausnahme der *Pivot_column* und *Value_column*, werden als Gruppierungsspalten des Pivot-Operators bezeichnet. Weitere Informationen zu PIVOT und UNPIVOT, finden Sie unter [mithilfe von PIVOT und UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 PIVOT führt einen Gruppierungsvorgang für die Eingabetabelle in Bezug auf die Gruppierungsspalten aus und gibt für jede Gruppe eine Zeile zurück. Darüber hinaus enthält die Ausgabe eine Spalte für jeden Wert im angegebenen der *Column_list* , angezeigt wird, der *Pivot_column* von der *Input_table*.  
  
 Weitere Informationen finden Sie im nachfolgenden Abschnitt mit Hinweisen.  
  
 *aggregate_function*  
 Eine system- oder benutzerdefinierte Aggregatfunktion, die mindestens eine Eingabe akzeptiert. Die Aggregatfunktion muss bezüglich NULL-Werten invariant sein. Eine bezüglich NULL-Werten invariante Aggregatfunktion berücksichtigt beim Auswerten des Aggregatwerts keine NULL-Werte in der Gruppe.  
  
 Die systembasierte Aggregatfunktion COUNT(*) ist nicht zulässig.  
  
 *value_column*  
 Die Wertspalte des PIVOT-Operators. Bei Verwendung mit UNPIVOT, *Value_column* kann nicht der Name einer vorhandenen Spalte in der Eingabe *Table_source*.  
  
 FÜR *Pivot_column*  
 Entspricht der Pivotspalte des PIVOT-Operators. *Pivot_column* eines Typs, der implizit oder explizit konvertiert werden kann, muss **nvarchar()**. Diese Spalte darf nicht sein **Image** oder **Rowversion**.  
  
 Wenn UNPIVOT verwendet wird, *Pivot_column* ist der Name der Ausgabespalte, die eingeschränkt wird die *Table_source*. Es darf nicht in eine vorhandene Spalte sein *Table_source* mit diesem Namen.  
  
 IN (*Column_list* )  
 Führt Sie in der PIVOT-Klausel, die Werte in der *Pivot_column* , die die Spaltennamen der Ausgabetabelle zu. Die Liste kann keine Spaltennamen, die bereits existieren angeben, in der Eingabe *Table_source* pivotiert werden wird.  
  
 In der UNPIVOT-Klausel sind die Spalten *Table_source* ,-Spalte eingeschränkt werden in einem einzelnen *Pivot_column*.  
  
 *table_alias*  
 Entspricht dem Aliasnamen der Ausgabetabelle. *Pivot_table_alias* muss angegeben werden.  
  
 UNPIVOT \< Unpivot_clause >  
 Gibt an, dass die Eingabetabelle aus mehreren Spalten in eingeschränkt wird *Column_list* in einer einzelnen Spalte namens *Pivot_column*. Weitere Informationen zu PIVOT und UNPIVOT, finden Sie unter [mithilfe von PIVOT und UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 ALS der \<Datum_Uhrzeit >  

**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Gibt eine Tabelle mit einem einzelnen Datensatz für jede Zeile zurück, die die Werte enthält, die zum angegebenen Zeitpunkt in der Vergangenheit real (aktuell) waren. Intern wird eine Union zwischen der temporalen Tabelle und ihrer Verlaufstabelle ausgeführt, und die Ergebnisse werden gefiltert, dass die Werte in der Zeile zurückgegeben, die vom angegebenen Zeitpunkt gültig war die  *\<Datum_Uhrzeit >* Parameter. Der Wert für eine Zeile wird für gültig befunden Wenn die *System_start_time_column_name* Wert ist kleiner als oder gleich der  *\<Datum_Uhrzeit >* Parameterwert und die *System_end_time_ Column_name* Wert ist größer als die  *\<Datum_Uhrzeit >* Parameterwert.   
  
 FROM \<start_date_time> TO \<end_date_time>

**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

  
 Gibt eine Tabelle mit den Werten für alle Datensatzversionen, die innerhalb des angegebenen Zeitraums, unabhängig davon, ob sie vor dem aktiv waren die  *\<start_datum_uhrzeit >* Parameterwert für die Argument ist oder nicht mehr aktiviert, wenn die  *\<ende_datum_uhrzeit >* Parameterwert für das TO-Argument. Intern wird eine Union zwischen der temporalen Tabelle und ihrer Verlaufstabelle ausgeführt, und die Ergebnisse werden so gefiltert, dass die Werte für alle Zeilenversionen zurückgegeben werden, die zu irgendeinem Zeitpunkt innerhalb des angegebenen Zeitbereichs aktiv waren. Zeilen, die genau an dem durch die FROM-Endpunkt definierten unteren Grenzwert aktiv wurden, sind enthalten, und Zeilen, die genau an dem durch den TO-Endpunkt definierten oberen Grenzwert aktiv wurden, sind nicht enthalten.  
  
 BETWEEN \<start_date_time> AND \<end_date_time>  

**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gleich wie oben in der **FROM \<startdatum_uhrzeit > TO \<ende_datum_uhrzeit >** Beschreibung, außer sie Zeilen, die auf die enthalten durch definierten oberen Grenzwert aktiv wurden die \<enddatum_uhrzeit > Endpunkt.  
  
 CONTAINED IN (\<start_date_time> , \<end_date_time>)  

**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Gibt eine Tabelle mit den Werten für alle Datensatzversionen zurück, die innerhalb des von den zwei Datums-/Uhrzeitwerten für das Argument CONTAINED IN definierten Zeitbereichs geöffnet und geschlossen wurden. Zeilen, die genau beim unteren Grenzwert aktiv wurden, oder deren Aktivität genau beim oberen Grenzwert endete, sind enthalten.  
  
 ALL  
 Gibt eine Tabelle mit den Werten aus der alle Zeilen aus der aktuellen Tabelle und der Verlaufstabelle zurück.  
  
## <a name="remarks"></a>Hinweise  
 Die FROM-Klausel unterstützt die SQL-Syntax von SQL-92 für verknüpfte und abgeleitete Tabellen. Die SQL-92-Syntax stellt die Joinoperatoren INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER und CROSS zur Verfügung.  
  
 UNION und JOIN in einer FROM-Klausel werden in Sichten, abgeleiteten Tabellen und Unterabfragen unterstützt.  
  
 Ein Selbstjoin ist eine Tabelle, die mit sich selbst verknüpft ist. Vorgänge zum Einfügen und Aktualisieren, die auf einem Selbstjoin basieren, werden gemäß Reihenfolge der FROM-Klausel ausgeführt.  
  
 Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verteilungs- und Kardinalitätsstatistiken von Verbindungsservern berücksichtigt, die Spaltenverteilungsstatistiken bereitstellen, ist der REMOTE-Joinhinweis nicht erforderlich, um eine Remotebewertung eines Joins zu erzwingen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageprozessor berücksichtigt Remotestatistiken und bestimmt, ob eine Remotejoinstrategie geeignet ist. Der REMOTE-Joinhinweis ist für Anbieter nützlich, die keine Spaltenverteilungsstatistiken bereitstellen.  
  
## <a name="using-apply"></a>Verwenden von APPLY  
 Der linke und der rechte Operand des APPLY-Operators sind Tabellenausdrücke. Der Hauptunterschied zwischen diesen Operanden besteht darin, die die *Right_table_source* können eine Tabellenwert-Funktion, die eine Spalte aus der *Left_table_source* als eines der Argumente der Funktion. Die *Left_table_source* Tabellenwertfunktionen enthalten jedoch darf keine Argumente, die Spalten aus der *Right_table_source*.  
  
 Der APPLY-Operator funktioniert folgendermaßen, um die Tabellenquelle für die FROM-Klausel zu produzieren:  
  
1.  Wertet *Right_table_source* für jede Zeile von der *Left_table_source* um Rowsets zu erstellen.  
  
     Die Werte in der *Right_table_source* richten sich nach *Left_table_source*. *Right_table_source* etwa folgendermaßen dargestellt werden kann: `TVF(left_table_source.row)`, wobei `TVF` ist eine Funktion mit Tabellenrückgabe.  
  
2.  Kombiniert die Resultsets werden für jede Zeile in der Auswertung erzeugt *Right_table_source* mit der *Left_table_source* durch eine UNION ALL-Operation.  
  
     Die Liste der Spalten, die durch das Ergebnis des APPLY-Operators erstellt, ist der Satz von Spalten aus der *Left_table_source* kombiniert, die mit der Liste der Spalten aus der *Right_table_source*.  
  
## <a name="using-pivot-and-unpivot"></a>Verwenden von PIVOT und UNPIVOT  
 Die *Pivot_column* und *Value_column* sind Gruppierungsspalten, die vom PIVOT-Operator verwendet werden. PIVOT führt dabei die folgenden Schritte aus, um das Ausgaberesultset zu erhalten:  
  
1.  Führt eine GROUP BY-Klausel für die *Input_table* für die Gruppierung und produziert eine Ausgabezeile für jede Gruppe.  
  
     Das Gruppieren von Spalten in der Ausgabezeile Abrufen der entsprechenden Werte für diese Gruppe in der *Input_table*.  
  
2.  Generiert folgendermaßen Werte für die Spalten in der Spaltenliste für jede Ausgabezeile:  
  
    1.  Zusätzliches Gruppieren der Zeilen in der GROUP BY im vorherigen Schritt für generiert die *Pivot_column*.  
  
         Für jede Spalte in der *Column_list*, Auswählen einer Untergruppe, das die Bedingung erfüllt:  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *Aggregate_function* erfolgt eine Auswertung anhand der *Value_column* in dieser Untergruppe und das Ergebnis wird zurückgegeben als Wert des entsprechenden *Output_column*. Wenn die Untergruppe leer ist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert einen null-Wert für diesen *Output_column*. Wenn die Aggregatfunktion COUNT ist und die Untergruppe leer ist, wird null (0) zurückgegeben.  

> [!NOTE]
> Die Spalten-IDs in der `UNPIVOT` -Klausel folgen die katalogsortierung. Für [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], die Sortierung ist immer `SQL_Latin1_General_CP1_CI_AS`. Für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] teilweise eigenständige Datenbanken, die Sortierung ist immer `Latin1_General_100_CI_AS_KS_WS_SC`. Wenn die Spalte mit den anderen Spalten, und klicken Sie dann auf eine Collate-Klausel kombiniert wird (`COLLATE DATABASE_DEFAULT`) ist erforderlich, um Konflikte zu vermeiden.   
  
 Weitere Informationen zu PIVOT und UNPIVOT, einschließlich Beispielen, finden Sie unter [mithilfe von PIVOT und UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigungen für die DELETE-, SELECT- oder UPDATE-Anweisung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-simple-from-clause"></a>A. Verwenden einer einfachen FROM-Klausel  
 Im folgenden Beispiel werden die `TerritoryID`- und `Name`-Spalten aus der `SalesTerritory`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank abgerufen.  
  
```sql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. Verwenden der TABLOCK- und HOLDLOCK-Optimierungshinweise  
 Die folgende Teiltransaktion zeigt, wie eine explizite freigegebene Tabellensperre auf die `Employee`-Tabelle angewendet und der Index gelesen wird. Die Sperre bleibt während der gesamten Transaktion bestehen.  
  
```sql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. Verwenden der SQL-92-CROSS JOIN-Syntax  
 Im folgenden Beispiel wird das Kreuzprodukt der beiden Tabellen `Employee` und `Department` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Eine Liste aller möglichen Kombinationen von `BusinessEntityID` Zeilen und alle `Department` -namenspalten wird zurückgegeben.  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. Verwenden der SQL-92-FULL OUTER JOIN-Syntax  
 Im folgenden Beispiel werden der Produktname und alle zugehörigen Kaufaufträge in der `SalesOrderDetail`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Außerdem werden Kaufaufträge zurückgegeben, für die kein Produkt in der `Product`-Tabelle aufgeführt ist. Darüber hinaus werden Produkte mit einem anderen Kaufauftrag als dem in der `Product`-Tabelle aufgeführten Kaufauftrag zurückgegeben.  
  
```sql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. Verwenden der SQL-92 LEFT OUTER JOIN-Syntax  
 Im folgenden Beispiel werden zwei Tabellen über `ProductID` verknüpft und die nicht entsprechenden Zeilen aus der linken Tabelle aufbewahrt. Die `Product`-Tabelle wird mit der `SalesOrderDetail`-Tabelle über die `ProductID`-Spalten in den beiden Tabellen verglichen. Im Resultset werden alle bestellten und nicht bestellten Produkte angezeigt.  
  
```sql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. Verwenden der SQL-92-INNER JOIN-Syntax  
 Im folgenden Beispiel werden alle Produktnamen und Verkaufsauftragsnummern zurückgegeben.  
  
```sql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. Verwenden der SQL-92-RIGHT OUTER JOIN-Syntax  
 Im folgenden Beispiel werden zwei Tabellen über `TerritoryID` verknüpft und die nicht entsprechenden Zeilen aus der rechten Tabelle aufbewahrt. Die `SalesTerritory`-Tabelle wird mit der `SalesPerson`-Tabelle über die `TerritoryID`-Spalte in den beiden Tabellen verglichen. Im Resultset werden alle Vertriebsmitarbeiter unabhängig davon aufgeführt, ob ihnen ein Gebiet zugewiesen ist.  
  
```sql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. Verwenden von HASH- und MERGE-Joinhinweisen  
 Im folgenden Beispiel werden die drei Tabellen `Product`, `ProductVendor` und `Vendor` verknüpft, um eine Liste der Produkte und deren Anbieter zu produzieren. Der Abfrageoptimierer verknüpft `Product` und `ProductVendor` (`p` und `pv`) mit einem MERGE-Join. Das Ergebnis des MERGE-Joins von `Product` und `ProductVendor` (`p` und `pv`) wird mit der `Vendor`-Tabelle verknüpft und ergibt (`p` und `pv`) und `v`. Dabei wird ein HASH-Join angewendet.  
  
> [!IMPORTANT]  
>  Nach Angabe eines Joinhinweises muss das INNER-Schlüsselwort für jeder auszuführende innere Join explizit angegeben werden.  
  
```sql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>I. Verwenden einer abgeleiteten Tabelle  
 Im folgenden Beispiel wird eine abgeleitete Tabelle verwendet. Mit einer `SELECT`-Anweisung nach der `FROM`-Klausel werden die Vor- und Nachnamen aller Mitarbeiter und ihre Wohnorte zurückgegeben.  
  
```sql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. Verwenden von TABLESAMPLE, um Daten von einem Beispiel für Zeilen in einer Tabelle zu lesen  
 Im folgenden Beispiel wird `TABLESAMPLE` in der `FROM`-Klausel verwendet, um ungefähr `10`-Prozent aller Zeilen in der `Customer`-Tabelle zurückzugeben.  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>K. Verwenden von APPLY  
 Im folgenden Beispiel wird vorausgesetzt, dass die folgenden Tabellen mit dem folgenden Schema in der Datenbank vorhanden sind:  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 Außerdem ist eine Tabellenwertfunktion vorhanden: `GetReports(MgrID)` gibt eine Liste der `EmpID` direkt oder indirekt unterstellten Mitarbeiter zurück (`EmpLastName`, `EmpSalary`, `MgrID`).  
  
 Im Beispiel werden mit `APPLY` alle Abteilungen und alle Mitarbeiter in dieser Abteilung zurückgegeben. Wenn eine bestimmte Abteilung keine Mitarbeiter hat, werden für diese Abteilung keine Zeilen zurückgegeben.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 Wenn die Abfrage Zeilen für diese Abteilungen ohne Mitarbeiter produzieren soll, die NULL-Werte für die Spalten `EmpID`, `EmpLastName` und `EmpSalary` produziert, verwenden Sie stattdessen `OUTER APPLY`.  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>L. Verwenden von CROSS APPLY  
 Im folgenden Beispiel wird eine Momentaufnahme aller im Plancache gespeicherten Abfragen abgerufen, indem die dynamische Verwaltungssicht `sys.dm_exec_cached_plans` abgefragt wird, um die Planhandles aller Abfragepläne im Cache abzurufen. Dann wird der `CROSS APPLY`-Operator angegeben, um die Planhandles an `sys.dm_exec_query_plan` zu übergeben. Die XML-Showplanausgabe für jeden aktuell im Plancache gespeicherten Plan wird in der `query_plan` -Spalte der zurückgegebenen Tabelle angezeigt.  
  
```sql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>M. Verwenden FOR SYSTEM_TIME  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Im folgenden Beispiel wird das Argument der FOR SYSTEM_TIME AS OF Date_time_literal_or_variable zurückzugebenden Zeilen der Tabelle, die seit dem 1. Januar 2014 tatsächliche (aktuell) waren.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 Im folgenden Beispiel wird die Date_time_literal_or_variable FOR SYSTEM_TIME FROM Date_time_literal_or_variable-Argument, um Zeilen zurückzugeben, die während des Zeitraums definiert, wie mit dem 1. Januar 2013 beginnt und endet mit dem 1. Januar 2014 aktiv waren, exklusive obere Grenze.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 Im folgenden Beispiel wird die für SYSTEM_TIME zwischen Date_time_literal_or_variable und Date_time_literal_or_variable-Argument, um zurückzugeben, alle Zeilen, die während des Zeitraums definiert, wie mit dem 1. Januar 2013 beginnt und endet mit dem 1. Januar 2014 aktiv waren, der oberen Grenze liegen.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 Im folgenden Beispiel wird der FOR SYSTEM_TIME CONTAINED IN (Date_time_literal_or_variable, Date_time_literal_or_variable)-Argument, um Zeilen zurückzugeben, die geöffnet und geschlossen wurden während des Zeitraums, der als "mit dem 1. Januar 2013 beginnt und endet mit" definiert wurden 1. Januar 2014.  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 Im folgenden Beispiel wird eine Variable statt ein Literal der Begrenzungswerte des Datums für die Abfrage bereitstellen.  
  
```sql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>N. Verwenden der INNER JOIN-syntax  
 Das folgende Beispiel gibt die `SalesOrderNumber`, `ProductKey`, und `EnglishProductName` Spalten aus der `FactInternetSales` und `DimProduct` Tabellen Where des Joinschlüssels `ProductKey`, in beiden Tabellen entspricht. Die `SalesOrderNumber` und `EnglishProductName` Spalten jeweils in eine der Tabellen nur vorhanden sein, daher ist es nicht erforderlich, den Tabellenalias mit den folgenden Spalten anzugeben, wie gezeigt; diese Aliase sind aus Gründen der Lesbarkeit. Das Wort **AS** vor dem Alias Name ist nicht erforderlich, jedoch wird empfohlen, zur besseren Lesbarkeit und dem ANSI-Standard entsprechen.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Da die `INNER` Schlüsselwort ist nicht für innere Verknüpfungen erforderlich, diese Abfrage kann als geschrieben werden:  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 Ein `WHERE` Klausel kann auch zum Erstellen von dieser Abfrage um zurückgegebenen Ergebnisse zu begrenzen. In diesem Beispiel beschränkt die Ergebnisse auf `SalesOrderNumber` höhere Werte als "SO5000":  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>O. Mithilfe der LEFT OUTER JOIN und RIGHT OUTER JOIN-syntax  
 Das folgende Beispiel verknüpft die `FactInternetSales` und `DimProduct` Tabellen in der `ProductKey` Spalten. Die linker äußerer Join-Syntax wird beibehalten, die nicht entsprechenden Zeilen aus der linken Seite (`FactInternetSales`) Tabelle. Da die `FactInternetSales` Tabelle enthält keine `ProductKey` Werte, die nicht entsprechen der `DimProduct` Tabelle, diese Abfrage gibt dieselben Zeilen wie im ersten inneren Join-Beispiel oben.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Diese Abfrage kann auch ohne formuliert werden die `OUTER` Schlüsselwort.  
  
 Rechte äußere Joins werden nicht übereinstimmenden Zeilen aus der rechten Tabelle beibehalten. Im folgende Beispiel gibt dieselben Zeilen wie im obigen linker äußerer Join-Beispiel.  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Die folgende Abfrage verwendet die `DimSalesTerritory` Tabelle als die linke Tabelle in einem linken äußeren Join. Ruft ab den `SalesOrderNumber` Werte aus der `FactInternetSales` Tabelle. Wenn es keine Aufträge für einen bestimmten sind `SalesTerritoryKey`, die Abfrage eine gibt NULL zurück, für die `SalesOrderNumber` für diese Zeile. Diese Abfrage wird sortiert nach der `SalesOrderNumber` Spalte, sodass alle NULL-Werte in dieser Spalte wird am oberen Rand der Ergebnisse angezeigt.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Diese Abfrage kann so umgeschrieben werden, mit einem rechten äußeren Join zu dieselben Ergebnisse abrufen:  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>P. Verwenden der FULL OUTER JOIN-syntax  
 Das folgende Beispiel zeigt einen vollständiger äußeren Join, die alle Zeilen aus beiden verknüpften Tabellen zurückgegeben, aber gibt NULL für Werte, die nicht übereinstimmen, aus der anderen Tabelle.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Diese Abfrage kann auch ohne formuliert werden die `OUTER` Schlüsselwort.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>Q. Verwenden der CROSS JOIN-syntax  
 Das folgende Beispiel gibt das Kreuzprodukt von der `FactInternetSales` und `DimSalesTerritory` Tabellen. Eine Liste aller möglichen Kombinationen von `SalesOrderNumber` und `SalesTerritoryKey` werden zurückgegeben. Beachten Sie das Fehlen der `ON` -Klausel in der Cross Join-Abfrage.  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>R. Verwenden einer abgeleiteten Tabelle  
 Im folgenden Beispiel wird eine abgeleitete Tabelle (eine `SELECT` Anweisung nach der `FROM` Klausel) zurückgeben der `CustomerKey` und `LastName` Spalten aller Kunden in der `DimCustomer` -Tabelle mit `BirthDate` Werte höher als 1. Januar 1970 und dem Nachnamen "Smith".  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S. Beispiel für einen Join-Hinweis reduzieren  
 Im folgenden Beispiel wird die `REDUCE` Join-Hinweis, die Verarbeitung der abgeleiteten Tabelle in der Abfrage zu ändern. Bei Verwendung der `REDUCE` Join-Hinweis in der folgenden Abfrage die `fis.ProductKey` projiziert wird, repliziert und unterschiedliche vorgenommen und dann hinzugefügt `DimProduct` während das Mischen von `DimProduct` auf `ProductKey`. Die daraus resultierende abgeleitete Tabelle wird auf verteilt `fis.ProductKey`.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="t-replicate-join-hint-example"></a>T. Beispiel für einen replizieren Join-Hinweis  
 Im folgenden Beispiel wird gezeigt, die gleiche Abfrage wie im vorherigen Beispiel, außer dass eine `REPLICATE` Join-Hinweis wird verwendet, statt die `REDUCE` Join-Hinweis. Verwenden der `REPLICATE` Hinweis bewirkt, dass die Werte in der `ProductKey` (verknüpfte) Spalte aus der `FactInternetSales` Tabelle auf allen Knoten repliziert werden sollen. Die `DimProduct` Tabelle ist verknüpft, auf die replizierten Version dieser Werte.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>U. Verwenden REDISTRIBUTE-Hinweis zum eine zufällige Verschiebung für einen Verteilungspunkt inkompatible Join zu gewährleisten.  
 Die folgende Abfrage verwendet den Abfragehinweis Redistribute-Hinweis auf einem Verteilungspunkt nicht kompatibel. Dadurch wird sichergestellt, dass der Abfrageoptimierer eine zufällige Verschiebung im Abfrageplan verwendet wird. Auch gewährleistet ist der Abfrageplan einen Verschiebevorgang Übertragung, der verschiebt eine verteilte Tabelle zu einer replizierten Tabelle sollte nicht verwendet wird.  
  
 Im folgenden Beispiel wird der REDISTRIBUTE-Hinweis eine zufällige Verschiebung für die FactInternetSales-Tabelle erzwungen, da es sich bei "ProductKey" ist die verteilungsspalte für DimProduct und nicht die verteilungsspalte für FactInternetSales.  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
