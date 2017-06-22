---
title: Columnstore-Indizes Abfrageleistung | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83acbcc4-c51e-439e-ac48-6d4048eba189
caps.latest.revision: 23
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b16232d4a183a75dd9cf76e57ca0751df19e3a2f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="columnstore-indexes---query-performance"></a>Columnstore-Indizes Abfrageleistung
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Empfehlungen zum Erreichen der sehr schnellen Abfrageleistung, die Columnstore-Indizes vom Design her bereitstellen können sollten.    
    
 Columnstore-Indizes können eine bis zu 100-fach bessere Leistung für Analyse- und Data Warehousing-Arbeitsauslastungen und eine bis zu 10-fach bessere Datenkomprimierung als herkömmliche Rowstore-Indizes erreichen.   Diese Empfehlungen helfen Ihnen, eine sehr schnelle Abfrageleistung zu erzielen, die Columnstore-Indizes vom Design her bereitstellen können sollten.  Weitere Erläuterungen zur Columnstore-Leistung finden Sie am Ende.    
    
## <a name="recommendations-for-improving-query-performance"></a>Empfehlungen zur Verbesserung der Abfrageleistung    
 Im Folgenden finden Sie einige Empfehlungen zum Erreichen der hohen Leistung, die Columnstore-Indizes vom Design her bereitstellen können sollten.    
    
### <a name="1-organize-data-to-eliminate-more-rowgroups-from-a-full-table-scan"></a>1. Organisieren Sie Daten, um weitere Zeilengruppen im Rahmen eines vollständigen Tabellenscans zu beseitigen.    
    
-   **Nutzen Sie die Einfügereihenfolge.** Im Allgemeinen werden in einem herkömmlichen Data Warehouse die Daten tatsächlich in zeitlicher Reihenfolge eingefügt und die Analyse erfolgt in der Zeitdimension. Beispiel: Analyse der Umsätze nach Quartal. Für diese Art der Arbeitsauslastung wird das Löschen der Zeilengruppe automatisch durchgeführt. In SQL Server 2016 können Sie die Anzahl der Zeilengruppen ermitteln, die als Teil der Abfrageverarbeitung ausgelassen werden.    
    
-   **Nutzen Sie den gruppierten Rowstore-Index.** Wenn das allgemeine Abfrageprädikat für eine Spalte (z. B. C1) gilt, die nicht mit der Einfügereihenfolge der Zeile verbunden ist, können Sie einen gruppierten Rowstore-Index für die Spalten C1 erstellen und durch das Löschen des gruppierten Rowstore-Indexes einen gruppierten Columnstore-Index erstellen. Wenn Sie bei der Erstellung des gruppierten Columnstore-Indexes explizit DOP (Grad an Parallelität) = 1 verwenden, wird der resultierende gruppierte Columnstore-Index perfekt nach Spalte C1 sortiert. Bei Angabe von DOP = 8 können Sie eine Überlappung der Werte über acht Zeilengruppen beobachten.  Ein häufiges Szenario für diese Strategie, wenn Sie zu Beginn einen Columnstore-Index mit großer Datenmenge erstellen. Beachten Sie bei einem nicht gruppierten Columnstore-Index (NCCI), dass die grundlegende Rowstore-Tabelle über einen gruppierten Index verfügt. Die Zeilen sind bereits sortiert. In diesem Fall wird der resultierende Columnstore-Index automatisch sortiert. Beachten Sie unbedingt Folgendes: Der Columnstore-Index behält die Reihenfolge der Zeilen nicht inhärent bei. Wenn neue Zeilen eingefügt oder ältere Zeilen aktualisiert werden, müssen Sie den Vorgang ggf. wiederholen, da die Abfrageleistung der Analyse abnehmen kann.    
    
-   **Nutzen Sie die Tabellenpartitionierung.** Sie können den Columnstore-Index partitionieren und dann durch Entfernen der Partition die Anzahl der zu scannenden Zeilengruppen reduzieren. In einer Faktentabelle werden beispielsweise die Einkäufe von Kunden gespeichert, und anhand eines allgemeinen Abfragemusters lassen sich die Einkäufe eines bestimmten Kunden in einem Quartal ermitteln. In diesem Fall können Sie die Einfügereihenfolge mit der Partitionierung für die Customer-Spalte kombinieren. Jede Partition enthält zeitlich sortierte Zeilen für einen bestimmten Kunden.    
    
