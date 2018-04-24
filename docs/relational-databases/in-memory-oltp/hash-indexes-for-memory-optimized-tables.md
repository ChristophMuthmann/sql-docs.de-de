---
title: Behandlung von Problemen bei Hashindizes für speicheroptimierte Tabellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: ''
ms.component: in-memory-oltp
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 64fdcae3d8dbecc594b0a673be08e5ba775a9432
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>Behandlung von Problemen bei Hashindizes für speicheroptimierte Tabellen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>Voraussetzung  
  
Wichtige Kontextinformationen für das Verständnis dieser Artikel sind verfügbar unter:  
  
- [Indizes für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [Hashindizes für speicheroptimierte Tabellen](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>Praktische Zahlen  
  
Wenn Sie einen Hashindex für eine speicheroptimierte Tabelle erstellen, muss die Anzahl der Buckets beim Erstellen angegeben werden. In den meisten Fällen sollte die Bucketanzahl das Ein- bis Zweifache der Anzahl eindeutiger Werte im Indexschlüssel betragen. 

Auch wenn **BUCKET_COUNT** geringfügig unter oder über dem bevorzugten Bereich liegt, ist die Leistung des Hashindexes wahrscheinlich tolerierbar oder akzeptabel. Legen Sie **BUCKET_COUNT** für Ihren Hashindex auf eine Anzahl fest, die in etwa der Anzahl der Zeilen entspricht, die die speicheroptimierte Tabelle nach Ihrer Einschätzung haben wird.  
Angenommen, Ihre wachsende Tabelle verfügt über 2.000.000 Zeilen, Sie gehen jedoch davon aus, dass die Anzahl auf das Zehnfache, sprich 20.000.000 Zeilen, anwachsen wird. Beginnen Sie mit einer Bucketanzahl, die dem 10-Fachen der Zeilenanzahl in der Tabelle entspricht. Dieses bietet Ihnen Raum für eine größere Anzahl von Zeilen.  
  
- Im Idealfall würden Sie die Bucketanzahl heraufsetzen, wenn die Zeilenanzahl die anfängliche Bucketanzahl erreicht.  
- Selbst wenn die Zeilenanzahl auf das 5-fache der Bucketanzahl anwächst, ist die Leistung in den meisten Situationen noch gut.  
  
Angenommen, ein Hashindex verfügt über 10.000.000 eindeutige Schlüsselwerte.  
  
- Die Bucketanzahl von 2.000.000 wäre der niedrigste akzeptable Wert. Das Ausmaß der Leistungseinbußen könnte tolerierbar sein.  
  
## <a name="too-many-duplicate-values-in-the-index"></a>Zu viele duplizierte Werte im Index?  
  
Wenn die Hash-indizierten Werte einen hohen Anteil von Duplikaten aufweisen, werden die Hashbuckets durch längere Ketten beeinträchtigt.  
  
Angenommen, Sie nutzen die gleiche SupportEvent-Tabelle aus dem früheren T-SQL-Syntax-Codeblock. Der folgende T-SQL-Code veranschaulicht, wie Sie das Verhältnis *aller* Werte zu *eindeutigen* Werten suchen und anzeigen können:  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- Ein Verhältnis von 10,0 oder höher bedeutet, dass ein Hash ein schlechter Indextyp sein würde. Verwenden Sie stattdessen einen nicht gruppierten Index.   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>Problembehandlung bei Hashindex-Bucketanzahl  
  
Dieser Abschnitt beschreibt die Problembehandlung hinsichtlich der Bucketanzahl für Ihren Hashindex.  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>Überwachen der Statistiken für Ketten und leere Buckets  
  
Sie können die statistische Integrität Ihrer Hashindizes überwachen, indem Sie die folgende T-SQL SELECT-Anweisung ausführen. Die SELECT-Anweisung verwendet die Datenverwaltungsansicht (DMV, Data Management View) mit dem Namen **sys.dm_db_xtp_hash_index_stats**.  
  
```sql
SELECT  
  QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
  i.name                   as [index],   
  h.total_bucket_count,  
  h.empty_bucket_count,  
    
  FLOOR((  
    CAST(h.empty_bucket_count as float) /  
      h.total_bucket_count) * 100)  
                            as [empty_bucket_percent],  
  h.avg_chain_length,   
  h.max_chain_length  
FROM  
        sys.dm_db_xtp_hash_index_stats  as h   
  JOIN sys.indexes                     as i  
          ON h.object_id = i.object_id  
          AND h.index_id  = i.index_id  
JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
JOIN sys.tables t on h.object_id=t.object_id
WHERE ia.type=1
ORDER BY [table], [index];  
```
  
Vergleichen Sie die SELECT-Ergebnisse mit den folgenden statistischen Richtlinien:  
  
- Leere Buckets:  
  - 33 % ist ein guter Zielwert, aber ein größerer Prozentsatz (sogar 90 %) ist in der Regel in Ordnung.  
  - Wenn die Bucketanzahl der Anzahl der eindeutigen Schlüsselwerte entspricht, sind etwa 33 % der Buckets leer.  
  - Ein Wert unter 10 % ist zu niedrig.  
- Ketten in Buckets:  
  - Eine durchschnittliche Kettenlänge von 1 ist ideal für den Fall, dass es keine doppelten Indexschlüsselwerte gibt. Kettenlängen bis zu 10 sind üblicherweise brauchbar.  
  - Wenn die durchschnittliche Kettenlänge größer als 10 ist und der Prozentsatz an leeren Buckets größer als 10 % ist, enthalten die Daten so viele Duplikate, dass ein Hashindex möglicherweise nicht der am besten geeignete Typ ist.  
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>Demonstration von Ketten und leeren Buckets  
  
Der folgende T-SQL-Codeblock bietet Ihnen eine einfache Möglichkeit zum Testen von `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. Der Codeblock wird in einer Minute ausgeführt. Hier sind die Phasen des folgenden Codeblocks:  
  
1. Erstellen einer speicheroptimiertem Tabelle mit wenigen Hashindizes.  
2. Ausfüllen der Tabelle mit Tausenden von Zeilen.  
    A. Es wird ein modulo-Operator verwendet, um die Rate der duplizierten Werte in der StatusCode-Spalte zu konfigurieren.  
    B. Die Schleife fügt 262.144 Zeilen in etwa einer Minute ein.  
3. Ausdrucken einer Meldung (PRINT), mit der Sie aufgefordert werden, die frühere SELECT-Anweisung aus **sys.dm_db_xtp_hash_index_stats**auszuführen.  
  
```sql
DROP TABLE IF EXISTS SalesOrder_Mem;  
go  
  
  
CREATE TABLE SalesOrder_Mem  
(  
  SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
  OrderSequence  int               NOT NULL,  
  OrderDate      datetime2(3)      NOT NULL,  
  StatusCode     tinyint           NOT NULL,  
  
  PRIMARY KEY NONCLUSTERED  
      HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
  
  INDEX ix_OrderSequence  
      HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
  
  INDEX ix_StatusCode  
      HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
  
  INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
)  
  WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
--------------------  
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
Die vorangehende `INSERT`-Schleife führt Folgendes aus:  
  
- Einfügen von eindeutigen Werten für den Primärschlüsselindex und für *ix_OrderSequence*.  
- Einfügen von hunderttausenden Zeilen, die nur 8 eindeutige Werte für `StatusCode` darstellen. Daher kommt es zu einer hohen Rate von Wertduplikaten im Index *ix_StatusCode*.  
  
Überprüfen Sie zur Problembehandlung bei nicht optimaler Bucketanzahl die folgende Ausgabe der SELECT-Anweisung von **sys.dm_db_xtp_hash_index_stats**. Für diese Ergebnisse haben wir der aus Abschnitt D.1 kopierten SELECT-Anweisung `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` hinzugefügt.  
  
Unsere `SELECT`-Ergebnisse werden nach dem Code angezeigt, zur besseren Anzeige künstlich aufgeteilt in zwei schmalere Ergebnistabellen.  
  
- Hier sind die Ergebnisse für die *Bucketanzahl*.  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
- Das Nächste sind die Ergebnisse für die *Kettenlänge*.  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
Untersuchen Sie die oben stehenden Ergebnistabellen auf die drei Hashindizes:  
  
*ix_StatusCode:*  
  
- 50 %der Buckets sind leer, das ist positiv.  
- Die durchschnittliche Kettenlänge ist jedoch mit 65536 sehr hoch.  
  - Dies weist auf eine große Anzahl duplizierter Werte hin.  
  - Die Verwendung eines Hashindexes ist in diesem Fall daher nicht angemessen. Stattdessen sollte ein nicht gruppierter Index verwendet werden.  
  
*ix_OrderSequence:*  
  
- 0 % der Buckets sind leer. Dieser Wert ist zu niedrig.  
- Die durchschnittliche Kettenlänge beträgt 8, auch wenn alle Werte in diesem Index eindeutig sind.  
  - Daher sollte die Bucketanzahl erhöht werden, um die durchschnittliche Kettenlänge an einen Wert in der Nähe von 2 oder 3 zu reduzieren.  
- Da der Indexschlüssel 262144 eindeutige Werte enthält, sollte die Bucketanzahl mindestens 262144 betragen.  
  - Wenn zukünftiges Wachstum erwartet wird, sollte die Bucketanzahl größer sein.  
  
*Primärschlüsselindex (PK_SalesOrder_…):*  
  
- 36 %der Buckets sind leer, das ist positiv.  
- Die durchschnittliche Kettenlänge beträgt 1, was ebenfalls positiv ist. Es ist keine Änderung erforderlich.  
  
### <a name="balancing-the-trade-off"></a>Abwägung  
  
OLTP-Arbeitsauslastungen konzentrieren sich auf einzelne Zeilen. Vollständige Tabellenscans befinden sich normalerweise nicht im leistungskritischen Pfad für OLTP-Arbeitsauslastungen. Deshalb müssen Sie die **Arbeitsspeicherauslastung** und die **Leistung von Gleichheitstests und Einfügevorgängen** gegeneinander abwägen.  
  
**Wenn die Arbeitsspeicherauslastung wichtiger ist:**  
  
- Wählen Sie eine Bucketanzahl in der Nähe der Anzahl der Indexschlüsseldatensätze.  
- Die Bucketanzahl sollte nicht deutlich niedriger sein als die Anzahl der Indexschlüsselwerte, da dies Auswirkungen auf die meisten DML-Vorgänge sowie die Zeit hat, die zum Wiederherstellen der Datenbank nach einem Neustart des Servers benötigt wird.  
  
**Wenn die Leistung von Gleichheitstests wichtiger ist:**  
  
- Ist eine höhere Bucketanzahl mit der doppelten oder drei Mal so großen Anzahl von eindeutigen Indexwerten geeignet. Eine höhere Anzahl bedeutet:  
  - Schnellerer Abruf bei der Suche nach einem bestimmten Wert.  
  - Eine erhöhte Arbeitsspeicherauslastung.  
  - Ein größerer Zeitaufwand für eine vollständige Überprüfung des Hashindexes.  
  

##  <a name="Additional_Reading"></a> Zusätzliches Lesematerial  
 [Hashindizes für speicheroptimierte Tabellen](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [Nicht gruppierter Indizes für speicheroptimierte Tabellen](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  
