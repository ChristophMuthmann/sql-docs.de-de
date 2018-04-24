---
title: INSERT (SQL-Graph) | Microsoft-Dokumentation
description: INSERT-Syntax für SQL-Graph-Knoten- oder Edgetabellen.
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: d7d93bfc1ffa3e926bc8e9dcdea46183a0801155
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="insert-sql-graph"></a>INSERT (SQL-Graph)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Fügt einer `node`- oder `edge`-Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mindestens eine Zeile hinzu. 

> [!NOTE]   
>  Standard Transact-SQL-Anweisungen finden Sie unter [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>INSERT INTO – Syntax für Knotentabellen 
Die Syntax für das Einfügen in eine Knotentabelle entspricht der einer regulären Tabelle. 

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
 In diesem Dokument werden Argumente für SQL-Graph beschrieben. Eine vollständige Liste und Beschreibung der unterstützten Argumente in der INSERT-Anweisung finden Sie unter [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).

 INTO  
 Ein optionales Schlüsselwort, das zwischen `INSERT` und der Zieltabelle verwendet werden kann.  
  
 *search_condition_with_match*   
 Die `MATCH`-Klausel kann während des Einfügens in eine Knoten- oder Edgetabelle in einer geschachtelten Abfrage verwendet werden. Die `MATCH`-Abfragesyntax finden Sie unter [GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md).

 *graph_search_pattern*   
 Suchmuster, das der `MATCH`-Klausel als Teil des Graph-Prädikats bereitgestellt wird.

 *edge_table_column_list*   
 Benutzer müssen Werte für `$from_id` und `$to_id` angeben, wenn sie etwas in eine Edgetabelle einfügen. Wenn ein Wert nicht angegeben oder in eine dieser Spalten NULL eingefügt wird, wird ein Fehler zurückgegeben. 
  

## <a name="remarks"></a>Remarks  
Das Einfügen in eine Knotentabelle entspricht dem Einfügen in eine relationale Tabelle. Werte für die $node_id-Spalte werden automatisch generiert.

Beim Einfügen in eine Edgetabelle müssen Benutzer Werte für die Spalten `$from_id` und `$to_id` angeben.   

Masseneinfügung in Knotentabellen entspricht der Masseneinfügung in eine relationale Tabelle.

Vor der Masseneinfügung in eine Edgetabelle müssen die Knotentabellen importiert werden. Anschließend können Werte für `$from_id` und `$to_id` aus der `$node_id`-Spalte der Knotentabelle extrahiert werden und als Edges eingefügt werden. 

  
### <a name="permissions"></a>Berechtigungen  
 Die INSERT-Berechtigung ist für die Zieltabelle erforderlich.  
  
 Mitglieder der festen Serverrolle **sysadmin**, der festen Datenbankrollen **db_owner** und **db_datawriter** und der Tabellenbesitzer erhalten standardmäßig INSERT-Berechtigungen. Mitglieder der Rollen **sysadmin**, **db_owner** und **db_securityadmin** sowie der Tabellenbesitzer können Berechtigungen an andere Benutzer übertragen.  
  
 Zum Ausführen von INSERT mit der Option BULK der OPENROWSET-Funktion müssen Sie Mitglied der festen Serverrolle **sysadmin** oder der festen Serverrolle **bulkadmin** sein.  
  

## <a name="examples"></a>Beispiele  
  
#### <a name="a--insert-into-node-table"></a>A.  Einfügen in Knotentabellen  
 Im folgenden Beispiel wird eine Knotentabelle für Personen erstellt, und es werden zwei Reihen in diese Tabelle eingefügt.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  Einfügen in Edgetabellen  
 Im folgenden Beispiel wird eine Edgetabelle für Freunde erstellt und ein Edge in diese Tabelle eingefügt.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Graph Processing with SQL Server 2017 (Graph-Verarbeitung mit SQL Server-2017)](../../relational-databases/graphs/sql-graph-overview.md)  


