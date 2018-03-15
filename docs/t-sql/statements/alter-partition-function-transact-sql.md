---
title: ALTER PARTITION FUNCTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66b921eb3bd6378d20de11a0197a20c957d14ac6
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert eine Partitionsfunktion durch Teilen oder Zusammenführen der Begrenzungswerte. Durch Ausführen von ALTER PARTITION FUNCTION kann eine Partition einer Tabelle oder eines Index, die bzw. der die Partitionsfunktion verwendet, in zwei Partitionen aufgeteilt werden, oder zwei Partitionen können zu einer einzigen Partition zusammengeführt werden.  
  
> [!CAUTION]  
>  Mehrere Tabellen oder Indizes können dieselbe Partitionsfunktion verwenden. ALTER PARTITION FUNCTION wirkt sich auf alle Tabellen und Indizes in einer einzigen Transaktion aus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *partition_function_name*  
 Der Name der Partitionsfunktion, die geändert werden soll.  
  
 SPLIT RANGE ( *boundary_value* )  
 Fügt der Partitionsfunktion eine Partition hinzu. *boundary_value* bestimmt den Bereich der neuen Partition und muss von den vorhandenen Begrenzungsbereichen der Partitionsfunktion abweichen. Basierend auf *boundary_value* teilt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen der vorhandenen Bereiche in zwei Bereiche auf. Der Bereich mit dem neuen *boundary_value*-Wert wird als die neue Partition betrachtet.  
  
 Eine Dateigruppe muss online vorhanden sein und vom Partitionsschema, das die Partitionsfunktion verwendet, zum Speichern der neuen Partition als NEXT USED markiert werden. Dateigruppen werden in einer CREATE PARTITION SCHEME-Anweisung Partitionen zugeordnet. Falls eine CREATE PARTITION SCHEME-Anweisung mehr Dateigruppen als erforderlich zuordnet (in der CREATE PARTITION FUNCTION-Anweisung werden weniger Partitionen als Dateigruppen zum Speichern erstellt), sind nicht zugewiesene Dateigruppen vorhanden, und eine davon wird vom Partitionsschema als NEXT USED markiert. In dieser Dateigruppe wird die neue Partition gespeichert. Falls vom Partitionsschema keine Dateigruppen als NEXT USED markiert werden, müssen Sie mit ALTER PARTITION SCHEME eine Dateigruppe hinzufügen oder eine vorhandene Dateigruppe zum Speichern der neuen Partition festlegen. Für eine Dateigruppe, in der bereits Partitionen vorhanden sind, können zusätzliche Partitionen festgelegt werden. Eine Partitionsfunktion kann bei mehreren Partitionsschemas verwendet werden. Deshalb müssen alle Partitionsschemas, die die Partitionsfunktion verwenden, der Sie Partitionen hinzufügen, eine NEXT USED-Dateigruppe aufweisen. Andernfalls wird für ALTER PARTITION FUNCTION ein Fehler gemeldet, und es werden die Partitionsschemas angezeigt, für die eine NEXT USED-Dateigruppe fehlt.  
  
 Wenn Sie alle Partitionen in derselben Dateigruppe erstellen, wird diese Dateigruppe anfänglich automatisch der NEXT USED-Dateigrupp zugewiesen. Nach der Ausführung eines Teilungsvorgangs gibt es jedoch keine festgelegte NEXT USED-Dateigruppe mehr. Sie müssen die Dateigruppe explizit mit ALTER PARITION SCHEME der NEXT USED-Dateigruppe zuweisen. Andernfalls schlägt ein nachfolgender Teilungsvorgang fehl.  
  
> [!NOTE]  
>  Einschränkungen im Zusammenhang mit dem Columnstore-Index: Wenn ein Columnstore-Index für die Tabelle vorhanden ist, können nur leere Partitionen aufgeteilt werden. Vor dem Ausführen dieses Vorgangs müssen Sie den Columnstore-Index löschen oder deaktivieren.  
  
 MERGE [ RANGE ( *boundary_value*) ]  
 Löscht eine Partition und führt Werte in der Partition mit einer der restlichen Partitionen zusammen. RANGE (*boundary_value*) muss ein vorhandener Begrenzungswert sein, mit dem die Werte aus der gelöschten Partition zusammengeführt werden. Die Dateigruppe, in der *boundary_value* ursprünglich vorhanden war, wird aus dem Partitionsschema entfernt, wenn sie nicht von einer verbleibenden Partition verwendet oder mit der NEXT USED-Eigenschaft gekennzeichnet wird. Die zusammengeführte Partition befindet sich in der Dateigruppe, die *boundary_value* ursprünglich nicht enthielt. *boundary_value* ist ein konstanter Ausdruck, der auf Variablen (einschließlich Variablen eines benutzerdefinierten Typs) oder Funktionen (einschließlich benutzerdefinierter Funktionen) verweisen kann. Er kann nicht auf einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausdruck verweisen. *boundary_value* muss entweder mit dem Datentyp der entsprechenden Partitionierungsspalte übereinstimmen oder implizit in den Datentyp der entsprechenden Partitionierungsspalte konvertiert werden können. Während der impliziten Konvertierung kann der Wert nicht so abgeschnitten werden, dass die Größe und die Dezimalstellen dieses Werts mit denen des entsprechenden *input_parameter_type*-Werts nicht übereinstimmen.  
  
