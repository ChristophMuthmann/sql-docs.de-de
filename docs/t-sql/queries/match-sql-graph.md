---
title: "Übereinstimmung (SQL-Diagramm) | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db211fa0988f2dbe6a72291f898d670d44d3f215
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="match-transact-sql"></a>Übereinstimmung (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

  Gibt eine Suchbedingung für ein Diagramm an. Übereinstimmung kann nur mit Graph Knoten und Rand Tabellen in der SELECT-Anweisung als Teil der WHERE-Klausel verwendet werden. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
    {<node_alias> { 
                     { <-( <edge_alias> )- } 
                   | { -( <edge_alias> )-> }
                 <node_alias> 
                 } 
     }
     [ { AND } { ( <graph_search_pattern> ) } ]
     [ ,...n ]
  
<node_alias> ::=
    node_table_name | node_alias 

<edge_alias> ::=
    edge_table_name | edge_alias
```

## <a name="arguments"></a>Argumente  
*graph_search_pattern*  
Gibt das Muster für Suchen oder einen Pfad im Diagramm zu durchlaufen. Dieses Muster wird ASCII-Grafiken Syntax verwendet, um einen Pfad im Diagramm zu durchlaufen. Das Muster wird von einem Knoten zu einem anderen über eine Kante, in die Richtung des Pfeils bereitgestellt. Edge-Namen oder Aliase werden in Parantheses bereitgestellt. Node Names oder Aliase werden an beiden Enden des Pfeils angezeigt. Der Pfeil gelangen in beide Richtungen im Muster.

*node_alias*  
Name oder Alias, der eine Knotentabelle in der FROM-Klausel angegeben.

*edge_alias*  
Name oder Alias einer Edge-Tabelle in der FROM-Klausel angegeben.


## <a name="remarks"></a>Hinweise  
Die Knotennamen in Übereinstimmung können wiederholt werden.  Ein Knoten kann sein, also eine beliebige Anzahl von Zeiten in der gleichen Abfrage durchlaufen.  
Ein Edge-Name kann nicht in Übereinstimmung wiederholt werden.  
Ein Rand in beide Richtungen zeigen kann muss, jedoch eine explizite Richtung.  
ODER und NOT-Operatoren werden in das Muster nicht unterstützt. Übereinstimmung kann mit anderen Ausdrücken verwenden und in der WHERE-Klausel kombiniert werden. Kombinieren sie jedoch mit anderen Ausdrücken, die mit OR oder nicht wird nicht unterstützt. 

## <a name="examples"></a>Beispiele  
### <a name="a--find-a-friend"></a>A.  Suchen Sie einen "Friend" 
 Das folgende Beispiel erstellt eine Tabelle der Person-Knoten und Freunde Rahmentabelle, einige Daten einfügt und verwendet dann Übereinstimmung Friends von Alice, eine Person im Diagramm gefunden.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';

 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  Suchen Sie einen "Friend" "Friend"
 Im folgenden Beispiel wird versucht, einen "Friend" Alice "Friend" zu finden. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  Weitere `MATCH` Muster
 Im folgenden werden einige weitere Möglichkeiten, die in denen ein Muster in Übereinstimmung angegeben werden kann.

 ```
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>Siehe auch  
 [Erstellen von Tabellen &#40; Diagramm der SQL &#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL-Diagramm)](../../t-sql/statements/insert-sql-graph.md)]  
 [Diagramm mit SQL Server-2017 verarbeiten](../../relational-databases/graphs/sql-graph-overview.md)  

