---
title: 'Columnstore-Indizes: Abfrageleistung | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 83acbcc4-c51e-439e-ac48-6d4048eba189
caps.latest.revision: 23
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 08222b4c7af5a62040f808bee56f181ed25149dd
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="columnstore-indexes---query-performance"></a>Columnstore-Indizes: Abfrageleistung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Empfehlungen zum Erreichen der sehr schnellen Abfrageleistung, die Columnstore-Indizes vom Design her bereitstellen können sollten.    
    
 Columnstore-Indizes können eine bis zu 100-fach bessere Leistung für Analyse- und Data Warehousing-Arbeitsauslastungen und eine bis zu 10-fach bessere Datenkomprimierung als herkömmliche Rowstore-Indizes erreichen. Diese Empfehlungen unterstützen Sie beim Erzielen der schnellen Abfrageleistung, für die Columnstore-Indizes entwickelt wurden. Weitere Erläuterungen zur Columnstore-Leistung finden Sie am Ende.    
    
## <a name="recommendations-for-improving-query-performance"></a>Empfehlungen zur Verbesserung der Abfrageleistung    
 Im Folgenden finden Sie einige Empfehlungen zum Erreichen der hohen Leistung, für die Columnstore-Indizes entwickelt wurden.    
    
### <a name="1-organize-data-to-eliminate-more-rowgroups-from-a-full-table-scan"></a>1. Organisieren Sie Daten, um weitere Zeilengruppen im Rahmen eines vollständigen Tabellenscans zu beseitigen.    
    
-   **Nutzen Sie die Einfügereihenfolge.** Im Allgemeinen werden in einem herkömmlichen Data Warehouse die Daten in zeitlicher Reihenfolge eingefügt. Die Analyse erfolgt in der Zeitdimension. Beispiel: Analyse der Umsätze nach Quartal. Für diese Art der Arbeitsauslastung wird das Löschen der Zeilengruppe automatisch durchgeführt. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie die Anzahl der Zeilengruppen ermitteln, die während der Abfrageverarbeitung ausgelassen werden.    
    
-   **Nutzen Sie den gruppierten Rowstore-Index.** Wenn das allgemeine Abfrageprädikat für eine Spalte (z.B. C1) gilt, die nicht mit der Einfügereihenfolge der Zeile verbunden ist, können Sie einen gruppierten Rowstore-Index für die Spalte C1 erstellen und durch das Löschen des gruppierten Rowstore-Indexes einen gruppierten Columnstore-Index erstellen. Wenn Sie bei der Erstellung des gruppierten Columnstore-Indexes explizit `MAXDOP = 1` verwenden, wird der resultierende gruppierte Columnstore-Index nach Spalte C1 sortiert. Bei Angabe von `MAXDOP = 8` können Sie eine Überlappung der Werte über acht Zeilengruppen beobachten. Ein häufiges Szenario für diese Strategie, wenn Sie zu Beginn einen Columnstore-Index mit großer Datenmenge erstellen. Beachten Sie bei einem nicht gruppierten Columnstore-Index (NCCI), dass die grundlegende Rowstore-Tabelle über einen gruppierten Index verfügt. Die Zeilen sind bereits sortiert. In diesem Fall wird der resultierende Columnstore-Index automatisch sortiert. Beachten Sie unbedingt Folgendes: Der Columnstore-Index behält die Reihenfolge der Zeilen nicht inhärent bei. Wenn neue Zeilen eingefügt oder ältere Zeilen aktualisiert werden, müssen Sie den Vorgang ggf. wiederholen, da die Abfrageleistung der Analyse abnehmen kann.    
    
-   **Nutzen Sie die Tabellenpartitionierung.** Sie können den Columnstore-Index partitionieren und dann durch Entfernen der Partition die Anzahl der zu scannenden Zeilengruppen reduzieren. In einer Faktentabelle werden beispielsweise die Einkäufe von Kunden gespeichert, und anhand eines allgemeinen Abfragemusters lassen sich die Einkäufe eines bestimmten Kunden in einem Quartal ermitteln. In diesem Fall können Sie die Einfügereihenfolge mit der Partitionierung für die Spalte „Customer“ kombinieren. Jede Partition enthält zeitlich sortierte Zeilen für einen bestimmten Kunden.    
    
