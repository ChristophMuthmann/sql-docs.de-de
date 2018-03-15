---
title: CREATE TABLE (SQL-Graph) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe8ace1b8f8c55c14d4807514fcb1436f6966fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (SQL-Graph)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Erstellt entweder als `NODE`- oder `EDGE`-Tabelle eine neue SQL-Graph-Tabelle. 
  
> [!NOTE]   
>  Standardanweisungen für Transact-SQL finden Sie unter [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>Argumente  
In diesem Dokument werden nur Argumente für SQL-Graph aufgelistet. Eine vollständige Liste und Beschreibung der unterstützten Argumente finden Sie unter [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).

 *database_name*    
 Der Name der Datenbank, in der die Tabelle erstellt wird. *database_name* muss dem Namen einer vorhandenen Datenbank entsprechen. Wird *database_name* nicht angegeben, wird standardmäßig die aktuelle Datenbank verwendet. Der Anmeldename für die aktuelle Verbindung muss einer vorhandenen Benutzer-ID in der durch *database_name* angegebenen Datenbank zugeordnet sein. Diese Benutzer-ID muss über CREATE TABLE-Berechtigungen verfügen.  
  
 *schema_name*    
 Der Name des Schemas, zu dem die neue Tabelle gehört.  
  
 *table_name*    
 Der Name der Knoten- oder Edgetabelle. Tabellennamen müssen die Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) erfüllen. *table_name* kann höchstens 128 Zeichen aufweisen, ausgenommen lokale temporäre Tabellennamen (Namen mit einem einzelnen Nummernzeichen (#) als Präfix), bei denen maximal 116 Zeichen zulässig sind.  
  
 NODE   
 Erstellt eine Knotentabelle

 EDGE  
 Erstellt eine Edgetabelle  
  
## <a name="remarks"></a>Remarks  
Das Erstellen einer temporären Tabelle als Knoten- oder Edgetabelle wird nicht unterstützt.  

Das Erstellen einer Knoten- oder Edgetabelle als temporale Tabelle wird nicht unterstützt.

Stretch Database wird für Knoten- oder Edgetabellen nicht unterstützt.

Knoten- oder Edgetabellen können keine externen Tabellen sein (es besteht keine Unterstützung von PolyBase für Graph-Tabellen). 
  
 
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-a-node-table"></a>A. Erstellen einer `NODE`-Tabelle
 Im folgenden Beispiel wird das Erstellen einer `NODE`-Tabelle veranschaulicht.

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Erstellen einer `EDGE`-Tabelle
Im folgenden Beispiel wird das Erstellen von `EDGE`-Tabellen veranschaulicht.

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Graph Processing with SQL Server 2017 (Graph-Verarbeitung mit SQL Server-2017)](../../relational-databases/graphs/sql-graph-overview.md)

