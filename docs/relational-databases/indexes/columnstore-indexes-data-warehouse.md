---
title: 'Columnstore-Indizes: Data Warehouse | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 21fd153b-116d-47fc-a926-f1528299a391
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bce265c81c06adf13b70e5e4c05565b44120bb94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="columnstore-indexes---data-warehouse"></a>Columnstore-Indizes: Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Columnstore-Indizes sind in Verbindung mit der Partitionierung unverzichtbar für die Erstellung eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Data Warehouse.  
  
## <a name="whats-new"></a>Neuigkeiten  
 In[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wurden die folgenden Funktionen für Columnstore-Leistungsverbesserungen eingeführt:  
  
-   AlwaysOn unterstützt das Abfragen eines Columnstore-Indexes auf einem lesbaren sekundären Replikat.  
-   Multiple Active Result Sets (MARS) unterstützt Columnstore-Indizes.  
-   Eine neue dynamische Verwaltungssicht [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) bietet Informationen über das Beheben von Leistungsproblemen auf Zeilengruppenebene.  
-   Singlethread-Abfragen für Columnstore-Indizes können im Batchmodus ausgeführt werden. Früher konnten nur Multithread-Abfragen im Batchmodus ausgeführt werden.  
-   Der `SORT`-Operator wird im Batchmodus ausgeführt.  
-   Mehrere `DISTINCT`-Vorgänge werden im Batchmodus ausgeführt.  
-   Window Aggregates wird jetzt im Batchmodus für Datenbank-Kompatibilitätsgrad 130 und höher ausgeführt.  
-   Aggregatweitergabe für die effiziente Verarbeitung von Aggregaten. Wird für alle Datenbank-Kompatibilitätsgrade unterstützt.  
-   Zeichenfolgenprädikatweitergabe für die effiziente Verarbeitung von Zeichenfolgenprädikaten. Wird für alle Datenbank-Kompatibilitätsgrade unterstützt.  
-   Momentaufnahmenisolation für den Datenbank-Kompatibilitätsgrad 130 und höher  
  
## <a name="improve-performance-by-combining-nonclustered-and-columnstore-indexes"></a>Verbessern der Leistung durch Kombinieren von nicht gruppierten Indizes und Columnstore-Indizes  
 Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]können Sie nicht gruppierte Indizes für einen gruppierten Columnstore-Index definieren.   
  
### <a name="example-improve-efficiency-of-table-seeks-with-a-nonclustered-index"></a>Beispiel: Verbessern der Effizienz von Suchabfragen auf Tabellen mit einem nicht gruppierten Index  
 Sie können einen nicht gruppierten Index erstellen, der Abfragen ausführt, die am besten mit Tabellenvorgängen funktionieren, um die Effizienz von Tabellenvorgängen in einem Data Warehouse zu verbessern. Zum Beispiel erzielen Abfragen, die nach übereinstimmenden Werten suchen oder eine kleine Anzahl von Werten zurückgeben, eine bessere Leistung für einen B-Strukturindex als für einen Columnstore-Index. Ein vollständiger Tabellenscan durch den Columnstore-Index ist für die Abfragen nicht erforderlich. Das korrekte Ergebnis wird durch eine binäre Suche in einem B-Strukturindex schneller zurückgeben.  
  
```sql  
--BASIC EXAMPLE: Create a nonclustered index on a columnstore table.  
  
--Create the table  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int  
);  
GO  
  
--Store the table as a columnstore.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account;  
GO  
  
--Add a nonclustered index.  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
```  
  
### <a name="example-use-a-nonclustered-index-to-enforce-a-primary-key-constraint-on-a-columnstore-table"></a>Beispiel: Verwenden eines nicht gruppierten Indexes zum Erzwingen einer Primärschlüsseleinschränkung für eine Columnstore-Tabelle  
 Programmbedingt lässt eine Columnstore-Tabelle keine Primärschlüsseleinschränkung zu. Jetzt können Sie einen nicht gruppierten Index für eine Columnstore-Tabelle verwenden, um eine Primärschlüsseleinschränkung zu erzwingen. Ein Primärschlüssel entspricht einer UNIQUE-Einschränkung für eine Spalte, die ungleich NULL ist, und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementiert eine UNIQUE-Einschränkung als nicht gruppierten Index. Das folgende Beispiele kombiniert diese Fakten und definiert eine UNIQUE-Einschränkung für den Kontoschlüssel der Spalte, die ungleich NULL ist. Das Ergebnis ist ein nicht gruppierter Index, der eine Primärschlüsseleinschränkung als eine UNIQUE-Einschränkung für eine Spalte, die ungleich NULL ist erzwingt.  
  
 Als Nächstes wird die Tabelle zu einem gruppierten Columnstore-Index konvertiert. Bei der Konvertierung besteht der nicht gruppierte Index weiterhin. Das Ergebnis ist ein gruppierter Columnstore-Index mit einem nicht gruppierten Index, der eine Primärschlüsseleinschränkung erzwingt. Da jedes Update oder jedes Einfügen in die Columnstore-Tabelle außerdem Auswirkungen auf den nicht gruppierten Index hat, verursachen alle Vorgänge, die die UNIQUE-Einschränkung und die nicht-NULL verletzen, einen Fehler im ganzen Vorgang.  
  
 Das Ergebnis ist ein Columnstore-Index mit einem nicht gruppierten Index, der eine Primärschlüsseleinschränkung für beide Indizes erzwingt.  
  