### <a name="2-plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>2. Planen Sie ausreichend Arbeitsspeicher für eine parallele Erstellung von Columnstore-Indizes ein    
 Bei der Erstellung eines Columnstore-Indexes handelt es sich standardmäßig um einen parallel ausgeführten Vorgang, sofern der verfügbare Arbeitsspeicher nicht eingeschränkt ist. Die parallele Indexerstellung erfordert mehr Arbeitsspeicher als die serielle Erstellung des Index. Wenn ausreichend Arbeitsspeicher verfügbar ist, dauert das Erstellen eines Columnstore-Indexes 1,5-mal so lange wie das Erstellen einer B-Struktur für die gleichen Spalten.    
    
 Der Speicherplatz, der für das Erstellen eines Columnstore-Indexes erforderlich ist, hängt von der Anzahl von Spalten, der Anzahl der Zeichenfolgenspalten, dem Grad der Parallelität (Degree of Parallelism, DOP) und von den Eigenschaften der Daten ab. Wenn die Tabelle beispielsweise weniger als eine Million Zeilen aufweist, verwendet SQL Server nur einen Thread, um den Columnstore-Index zu erstellen.    
    
 Wenn die Tabelle mehr als eine Million Zeilen aufweist, SQL Server aber keine ausreichend dimensionierte Arbeitsspeicherzuweisung abrufen kann, um den Index mit MAXDOP zu erstellen, verringert SQL Server MAXDOP automatisch nach Bedarf, um es auf den verfügbaren Arbeitsspeicher zu beschränken.  In bestimmten Fällen muss DOP auf eins verringert werden, um den Index mit eingeschränktem Arbeitsspeicher zu erstellen.    
    
 Ab SQL Server 2016 wird die Abfrage immer im Batchmodus ausgeführt. In früheren Versionen wird die Batchausführung nur verwendet, wenn DOP größer als 1 ist.    
    
## <a name="columnstore-performance-explained"></a>Erläuterungen zur Columnstore-Leistung    
 Columnstore-Indizes erzielen eine hohe Abfrageleistung durch die Kombination der Hochgeschwindigkeits-In-Memory-Modusbatchverarbeitung mit Techniken, die die E/A-Anforderungen erheblich reduzieren.  Da bei der analytischen Abfrage eine große Anzahl von Zeilen gescannt werden, sind sie in der Regel E/A-gebunden, sodass eine E/A-Reduzierung während der Abfrageausführung maßgeblich für das Design der Columnstore-Indizes ist.  Sobald die Daten in den Arbeitsspeicher gelesen wurden, ist es wichtig, dass die Anzahl der In-Memory-Vorgänge reduziert wird.    
    
 Columnstore-Indizes reduzieren die E/A und optimieren die In-Memory-Vorgänge mithilfe einer hohen Datenkomprimierung, Columnstore-Löschung, Löschung von Zeilengruppen und Batchverarbeitung.    
    
### <a name="data-compression"></a>Datenkomprimierung    
 Columnstore-Indizes erzielen eine bis zu 10 Mal höhere Datenkomprimierung als Rowstore-Indizes.  Dadurch wird die zum Ausführen der Analyseabfragen erforderliche E/A erheblich verringert, womit wiederum die Abfrageleistung verbessert wird.    
    
-   Columnstore-Indizes lesen komprimierte Daten vom Datenträger, was bedeutet, dass weniger Datenbytes in den Arbeitsspeicher gelesen werden müssen.    
    
-   Columnstore-Indizes speichern Daten in komprimierter Form im Arbeitsspeicher, wodurch die E/A reduziert wird, da die Häufigkeit der Lesevorgänge der gleichen Daten in den Arbeitsspeicher reduziert wird.  Beispielsweise können Columnstore-Indizes bei 10-facher Komprimierung 10 Mal mehr Daten im Arbeitsspeicher aufbewahren als wenn die Daten in unkomprimierter Form gespeichert werden. Wenn sich mehr Daten im Arbeitsspeicher befinden, ist es wahrscheinlicher, dass der Columnstore-Index die benötigten Daten im Arbeitsspeicher findet, wobei zusätzliche Lesevorgänge vom Datenträger anfallen.    
    