### <a name="2-plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>2. Planen Sie ausreichend Arbeitsspeicher für eine parallele Erstellung von Columnstore-Indizes ein    
 Bei der Erstellung eines Columnstore-Indexes handelt es sich standardmäßig um einen parallel ausgeführten Vorgang, sofern der verfügbare Arbeitsspeicher nicht eingeschränkt ist. Die parallele Indexerstellung erfordert mehr Arbeitsspeicher als die serielle Erstellung des Index. Wenn ausreichend Arbeitsspeicher verfügbar ist, dauert das Erstellen eines Columnstore-Indexes 1,5-mal so lange wie das Erstellen einer B-Struktur für die gleichen Spalten.    
    
 Der Speicherplatz, der für das Erstellen eines Columnstore-Indexes erforderlich ist, hängt von der Anzahl von Spalten, der Anzahl der Zeichenfolgenspalten, dem Grad der Parallelität (Degree of Parallelism, DOP) und von den Eigenschaften der Daten ab. Wenn die Tabelle beispielsweise weniger als eine Million Zeilen aufweist, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur einen Thread, um den Columnstore-Index zu erstellen.    
    
 Wenn die Tabelle mehr als eine Million Zeilen aufweist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber keine ausreichend dimensionierte Arbeitsspeicherzuweisung abrufen kann, um den Index mit MAXDOP zu erstellen, verringert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `MAXDOP` automatisch nach Bedarf, um es auf den verfügbaren Arbeitsspeicher zu beschränken.  In bestimmten Fällen muss DOP auf eins verringert werden, um den Index mit eingeschränktem Arbeitsspeicher zu erstellen.    
    
 Ab SQL [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird die Abfrage immer im Batchmodus ausgeführt. In früheren Versionen wird die Batchausführung nur verwendet, wenn DOP größer als 1 ist.    
    
## <a name="columnstore-performance-explained"></a>Erläuterungen zur Columnstore-Leistung    
 Columnstore-Indizes erzielen eine hohe Abfrageleistung durch die Kombination der Hochgeschwindigkeits-In-Memory-Modusbatchverarbeitung mit Techniken, die E/A-Anforderungen erheblich reduzieren.  Da bei analytischen Abfragen eine große Anzahl von Zeilen gescannt werden, sind diese in der Regel E/A-gebunden, sodass eine E/A-Reduzierung während der Abfrageausführung maßgeblich für das Design der Columnstore-Indizes ist.  Sobald die Daten in den Arbeitsspeicher gelesen wurden, ist es wichtig, dass die Anzahl der In-Memory-Vorgänge reduziert wird.    
    
 Columnstore-Indizes reduzieren die E/A-Vorgänge und optimieren die In-Memory-Vorgänge mithilfe einer hohen Datenkomprimierung sowie der Columnstore-Löschung, der Löschung von Zeilengruppen und der Batchverarbeitung.    
    
### <a name="data-compression"></a>Datenkomprimierung    
 Columnstore-Indizes erzielen eine bis zu 10 Mal höhere Datenkomprimierung als Rowstore-Indizes. Dadurch werden die zum Ausführen der Analyseabfragen erforderlichen E/A-Vorgänge erheblich verringert, wodurch die Abfrageleistung verbessert wird.    
    
-   Columnstore-Indizes lesen komprimierte Daten vom Datenträger, was bedeutet, dass weniger Datenbytes in den Arbeitsspeicher gelesen werden müssen.    
    
-   Columnstore-Indizes speichern Daten in komprimierter Form im Arbeitsspeicher, wodurch E/A-Vorgänge reduziert werden, da die Häufigkeit der Lesevorgänge der gleichen Daten in den Arbeitsspeicher reduziert wird. Beispielsweise können Columnstore-Indizes bei zehnfacher Komprimierung zehnmal mehr Daten im Arbeitsspeicher aufbewahren als bei der Speicherung der Daten in unkomprimierter Form. Wenn sich mehr Daten im Arbeitsspeicher befinden, ist es wahrscheinlicher, dass der Columnstore-Index die benötigten Daten im Arbeitsspeicher findet, wobei zusätzliche Lesevorgänge vom Datenträger anfallen.    
    
-   Columnstore-Indizes komprimieren Daten nach Spalten anstatt nach Zeilen, wodurch hohe Komprimierungsraten erzielt und die Größe der auf dem Datenträger gespeicherten Daten reduziert werden. Jede Spalte wird separat komprimiert und gespeichert.  Daten in einer Spalte haben immer den gleichen Datentyp und tendenziell auch ähnliche Werte. Die Datenkomprimierungstechniken sind sehr gut, um höhere Komprimierungsraten zu erreichen, wenn die Werte ähnlich sind.    
    
-   Wenn eine Faktentabelle beispielsweise Kundenadressen und eine Spalte für das Land enthält, beträgt die Gesamtzahl der möglichen Werte weniger als 200. Einige dieser Werte werden mehrmals wiederholt. Wenn die Faktentabelle 100 Millionen Zeilen enthält, lässt sich die Länderspalte problemlos komprimieren und erfordert nur sehr wenig Speicherplatz. Eine zeilenweise Komprimierung kann auf diese Weise nicht von der Ähnlichkeit der Spaltenwerte profitieren. Daher werden hierbei mehr Bytes verwendet, um die Werte in der Länderspalte zu komprimieren.    
    
### <a name="column-elimination"></a>Spaltenlöschung    
 Columnstore-Indizes überspringen den Lesevorgang von Spalten, die für das Ergebnis der Abfrage nicht erforderlich sind. Durch die sogenannte Spaltenlöschung werden die E/A-Vorgänge für die Abfrageausführung weiter reduziert, wodurch die Abfrageleistung verbessert wird.    
    
-   Die Spaltenlöschung ist möglich, da die Daten nach Spalten organisiert und komprimiert sind. Im Gegensatz dazu werden beim zeilenweisen Speichern von Daten die Werte der einzelnen Zeilen physisch zusammen gespeichert und können nicht problemlos getrennt werden. Der Abfrageprozessor muss eine ganze Zeile einlesen, um bestimmte Spaltenwerte abrufen zu können, wodurch die E/A-Vorgänge erhöht werden, da zusätzliche Daten unnötigerweise in den Arbeitsspeicher gelesen werden.    
    
-   Wenn eine Tabelle beispielsweise 50 Spalten hat und die Abfrage nur 5 dieser Spalten verwendet, ruft der Columnstore-Index nur die 5 Spalten vom Datenträger ab. Das Einlesen der anderen 45 Spalten wird übersprungen. Dadurch werden die E/A-Vorgänge um weitere 90 % reduziert, vorausgesetzt, dass alle Spalten eine ähnliche Größe aufweisen. Wenn die gleichen Daten in einer Zeilengruppe gespeichert sind, muss der Abfrageprozessor die zusätzlichen 45 Spalten lesen.    
    
### <a name="rowgroup-elimination"></a>Zeilengruppenlöschung    
 Bei vollständigen Tabellenscans entspricht ein großer Prozentsatz der Daten in der Regel nicht den Abfrageprädikatskriterien. Mithilfe von Metadaten kann der Columnstore-Index das Einlesen der Zeilengruppen überspringen, die keine für das Abfrageergebnis erforderlichen Daten enthalten. Dabei werden keine tatsächlichen E/A-Vorgänge durchgeführt. Durch die sogenannte Zeilengruppenlöschung werden die E/A-Vorgänge für vollständige Tabellenscans weiter reduziert, wodurch die Abfrageleistung verbessert wird.    
    
 **Wann muss ein Columnstore-Index einen vollständigen Tabellenscan durchführen?**    
    
 Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie einen oder mehrere reguläre nicht gruppierte B-Strukturindizes für einen gruppierten Columnstore-Index genauso wie für einen Rowstore-Heap erstellen. Die nicht gruppierten B-Strukturindizes können eine Abfrage mit einem Gleichheitsprädikat oder einem Prädikat mit einem kleinen Wertebereich beschleunigen.  Bei komplexeren Prädikaten kann der Abfrageoptimierer sich für einen vollständigen Tabellenscan entscheiden. Ohne die Fähigkeit, Zeilengruppen zu überspringen, wäre ein vollständiger Tabellenscan sehr zeitaufwändig, insbesondere bei großen Tabellen.    
    
 **Wann profitiert eine Analyseabfrage von einer Zeilengruppenlöschung für einen vollständigen Tabellenscan?**    
    
 Ein Einzelhandelsunternehmen hat beispielsweise seine Vertriebsdaten mithilfe einer Faktentabelle mit gruppiertem Columnstore-Index modelliert. Bei jedem neuen Verkauf werden verschiedene Attribute der Transaktion gespeichert, einschließlich des Verkaufsdatums eines Produkts. Obwohl Columnstore-Indizes keine sortierte Reihenfolge sicherstellen, werden die Zeilen in dieser Tabelle interessanterweise nach Datum sortiert geladen. Mit der Zeit wächst diese Tabelle. Auch wenn das Einzelhandelsunternehmen Verkaufsdaten der letzten 10 Jahre speichert, muss bei einer Analyseabfrage nur ein Aggregat für das letzte Quartal berechnet werden. Mit Columnstore-Indizes können Sie es vermeiden, auf die Daten der vorherigen 39 Quartale zuzugreifen, indem nur die Metadaten für die Datumsspalte untersucht werden. Dies entspricht einer zusätzlichen Reduzierung der Datenmenge, die in den Arbeitsspeicher gelesen und verarbeitet wird, von 97 %.    
    
 **Welche Zeilengruppen werden bei einem vollständigen Tabellenscan übersprungen?**    
    
 Um zu bestimmen, welche Zeilengruppen gelöscht werden sollen, verwendet der Columnstore-Index Metadaten, um die Mindest- und Maximalwerte jedes Spaltensegments für jede Zeilengruppe zu speichern. Wenn keiner der Spaltensegmentbereiche die Kriterien für Abfrageprädikate erfüllt, wird die gesamte Zeilengruppe übersprungen, ohne tatsächliche E/A-Vorgänge auszuführen. Dies funktioniert, da die Daten in der Regel in sortierter Reihenfolge geladen werden, und auch wenn eine Sortierung der Zeilen nicht garantiert werden kann, befinden sich ähnliche Datenwerte häufig innerhalb derselben Zeilengruppe oder in einer benachbarten Zeilengruppe.    
    
 Weitere Informationen zu Zeilengruppen finden Sie unter „Beschreibung von Columnstore-Indizes“.    
    
### <a name="batch-mode-execution"></a>Batchmodusausführung    
 Bei der Batchmodusausführung handelt es sich um die gemeinsame Verarbeitung eines Zeilensatzes, in der Regel bis zu 900 Zeilen, aus Gründen der Ausführungseffizienz. Die Abfrage `SELECT SUM (Sales) FROM SalesData` aggregiert beispielsweise den Gesamtumsatz aus der Tabelle „SalesData“. Bei der Batchmodusausführung berechnet das Abfrageausführungsmodul das Aggregat in Gruppen von 900 Werten. Dadurch werden Metadaten, Zugriffskosten und andere Aufwandsarten auf alle Zeilen in einem Batch verteilt, anstatt die Kosten für jede Zeile zu zahlen, wodurch der Codepfad erheblich reduziert wird. Bei der Batchmodusverarbeitung kommen, sofern möglich, komprimierte Daten zum Einsatz. Zugleich werden einige der Exchange-Operatoren beseitigt, die bei der Zeilenmodusverarbeitung verwendet werden. Dies beschleunigt die Ausführung von Analyseabfragen in beträchtlichem Maße.    
    
 Nicht alle Abfrageausführungsoperatoren können im Batchmodus ausgeführt werden. DML-Vorgänge, wie z. B. Einfügen, Löschen oder Aktualisieren, werden z. B. Zeile für Zeile ausgeführt. Batchmodusoperatoren richten sich an Operatoren, um die Abfrageleistung wie Scan, Join, Aggregate, Sort und so weiter zu beschleunigen. Da der Columnstore-Index in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt wurde, gibt es eine nachhaltige Initiative, um die Operatoren zu erweitern, die im Batchmodus ausgeführt werden können. Die folgende Tabelle führt die Operatoren auf, die im Batchmodus gemäß der Produktversion ausgeführt werden.    
    
|Batchmodusoperatoren|Einsatz|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)]¹|Kommentare|    
|---------------------------|------------------------|---------------------|---------------------|---------------------------------------|--------------|    
|DML-Vorgänge (Insert, Delete, Update, Merge)||nein|nein|nein|DML ist kein Batchmodusvorgang, da es nicht parallel ist. Auch wenn die serielle Batchmodusverarbeitung aktiviert wird, kommt es zu keiner maßgeblichen Leistungssteigerung, wenn DML im Batchmodus verarbeitet wird.|    
|Columnstore Index Scan|SCAN|NA|ja|ja|Bei Columnstore-Indizes kann das Prädikat mittels Push an den SCAN-Knoten übertragen werden.|    
|Columnstore Index Scan (nicht gruppiert)|SCAN|ja|ja|ja|ja|    
|Index Seek||NA|NA|nein|Es wird ein Suchvorgang im Zeilenmodus durch einen nicht gruppierten B-Strukturindex durchgeführt.|    
|Compute Scalar|Ausdruck, dessen Auswertung einen Skalarwert ergibt.|ja|ja|ja|Es gibt jedoch einige Einschränkungen hinsichtlich des Datentyps. Dies gilt für alle Batchmodusoperatoren.|    
|Verkettung|UNION und UNION ALL|nein|ja|ja||    
|filter|Anwenden von Prädikaten|ja|ja|ja||    
|Hash Match|Hashbasierte Aggregatfunktionen, äußerer Hashjoin, rechter Hashjoin, linker Hashjoin, rechter innerer Join, linker innerer Join|ja|ja|ja|Einschränkungen für die Aggregation: keine Mindest-/Maximalwerte für Zeichenfolgen. Verfügbare Aggregationsfunktionen: sum/count/avg/min/max.<br />Einschränkungen für Join: keine nicht übereinstimmenden Typ-Joins für nicht ganzzahlige Typen.|    
|Merge Join||nein|nein|nein||    
|Multithread-Abfragen||ja|ja|ja||    
|Nested Loops||nein|nein|nein||    
|Singlethread-Abfragen unter MAXDOP 1||nein|nein|ja||    
|Singlethread-Abfragen mit einem seriellen Abfrageplan||nein|nein|ja||    
|Sort|Order by-Klausel für SCAN mit Columnstore-Index|nein|nein|ja||    
|Top Sort||nein|nein|ja||    
|Window Aggregates||NA|NA|ja|Neuer Operator in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|    
    
 ¹gilt für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Tarife Premium, Standard (S3 und höher) und alle virtuelle Kern-Tarife sowie [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]    
    
