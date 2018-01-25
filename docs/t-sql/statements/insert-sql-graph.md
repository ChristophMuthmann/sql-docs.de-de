---
title: INSERT (SQL-Diagramm) | Microsoft Docs
description: "Fügen Sie die Syntax für das Diagramm der SQL-Knoten oder Edge-Tabellen."
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: "1"
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6bac7f1d7da67f319a9c84425b370bb61a35ca19
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="insert-sql-graph"></a>INSERT (SQL-Diagramm)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Fügt eine oder mehrere Zeilen auf einer `node` oder `edge` in Tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]   
>  Standard Transact-SQL-Anweisungen finden Sie unter [Tabelle einfügen (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>Einfügen von Knoten Table-Syntax 
Die Syntax für das Einfügen in eine Knotentabelle entspricht, die von einer regulären Tabelle. 

```  
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>Argumente  
 Dieses Dokument beschreibt die Argumente, die für SQL-Diagramm. Eine vollständige Liste und Beschreibung der unterstützten Argumente in der INSERT-Anweisung finden Sie unter [Tabelle einfügen (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 Ein optionales Schlüsselwort, das zwischen verwendet werden können `INSERT` und die Zieltabelle.  
  
 *search_condition_with_match*   
 `MATCH`Klausel kann beim Einfügen in einen Knoten oder Edge-Tabelle in einer Unterabfrage verwendet werden. Für `MATCH` Anweisungssyntax, finden Sie unter [GRAPH Übereinstimmung (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 Suchmuster bereitgestellt, um `MATCH` -Klausel als Teil des Diagramm-Prädikats.

 *edge_table_column_list*   
 Benutzer müssen Geben Sie Werte für `$from_id` und `$to_id` beim Einfügen in eine Kante. Wenn kein Wert angegeben ist, oder NULL-Werte in diesen Spalten eingefügt werden, wird ein Fehler zurückgegeben werden. 
  

## <a name="remarks"></a>Hinweise  
Einfügen in einen Knoten entspricht der in einer relationalen Tabelle eingefügt. Werte für die $ "node_id" Spalte werden automatisch generiert.

Beim Einfügen in eine Rahmentabelle, müssen Benutzer geben Sie Werte für `$from_id` und `$to_id` Spalten.   

BULK Insert bleibt für Knotentabelle ist identisch mit der einer relationalen Tabelle.

Bevor die masseneinfügung in eine Rahmentabelle eingefügt müssen die Knoten Tabellen importiert werden. Werte für `$from_id` und `$to_id` können dann extrahiert werden, aus der `$node_id` -Spalte der Knotentabelle und als Ränder eingefügt. 

  
### <a name="permissions"></a>Berechtigungen  
 Die INSERT-Berechtigung ist für die Zieltabelle erforderlich.  
  
 Legen Sie Berechtigungen erhalten standardmäßig Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** und **Db_datawriter** festen Datenbankrollen und der Besitzer der Tabelle. Mitglieder der **Sysadmin**, **Db_owner**, und die **Db_securityadmin** Rollen sowie der Tabellenbesitzer können Berechtigungen an andere Benutzer übertragen.  
  
 Zum Ausführen von INSERT mit der Option BULK der OPENROWSET-Funktion muss ein Mitglied der **Sysadmin** feste Serverrolle oder die **Bulkadmin** festen Serverrolle.  
  

## <a name="examples"></a>Beispiele  
  
#### <a name="a--insert-into-node-table"></a>A.  Knotentabelle einfügen  
 Im folgende Beispiel wird eine Tabelle der Person-Knoten erstellt und 2 Zeilen in dieser Tabelle eingefügt.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  Legen Sie in der Rahmentabelle  
 Im folgende Beispiel wird eine "Friend" Edge-Tabelle erstellt und eine Kante in die Tabelle eingefügt.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>Siehe auch  
 [INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Diagramm mit SQL Server-2017 verarbeiten](../../relational-databases/graphs/sql-graph-overview.md)  