-   Columnstore-Indizes komprimieren Daten nach Spalten anstatt nach Zeilen, wodurch hohe Komprimierungsraten erzielt und die Größe der auf dem Datenträger gespeicherten Daten reduziert werden. Jede Spalte wird separat komprimiert und gespeichert.  Daten in einer Spalte haben immer den gleichen Datentyp und tendenziell auch ähnliche Werte. Die Datenkomprimierungstechniken sind sehr gut, um höhere Komprimierungsraten zu erreichen, wenn die Werte ähnlich sind.    
    
-   Wenn eine Faktentabelle beispielsweise Kundenadressen enthält und eine Spalte für das Land, beträgt die Gesamtzahl der möglichen Werte weniger als 200.  Einige dieser Werte werden mehrmals wiederholt.  Wenn die Faktentabelle 100 Millionen Zeilen enthält, lässt sich die Länderspalte problemlos komprimieren und erfordert nur sehr wenig Speicherplatz. Eine zeilenweise Komprimierung kann auf diese Weise nicht von der Ähnlichkeit der Spaltenwerte profitieren. Daher werden hierbei mehr Bytes verwendet, um die Werte in der Länderspalte zu komprimieren.    
    
### <a name="column-elimination"></a>Spaltenlöschung    
 Columnstore-Indizes überspringen den Lesevorgang von Spalten, die für das Ergebnis der Abfrage nicht erforderlich sind. Dank dieser Fähigkeit, auch Spaltenlöschung genannt, wird die E/A für die Abfrageausführung weiter reduziert, was die Abfrageleistung verbessert.    
    
-   Die Spaltenlöschung ist möglich, da die Daten nach Spalten organisiert und komprimiert sind.   Im Gegensatz dazu werden beim zeilenweisen Speichern von Daten die Werte der einzelnen Zeilen physisch zusammen gespeichert und können nicht problemlos getrennt werden. Der Abfrageprozessor muss eine ganze Zeile einlesen, um bestimmte Spaltenwerte abrufen zu können, wodurch die E/A erhöht wird, da zusätzliche Daten unnötigerweise in den Arbeitsspeicher gelesen werden.    
    
-   Wenn eine Tabelle beispielsweise 50 Spalten hat und die Abfrage nur 5 dieser Spalten verwendet, ruft der Columnstore-Index nur die 5 Spalten vom Datenträger ab. Das Einlesen der anderen 45 Spalten wird übersprungen. Dies reduziert die E/A um weitere 90 %, vorausgesetzt alle Spalten haben eine ähnliche Größe.  Wenn die gleichen Daten in einer Zeilengruppe gespeichert sind, muss der Abfrageprozessor die zusätzlichen 45 Spalten lesen.    
    