### <a name="aggregate-pushdown"></a>Aggregatweitergabe    
 Ein normaler Ausführungspfad zur Aggregatberechnung, um die qualifizierenden Zeilen aus dem SCAN-Knoten abzurufen und die Werte im Batchmodus zu aggregieren. Dadurch wird eine gute Leistung bereitgestellt. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] kann der Aggregatvorgang jedoch mittels Push an den SCAN-Knoten weitergegeben werden, um die Leistung der Aggregatberechnung in erheblichem Maße zusätzlich zur Ausführung im Batchmodus zu verbessern, sofern folgende Bedingungen erfüllt sind: 
 
-    Bei den Aggregaten handelt es sich um `MIN`, `MAX`, `SUM`, `COUNT` und `COUNT(*)`. 
-  Der Aggregatoperator muss sich über dem SCAN-Knoten oder über dem SCAN-Knoten mit `GROUP BY` befinden.
-  Dieses Aggregat ist kein eindeutiges Aggregat.
-  Die Aggregatspalte ist keine Zeichenfolgenspalte.
-  Die Aggregatspalte ist keine virtuelle Spalte. 
-  Der Datentyp für die Eingabe und Ausgabe muss einer der folgenden sein und in 64 Bit passen.
    -  `tinyint`, `int`, `bigint`, `smallint`, `bit`
    -  `smallmoney`, `money`, `decimal` und `numeric` mit einer Genauigkeit von <= 18
    -  `smalldate`, `date`, `datetime`, `datetime2`, `time`
    
 Aggregatweitergabe wird durch effiziente Aggregation von komprimierten/codierten Daten bei Cache-entlastender Ausführung und durch Nutzung von SIMD weiter beschleunigt.    
    
 ![aggregate pushdown](../../relational-databases/indexes/media/aggregate-pushdown.jpg "aggregate pushdown")    
    
