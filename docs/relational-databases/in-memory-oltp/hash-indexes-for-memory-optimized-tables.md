---
title: "Hashindizes für speicheroptimierte Tabellen | Microsoft-Dokumentation"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b1acbcd97dfabfa5d23fa82e55d4eb01101233aa
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>Hashindizes für speicheroptimierte Tabellen
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
Dieser Artikel beschreibt die *Hashindextypen*, die für eine speicheroptimierte Tabelle zur Verfügung stehen. Der Artikel enthält Folgendes:  
  
- Kurze Codebeispiele zum Veranschaulichen der Transact-SQL-Syntax  
- Beschreibt die Grundlagen von Hashindizes.  
- Beschreibt, [wie eine entsprechende Bucketanzahl geschätzt wird](#configuring_bucket_count).  
- Beschreibung des Designs und der Verwaltung Ihrer Hashindizes  
  
  
#### <a name="prerequisite"></a>Voraussetzung  
  
Wichtige Kontextinformationen für das Verständnis dieser Artikel sind verfügbar unter:  
  
- [Indizes für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Syntax für speicheroptimierte Indizes  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Codebeispiel für Syntax  
  
Dieser Unterabschnitt enthält einen Transact-SQL-Codeblock, der die verfügbare Syntax zum Erstellen eines Hashindexes für eine speicheroptimierte Tabelle darstellt:  
  
- Das Beispiel zeigt, dass der Hashindex in der CREATE TABLE-Anweisung deklariert wird.  
  - Sie können den Hashindex stattdessen in einer separaten [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) -Anweisung deklarieren.  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

Informationen, wie Sie den richtigen `BUCKET_COUNT` -Wert für Ihre Daten ermitteln, finden Sie unter [Konfigurieren der Hashindex-Bucketanzahl](#configuring_bucket_count). 
  
## <a name="b-hash-indexes"></a>B. Hashindizes  
  
  
### <a name="b1-performance-basics"></a>B.1 Grundlagen zur Leistung  
  
Die Leistung eines Hash-Indexes ist:  
  
- Ausgezeichnet, wenn die WHERE-Klausel einen *genauen* Wert für jede Spalte im Hashindexschlüssel angibt.  
- Schlecht, wenn die WHERE-Klausel im Indexschlüssel nach einem *Wertebereich* sucht.  
- Schlecht, wenn die WHERE-Klausel einen bestimmten Wert für die erste Spalte eines zweispaltigen Hashindexschlüssels angibt, aber kein Wert für die *zweite* Spalte des Schlüssels angegeben wird.  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 Deklarationseinschränkungen  
  
Ein Hashindex kann nur für eine speicheroptimierte Tabelle vorhanden sein. Er kann nicht in einer datenträgerbasierten Tabelle vorhanden sein.  
  
Ein Hashindex kann deklariert werden als:  
  
- UNIQUE, oder standardmäßig nicht eindeutig.  
- NONCLUSTERED. Dies ist die Standardeinstellung.   
  
  
Hier ist ein Beispiel der Syntax zum Erstellen eines Hashindexes außerhalb der CREATE TABLE-Anweisung:  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 Buckets und Hashfunktion  
  
Ein Hashindex verankert seine Schlüsselwerte in einem sogenannten *Bucket* -Array:  
  
- Jeder Bucket umfasst 8 Bytes, die zum Speichern der Arbeitsspeicheradresse einer Linkliste von Schlüsseleinträgen verwendet werden.  
- Jeder Eintrag ist ein Wert für einen Indexschlüssel zuzüglich der Adresse für die entsprechende Zeile in der zugrunde liegenden speicheroptimierten Tabelle.  
  - Jeder Eintrag verweist in einer Linkliste von Einträgen – alle mit dem aktuellen Bucket verkettet – auf den nächsten Eintrag.  
  
  
Der Hashalgorithmus versucht, alle eindeutigen Schlüsselwerte gleichmäßig auf seine Buckets zu verteilen, doch das Ideal vollkommener Gleichmäßigkeit wird nicht erreicht. Alle Instanzen eines bestimmten Schlüsselwerts werden mit dem gleichen Bucket verkettet. Der Bucket könnte auch in allen Instanzen eines anderen Schlüsselwerts gemischt worden sein.  
  
- Diese Mischung wird als *Hashkonflikt*bezeichnet. Konflikte sind häufig, jedoch nicht ideal.  
- Ein realistisches Ziel wäre es, wenn 30 % der Buckets zwei verschiedene Schlüsselwerte enthalten.  
  
  
Sie deklarieren, wie viele Buckets ein Hashindex haben soll.  
  
- Je geringer das Verhältnis von Buckets zu Tabellenzeilen oder eindeutigen Werten, desto länger wird die durchschnittliche Bucketlinkliste.  
- Kurze Linklisten können schneller verarbeitet werden als lange Linklisten.  
  
  
SQL Server hat eine Hashfunktion, die für alle Hashindizes verwendet wird.  
  
- Die Hashfunktion ist deterministisch: Beim gleichen Eingabeschlüsselwert gibt sie konsistent den gleichen Bucketslot aus.  
- Die Ausgaben der Hashfunktion bilden durch wiederholte Aufrufe tendenziell eine Poisson- oder Glockenkurvenverteilung und keine flache lineare Verteilung.  
  
  
Die Interaktion zwischen dem Hashindex und den Buckets wird im folgenden Bild zusammengefasst.  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "Indexschlüssel, in die Hash-Funktion eingegeben, die Ausgabe ist die Adresse eines Hashbuckets, der auf den Anfang der Kette verweist.")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 Zeilenversionen und automatische Speicherbereinigung  
  
  
In einer speicheroptimierten Tabelle mit einer Zeile, die von einem SQL UPDATE betroffen ist, erstellt die Tabelle eine aktualisierte Version der Zeile. Während der Updatetransaktion können andere Sitzungen möglicherweise die ältere Version der Zeile lesen und so den Leistungsabfall vermeiden, der mit einer Zeilensperre einhergeht.  
  
Der Hashindex kann möglicherweise auch verschiedene Versionen seiner Einträge haben, um das Update zu berücksichtigen.  
  
Wenn die älteren Versionen später nicht mehr erforderlich sind, durchsucht ein Thread der automatischen Speicherbereinigung (GC, Garbage Collection) die Buckets und Verknüpfung, um alte Einträge zu beseitigen. Der GC-Thread bietet eine bessere Leistung, wenn die Kettenlängen kurz sind.   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>C. Konfigurieren der Hashindex-Bucketanzahl  
  
Die Hashindex-Bucketanzahl wird während der Indexerstellung angegeben und kann mit der ALTER TABLE... ALTER INDEX REBUILD-Syntax geändert werden.  
  
In den meisten Fällen sollte die Bucketanzahl das Ein- bis Zweifache der Anzahl eindeutiger Werte im Indexschlüssel betragen.   
Möglicherweise können Sie nicht immer prognostizieren, wie viele Werte ein bestimmter Indexschlüssel enthalten kann oder wird. Die Leistung ist in der Regel dennoch gut, falls der **BUCKET_COUNT** -Wert im Rahmen des 10-fachen der tatsächlichen Anzahl der Schlüsselwerte liegt, und die Überschätzung ist im Allgemeinen besser als die Unterschätzung.  
  
Zu *wenige* Buckets hat die folgenden Nachteile:  
  
- Mehr Hashkonflikte von eindeutigen Schlüsselwerten.  
  - Jeder eindeutige Wert wird gezwungen, denselben Bucket mit einem anderen eindeutigen Wert zu nutzen.  
  - Die durchschnittliche Kettenlänge pro Bucket nimmt zu.  
  - Je länger die Bucketkette, desto langsamer die Gleichheitssuche in Index und .  
  
Zu *viele* Buckets hat die folgenden Nachteile:  
  
- Bei einer zu hohen Bucketanzahl können möglicherweise mehr leere Buckets auftreten.  
  - Leere Buckets beeinträchtigen die Leistung der vollständigen Indexscans. Wenn diese regelmäßig ausgeführt werden, erwägen Sie eine Bucketanzahl, die annähernd der Anzahl eindeutiger Indexschlüsselwerte entspricht.  
  - Leere Buckets belegen Speicher, wobei jeder Bucket allerdings nur 8 Bytes belegt.  
    
  
> [!NOTE]
> Das Hinzufügen von weiteren Buckets trägt nichts zur Reduzierung der Verkettung von Einträgen bei, die sich einen duplizierten Wert teilen. Die Rate der Wertduplizierung wird verwendet, um zu entscheiden, ob ein Hash den entsprechenden Indextyp hat, nicht um die Bucketanzahl zu berechnen.  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 Praktische Zahlen  
  
Auch wenn die **BUCKET_COUNT** geringfügig unter oder über dem bevorzugten Bereich liegt, ist die Leistung des Hashindexes wahrscheinlich tolerierbar oder akzeptabel. Es kommt zu keiner Krise.  
  
Geben Sie Ihrem Hashindex eine **BUCKET_COUNT** , die in etwa der Anzahl der Zeilen entspricht, die nach Ihrer Vorhersage die speicheroptimierte Tabelle haben wird.  
  
Angenommen, Ihre wachsende Tabelle verfügt über 2.000.000 Zeilen, Sie sagen jedoch vorher, dass die Anzahl auf das 10-Fache, sprich 20.000.000 Zeilen, anwachsen wird. Beginnen Sie mit einer Bucketanzahl, die dem 10-Fachen der Zeilenanzahl in der Tabelle entspricht. Dieses bietet Ihnen Raum für eine größere Anzahl von Zeilen.  
  
- Im Idealfall würden Sie die Bucketanzahl heraufsetzen, wenn die Zeilenanzahl die anfängliche Bucketanzahl erreicht.  
- Selbst wenn die Zeilenanzahl auf das 5-fache der Bucketanzahl anwächst, ist die Leistung in den meisten Situationen noch gut.  
  
Angenommen, ein Hashindex verfügt über 10.000.000 eindeutige Schlüsselwerte.  
  
- Die Bucketanzahl von 2.000.000 wäre der niedrigste akzeptable Wert. Das Ausmaß der Leistungseinbußen könnte tolerierbar sein.  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 Zu viele duplizierte Werte im Index?  
  
Wenn die Hash-indizierten Werte einen hohen Anteil von Duplikaten aufweisen, werden die Hashbuckets durch längere Ketten beeinträchtigt.  
  
Angenommen, Sie nutzen die gleiche SupportEvent-Tabelle aus dem früheren T-SQL-Syntax-Codeblock. Der folgende T-SQL-Code veranschaulicht, wie Sie das Verhältnis *aller* Werte zu *eindeutigen* Werten suchen und anzeigen können:  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- Ein Verhältnis von 10,0 oder höher bedeutet, dass ein Hash ein schlechter Indextyp sein würde. Verwenden Sie stattdessen einen nicht gruppierten Index.   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>D. Problembehandlung bei Hashindex-Bucketanzahl  
  
Dieser Abschnitt beschreibt die Problembehandlung hinsichtlich der Bucketanzahl für Ihren Hashindex.  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 Überwachen der Statistiken für Ketten und leere Buckets  
  
Sie können die statistische Integrität Ihrer Hashindizes überwachen, indem Sie die folgende T-SQL SELECT-Anweisung ausführen. Die SELECT-Anweisung verwendet die Datenverwaltungsansicht (DMV, Data Management View) mit dem Namen **sys.dm_db_xtp_hash_index_stats**.  
  
  
```t-sql
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
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 Demonstration von Ketten und leeren Buckets  
  
  
Der folgende T-SQL-Codeblock bietet Ihnen eine einfache Möglichkeit zum Testen von `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. Der Codeblock wird in einer Minute ausgeführt. Hier sind die Phasen des folgenden Codeblocks:  
  
  
1. Erstellen einer speicheroptimiertem Tabelle mit wenigen Hashindizes.  
2. Ausfüllen der Tabelle mit Tausenden von Zeilen.  
    A. Es wird ein modulo-Operator verwendet, um die Rate der duplizierten Werte in der StatusCode-Spalte zu konfigurieren.  
    B. Die Schleife fügt 262144 Zeilen in etwa einer Minute ein.  
3. Ausdrucken einer Meldung (PRINT), mit der Sie aufgefordert werden, die frühere SELECT-Anweisung aus **sys.dm_db_xtp_hash_index_stats**auszuführen.  
  
  
```t-sql
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
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
Die vorangehende INSERT-Schleife führt Folgendes aus:  
  
- Einfügen von eindeutigen Werten für den Primärschlüsselindex und für „ix_OrderSequence“  
- Einfügen von einigen hunderttausend Zeilen, die nur 8 eindeutige Werte für den StatusCode darstellen. Daher kommt es zu einer hohen Rate von Wertduplikaten im Index „ix_StatusCode“.  
  
Überprüfen Sie zur Problembehandlung bei nicht optimaler Bucketanzahl die folgende Ausgabe der SELECT-Anweisung von **sys.dm_db_xtp_hash_index_stats**. Für diese Ergebnisse haben wir der aus Abschnitt D.1 kopierten SELECT-Anweisung `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` hinzugefügt.  
  
  
  
Unsere SELECT-Ergebnisse werden nach dem Code angezeigt, zur besseren Anzeige künstlich aufgeteilt in zwei schmalere Ergebnistabellen.  
  
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
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 Ausgleichen des Trade-Offs  
  
OLTP-Arbeitsauslastungen konzentrieren sich auf einzelne Zeilen. Vollständige Tabellenscans befinden sich normalerweise nicht im leistungskritischen Pfad für OLTP-Arbeitsauslastungen. Daher müssen Sie den Trade-Off zwischen Folgendem ausgleichen:  
  
- Größe der Arbeitsspeicherauslastung; im Vergleich zur  
- Leistung von Gleichheitstests und von Einfügevorgängen.  
  
  
*Wenn die Arbeitsspeicherauslastung wichtiger ist:*  
  
- Wählen Sie eine Bucketanzahl in der Nähe der Anzahl der Indexschlüsseldatensätze.  
- Die Bucketanzahl sollte nicht deutlich niedriger sein als die Anzahl der Indexschlüsselwerte, da dies Auswirkungen auf die meisten DML-Vorgänge sowie die Zeit hat, die zum Wiederherstellen der Datenbank nach einem Neustart des Servers benötigt wird.  
  
  
*Wenn die Leistung von Gleichheitstests wichtiger ist:*  
  
- Ist eine höhere Bucketanzahl mit der doppelten oder drei Mal so großen Anzahl von eindeutigen Indexwerten geeignet. Eine höhere Anzahl bedeutet:  
  - Schnellerer Abruf bei der Suche nach einem bestimmten Wert.  
  - Eine erhöhte Arbeitsspeicherauslastung.  
  - Ein größerer Zeitaufwand für eine vollständige Überprüfung des Hashindexes.  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>E. Stärken von Hashindizes  
  
  
Ein Hashindex ist gegenüber einem nicht gruppierten Index zu bevorzugen, wenn:  
  
- Abfragen die indizierte Spalte testen mithilfe einer WHERE-Klausel mit einer Ungleichheit wie im Folgenden:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 Mehrspaltige Hashindexschlüssel  
  
  
Ihr Zweispaltenindex könnte ein nicht gruppierter Index oder ein Hashindex sein. Nehmen wir an, die Indexspalten sind „col1“ und „col2“. Gemäß der folgenden SQL-SELECT-Anweisung wäre nur der nicht gruppierte Index für den Abfrageoptimierer nützlich:  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
Der Hashindex benötigt die WHERE-Klausel, um einen Gleichheitstest für die einzelnen Spalten im Schlüssel anzugeben. Ansonsten ist der Hashindex für den Optimierer nicht sinnvoll.  
  
Genauso wenig ist der Indextyp nützlich, wenn die WHERE-Klausel nur die zweite Spalte im Indexschlüssel angibt.  