### <a name="rowgroup-elimination"></a>Zeilengruppenlöschung    
 Bei vollständigen Tabellenscans entspricht ein großer Prozentsatz der Daten in der Regel nicht den Abfrageprädikatskriterien. Mithilfe von Metadaten kann der Columnstore-Index das Einlesen der Zeilengruppen überspringen, die keine für das Abfrageergebnis erforderlichen Daten enthalten, und das alles ohne tatsächliche E/A.  Dank dieser Fähigkeit, auch Zeilengruppenlöschung genannt, wird die E/A für vollständige Tabellenscans weiter reduziert, was die Abfrageleistung verbessert.    
    
 **Wann muss ein Columnstore-Index einen vollständigen Tabellenscan durchführen?**    
    
 Ab SQL Server 2016 können Sie einen oder mehrere reguläre nicht gruppierte BTree-Indizes für einen gruppierten Columnstore-Index genauso wie für einen Rowstore-Heap erstellen.  Die nicht gruppierten BTree-Indizes können eine Abfrage mit einem Gleichheitsprädikat oder einem Prädikat mit einem kleinen Wertebereich beschleunigen.  Bei komplexeren Prädikaten kann der Abfrageoptimierer sich für einen vollständigen Tabellenscan entscheiden. Ohne die Fähigkeit, Zeilengruppen zu überspringen, wäre ein vollständiger Tabellenscan sehr zeitaufwändig, insbesondere bei großen Tabellen.    
    
 **Wann profitiert eine Analyseabfrage von einer Zeilengruppenlöschung für einen vollständigen Tabellenscan?**    
    
 Ein Einzelhandelsunternehmen hat beispielsweise seine Vertriebsdaten mithilfe einer Faktentabelle mit gruppiertem Columnstore-Index modelliert. Bei jedem neuen Verkauf werden verschiedene Attribute der Transaktion gespeichert, einschließlich des Verkaufsdatums. Obwohl Columnstore-Indizes keine sortierte Reihenfolge sicherstellen, werden die Zeilen in dieser Tabelle interessanterweise nach Datum sortiert geladen.   Mit der Zeit wächst diese Tabelle. Auch wenn das Einzelhandelsunternehmen Verkaufsdaten der letzten 10 Jahre speichert, muss bei einer Analyseabfrage nur ein Aggregat für das letzte Quartal berechnet werden. Mit Columnstore-Indizes können Sie es vermeiden, auf die Daten der vorherigen 39 Quartale zuzugreifen, indem nur die Metadaten für die Datumsspalte untersucht werden.  Dies entspricht einer zusätzlichen Reduzierung der Datenmenge, die in den Arbeitsspeicher gelesen und verarbeitet wird, von 97 %.    
    
 **Welche Zeilengruppen werden bei einem vollständigen Tabellenscan übersprungen?**    
    
 Um zu bestimmen, welche Zeilengruppen gelöscht werden sollen, verwendet der Columnstore-Index Metadaten, um die Mindest- und Maximalwerte jedes Spaltensegments für jede Zeilengruppe zu speichern. Wenn keiner der Spaltensegmentbereiche die Abfrageprädikatskriterien erfüllt, wird die gesamte Zeilengruppe übersprungen, ohne tatsächliche E/A-Vorgänge auszuführen. Dies funktioniert, da die Daten in der Regel in sortierter Reihenfolge geladen werden, und auch wenn eine Sortierung der Zeilen nicht garantiert werden kann, befinden sich ähnliche Datenwerte häufig innerhalb derselben Zeilengruppe oder in einer benachbarten Zeilengruppe.    
    
 Weitere Informationen zu Zeilengruppen finden Sie unter „Beschreibung von Columnstore-Indizes“.    
    
### <a name="batch-mode-execution"></a>Batchmodusausführung    
 Bei der Batchmodusausführung handelt es sich um die gemeinsame Verarbeitung eines Zeilensatzes, in der Regel bis zu 900 Zeilen, aus Gründen der Ausführungseffizienz. Beispiel: Die Abfrage  `Select SUM (Sales)from SalesData` aggregiert den Gesamtumsatz aus der Tabelle „SalesData“.    Bei der Batchmodusausführung berechnet das Abfrageausführungsmodul das Aggregat in Gruppen von 900 Werten.  Dadurch werden Metadaten, Zugriffskosten und andere Aufwandsarten auf alle Zeilen in einem Batch verteilt, anstatt die Kosten für jede Zeile zu zahlen, wodurch der Codepfad erheblich reduziert wird.  Bei der Batchmodusverarbeitung kommen, sofern möglich, komprimierte Daten zum Einsatz. Zugleich werden einige der Exchange-Operatoren beseitigt, die bei der Zeilenmodusverarbeitung verwendet werden.  Dies beschleunigt die Ausführung von Analyseabfragen in beträchtlichem Maße.    
    
 Nicht alle Abfrageausführungsoperatoren können im Batchmodus ausgeführt werden. DML-Vorgänge, wie z. B. Einfügen, Löschen oder Aktualisieren, werden z. B. Zeile für Zeile ausgeführt. Batchmodusoperatoren richten sich an Operatoren, um die Abfrageleistung wie Scan, Join, Aggregate, Sort und so weiter zu beschleunigen.  Da der Columnstore-Index in SQL Server 2012 eingeführt wurde, gibt es eine nachhaltige Initiative, um die Operatoren zu erweitern, die im Batchmodus ausgeführt werden können. Die folgende Tabelle zeigt die Operatoren, die im Batchmodus gemäß der Produktversion ausgeführt werden.    
    
