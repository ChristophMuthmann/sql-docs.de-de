---
title: Erstellen der Tabelle (SQL-Diagramm) | Microsoft Docs
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
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c32a8c4f683f20c4384089c1d2552614090f9b3d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-sql-graph"></a>Erstellen der Tabelle (SQL-Diagramm)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Erstellt eine neue Tabelle der SQL-Diagramm entweder als eine `NODE` oder eine `EDGE` Tabelle. 
  
> [!NOTE]   
>  Standard Transact-SQL-Anweisungen finden Sie unter [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
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
Dieses Dokument Listet nur die SQL-Diagramm für Argumente. Eine vollständige Liste und Beschreibung der unterstützten Argumente finden Sie unter [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *Datenbankname*    
 Der Name der Datenbank, in der die Tabelle erstellt wird. *Database_name* müssen den Namen einer vorhandenen Datenbank angeben. Wenn nicht angegeben, *Database_name* Standardwerte auf die aktuelle Datenbank. Der Anmeldename für die aktuelle Verbindung muss einer vorhandenen Benutzer-ID in der durch den angegebenen Datenbank zugeordnet werden *Database_name*, und diese Benutzer-ID muss über CREATE TABLE-Berechtigungen verfügen.  
  
 *schema_name*    
 Der Name des Schemas, zu dem die neue Tabelle gehört.  
  
 *Tabellenname*    
 Ist der Name der Tabelle Knoten oder Edge. Tabellennamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md). *TABLE_NAME* kann maximal 128 Zeichen enthalten, mit Ausnahme von lokalen temporären Tabellennamen (Namen mit dem Präfix ein einzelnen Nummernzeichen (#)), die 116 Zeichen nicht überschreiten.  
  
 KNOTEN   
 Erstellt eine Knotentabelle.

 EDGE  
 Erstellt eine Rahmentabelle an.  
  
## <a name="remarks"></a>Hinweise  
Erstellen eine temporäre Tabelle als Knoten oder Edge-Tabelle wird nicht unterstützt.  

Erstellen eine Knoten oder Edge-Tabelle als eine temporale Tabelle wird nicht unterstützt.

Stretch-Datenbank ist für Knoten oder Edge-Tabelle nicht unterstützt.

Knoten oder Edge Tabellen darf nicht auf externe Tabellen (keine Polybase-Unterstützung für Diagramm Tabellen) sein. 
  
 
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-a-node-table"></a>A. Erstellen einer `NODE` Tabelle
 Im folgende Beispiel wird gezeigt, wie zum Erstellen einer `NODE` Tabelle

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Erstellen einer `EDGE` Tabelle
Die folgenden Beispiele zeigen, wie erstellen `EDGE` Tabellen

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


## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL-Diagramm)](../../t-sql/statements/insert-sql-graph.md)]  
 [Diagramm mit SQL Server-2017 verarbeiten](../../relational-databases/graphs/sql-graph-overview.md)


