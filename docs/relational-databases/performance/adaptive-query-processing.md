---
title: Adaptive Abfrageverarbeitung in SQL-Datenbanken von Microsoft | Microsoft-Dokumentation
description: Funktionen zur adaptiven Abfrageverarbeitung, die die Abfrageleistung in SQL Server (2017 und höher) und in der Azure SQL-Datenbank verbessern
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54daefe15f62d9ccc708770f25b7603ae817872c
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="adaptive-query-processing-in-sql-databases"></a>Adaptive Abfrageverarbeitung in SQL-Datenbanken
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

In diesem Artikel werden die folgenden Features zur adaptiven Abfrageverarbeitung beschrieben, die Sie zur Verbesserung der Abfrageleistung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] verwenden können:
- Feedback zur Speicherzuweisung im Batchmodus
- Adaptiver Join im Batchmodus
- Verschachtelte Ausführung 

Prinzipiell führt SQL Server eine Abfrage wie folgt durch:
1. Der Prozess der Abfragenoptimierung generiert einen Satz von durchführbaren Ausführungsplänen für bestimmten Abfragen. Währenddessen wird der Aufwand der Planoptionen geschätzt, und der Plan mit dem geringsten Aufwand wird verwendet.
1. Der Prozess der Abfrageausführung verwendet den vom Abfrageoptimierer ausgewählten Plan zum Ausführen.
    
Manchmal ist der vom Abfrageoptimierer ausgewählte Plan nicht optimal. Dies kann mehrere Gründe haben. Beispielsweise kann die Zahl der Reihen, die durch den Abfrageplan laufen, inkorrekt sein. Der geschätzte Aufwand hilft dabei, zu bestimmen, welcher Plan bei der Ausführung verwendet wird. Wenn die Kardinalitätsschätzungen inkorrekt sind, wird der ursprüngliche Plan trotz der schlechten ursprünglichen Schätzung verwendet.