Die Aggregatweitergabe wird beispielsweise in den beiden folgenden Abfragen durchgeführt:    
    
```sql     
SELECT  productkey, SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
GROUP BY productkey    
    
SELECT  SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
```    
    
### <a name="string-predicate-pushdown"></a>Zeichenfolgenprädikatweitergabe    
Beim Entwurf eines Data Warehouse-Schemas besteht die empfohlene Schemamodellierung darin, ein Sternschema oder Schneeflockenschema zu verwenden, das aus einer oder mehreren Faktentabellen und vielen Dimensionstabellen besteht. Die [Faktentabelle](https://en.wikipedia.org/wiki/Fact_table) speichert die Unternehmensmessungen oder -transaktionen, und die [Dimensionstabelle](https://en.wikipedia.org/wiki/Dimension_table) speichert die Dimensionen, anhand derer die Fakten analysiert werden müssen.    
    
Bei einem Fakt kann es sich beispielsweise um einen Datensatz für den Verkauf eines bestimmten Produkts in einer bestimmten Region handeln, während die Dimension eine Reihe von Regionen, Produkten usw. darstellt. Die Fakten- und Dimensionstabellen sind über eine Primär-/Fremdschlüsselbeziehung miteinander verbunden. Die am häufigsten verwendeten Abfragen verbinden eine oder mehrere Dimensionstabellen mit der Faktentabelle.    
    
Betrachten Sie z.B. eine Dimensionstabelle namens `Products`. Ein typischer Primärschlüssel wäre `ProductCode`, der in der Regel als Zeichenfolgendatentyp dargestellt wird. Für die Abfrageleistung hat es sich bewährt, einen Ersatzschlüssel zu erstellen (in der Regel eine Spalte mit ganzen Zahlen), um aus der Faktentabelle auf die Zeile in der Dimensionstabelle zu verweisen.    
    
Der Columnstore-Index führt die Analyseabfragen mit Joins/Prädikaten mit Schlüsseln auf numerischer Basis bzw. Ganzzahlbasis sehr effizient aus. Bei vielen Kundenworkloads wurden jedoch zeichenfolgenbasierte Spalten verwendet, die Fakt-/Dimensionstabellen verknüpfen. Dies führte dazu, dass die Abfrageleistung mit Columnstore-Indizes nicht gut war. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] verbessert die Leistung von Analyseabfragen mit zeichenfolgenbasierten Spalten erheblich, indem die Prädikate mit Zeichenfolgenspalten an den SCAN-Knoten weitergegeben werden.    
    
