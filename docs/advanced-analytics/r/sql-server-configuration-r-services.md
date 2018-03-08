---
title: SQL Server-Konfiguration (R Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5716fced7dd2be49c580222b9ae155451cf8f426
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="sql-server-configuration-for-use-with-r"></a>SQL Server-Konfiguration für die Verwendung mit R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist die zweite aus einer Reihe, die zur leistungsoptimierung für R-Dienste basierend auf zwei Fallstudien beschreibt.  Dieser Artikel enthält Hinweise zur Hardware und Netzwerk des Computers, der zum Ausführen von SQL Server R Services verwendet wird. Es enthält auch Informationen zu Methoden zum Konfigurieren der SQL Server-Instanz, Datenbank oder in einer Lösung verwendeten Tabellen. Da die Verwendung von NUMA in SQL Server die Linie zwischen Hardware und Datenbank-Optimierungen verwischt, wird ein dritter Abschnitt CPU Affinitization und Ressource Governance ausführlich erläutert.

> [!TIP]
> Wenn Sie SQL Server vertraut sind, sollten auch die Optimierung Leistungsleitfaden zu SQL Server zu lesen: [überwachen und optimieren für Leistung](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Hardware-Optimierung

Optimierung des Servercomputers ist wichtig, um sicherzustellen, dass ausreichend Ressourcen zum Ausführen externer Skripts stehen. Wenn die Ressourcen beschränkt sind, können Sie wie diese Symptome auf:

- Auftragsausführung ist verzögert oder anderen Datenbankvorgängen Priorisierung abgebrochen
- Fehler "Kontingent wurde überschritten" führte dazu, dass R-Skript ohne Abschluss beendet werden soll.
- Laden von Daten in den R-Arbeitsspeicher abgeschnitten, wird für unvollständige Ergebnisse

### <a name="memory"></a>Speicher

Der auf einem Computer verfügbare Arbeitsspeicher kann sich stark auf die Leistung komplexerer analytischer Algorithmen auswirken. Nicht genügend Arbeitsspeicher beeinträchtigt den Grad der Parallelität, bei Verwendung der SQL-computekontext. Ebenso kann dadurch die verarbeitbare Segmentgröße (Zeilen pro Lesevorgang) beeinträchtigt werden sowie die Anzahl gleichzeitiger Sitzungen, die unterstützt werden kann.

Mindestens 32 GB wird dringend empfohlen. Wenn Sie mehr als 32 GB zur Verfügung haben, können Sie die SQL-Datenquelle, um weitere Zeilen in jedem Lesevorgang verwenden, um die Leistung zu verbessern konfigurieren.

Sie können auch von der Instanz belegte verwalten. Standardmäßig wird SQL Server über externe Skriptprozesse priorisiert, wenn Speicher belegt wurde. In einer Standardinstallation von R Services ist nur 20 % des verfügbaren Speichers zu r zugeordnet.

Dies ist normalerweise nicht hoch genug für Data Science-Aufgaben, aber weder SQLServer-Instanz Arbeitsspeicher .NET-Threadpool blockiert werden sollen. Sie sollten experimentieren und Optimieren der speicherbelegung zwischen dem Datenbankmodul, verwandte Dienste und externer Skripts, mit der Vereinbarung, die die optimale Konfiguration von Fall zu Fall unterschiedlich.

Für das Modell fortsetzen übereinstimmende externes Skript Verwendung starker wurde und keine andere Datenbank Datenbankmoduldienste ausgeführt wurden; aus diesem Grund wurden externer Skripts, die zugeordneten Ressourcen auf 70 % erhöht die beste Konfiguration bereit skriptleistung war.

### <a name="power-options"></a>Energieoptionen

Auf dem Windows-Betriebssystem die **hohe Leistung** Energieoption sollte verwendet werden. Mit einer anderen Einstellung führt eine verringerte oder inkonsistente Leistung bei Verwendung von SQL Server.

### <a name="disk-io"></a>Eingabe bzw. Ausgabe von Laufwerken

Trainings- und Vorhersageinstanz für Aufträge mithilfe von R Services grundsätzlich e/a sind gebunden, und richten sich nach der Geschwindigkeit des der Datenträger, denen auf die Datenbank gespeichert ist. Schnellere Laufwerken, z. B. Solid State Drives (SSD) können nützlich sein.

Die Laufwerk-E/A hängt auch von anderen Anwendungen ab, die auf das Laufwerk zugreifen: z.B. von Lesevorgängen in einer Datenbank anderer Clients. Die E/A-Leistung des Laufwerks kann auch von den Einstellungen für das verwendete Dateisystem beeinträchtigt werden, wie z.B. von der vom Dateisystem verwendeten Blockgröße.

Wenn mehrere Laufwerke verfügbar sind, fordert die Datenbanken auf einem anderen Laufwerk als SQLServer damit angefordert wird, die für das Datenbankmodul nicht einen anderen Datenträger als festgelegten Speicher für Daten, die in der Datenbank gespeichert.

Die Laufwerk-E/A kann die Leistung deutlich beeinträchtigen, wenn analytische RevoScaleR-Funktionen ausgeführt werden, die während des Trainings mehrere Iterationen verwenden. Beispielsweise `rxLogit`, `rxDTree`, `rxDForest`, und `rxBTrees` alle mehrere Durchgänge verwenden. Wenn die Datenquelle SQL Server ist, verwenden diese Algorithmen temporäre Dateien, die optimiert werden, um die Daten zu erfassen. Diese Dateien werden nach dem Abschluss der Sitzung automatisch bereinigt. Mit einem Hochleistungs-Datenträger für Lese-/Schreibvorgänge kann die insgesamt verstrichene Zeit für diese Algorithmen erheblich verbessern.

> [!NOTE]
> Frühere Versionen von R Services erforderlich 8.3-Dateiname-Unterstützung auf Windows-Betriebssystemen. Diese Beschränkung wurde nach dem Service Pack 1 aufgehoben. Allerdings können Sie fsutil.exe verwenden, um zu bestimmen, ob ein Laufwerk 8.3-Dateinamen unterstützt, oder um Unterstützung zu aktivieren, wenn dies nicht der Fall.

### <a name="paging-file"></a>Auslagerungsdatei

Das Windows-Betriebssystem verwendet eine Auslagerungsdatei, um Abstürze zu verwalten und virtuelle Arbeitsspeicherseiten zu speichern. Wenn Sie eine exzessive Auslagerung bemerken, ziehen Sie in Betracht, den physischen Arbeitsspeicher des Computers zu erweitern. Auch wenn mehr physischer Arbeitsspeicher die Auslagerung nicht vollständig eliminiert, wird der Auslagerungsbedarf doch gesenkt.

Auch die Geschwindigkeit des Laufwerks, auf dem die Auslagerungsdatei gespeichert ist, kann die Leistung beeinträchtigen. Wenn Sie die Auslagerungsdatei auf einem SSD speichern oder mehrere Auslagerungsdateien SSD-übergreifend verwenden, kann dies die Leistung verbessern.

Informationen zum Ändern der Größe der Auslagerungsdatei, finden Sie unter [Gewusst wie: Bestimmen der geeigneten Auslagerungsdateigröße für 64-Bit-Versionen von Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Optimierungen auf Instanz- oder Datenbankebene

Optimierung der SQL Server-Instanz ist der Schlüssel für die effiziente Ausführung externer Skripts.

> [!NOTE]
> Die optimalen Einstellungen unterscheiden sich je nach Größe und Typ der Daten, die Anzahl der Spalten, die Sie für die Bewertung oder Trainieren eines Modells verwenden.
> 
> Sie können überprüfen, dass die Ergebnisse der bestimmte Optimierungen im endgültigen Artikel: [Leistungsoptimierung - Fallstudien](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Beispielskripts, finden Sie in der separaten [GitHub-Repository](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Tabellenkomprimierung

E/a-Leistung kann häufig verbessert werden, mithilfe von Komprimierung oder einer einspaltigen Datenspeicher. Im Allgemeinen ist Daten häufig wiederholt in verschiedenen Spalten in einer Tabelle mit Columnstore diese Wiederholungen nutzt beim Komprimieren der Daten.

Ein Columnstore möglicherweise nicht so effizient, wenn zahlreiche einfügungen in die Tabelle vorhanden sind, aber es ist eine gute Wahl, wenn die Daten statisch sind oder nur selten geändert werden. Wenn sich ein spaltenbasierter Speicher nicht eignet, können Sie die E/A verbessern, indem Sie die Komprimierung in einer überwiegend zeilenorientierten Tabelle aktivieren.

Weitere Informationen finden Sie in folgenden Dokumenten:

+ [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)

+ [Aktivieren der Komprimierung für eine Tabelle oder einen index](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Speicheroptimierte Tabellen

Speicher ist heute nicht mehr für moderne Computer ein Problem. Wie Hardwarespezifikationen zu verbessern weiter, ist es relativ einfach, RAM an gute Werte abzurufen. Allerdings zur gleichen Zeit Daten ist schneller als jemals zuvor erzeugt wird, und die Daten mit geringer Latenz verarbeitet werden müssen.

Speicheroptimierte Tabellen stellen eine Lösung, sie die sehr viel Arbeitsspeicher in erweiterten Computer zur Lösung des Problems von big Data verfügbar nutzen dar. Speicheroptimierte Tabellen befinden sich hauptsächlich im Arbeitsspeicher, sodass Daten auslesen und in den Speicher geschrieben. Um Dauerhaftigkeit zu gewährleisten wird eine zweite Kopie der Tabelle auf dem Datenträger beibehalten, und Daten werden nur während der datenbankwiederherstellung vom Datenträger gelesen.

Wenn Sie zum Lesen aus und häufig in Tabellen geschrieben werden müssen, können durch Speicheroptimierte Tabellen mit hoher Skalierbarkeit und geringe Latenz.  Im Szenario Resume-Abgleich mit der von speicheroptimierten Tabellen konnten wir alle Resume-Funktionen aus der Datenbank gelesen und in den Hauptspeicher zum Abgleich mit dem neuen Auftrag Fehlernachrichten zu speichern. Dies verringert erheblich die Datenträger-e/a.

Zusätzliche Leistungssteigerungen wurden erreicht, indem Sie eine Speicheroptimierte Tabelle während der Verfassung Vorhersagen zurück an die Datenbank aus mehreren gleichzeitigen Batches. Die Verwendung von speicheroptimierten Tabellen auf SQL Server werden mit geringer Latenz für Tabelle Lese- und Schreibvorgänge aktiviert.

Die Benutzeroberfläche wurde auch während der Entwicklung eine nahtlose. Dauerhafte Speicheroptimierte Tabellen wurden zur gleichen Zeit erstellt, die die Datenbank erstellt wurde. Deshalb verwendet die Entwicklung den gleichen Workflow unabhängig davon, wo die Daten gespeichert wurde.

### <a name="processor"></a>Prozessor

SQL Server können parallele Aufgaben mithilfe der verfügbaren Kerne auf dem Computer; die mehrere Kerne, die verfügbar sind, desto besser die Leistung. Erhöhen der Anzahl von Kernen für e/a-gebundene Vorgänge nicht helfen kann, gebundenen CPU Algorithmen Vorteil aus schnellerer CPUs mit vielen Kernen.

Da der Server normalerweise gleichzeitig von mehreren Benutzern verwendet wird, muss der Datenbankadministrator die ideale Anzahl von Kernen bestimmen, die zur Unterstützung von Peak Arbeitslast Berechnungen erforderlich sind.

### <a name="resource-governance"></a>Die Ressourcenkontrolle

In den Editionen, die Ressourcenkontrolle unterstützen, können Sie Ressourcenpools verwenden, um anzugeben, dass bestimmte arbeitsauslastungen eine Anzahl von CPUs zugeordnet werden. Sie können auch die Menge des Arbeitsspeichers für bestimmte arbeitsauslastungen verwalten.

Die Ressourcenkontrolle in SQL Server können Sie die Überwachung und Kontrolle über die verschiedenen Ressourcen, die von SQL Server verwendet und von r zu zentralisieren. Beispielsweise können Sie die Hälfte den verfügbaren Arbeitsspeicher für das Datenbankmodul, um sicherzustellen, dass diesem Kern Dienste immer trotz vorübergehenden größere arbeitsauslastungen ausführen können zuweisen.

Der Standardwert für den Arbeitsspeicherverbrauch durch externe Skripts ist auf 20 % des insgesamt für SQL Server selbst verfügbaren Arbeitsspeichers beschränkt. Dieser Grenzwert gilt standardmäßig um sicherzustellen, dass alle Aufgaben, die auf dem Datenbankserver beruhen durch R-Aufträgen mit langer nicht schwerwiegend beeinträchtigt werden. Diese Einschränkungen können vom Datenbankadministrator angepasst werden. In vielen Fällen ist der Grenzwert von 20 % nicht ausreichend, um schwerwiegende Machine learning-arbeitsauslastungen zu unterstützen.

Sind die Konfigurationsoptionen unterstützt **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, und **MAX_PROCESSES**. Um die aktuellen Einstellungen anzuzeigen, verwenden Sie diese Anweisung aus:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Wenn der Server für R Services in erster Linie verwendet wird, kann es MAX_CPU_PERCENT auf 40 % oder 60 % erhöhen hilfreich sein.

-  Wenn viele R-Sitzungen auf den gleichen Server gleichzeitig verwenden müssen, sollten alle drei Einstellungen erhöht werden.

Um die zugeordnete Ressourcenwerte zu ändern, verwenden Sie T-SQL-Anweisungen.

+ Diese Anweisung wird die Auslastung des Speichers auf 40 % festgelegt:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Diese Anweisung legt alle drei konfigurierbaren Werte fest:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Wenn Sie ein Arbeitsspeicher, CPU oder max prozesseinstellung ändern, und klicken Sie dann auf die Einstellungen sofort angewendet werden soll, führen Sie diese Anweisung:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA-Hardware-NUMA und CPU-Affinität

Wenn Sie SQL Server als computekontext verwenden möchten, können Sie manchmal eine bessere Leistung erzielen, durch das Optimieren der Einstellungen im Zusammenhang mit NUMA und der Prozessor-Affinität. 

Systeme mit _NUMA-Hardware_ haben mehrere Systembusse, von denen jeder eine kleine Gruppe von Prozessoren bedient. Jede CPU kann Arbeitsspeicher von anderen Gruppen auf kohärente Weise zugreifen. Jede dieser Gruppen stellt einen NUMA-Knoten dar. Wenn Sie über NUMA-Hardware verfügen, können Sie sie ggf. so konfigurieren, dass anstelle von NUMA Interleave-Speicher verwendet wird. In diesem Fall wird Windows und daher von SQL Server nicht als NUMA erkannt. 

Führen Sie die folgende Abfrage aus, um die Anzahl der für SQL Server verfügbaren Speicherknoten zu suchen:

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Wenn die Abfrage einen einzigen Speicherknoten (Knoten 0) zurückgibt, Sie verfügen nicht über die NUMA-Hardware oder die Hardware ist als interleaved (nicht-NUMA) konfiguriert. SQL Server ignoriert auch Hardware-NUMA bei der es maximal vier CPUs oder mindestens einen Knoten nur eine CPU aufweist.

Wenn Ihr Computer verfügt über mehrere Prozessoren, aber keinen Hardware-NUMA, können Sie auch [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) auf CPUs in kleinere Gruppen unterteilen.  Die Soft-NUMA-Funktion ist in SQL Server 2016 und SQL Server-2017 automatisch aktiviert, beim Starten des SQL Server-Diensts.

Wenn Soft-NUMA aktiviert ist, werden die Knoten für Sie automatisch von SQL Server verwaltet; um bestimmte arbeitsauslastungen zu optimieren, Sie können jedoch deaktivieren _weicher Affinität_ und CPU-Affinität für die soft-NUMA-Knoten manuell konfigurieren. Dies können Sie bieten mehr Kontrolle über die arbeitsauslastungen zugewiesen sind, auf die Knoten beschränkt, insbesondere, wenn Sie eine Edition von SQL Server verwenden, die Unterstützung der Ressourcenkontrolle. Durch Angabe der CPU-Affinität und zum Ausrichten von Ressourcenpools für Gruppen von CPUs, können Sie die Wartezeit reduzieren und stellen Sie sicher, dass verwandte Prozesse im selben NUMA-Knoten ausgeführt werden.

Das generelle Verfahren zum Konfigurieren von Soft-NUMA und CPU-Affinität für die Unterstützung von R-Arbeitslasten ist wie folgt aus:

1. Aktivieren von Soft-NUMA, falls verfügbar
2. Prozessor-Affinität definieren
3. Erstellen von Ressourcenpools für externe Prozesse mit [der Ressourcenkontrolle](../r/resource-governance-for-r-services.md)
4. Weisen Sie die [Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/resource-governor-workload-group.md) an bestimmten affinitätsgruppen

Details, einschließlich Beispielcode finden Sie in diesem Lernprogramm: [SQL Optimierung Tipps und Tricks (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Weitere Ressourcen:**

+ [Soft-NUMA in SQLServer](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Zuordnen von Soft-NUMA-Knoten zu CPUs

+ [Automatischer Soft-NUMA: gerade ausgeführt wird, schneller (Bob Ward)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   Beschreibt Verlauf sowie Details zur Implementierung mit der Leistung auf neueren Multikern-Servern.

## <a name="task-specific-optimizations"></a>Aufgabenspezifische Optimierungen

In diesem Abschnitt werden die Methoden, die in diese Fallstudien und in anderen Tests, für bestimmte Machine learning-arbeitsauslastungen optimieren übernommen zusammengefasst. Übliche arbeitsauslastungen enthalten, das Modelltraining, merkmalsextraktion und namens Feature Engineering und verschiedene Szenarien für die Bewertung: einzeiliges, kleine Batch und großen Batches.

### <a name="feature-engineering"></a>Featureentwicklung

Eine Schwachstelle mit R ist, dass es in der Regel auf einer einzigen CPU verarbeitet wird. Dies ist die wichtigsten Leistungsengpässe für zahlreiche Tasks besonders feature Engineering-Team. In der Projektmappe fortsetzen übereinstimmende erstellt das Feature engineering Task allein 2.500 Kreuzprodukt-Funktionen, die mit den ursprünglichen 100 Funktionen kombiniert werden musste. Dieser Task würde sehr viel Zeit in Anspruch nehmen, wenn alles auf einer einzigen CPU erfolgt wäre.

Es gibt mehrere Möglichkeiten zum Verbessern der Leistung namens Feature Engineering. Sie können entweder den R-Code zu optimieren und merkmalsextraktion im Modellierungsprozess beibehalten oder verschieben das Feature engineering-Vorgangs in SQL.

- Mithilfe von r Sie definieren eine Funktion, und übergeben Sie ihn dann als Argument für [RxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) während des Trainings. Wenn das Modell die parallelen Verarbeitung unterstützt, kann der Feature-engineering-Vorgang mit mehreren CPUs verarbeitet werden. Bei diesem Ansatz beachtet die Data Science-Team verbessert die Leistung von 16 % im Hinblick auf die Bewertung der Zeit. Dieser Ansatz erfordert jedoch ein Modell, das unterstützt Parallelisierung und eine Abfrage, die mit einem parallelen Plan ausgeführt werden kann.

- Verwenden von R mit einer SQL-computekontext. In einer Umgebung mit mehreren Prozessoren mit isolierten Ressourcen verfügbar sind, für die Ausführung von separaten Batches erreichen Sie größere Effizienz durch Isolierung der SQL-Abfragen, die für jeden Batch verwendet wird, um Daten aus Tabellen extrahieren und Einschränken der Daten auf der gleichen Arbeitsauslastungsgruppe. Methoden verwendet, um die Batches zu isolieren einschließen, Partitionierung und Verwendung von PowerShell, um eine eigene Abfrage parallel ausgeführt werden.

- Ad-hoc-parallele Ausführung: In einer SQL Server-computekontext, können Sie auf dem SQL-Datenbankmodul zu erzwingen, wenn möglich die parallele Ausführung und wenn diese Option gefunden wird, effizienter verlassen.

- Verwenden Sie T-SQL in einem separaten merkmalbereitstellung-Prozess. Die Funktionsdaten mit SQL precomputing in der Regel schneller ausgeführt wird.

### <a name="prediction-scoring-in-parallel"></a>Vorhersage (Bewertung), parallel

Einer der Vorteile von SQL Server ist die Fähigkeit, eine große Anzahl Zeilen gleichzeitig zu verarbeiten. Dieser Vorteil wird nie daher wie bei der Bewertung markiert. Im Allgemeinen ist das Modell nicht benötigt Zugriff auf alle Daten für die Bewertung, damit die Eingabedaten mit jede Arbeitsauslastungsgruppe eine Verarbeitungstasks partitioniert werden können.

Sie können auch die Eingabedaten als eine einzelne Abfrage senden, und SQL Server analysiert die Abfrage. Wenn es sich bei ein parallelen Abfrageplan für die Eingabedaten erstellt werden kann, werden automatisch Partitionen von Daten, die dem Knoten zugewiesen und führt die erforderlichen Joins und Aggregationen sowie Parallel.

Wenn Sie die Details zum Definieren einer gespeicherten Prozedur für die Verwendung in Bewertung interessiert sind, finden Sie das Beispielprojekt [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) und suchen Sie nach der Datei "step5_score_for_matching.sql". Das Beispiel Skript auch abfragestart verfolgt und Endzeiten und schreibt die Zeit für die SQL-Konsole, damit Sie die Leistung bewerten können.

### <a name="concurrent-scoring-using-resource-groups"></a>Gleichzeitige Bewertung von Ressourcengruppen

Um das Problem bewerteten skaliert werden sollen, empfiehlt sich, die map-reduce-Ansatz zu verwenden, in dem Millionen von Elementen in mehrere Batches aufgeteilt werden. Anschließend werden mehrere Bewertungsprofile Aufträge gleichzeitig ausgeführt werden. In diesem Framework Batches sind auf unterschiedlichen CPU-Gruppen verarbeitet, und die Ergebnisse werden gesammelt und zurück in die Datenbank geschrieben.

Dies ist der Ansatz wird in das Szenario fortsetzen übereinstimmende; die Ressourcenkontrolle in SQL Server ist jedoch wichtig für diesen Ansatz zu implementieren. Einrichten von Arbeitsauslastungsgruppen für externe Skripts für Aufträge, erkennen Sie R-Aufträge auf unterschiedlichen Prozessorgruppen Bewertung weiterleiten und zu schnellerem Durchsatz erzielen.

Die Ressourcenkontrolle ist auch hilfreich, belegen die verfügbaren Serverressourcen auf dem Server (CPU und Speicher), um Wettbewerb arbeitsauslastung zu minimieren. Sie können Klassifizierungsfunktionen einrichten, um zwischen verschiedenen Typen von R-Aufträge zu unterscheiden: Beispielsweise können Sie festlegen, dass Bewertung von einer Anwendung immer aufgerufen Priorität, akzeptiert werden, während Umschulung Aufträge mit niedriger Priorität haben. Diese Isolierung Ressource kann potenziell Ausführungszeit verbessern und besser vorhersagbaren Leistung bieten.

### <a name="concurrent-scoring-using-powershell"></a>Gleichzeitige Bewertung mithilfe von PowerShell

Wenn Sie die Daten zu partitionieren möchten, können Sie PowerShell-Skripts, um mehrere gleichzeitige Bewertungsaufgaben auszuführen. Zu diesem Zweck verwenden Sie das Invoke-SqlCmd-Cmdlet und initiieren Sie die Bewertungsaufgaben parallel zu.

In diesem Szenario fortsetzen übereinstimmende ausgelegt Parallelität wie folgt:

- 20 Prozessoren, die in vier Gruppen von jeweils fünf CPUs unterteilt sind. Jede Gruppe von CPUs befindet sich auf dem gleichen NUMA-Knoten.

- Maximale Anzahl von gleichzeitigen Batches, die auf acht festgelegt wurde.

- Jede Arbeitsauslastungsgruppe muss zwei Bewertungsaufgaben behandeln. Als eine Aufgabe wird abgeschlossen, Lesen von Daten und Bewertung beginnt, kann die andere Aufgabe starten, Lesen von Daten aus der Datenbank.

Um die PowerShell-Skripts für dieses Szenario zu anzuzeigen, öffnen Sie die Datei experiment.ps1 in die [Github Projekt](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Das Speichern von Modellen für Vorhersagen

Beim Training und Auswertung abgeschlossen ist und Sie einem bewährten Modell ausgewählt haben, wird empfohlen, das Modell in der Datenbank gespeichert, sodass sie für Vorhersagen verfügbar ist. Laden das vorberechnete Modell aus der Datenbank für die Vorhersage ist effizienter, da SQL Server-Machine Learning verwendet spezielle Serialisierung Algorithmen zum Speichern und Laden Modelle, beim Wechseln zwischen R und die Datenbank.

> [!TIP]
> Die PREDICT-Funktion können Sie in SQL Server 2017 bewerten, selbst wenn R nicht auf dem Server installiert ist. Begrenzte Modelltypen werden unterstützt, aus dem "revoscaler"-Paket.

Je nach Algorithmus, die Sie verwenden, kann einige Modelle sehr groß ist, jedoch vor allem, wenn ein großes DataSet trainiert. Beispielsweise Algorithmen wie **lm** oder **"glm"** generiert viele Zusammenfassungsdaten zusammen mit Regeln. Kommen Grenzwerte für die Größe eines Modells, die in einer Varbinary-Spalte gespeichert werden können, wird empfohlen, dass Sie unnötige Artefakte aus dem Modell auszuschließen, vor dem Speichern des Modells in der Datenbank für die Produktion.

## <a name="articles-in-this-series"></a>Artikel in dieser Serie

[Leistung optimieren für R – Einführung](../r/sql-server-r-services-performance-tuning.md)

[Optimieren der Leistung für R - SQL Server-Konfiguration](../r/sql-server-configuration-r-services.md)

[Optimieren der Leistung für R - R Optimierung von Code und Daten](../r/r-and-data-optimization-r-services.md)

[Performance Tuning - Fallstudien](../r/performance-case-study-r-services.md)