```sql 
--EXAMPLE: Enforce a primary key constraint on a columnstore table.   
  
--Create a rowstore table with a unique constraint.  
--The unique constraint is implemented as a nonclustered index.  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int,  
  
    CONSTRAINT uniq_account UNIQUE (AccountKey)  
);  
  
--Store the table as a columnstore.   
--The unique constraint is preserved as a nonclustered index on the columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX t_account_cci ON t_account  
  
--By using the previous two steps, every row in the table meets the UNIQUE constraint  
--on a non-NULL column.  
--This has the same end-result as having a primary key constraint  
--All updates and inserts must meet the unique constraint on the nonclustered index or they will fail.  
  
--If desired, add a foreign key constraint on AccountKey.  
  
ALTER TABLE [dbo].[t_account]  
WITH CHECK ADD FOREIGN KEY([AccountKey]) REFERENCES my_dimension(Accountkey); 
```  
  
### <a name="improve-performance-by-enabling-row-level-and-row-group-level-locking"></a>Verbessern der Leistung durch das Aktivieren von Sperren auf Zeilenebene und Zeilengruppenebene  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bietet eine präzise Sperrfunktion für Auswahl-, Update- und Löschvorgänge, um den nicht gruppierten Index für eine Columnstore-Index-Funktion zu ergänzen. Abfragen mit Sperren auf Zeilenebene für Index-Suchvorgänge können für einen nicht gruppierten Index ausgeführt werden. Abfragen mit Sperren auf Zeilengruppenebene für vollständige Tabellenscans können für den Columnstore-Index ausgeführt werden. Verwenden Sie diese Option, um eine höhere Lese/Schreib-Parallelität durch die korrekte Verwendung von Sperren auf Zeilenebene und Zeilengruppenebene zu erzielen.  
  
```sql  
--Granular locking example  
--Store table t_account as a columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account  
GO  
  
--Add a nonclustered index for use with this example  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
GO  
  
--Look at locking with access through the nonclustered index  
SET TRANSACTION ISOLATION LEVEL repeatable read;  
GO  
  
BEGIN TRAN  
    -- The query plan chooses a seek operation on the nonclustered index  
    -- and takes the row lock  
    SELECT * FROM t_account WHERE AccountKey = 100;  
END TRAN  
```  
  
### <a name="snapshot-isolation-and-read-committed-snapshot-isolations"></a>Momentaufnahme-Isolation und Momentaufnahmen mit der Isolationsstufe READ  
 Verwenden Sie die Momentaufnahmeisolation (snapshot-isolation; SI), um die Transaktionskonsistenz zu gewährleisten und die Read Committed-Momentaufnahmeisolation (read-committed snapshot isolations; RCSI), um Konsistenz auf Anweisungsebene für Abfragen auf Columnstore-Indizes zu gewährleisten. Dadurch können Abfragen ohne Blockierung von Datenschreibern ausgeführt werden. Dieses nicht blockierende Verhalten verringert auch beträchtlich die Wahrscheinlichkeit für Deadlocks bei komplexen Transaktionen. Weitere Informationen finden Sie unter [Momentaufnahmeisolation in SQL Server](http://msdn.microsoft.com/library/tcbchxcb\(v=vs.110\).aspx) auf MSDN.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Columnstore Indexes Design Guidance (Leitfaden zum Entwerfen von Columnstore-Indizes)](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Columnstore Indexes Data Loading Guidance (Leitfaden zum Laden von Daten in Columnstore-Indizes)](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Abfrageleistung für Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Columnstore-Index-Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
 [Columnstore Index Architecture (Columnstore-Indizes: Architektur)](../../relational-databases/sql-server-index-design-guide.md#columnstore_index) 
  