|Batchmodusoperatoren|Einsatz|SQL Server 2012|SQL Server 2014|SQL Server 2016 und SQL-Datenbank¹|Kommentare|    
|---------------------------|------------------------|---------------------|---------------------|---------------------------------------|--------------|    
|DML-Vorgänge (Insert, Delete, Update, Merge)||Nein|Nein|Nein|DML ist kein Batchmodusvorgang, da es nicht parallel ist. Auch wenn die serielle Batchmodusverarbeitung aktiviert wird, kommt es zu keiner maßgeblichen Leistungssteigerung, wenn DML im Batchmodus verarbeitet wird.|    
|Columnstore Index Scan|SCAN|NA|Ja|Ja|Bei Columnstore-Indizes kann das Prädikat mittels Push an den SCAN-Knoten übertragen werden.|    
|Columnstore Index Scan (nicht gruppiert)|SCAN|Ja|Ja|Ja|Ja|    
|Index Seek||NA|NA|Nein|Es wird ein Suchvorgang im Zeilenmodus durch einen nicht gruppierten BTree-Index durchgeführt.|    
|Compute Scalar|Ausdruck, dessen Auswertung einen Skalarwert ergibt.|Ja|Ja|Ja|Es gibt jedoch einige Einschränkungen hinsichtlich des Datentyps. Dies gilt für alle Batchmodusoperatoren.|    
|Verkettung|UNION und UNION ALL|Nein|Ja|Ja||    
|filter|Anwenden von Prädikaten|Ja|Ja|Ja||    
|Hash Match|Hashbasierte Aggregatfunktionen, äußerer Hashjoin, rechter Hashjoin, linker Hashjoin, rechter innerer Join, linker innerer Join|Ja|Ja|Ja|Einschränkungen für die Aggregation: keine Mindest-/Maximalwerte für Zeichenfolgen. Verfügbare Aggregationsfunktionen: sum/count/avg/min/max.<br />Einschränkungen für Join: keine nicht übereinstimmenden Typ-Joins für nicht ganzzahlige Typen.|    
|Merge Join||Nein|Nein|Nein||    
|Multithread-Abfragen||Ja|Ja|Ja||    
|Nested Loops||Nein|Nein|Nein||    
|Singlethread-Abfragen unter MAXDOP 1||Nein|Nein|Ja||    
|Singlethread-Abfragen mit einem seriellen Abfrageplan||Nein|Nein|Ja||    
|Sort|Order by-Klausel für SCAN mit Columnstore-Index|Nein|Nein|Ja||    
|Top Sort||Nein|Nein|Ja||    
|Window Aggregates||NA|NA|Ja|Neuer Operator in SQL Server 2016.|    
    
 ¹Gilt für SQL Server 2016, SQL-Datenbank V12 Premium-Edition und SQL Data Warehouse    
    
### <a name="aggregate-pushdown"></a>Aggregatweitergabe    
 Eine normaler Ausführungspfad zur Aggregatsberechnung, um die qualifizierenden Zeilen aus dem SCAN-Knoten abzurufen und die Werte im Batchmodus zu aggregieren.  Dies bietet eine gute Leistung. Ab SQL Server 2016 kann der Aggregatsvorgang jedoch mittels Push an den SCAN-Knoten weitergegeben werden, um die Leistung der Aggregatsberechnung in erheblichem Maße zusätzlich zum Batchmodus auszuführen, sofern folgende Bedingungen erfüllt sind    
    
-   Unterstützte Aggregatoperatoren sind: MIN, MAX, SUM, COUNT, AVG    
    
-   Jeder Datentyp <= 64 Bit wird unterstützt.  Bigint wird z. B. unterstützt, da seine Größe 8 Bytes beträgt, dezimal (38,6) wird jedoch nicht unterstützt, da es 17 Bytes groß ist. Außerdem werden keine Zeichenfolgentypen unterstützt.    
    
-   Aggregatoperator muss über dem SCAN-Knoten oder SCAN-Knoten mit Group by sein    
    
 Aggregatweitergabe wird durch effiziente Aggregation von komprimierten/codierten Daten bei Cache-entlastender Ausführung und durch Nutzung von SIMD weiter beschleunigt.    
    
 ![aggregate pushdown](../../relational-databases/indexes/media/aggregate-pushdown.jpg "aggregate pushdown")    
    
 Aggregatweitergabe wird beispielsweise in den beiden folgenden Abfragen durchgeführt:    
    
```    
    
SELECT  productkey, SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
GROUP BY productkey    
    
SELECT  SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
```    
    
