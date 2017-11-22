---
title: SQL-Graph-Architektur | Microsoft Docs
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: graphs
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: 
caps.latest.revision: "1"
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4ca6de15012a8fb929c207ab1a79a41607bd74cc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-graph-architecture"></a>Architektur der SQL-Diagramm  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Erfahren Sie, wie SQL-Diagramm entworfen wird. Die Grundlagen wissen es einfacher zu verstehen, andere SQL-Diagramm Artikel.
 
## <a name="sql-graph-database"></a>SQL-Graph-Datenbank
Benutzer können einem Diagramm pro Datenbank erstellen. Ein Diagramm ist eine Auflistung von Knoten und Edge-Tabellen. Knoten oder Edge Tabellen unter dem alle Schemas in der Datenbank erstellt werden, aber sie alle für ein logisches Diagramm gehören. Eine Knotentabelle ist die Auflistung von ähnlichen Typ der Knoten. Beispielsweise enthält eine Knoten-Personentabelle alle Knoten der Person, die zu einem Diagramm gehören. Auf ähnliche Weise wird eine Rahmentabelle eine Auflistung von ähnlichen Typ der Kanten. Beispielsweise enthält eine Rahmentabelle Freunde alle Seiten, die eine Person an eine andere Person eine Verbindung herstellen. Da Knoten und Kanten in Tabellen gespeichert sind, werden die meisten Vorgänge für reguläre Tabellen unterstützt für Knoten oder Edge-Tabellen unterstützt. 
 
 
![Architektur der SQL-Diagramm](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql Graph-Datenbankarchitektur")   

Abbildung 1: Diagramm der SQL-Datenbankarchitektur
 
## <a name="node-table"></a>Knotentabelle
Eine Knotentabelle stellt eine Entität in einem Diagramm Schema. Jedes Mal, wenn eine Knotentabelle zusammen mit den benutzerdefinierten Spalten einen impliziten erstellt wird, `$node_id` Spalte erstellt, die einen bestimmten Knoten in der Datenbank eindeutig identifiziert. Die Werte in `$node_id` werden automatisch generiert und sind eine Kombination aus `object_id` dieser Knotentabelle und eine intern erzeugte Bigint-Wert. Jedoch, wenn die `$node_id` Spalte ausgewählt ist, ein berechneter Wert in Form einer JSON-Zeichenfolge wird angezeigt. Darüber hinaus `$node_id` Pseudospalten handelt, das einen internen Namen mit hexadezimalen Zeichenfolge in der er zugeordnet ist. Bei Auswahl `$node_id` aus der Tabelle den Namen der Spalte hostnamensadresse `$node_id_<hex_string>`. Mithilfe von Pseudo-Spaltennamen in Abfragen ist die empfohlene Methode von Abfragen an das interne `$node_id` Spalten- und hexadezimale Zeichenfolge mit interner Name sollte vermieden werden.

Es wird empfohlen, dass Benutzer erstellen eine unique-Einschränkung oder einen index auf die `$node_id` Spalte zum Zeitpunkt der Erstellung des Knotentabelle, aber wenn Sie eine nicht erstellt, den Standardwert eindeutiger nicht gruppierten Index wird automatisch erstellt. Allerdings wird ein Index für eine Graph Pseudo-Spalte für die zugrunde liegende interne Spalten erstellt. D. h. ein Index erstellt, auf die `$node_id` Spalte erscheint auf der internen `graph_id_<hex_string>` Spalte.   


## <a name="edge-table"></a>Edge-Tabelle
Eine Rahmentabelle stellt eine Beziehung in einem Diagramm dar. Ränder werden immer weitergeleitet, und verbinden Sie zwei Knoten. Eine Rahmentabelle kann Benutzer Modell viele-zu-viele-Beziehungen im Diagramm. Eine Rahmentabelle kann oder möglicherweise keine benutzerdefinierten Attribute darin haben. Jedes Mal, wenn eine Rahmentabelle erstellt wird, zusammen mit den benutzerdefinierten Attributen, werden drei implizite Spalten in der Rahmentabelle erstellt:

|Spaltenname    |Description  |
|---   |---  |
|`$edge_id`   |Identifiziert eindeutig eine bestimmte Kante in der Datenbank. Es wird eine generierte Spalte und der Wert ist eine Kombination von Object_id die Rahmentabelle und einem intern generierten Bigint-Wert. Jedoch, wenn die `$edge_id` Spalte ausgewählt ist, ein berechneter Wert in Form einer JSON-Zeichenfolge wird angezeigt. `$edge_id`ist eine Pseudospalte, die einen internen Namen mit hexadezimalen Zeichenfolge in der er zugeordnet ist. Bei Auswahl `$edge_id` aus der Tabelle den Namen der Spalte hostnamensadresse `$edge_id_\<hex_string>`. Mithilfe von Pseudo-Spaltennamen in Abfragen ist die empfohlene Methode von Abfragen an das interne `$edge_id` Spalten- und hexadezimale Zeichenfolge mit interner Name sollte vermieden werden. |
|`$from_id`   |Speichert die `$node_id` des Knotens, von der Rand, stammt.  |
|`$to_id`   |Speichert die `$node_id` des Knotens, an dem am Rand wird beendet. |

Werden die Knoten, die eine bestimmte Kante eine Verbindung herstellen kann, im eingefügten Daten unterliegt den `$from_id` und `$to_id` Spalten. In der ersten Version ist es nicht möglich, die Einschränkungen für die Edge-Tabelle, um zu verhindern, dass er alle zwei Arten von Knoten verbinden zu definieren. D. h. kann ein Rand zwei Knoten im Diagramm, unabhängig von deren Typen verbinden.

Ähnlich wie die `$node_id` Spalte, es wird empfohlen, dass Benutzer auf ein eindeutiger Index oder eine Einschränkung erstellen die `$edge_id` Spalte zum Zeitpunkt der Erstellung der Rahmentabelle, aber wenn Sie eine nicht erstellt, ein eindeutiger nicht gruppierter Index wird automatisch erstellt, auf Standard Diese Spalte. Allerdings wird ein Index für eine Graph Pseudo-Spalte für die zugrunde liegende interne Spalten erstellt. D. h. ein Index erstellt, auf die `$edge_id` Spalte erscheint auf der internen `graph_id_<hex_string>` Spalte. Es wird außerdem empfohlen, für OLTP-Szenarien, die Benutzer auf einen Index erstellen (`$from_id`, `$to_id`)-Spalten sowie für schnellere Suchvorgänge in Richtung des Rands.  

Abbildung 2 zeigt, wie Knoten und Edge-Tabellen in der Datenbank gespeichert werden. 

![Person Freunde Tabellen](../../relational-databases/graphs/media/person-friends-tables.png "Person-Knoten und Freunde edge-Tabellen")   

Abbildung 2: Knoten- und Edge-tabellendarstellung



## <a name="metadata"></a>Metadaten
Verwenden Sie diese Metadatenansichten, um Attribute von einem Knoten oder Edge-Tabelle anzuzeigen.
 
### <a name="systables"></a>sys.tables
Die folgenden neuen, bit-Typ, werden Spalten hinzugefügt werden, um SYS. TABELLEN. Wenn `is_node` auf 1, der angibt, dass die Tabelle eine Knotentabelle festgelegt ist und wenn `is_edge` auf 1, der angibt, dass die Tabelle eine Rahmentabelle festgelegt ist.
 
|Spaltenname |Datentyp |Description |
|--- |---|--- |
|is_node |bit |1 = Dies ist eine Knotentabelle |
|is_edge |bit |1 = Dies ist eine Rahmentabelle |
 
### <a name="syscolumns"></a>sys.columns
Die `sys.columns` -Sicht enthält zusätzliche Spalten `graph_type` und `graph_type_desc`, um anzugeben, dass den Typ der Spalte in Knoten und Edge-Tabellen.
 
|Spaltenname |Datentyp |Description |
|--- |---|--- |
|graph_type |int |Interne Spalte mit einem Satz von Werten. Die Werte liegen zwischen 1 bis 8 für Graph-Spalten und NULL für andere.  |
|graph_type_desc |nvarchar(60)  |interne Spalte mit einem Satz von Werten |
 
Die folgende Tabelle enthält die gültigen Werte für `graph_type` Spalte

|Spaltenwert  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns`Außerdem speichert Informationen zu impliziten Spalten in Tabellen Knoten oder Edge erstellt. Folgende Informationen kann von sys.columns abgerufen werden, jedoch nicht Benutzern diese Spalten auswählen, aus einem Knoten oder Edge-Tabelle. 

Impliziten Spalten in einer Knotentabelle  
|Spaltenname    |Datentyp  |is_hidden  |Anmerkung  |
|---  |---|---|---  |
|Graph_id_\<Hex_string > |bigint |1  |interne Graph_id-Spalte  |
|$Node_id_\<Hex_string > |NVARCHAR   |0  |Externe Knoten-Id-Spalte  |

Impliziten Spalten in einer Rahmentabelle  
|Spaltenname    |Datentyp  |is_hidden  |Anmerkung  |
|---  |---|---|---  |
|Graph_id_\<Hex_string > |bigint |1  |interne Graph_id-Spalte  |
|$Edge_id_\<Hex_string > |NVARCHAR   |0  |externe Edge-Id-Spalte  |
|From_obj_id_\<Hex_string >  |INT    |1  |interne zu Objekt-Id von Knoten  |
|From_id_\<Hex_string >  |bigint |1  |Interne aus Knoten graph_id  |
|$From_id_\<Hex_string > |NVARCHAR   |0  |externe aus Knoten-id  |
|To_obj_id_\<Hex_string >    |INT    |1  |interne Objekt-ID von Knoten  |
|To_id_\<Hex_string >    |bigint |1  |Für Knoten Graph_id intern  |
|$To_id_\<Hex_string >   |NVARCHAR   |0  |externe Knoten-ID  |
 
### <a name="system-functions"></a>Systemfunktionen
Die folgenden integrierten Funktionen hinzugefügt werden. Dies hilft Benutzern, die Informationen aus den generierten Spalten extrahiert werden. Beachten Sie, dass diese Methoden die Eingaben des Benutzers nicht überprüft werden. Wenn der Benutzer ein ungültiges gibt `sys.node_id` die-Methode des entsprechenden Nachrichtenteils zu extrahieren und zurückzugeben. OBJECT_ID_FROM_NODE_ID dauert beispielsweise ein `$node_id` als Eingabe und gibt die Object_id zurück, der Tabelle, der dieser Knoten gehört zu einem. 
 
|Integrierte   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Extrahieren Sie die Object_id aus einer "node_id"  |
|GRAPH_ID_FROM_NODE_ID  |Extrahieren Sie die Graph_id aus einem "node_id"  |
|NODE_ID_FROM_PARTS |Erstellen Sie eine "node_id" aus einem Object_id und eine graph_id  |
|OBJECT_ID_FROM_EDGE_ID |Extrahieren von Object_id aus edge_id  |
|GRAPH_ID_FROM_EDGE_ID  |Extrahieren Sie die Identität aus edge_id  |
|EDGE_ID_FROM_PARTS |Erstellen von Edge_id von Object_id und Identität  |



## <a name="transact-sql-reference"></a>Transact-SQL-Referenz 
Erfahren Sie, den [!INCLUDE[tsql-md](../../includes/tsql-md.md)] Erweiterungen eingeführt in SQL Server und Azure SQL-Datenbank, die ermöglichen, erstellen und Abfragen von Graph-Objekte. Die Abfrage-spracherweiterungen können die Abfrage und durchlaufen Sie das Diagramm mit ASCII-ClipArt-Syntax.
 
### <a name="data-definition-language-ddl-statements"></a>Anweisungen von Data Definition Language (DDL)
|Task   |Verwandtes Thema  |Hinweise
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE `wird jetzt erweitert, um das Erstellen einer Tabelle als Knoten oder EDGE als unterstützt. Beachten Sie, dass eine Rahmentabelle möglicherweise keine Benutzer ggf. benutzerdefinierten Attributen.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Knoten und Edge-Tabellen können geändert werden, die gleiche Weise wie eine relationale Tabelle ist, verwendet die `ALTER TABLE`. Benutzer können hinzufügen oder Ändern von benutzerdefinierten Spalten, Indizes oder Einschränkungen. Allerdings Ändern von internen Graph Spalten, z. B. `$node_id` oder `$edge_id`, führt zu einem Fehler.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Benutzer können Indizes für Pseudospalten und benutzerdefinierter Spalten in Knoten und Edge-Tabellen erstellen. Alle Indextypen werden unterstützt, einschließlich gruppierten und nicht gruppierten columnstore-Indizes.  |
|DROP TABLE |[DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)  |Knoten und Edge-Tabellen können gelöscht werden, die gleiche Weise wie eine relationale Tabelle ist, verwendet die `DROP TABLE`. In dieser Version sind jedoch keine Einschränkungen aus, um sicherzustellen, dass keine Kanten zeigen Sie auf einen gelöschten Knoten kaskadierenden Löschen des Randes, beim Löschen eines Knotens oder Knotentabelle wird nicht unterstützt. Es wird empfohlen, wenn eine Knotentabelle gelöscht wird, Benutzer alle Ränder verbunden, auf die Knoten in dieser Knotentabelle manuell, um die Integrität des Diagramms verwalten ablegen.  |


### <a name="data-manipulation-language-dml-statements"></a>DDL-Anweisungen Data Manipulation Language (DML)
|Task   |Verwandtes Thema  |Hinweise
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|In einer Knotentabelle eingefügt wird unterscheidet sich nicht in einer relationalen Tabelle eingefügt. Die Werte für `$node_id` Spalte wird automatisch generiert. Beim Einfügen eines Werts in `$node_id` oder `$edge_id` Spalte führt zu einem Fehler. Benutzer müssen Geben Sie Werte für `$from_id` und `$to_id` Spalten beim Einfügen in eine Rahmentabelle. `$from_id`und `$to_id` sind die `$node_id` Werte der Knoten, die ein bestimmter Rand verbindet.  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Daten aus Knoten oder Edge-Tabellen können auf gleiche Weise gelöscht werden, da sie vom relationalen Tabellen gelöscht werden. In dieser Version sind jedoch keine Einschränkungen aus, um sicherzustellen, dass keine Kanten zeigen Sie auf einen gelöschten Knoten kaskadierten Löschung Rand beim Löschen eines Knotens wird nicht unterstützt. Es wird empfohlen, dass wenn ein Knoten gelöscht wurde, die verbindenden Rändern für diesen Knoten ebenfalls gelöscht werden um die Integrität des Diagramms beibehalten.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |Werte in den benutzerdefinierten Spalten können mithilfe der UPDATE-Anweisung aktualisiert werden. Aktualisieren der Spalten interne Graph `$node_id`, `$edge_id`, `$from_id` und `$to_id` ist nicht zulässig.  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE`Anweisung wird für einen Knoten oder Edge-Tabelle nicht unterstützt.  |


### <a name="query-statements"></a>Abfrageanweisungen
|Task   |Verwandtes Thema  |Hinweise
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|Knoten und Kanten intern als Tabellen gespeichert sind, daher werden die meisten der in einer Tabelle in SQL Server oder Azure SQL-Datenbank unterstützten Vorgänge unterstützt, auf den Knoten und Edge-Tabellen  |
|MATCH  | [Übereinstimmung &#40; Transact-SQL &#41;](../../t-sql/queries/match-sql-graph.md)|Übereinstimmung integrierte wurde eingeführt, um einen Musterabgleich und Traversal über das Diagramm zu unterstützen.  |



## <a name="limitations-and-known-issues"></a>Einschränkungen und bekannte Probleme  
Es gibt bestimmte Einschränkungen auf den Knoten und Edge-Tabellen in dieser Version:
* Lokale oder globale temporäre Tabellen können nicht Knoten oder Edge-Tabellen verwendet werden.
* Tabellentypen und Tabellenvariablen können nicht als einen Knoten oder Edge-Tabelle deklariert werden. 
* Knoten und Edge-Tabellen können nicht als temporale Tabellen mit systemversionsverwaltung erstellt werden.   
* Knoten und Edge-Tabellen können nicht von speicheroptimierten Tabellen verwendet werden.  
* Benutzer können nicht die From_id $ und $To_id Spalten ein Rand mit UPDATE-Anweisung aktualisieren. Um den Knoten zu aktualisieren, die ein Rand verbindet, haben Benutzer die neue Kante, die auf neue Knoten einfügen und Löschen von der vorherigen Abfrage.
* Datenbankübergreifende werden Abfragen von Graph-Objekte nicht unterstützt. 


## <a name="next-steps"></a>Nächste Schritte
Um die ersten Schritte mit der neuen Syntax finden Sie unter [SQL-Datenbank Graph - Beispiel](./sql-graph-sample.md)
 