> [!NOTE]  
>  Einschränkungen im Zusammenhang mit dem Columnstore-Index: Zwei nicht leere Partitionen, die einen Columnstore-Index enthalten, können nicht zusammengeführt werden. Vor dem Ausführen dieses Vorgangs müssen Sie den Columnstore-Index löschen oder deaktivieren.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Behalten Sie stets leere Partitionen an beiden Enden des Partitionsbereichs, um zu gewährleisten, dass die Partitionsteilung (vor dem Laden neuer Daten) und die Partitionszusammenführung (nach dem Entladen alter Daten) keine Datenverschiebungen verursachen. Vermeiden Sie das Aufteilen oder Zusammenführen gefüllter Partitionen. Dies kann äußerst ineffizient sein, da dadurch möglicherweise ein viermal größeres Protokoll erstellt wird, und zudem ernsthafte Sperren zur Folge haben.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 ALTER PARTITION FUNCTION partitioniert Tabellen und Indizes neu, die die Funktion in einem einzelnen atomaren Vorgang verwenden. Dieser Vorgang erfolgt jedoch offline, und in Abhängigkeit vom Umfang kann die Neupartitionierung ressourcenintensiv sein.  
  
 ALTER PARTITION FUNCTION kann nur zum Teilen einer Partition in zwei Partitionen oder zum Zusammenführen von zwei Partitionen zu einer Partition verwendet werden. Um die Partitionierung einer Tabelle anderweitig zu ändern (z. B. von 10 Partitionen in 5 Partitionen), können Sie eine der folgenden Optionen ausführen. Der Ressourcenverbrauch dieser Optionen hängt von der Systemkonfiguration ab:     
  
-   Erstellen Sie eine neue partitionierte Tabelle mit der gewünschten Partitionsfunktion, und fügen Sie dann mithilfe einer INSERT INTO...SELECT FROM-Anweisung die Daten aus der alten Tabelle in die neue Tabelle ein.  
  
-   Erstellen Sie einen partitionierten gruppierten Index für einen Heap.  
  
    > [!NOTE]  
    >  Das Löschen eines partitionierten gruppierten Index ergibt einen partitionierten Heap.  
  
-   Verwenden Sie die CREATE INDEX-Anweisung von [!INCLUDE[tsql](../../includes/tsql-md.md)] mit der DROP EXISTING = ON-Klausel, um einen vorhandenen partitionierten Index zu löschen und neu zu erstellen.  
  
-   Führen Sie eine Abfolge von ALTER PARTITION FUNCTION-Anweisungen aus.  
  
 Alle von ALTER PARTITION FUNCTION betroffenen Dateigruppen müssen online sein.  
  
 Für ALTER PARTITION FUNCTION wird ein Fehler gemeldet, wenn ein deaktivierter gruppierter Index für Tabellen vorhanden ist, die die Partitionsfunktion verwenden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird die Replikation beim Ändern einer Partitionsfunktion nicht unterstützt. Äderungen an einer Partitionsfunktion in der Veröffentlichungsdatenbank müssen in der Abonnementdatenbank manuell angewendet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Die folgenden Berechtigungen können zum Ausführen von ALTER PARTITION FUNCTION verwendet werden:  
  
-   ALTER ANY DATASPACE-Berechtigung. Diese Berechtigung gilt standardmäßig für Mitglieder der festen Serverrolle **sysadmin** und für Mitglieder der festen Datenbankrollen **db_owner** und **db_ddladmin** .  
  
-   Die Berechtigung CONTROL oder ALTER für die Datenbank, in der die Partitionsfunktion erstellt wurde.  
  
-   Die Berechtigung CONTROL SERVER oder ALTER ANY DATABASE auf dem Server der Datenbank, in der die Partitionsfunktion erstellt wurde.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. Teilen der Partition einer partitionierten Tabelle oder eines partitionierten Index in zwei Partitionen  
 Im folgenden Beispiel wird eine Partitionsfunktion zum Partitionieren einer Tabelle oder eines Indexes in vier Partitionen erstellt. `ALTER PARTITION FUNCTION` teilt eine Partition in zwei, sodass insgesamt fünf Partitionen entstehen.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. Zusammenführen von zwei Partitionen einer partitionierten Tabelle zu einer einzigen Partition  
 Im folgenden Beispiel wird dieselbe Partitionsfunktion wie oben erstellt, und anschließend werden zwei Partitionen zu einer einzigen Partition zusammengeführt, sodass sich insgesamt drei Partitionen ergeben.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Partitioned Tables and Indexes (Partitionierte Tabellen und Indizes)](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