### <a name="string-predicate-pushdown"></a>Zeichenfolgenprädikatweitergabe    
 Motivation: Beim Entwurf eines Data Warehouse-Schemas besteht die empfohlene Schemamodellierung darin, ein Sternschema oder Schneeflockenschema zu verwenden, das aus einer oder mehreren Faktentabellen und vielen Dimensionstabellen besteht. Die [Faktentabelle](https://en.wikipedia.org/wiki/Fact_table) speichert die Unternehmensmessungen oder -transaktionen, und die [Dimensionstabelle](https://en.wikipedia.org/wiki/Dimension_table) speichert die Dimensionen, anhand derer die Fakten analysiert werden müssen.    
    
 Bei einem Fakt kann es sich beispielsweise um einen Datensatz für den Verkauf eines bestimmten Produkts in einer bestimmten Region handeln, während die Dimension eine Reihe von Regionen, Produkten usw. darstellt. Die Fakten- und Dimensionstabellen sind über die Primär-/Fremdschlüsselbeziehung miteinander verbunden. Die am häufigsten verwendeten Abfragen verbinden eine oder mehrere Dimensionstabellen mit der Faktentabelle.    
    
 Betrachten Sie z. B. eine Dimensionstabelle namens „products“. Ein typischer Primärschlüssel wäre „productcode“, der in der Regel als Zeichenfolgendatentyp dargestellt wird.  Für die Abfrageleistung hat es sich bewährt, einen Ersatzschlüssel zu erstellen, in der Regel eine Integer-Spalte, um aus der Faktentabelle auf die Zeile in der Dimensionstabelle zu verweisen.    
    
 Der Columnstore-Index führt die Analyseabfragen mit Joins/Prädikaten mit Schlüsseln auf numerischer Basis bzw. Ganzzahlbasis sehr effizient aus.   Bei vielen Kundenarbeitsauslastungen wurden jedoch zeichenfolgenbasierte Spalten verwendet, die Fakt-/Dimensionstabellen verknüpfen, mit dem Ergebnis, dass die Abfrageleistung mit Columnstore-Index nicht so gut war.    SQL Server 2016 verbessert die Leistung von Analyseabfragen mit zeichenfolgenbasierten Spalten erheblich, indem die Prädikate mit Zeichenfolgenspalten an den SCAN-Knoten weitergegeben werden.    
    
 Die Zeichenfolgenprädikatweitergabe nutzt das primäre/sekundäre Wörterbuch, das bzw. die für Spalten erstellt wurde(n), um die Abfrageleistung zu verbessern.  Nehmen Sie z. B. ein Zeichenfolgenspaltensegment in einer Zeilengruppe, bestehend aus 100 unterschiedlichen Zeichenfolgenwerten. Dies bedeutet, dass jeder einzelne Zeichenfolgenwert bei einer Millionen Zeilen durchschnittlich 10.000 Mal referenziert wird.    
    
 Bei der Zeichenfolgenprädikatweitergabe berechnet die Abfrageausführung das Prädikat anhand der Werte im Wörterbuch. Wenn sich dies qualifiziert, werden alle Zeilen mit Bezug auf den Wörterbuchwert automatisch qualifiziert.   Dies verbessert die Leistung auf zwei Arten. Zunächst wird nur die qualifizierte Zeile zurückgegeben, wodurch die Anzahl der Zeilen reduziert wird, die aus dem SCAN-Knoten übertragen werden müssen. Dann wird die Anzahl von Zeichenfolgenvergleichen maßgeblich verringert. In diesem Beispiel sind nur 100 Zeichenfolgenvergleiche gegenüber einer Millionen Vergleiche erforderlich.     Es gibt einige Einschränkungen, wie unten beschrieben.    
    
-   Keine Zeichenfolgenprädikatweitergabe für Deltazeilengruppen. Es gibt kein Wörterbuch für Spalten in Deltazeilengruppen    
    
-   Keine Zeichenfolgenprädikatweitergabe wenn das Wörterbuch 64.000 Einträge überschreitet    
    
-   Ausdrücke, die als NULL-Werte ausgewertet werden, werden nicht unterstützt    
    
## <a name="see-also"></a>Siehe auch    
 Beschreibung von Columnstore-Indizes     
 Laden von Daten für Columnstore-Indizes     
 Columnstore-Indizes, Zusammenfassung der Funktionen nach Version     
 [Abfrageleistung für Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-query-performance.md)     
 [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)     
 Columnstore-Indizes für Data Warehousing     
 [Columnstore-Index-Defragmentierung](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)    
    
  