![Funktionen der adaptiven Abfrageverarbeitung](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>So aktivieren Sie die adaptive Abfrageverarbeitung
Sie können Workloads automatisch für die adaptive Abfrageverarbeitung zulassen, indem Sie den Kompatibilitätsgrad 140 für die Datenbank aktivieren.  Diesen können Sie mit Transact-SQL festlegen. Zum Beispiel:  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```

## <a name="batch-mode-memory-grant-feedback"></a>Feedback zur Speicherzuweisung im Batchmodus
Der Plan nach der Ausführung einer Abfrage in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält den für die Ausführung mindestens erforderlichen Speicherplatz und die ideale Speicherzuweisungsgröße, sodass alle Zeilen in den Speicher passen. Es gibt Leistungseinbußen, wenn die Speicherzuweisungsgrößen falsch sind. Zu große Zuweisungen führen zu verschwendetem Speicherplatz und geringerer Parallelität. Nicht ausreichende Speicherzuweisungen führen zu teuren Überläufen auf den Datenträger. Für wiederholte Workloads berechnet das Feedback zur Speicherzuweisung im Batchmodus den tatsächlich erforderlichen Speicherplatz für eine Abfrage neu und aktualisiert anschließend den Zuweisungswert des zwischengespeicherten Plans.  Wenn eine identische Abfrageanweisung ausgeführt wird, verwendet die Abfrage die angepasste Speicherzuweisungsgröße. Dadurch werden zu hohe Speicherzuweisungen verringert, die die Parallelität beeinträchtigen, und Probleme bei zu gering geschätzten Speicherzuweisungen behoben, die teuren Überläufe auf den Datenträger verursachen.
Der folgende Graph veranschaulicht ein Beispiel für den Gebrauch des Feedbacks zur adaptiven Speicherzuweisung im Batchmodus. Die erste Ausführung der Abfrage hat aufgrund von einer hoher Zahl von Überlaufen **88 Sekunden** in Anspruch genommen:   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![Hohe Zahl von Überläufen](./media/2_AQPGraphHighSpills.png)

Wenn das Feedback zur Speicherzuweisung aktiviert ist, dauert die zweite Ausführung **1 Sekunde** (vorher 88 Sekunden), Überläufe treten nicht mehr auf, und die Zuweisung ist höher: 

![Keine Überläufe](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>Größenanpassung des Feedbacks zur Speicherzuweisung im Batchmodus
Wenn bei einer Bedingung mit einer zu großen Speicherzuweisung der zugewiesene Speicher mehr als doppelt so groß ist als der tatsächlich verwendete Speicher, berechnet das Feedback zur Speicherzuweisung diese neu und aktualisiert den zwischengespeicherten Plan. Pläne mit Speicherzuweisungen unter 1 MB werden bei Überschreitungen nicht neu berechnet.
Bei einer Bedingung mit zu geringen Speicherzuweisungen, die bei Batchmodusoperatoren zu einem Überlauf auf einen Datenträger führen, löst das Feedback zur Speicherzuweisung eine Neuberechnung der Speicherzuweisung aus. Überlaufereignisse werden an das Feedback zur Speicherzuweisung gemeldet und können als XEvent-Ereignis *spilling_report_to_memory_grant_feedback* angegeben werden. Dieses Ereignis gibt die Knoten-ID aus dem Plan und der Größe der übergelaufenen Daten dieses Knotens zurück.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>Feedback zur Speicherzuweisung und parameterempfindliche Szenarios
Verschiedene Parameterwerte können auch unterschiedliche Abfragepläne erfordern, um optimale Ergebnisse zu bieten. Diese Art von Abfrage wird als „parameterempfindlich“ bezeichnet. Bei parameterempfindlichen Plänen deaktiviert sich das Feedback zur Speicherzuweisung in Abfragen selbst, wenn es nicht stabile Speicheranforderungen aufweist. Der Plan wird nach mehreren wiederholten Abfrageausführungen deaktiviert. Dies können Sie beobachten, indem Sie das XEvent *memory_grant_feedback_loop_disabled* überwachen. Weitere Informationen zur Parameterermittlung und -empfindlichkeit finden Sie im [Leitfaden zur Architektur der Abfrageverarbeitung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing).

### <a name="memory-grant-feedback-caching"></a>Caching des Feedbacks zur Speicherzuweisung
Das Feedback kann für eine einzelne Ausführung in einem zwischengespeicherten Plan gespeichert werden. Allerdings sind es aufeinanderfolgende Ausführungen dieser Anweisung, die von Anpassungen des Feedbacks zur Speicherzuweisung profitieren. Diese Funktion wird bei wiederholten Ausführungen von Anweisungen angewendet. Das Feedback zur Speicherzuweisung ändert nur den zwischengespeicherten Plan. Änderungen werden aktuell nicht im Abfragespeicher erfasst.
Das Feedback wird nicht übernommen, wenn der Plan aus dem Cache entfernt wird. Das Feedback geht ebenso verloren, wenn es zu einem Failover kommt. Eine Anweisung mit `OPTION (RECOMPILE)` erstellt einen neuen Plan und speichert diesen nicht zwischen. Da er nicht zwischengespeichert wird, wird auch kein Feedback zur Speicherzuweisung erzeugt und für diese Kompilierung und Ausführung auch nicht gespeichert.  Wenn allerdings eine äquivalente Anweisung (d.h. eine Anweisung mit dem gleichen Abfragehash), die **nicht** `OPTION (RECOMPILE)` verwendet hat, zwischengespeichert und dann erneut ausgeführt wird, kann die darauffolgende Anweisung vom Feedback zur Speicherzuweisung profitieren.

### <a name="tracking-memory-grant-feedback-activity"></a>Nachverfolgen der Aktivität des Feedbacks zur Speicherzuweisung
Sie können Ereignisse des Feedbacks zur Speicherzuweisung mit dem XEvent-Ereignis *memory_grant_updated_by_feedback* nachverfolgen. Dieses Ereignis verfolgt den Verlauf der Ausführungsanzahl, die Zahl von Aktualisierungen des Plans durch das Feedback zur Speicherzuweisung und die optimale zusätzliche Speicherzuweisung vor der Anpassung und nach der Anpassung des zwischengespeicherten Plans durch das Feedback zur Speicherzuweisung.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>Feedback zur Speicherzuweisung, Ressourcenkontrolle und Abfragehinweise
Der tatsächlich zugewiesene Speicher berücksichtigt die Abfragespeichereinschränkung, die von der Ressourcenkontrolle oder dem Abfragehinweis bestimmt wird.

## <a name="batch-mode-adaptive-joins"></a>Adaptive Joins im Batchmodus
Mit dem Feature der adaptiven Joins im Batchmodus können Sie wählen, ob Methoden für [Hashjoins oder Joins geschachtelter Schleifen](../../relational-databases/performance/joins.md) auf **nach** der Überprüfung der ersten Eingabe zurückgestellt werden. Der Operator für adaptive Joins definiert einen Schwellenwert, der bestimmt, wann zu einem Plan geschachtelter Schleifen gewechselt wird. Daher kann Ihr Plan während der Ausführung dynamisch zu einer passenderen Joinstrategie wechseln.
Funktionsweise:
-  Wenn die Anzahl der Zeilen der Buildjoineingabe so klein ist, dass ein Join geschachtelter Schleifen passender als ein Hashjoin wäre, wechselt Ihr Plan zu einem Algorithmus geschachtelter Schleifen.
-  Wenn die Buildjoineingabe eine bestimmte Anzahl an Zeilen übersteigt, wird nicht gewechselt, und Ihr Plan wird mit einem Hashjoin fortgesetzt.

Die folgende Abfrage veranschaulicht ein Beispiel für einen adaptiven Join:

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

Die Abfrage gibt 336 Zeilen zurück. Wenn Sie die [Liveabfragestatistik](../../relational-databases/performance/live-query-statistics.MD) aktivieren, sehen Sie den folgenden Plan:

![Abfrageergebnis: 336 Zeilen](./media/4_AQPStats336Rows.png)

Im Plan sehen wir das Folgende:
1. Ein Columnstore-Indexscan wurde verwendet, um Zeilen für die Buildphase des Hashjoins bereitzustellen.
1. Wir sehen den neuen Operator für adaptive Joins. Dieser Operator definiert einen Schwellenwert, der bestimmt, wann zu einem Plan geschachtelter Schleifen gewechselt wird. In diesem Beispiel beträgt der Schwellenwert 78 Zeilen. Alles, was &gt;= 78 Zeilen enthält, verwendet einen Hashjoin. Wenn der Schwellenwert nicht überschritten wird, wird ein Join geschachtelter Schleifen verwendet.
1. Da 336 Zeilen zurückgegeben werden, wird der Schwellenwert überschritten. Deshalb stellt der zweite Branch die Überprüfungsphase eines standardmäßigen Hashjoinvorgangs dar. Beachten Sie, dass die Liveabfragestatistik Zeilen anzeigt, die den Operator durchlaufen: in diesem Fall „672 von 672“.
1. Der letzte Branch ist der Clustered Index Seek, der vom Nested Loop-Join verwendet worden wäre, wäre der Schwellenwert nicht überschritten worden. Beachten Sie, dass „0 von 336“ Zeilen angezeigt werden (der Branch wird nicht verwendet).
 Schauen wir uns nun den Plan für die gleiche Abfrage, aber dieses Mal mit einem *Mengenwert* an, der nur eine Zeile in der Tabelle hat:
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
Die Abfrage gibt eine Zeile zurück. Wenn Sie die Liveabfragestatistik aktivieren, sehen Sie den folgenden Plan:

![Abfrageergebnis eine Zeile](./media/5_AQPStatsOneRow.png)

Im Plan sehen wir das Folgende:
- Bei einer zurückgegebenen Zeile durchlaufen Zeilen jetzt den Clustered Index Seek.
- Da die Buildphase des Hashjoins nicht fortgesetzt wurde, wird der zweite Branch nicht von Zeilen durchlaufen.

### <a name="adaptive-join-benefits"></a>Vorteile adaptiver Joins
Workloads mit häufiger Oszillation zwischen kleinen und großen Joineingabescans profitieren am meisten von dieser Funktion.

### <a name="adaptive-join-overhead"></a>Mehraufwand adaptiver Joins
Adaptive Joins erfordern mehr Speicherplatz als ein äquivalenter Plan eines indizierten Joins geschachtelter Schleifen. Der zusätzliche Speicherplatz wird so angefordert, als wären die geschachtelte Schleifen ein Hashjoin. Auch die Buildphase ist mit Aufwand verbunden: sowohl für einen Stop-and-Go-Vorgang als auch für einen äquivalenten Join eines Streamings geschachtelter Schleifen. Dieser zusätzliche Aufwand geht mit Flexibilität für Szenarios einher, in denen die Zeilenzahl möglicherweise in der Buildeingabe schwankt.

### <a name="adaptive-join-caching-and-re-use"></a>Zwischenspeichern und Wiederverwenden von adaptiven Joins
Adaptive Joins im Batchmodus funktionieren bei der ersten Ausführung einer Anweisung. Nach der ersten Kompilierung bleiben aufeinanderfolgende Ausführungen adaptiv und basieren auf dem Schwellenwert des kompilierten adaptiven Joins und den Laufzeitzeilen, die die Buildphase der äußeren Eingabe durchlaufen.

### <a name="tracking-adaptive-join-activity"></a>Nachverfolgen der Aktivität adaptiver Joins
Der Operator für adaptive Joins verfügt über folgende Planoperatorattribute:

| Planattribut | Description |
|--- |--- |
| AdaptiveThresholdRows | Gibt den beim Wechsel von einem Hashjoin zu einem Nested Loop-Join zu verwendenden Schwellenwert an |
| EstimatedJoinType | Gibt den erwarteten Jointyp an |
| ActualJoinType | Gibt in einem Plan an, welcher Joinalgorithmus basierend auf dem Schwellenwert verwendet wurde. |

Der geschätzte Plan zeigt die Form des adaptiven Joinplans an sowie den definierten Schwellenwert für adaptive Joins und den geschätzten Jointyp.

### <a name="adaptive-join-and-query-store-interoperability"></a>Interoperabilität von adaptiven Joins und dem Abfragespeicher
Der Abfragespeicher erfasst einen adaptiven Joinplan im Batchmodus und kann diesen erzwingen.

### <a name="adaptive-join-eligible-statements"></a>Zulässige Anweisungen für adaptive Joins
Ein logischer Join ist dann für adaptive Joins im Batchmodus zulässig, wenn er folgende Bedingungen erfüllt:
- Der Datenbank-Kompatibilitätsgrad beträgt 140.
- Die Abfrage ist eine SELECT-Anweisung (Anweisungen zur Datenmodifikation sind aktuell noch unzulässig).
- Der Join kann sowohl vom physischen Algorithmus eines indizierten Joins geschachtelter Schleifen als auch eines Hashjoins ausgeführt werden.
- Der Hashjoin verwendet den Batchmodus entweder über einen vorhandenen Columnstore-Index in der Abfrage oder eine mit Columnstore indizierte Tabelle, auf die direkt vom Join verwiesen wird.
- Die generierten alternativen Lösungen des Joins geschachtelter Schleifen und Hashjoins sollten dasselbe erste untergeordnete Element haben (äußerer Verweis).

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>Adaptive Joins und Nested Loop-Effizienz
Wenn ein adaptiver Join zu einem Vorgang geschachtelter Schleifen wechselt, verwendet er die Zeilen, die bereits vom Hashjoinbuild gelesen wurden. Der Operator liest **nicht** erneut die Zeilen des äußeren Verweises.

### <a name="adaptive-threshold-rows"></a>Adaptive Schwellenwertzeilen
Das folgende Diagramm zeigt eine beispielhafte Überschneidung zwischen dem Aufwand eines Hashjoins und dem Aufwand des alternativen Joins geschachtelter Schleifen.  Am Überschneidungspunkt wird der Schwellenwert bestimmt, der wiederum den für den Joinvorgang verwendeten Algorithmus bestimmt.

![Schwellenwert des Joins](./media/6_AQPJoinThreshold.png)

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>Verschachtelte Ausführung mit Tabellenwertfunktionen mit mehreren Anweisungen
Eine verschachtelte Ausführung ändert die unidirektionale Grenze zwischen der Optimierungs- und der Ausführungsphase für eine Ausführung mit einer Abfrage. Zudem können Pläne damit auf Grundlage der überarbeiteten Kardinalitätsschätzungen angepasst werden. Wenn Sie bei der Optimierung auf einen möglichen Kandidaten für eine verschachtelte Ausführung (bei der es sich aktuell um **Funktionen mit mehreren Anweisungen (MSTVFs)** handelt) stoßen, wird die Optimierung unterbrochen, die entsprechende Unterstruktur ausgeführt, die genauen Kardinalitätsschätzungen erfasst, und anschließend wird die Optimierung für Downstreamvorgänge wiederaufgenommen.
Die festgelegte Kardinalitätsschätzung von MSTVFs beträgt in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] „100“ und in früheren Versionen „1“. Die verschachtelte Ausführung löst Probleme bei der Leistung von Workloads, die auf die festgelegten Kardinalitätsschätzungen von MSTVFs zurückzuführen sind.

Die folgende Abbildung zeigt die Ausgabe einer Liveabfragestatistik, eine Teilmenge eines allgemeinen Ausführungsplans, der die Auswirkung festgelegter Kardinalitätsschätzungen von MSTVFs veranschaulicht. Sie sehen den tatsächlichen Zeilenfluss gegenüber dem geschätzten. Es gibt drei erwähnenswerte Bereiche des Plans (von rechts nach links):
1. Der MSTVF-Table Scan hat eine festgelegte Schätzung von 100 Zeilen. In diesem Beispiel gibt es allerdings 527.597 Zeilen, die den MSTVF Table Scan durchlaufen. Dies ist an der Liveabfragestatistik *527597 von 100* der tatsächlichen Elemente von geschätzten Elemente zu erkennen – die festgelegte Schätzung liegt also deutlich zu weit unten.
1. Für den Nested Loop-Vorgang wird davon ausgegangen, dass nur 100 Zeilen von der äußeren Seite des Joins zurückgegebene werden. Aufgrund der hohen Zahl an tatsächlich von MSTVF zurückgegebenen Zeilen sollten Sie sich aber für einen komplett anderen Joinalgorithmus entscheiden.
1. Beachten Sie, dass beim Hash Match-Vorgang ein kleines Warnsymbol angezeigt wird, das in diesem Fall darauf hinweist, dass es einen Überlauf auf den Datenträger hab.

![Zeilenfluss vs. geschätzte Zeilen](./media/7_AQPFlowThreeAreas.png)

Vergleichen Sie den vorherigen Plan mit dem tatsächlich generierten Plan mit aktivierter verschachtelter Ausführung:

![Verschachtelter Plan](./media/8_AQPInterleavedEnabledPlan.png)

1. Beachten Sie, dass der MSTVF-Table Scan jetzt die genaue Kardinalitätsschätzung widerspiegelt. Beachten Sie auch die Neuanordnung des Table Scans und der anderen Vorgänge.
1. Bei Joinalgorithmen haben Sie von einem Nested Loop-Vorgang zu einem Hash Match-Vorgang gewechselt, was für die vorhandene Zahl an Zeilen optimaler ist.
1. Beachten Sie auch, dass es keine Überlaufwarnungen mehr gibt, da mehr Speicherplatz auf Grundlage der tatsächlichen Zeilenzahl, die den MSTVF-Table Scan durchläuft, zugewiesen wird.

### <a name="interleaved-execution-eligible-statements"></a>Zulässige Anweisungen für verschachtelte Ausführungen
Verweisanweisungen von MSTVF in verschachtelten Ausführungen müssen aktuell schreibgeschützt sein und dürfen nicht Teil eines Datenmodifizierungsvorgangs sein. MSTVFs eignen sich nur für die verschachtelte Ausführung, wenn Sie Laufzeitkonstanten verwenden.

### <a name="interleaved-execution-benefits"></a>Vorteile der verschachtelten Ausführung
Allgemein gilt: Je höher der Unterschied zwischen der geschätzten und tatsächlichen Zeilenzahl in Verbindung mit der Zahl von Downstreamplanvorgängen ist, desto mehr wird die Leistung beeinträchtigt.
Allgemein profitieren Abfragen von der verschachtelten Ausführung, die:
1. eine große Diskrepanz zwischen der geschätzten und tatsächlichen Zeilenzahl für das temporäre Resultset aufweisen (in diesem Fall MSTVF);
1. und in denen die Abfrage empfindlich ist, was Änderungen der Größe des temporären Ergebnisses angeht. Dies geschieht typischerweise, wenn es eine komplexe Struktur über der Unterstruktur im Abfrageplan gibt.
Ein einfaches „SELECT *“ einer MSTVF profitiert nicht von einer verschachtelten Ausführung.

### <a name="interleaved-execution-overhead"></a>Aufwand der verschachtelten Ausführung
Der Aufwand sollte sehr gering oder nicht vorhanden sein. MSTVFs wurden bereits vor der Einführung der verschachtelten Ausführung materialisiert. Der Unterschied besteht jedoch darin, dass jetzt eine verzögerte Optimierung möglich ist sowie die anschließende Nutzung der Kardinalitätsschätzung des materialisierten Rowsets.
Genauso wie mit allen Änderungen, die sich auf Pläne auswirken, können sich einige Pläne so ändern, dass Sie einen schlechteren Plan für die Abfrage erhalten, auch wenn Sie eine bessere Kardinalität der Unterstruktur haben. Dies können Sie z.B. verhindern, indem Sie den Kompatibilitätsgrad wiederherstellen oder den Abfragespeicher verwenden, um das Verwenden der nicht rückläufigen Version des Plans zu erzwingen.

### <a name="interleaved-execution-and-consecutive-executions"></a>Verschachtelte Ausführung und nachfolgende Ausführungen
Sobald ein verschachtelter Ausführungsplan zwischengespeichert wurde, wird der Plan mit den überarbeiteten Schätzungen der ersten Ausführung für nachfolgende Ausführungen verwendet, ohne dass die verschachtelte Ausführung neu instantiiert werden muss.

### <a name="tracking-interleaved-execution-activity"></a>Nachverfolgen der Aktivität von verschachtelten Ausführungen
Sie können sich Verwendungsattribute im Ausführungsplan der Abfrage anschauen:

| Ausführungsplanattribut | Description |
| --- | --- |
| ContainsInterleavedExecutionCandidates | Gilt für den Knoten *QueryPlan*. Wenn dieser *true* lautet, gibt dieser an, dass der Plan mögliche Kandidaten für die überlappende Ausführung enthält. |
| IsInterleavedExecuted | Das Attribut des Elements *RuntimeInformation* befindet sich für den Knoten „TVF“ unter „RelOp“. Wenn es *true* entspricht, wurde der Vorgang im Zuge einer überlappenden Ausführung materialisiert. |

Sie können überlappende Ausführungen auch mit den folgenden XEvents nachverfolgen:

| XEvent | Description |
| ---- | --- |
| interleaved_exec_status | Dieses Ereignis wird ausgelöst, wenn eine verschachtelte Ausführung durchgeführt wird. |
| interleaved_exec_stats_update | Dieses Ereignis beschreibt die von der verschachtelten Ausführung aktualisierten Kardinalitätsschätzungen. |
| Interleaved_exec_disabled_reason | Dieses Ereignis wird ausgelöst, wenn eine Abfrage mit einem möglichen Kandidaten für eine verschachtelte Ausführung nicht verschachtelt ausgeführt wird. |

Eine Abfrage muss ausgeführt werden, damit die verschachtelte Ausführung die Kardinalitätsschätzungen für MSTVF überarbeiten kann. Allerdings zeigt der geschätzte Ausführungsplan immer noch an, wenn es Kandidaten für eine überlappende Ausführung gibt. Dies macht er mithilfe des showplan-Attributs `ContainsInterleavedExecutionCandidates`.    

### <a name="interleaved-execution-caching"></a>Zwischenspeichern der verschachtelte Ausführung
Wenn ein Plan aus dem Cache gelöscht oder entfernt wird, kommt es bei der Abfrageausführung zu einer neuen Kompilierung mit der verschachtelten Ausführung.
Eine Anweisung mit `OPTION (RECOMPILE)` erstellt einen neuen Plan mit der überlappenden Ausführung und speichert diesen nicht zwischen.     

### <a name="interleaved-execution-and-query-store-interoperability"></a>Geschachtelte Ausführung und Interoperabilität des Abfragespeichers
Pläne mit der verschachtelten Ausführung können erzwungen werden. Der Plan ist die Version mit angepassten Kardinalitätsschätzungen auf Grundlage der ersten Ausführung.    

## <a name="see-also"></a>Weitere Informationen finden Sie unter
[Leistungscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Leitfaden zur Architektur der Abfrageverarbeitung](../../relational-databases/query-processing-architecture-guide.md)    
[Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Joins](../../relational-databases/performance/joins.md)    
[Veranschaulichung der adaptiven Abfrageverarbeitung](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)          