Die Weitergabe von Zeichenfolgenprädikaten nutzt zur Verbesserung der Abfrageleistung das primäre bzw. sekundäre Wörterbuch, das für die Spalten erstellt wurde. Nehmen Sie z. B. ein Zeichenfolgenspaltensegment in einer Zeilengruppe, bestehend aus 100 unterschiedlichen Zeichenfolgenwerten. Das bedeutet, dass bei einer Million Zeilen auf jeden einzelnen Zeichenfolgenwert durchschnittlich 10.000 Mal verwiesen wird.    
    
Bei der Zeichenfolgenprädikatweitergabe berechnet die Abfrageausführung das Prädikat anhand der Werte im Wörterbuch. Wenn sich dies qualifiziert, werden alle Zeilen mit Bezug auf den Wörterbuchwert automatisch qualifiziert. Dies verbessert die Leistung auf zwei Arten:
1.  Es wird nur die qualifizierte Zeile zurückgegeben, wodurch die Anzahl der Zeilen reduziert wird, die aus dem SCAN-Knoten übertragen werden müssen. 
2.  Die Anzahl von Zeichenfolgenvergleichen wird maßgeblich verringert. In diesem Beispiel sind nur 100 Zeichenfolgenvergleiche gegenüber einer Millionen Vergleiche erforderlich. Wie im Folgenden beschrieben gibt es einige Einschränkungen:    
    -   Keine Zeichenfolgenprädikatweitergabe für Deltazeilengruppen. Es gibt kein Wörterbuch für Spalten in Deltazeilengruppen.    
    -   Keine Weitergabe von Zeichenfolgenprädikaten, wenn die Einträge im Wörterbuch eine Größe von 64 KB überschreiten.    
    -   Ausdrücke, die als NULL-Werte ausgewertet werden, werden nicht unterstützt.    
    
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
 [Columnstore Indexes Design Guidance (Leitfaden zum Entwerfen von Columnstore-Indizes)](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Columnstore Indexes Data Loading Guidance (Leitfaden zum Laden von Daten in Columnstore-Indizes)](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)     
 [Columnstore-Indizes für Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Columnstore Indexes Defragmentation (Defragmentierung von Columnstore-Indizes)](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)    
 [Columnstore Index Architecture (Columnstore-Indizes: Architektur)](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)     
  
