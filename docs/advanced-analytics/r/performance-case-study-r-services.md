---
title: "Leistung für R Services - Ergebnisse und Ressourcen | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65e3ca0b62da2a8412b92485316074a5f52fa080
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="performance-for-r-services-results-and-resources"></a>Leistung für R Services: Ergebnisse und Ressourcen

In diesem Artikel ist die vierte und letzte in einer Reihe, die zur leistungsoptimierung für R Services beschreibt. Dieser Artikel beschreibt die Methoden, die Ergebnisse und die Schlussfolgerungen zwei Fallstudien, die verschiedene Methoden zur Optimierung getestet.

Die zwei Fallstudien mussten unterschiedliche Ziele:

+ Die erste Fallstudie vom Entwicklungsteam R Services gesucht, um die Auswirkungen auf bestimmte Optimierungstechniken messen
+ Die zweite Fallstudie erprobt von einem Data scientists Team mehrere Methoden, um die bestmögliche Optimierung für ein bestimmtes bewerteten hohem Volumen-Szenario zu bestimmen.

In diesem Thema werden die detaillierten Ergebnisse der ersten Fallstudie aufgelistet. Für die zweite Fallstudie beschreibt eine Übersicht über die allgemeine Ergebnisse. Sind Sie am Ende dieses Themas Links für alle Skripts und Beispieldaten und Ressourcen, die von den ursprünglichen Autoren verwendet.

## <a name="performance-case-study-airline-dataset"></a>Leistung-Fallstudie: Airline-Dataset

Vom Entwicklungsteam von SQL Server R Services bietet diese Fallstudie getestet, die Auswirkungen der verschiedenen Optimierungen. Eine einzelne RxLogit-Modell erstellt wurde und Bewertung der nachzufolgen DataSet Airline-Aktivität. Optimierungen, die während des Trainings und Prozesse für die Bewertung der Auswirkungen der einzelnen Bewertung angewendet wurden.

- Github: [-Beispieldaten und -Skripts](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) für SQL Server-Optimierungen Überprüfung kennzeichnen

### <a name="test-methods"></a>Testmethoden

1. Das Dataset Airline-Aktivität besteht aus einer einzelnen Tabelle mit 10M Zeilen. Es wurde heruntergeladen und Bulk in SQL Server geladen.
2. Sechs Kopien der Tabelle vorgenommen wurden.
3. Verschiedene Änderungen angewendet wurden, die Kopien der Tabelle, um SQL Server-Funktionen, z. B. Page-Komprimierung, Row-Komprimierung, Indizierung, spaltenweise Datenspeicher usw. zu testen.
4. Vor und nach jeder Optimierung angewendet wurde, wurde Leistung gemessen.

| Tabellenname| Description|
|------|------|
| *airline* | Aus der ursprünglichen XDF-Datei mithilfe von `rxDataStep` konvertierte Daten.|                          |
| *airlineWithIntCol*   | *DayOfWeek* konvertiert in eine Ganzzahl anstatt in eine Zeichenfolge. Fügt auch eine *rowNum*-Spalte hinzu.|
| *airlineWithIndex*    | Die gleichen Daten wie in der *airlineWithIntCol*-Tabelle, jedoch mit einem einzigen gruppierten Index mit *rowNum*-Spalte.|
| *airlineWithPageComp* | Die gleichen Daten wie in der *airlineWithIndex*-Tabelle, jedoch mit aktivierter Seitenkomprimierung. Fügt auch die beiden Spalten *CRSDepHour* und *Late* hinzu, die aus *CRSDepTime* und *ArrDelay* berechnet werden. |
| *airlineWithRowComp*  | Die gleichen Daten wie in der *airlineWithIndex*-Tabelle, jedoch mit aktivierter Zeilenkomprimierung. Fügt auch die beiden Spalten *CRSDepHour* und *Late* hinzu, die aus *CRSDepTime* und *ArrDelay* berechnet werden. |
| *airlineColumnar*     | Ein spaltenbasierter Speicher mit einem einzigen gruppierten Index. Diese Tabelle wird mit Daten aus einer bereinigten CSV-Datei aufgefüllt.|

Jeder Test umfasste die folgenden Schritte aus:

1. Die automatische Speicherbereinigung für R wurde vor jedem Test eingeleitet.
2. Ein Logistisches Regressionsmodell wurde auf Basis der Tabellendaten erstellt. Der Wert von *rowsPerRead* wurde für jeden Test auf 500000 festgelegt.
3. Bewertungen wurden mithilfe des trainierten Modells generiert
4. Jeder Test, die bis zu sechs Mal ausgeführt wurde. Die Uhrzeit der ersten Ausführen ("kalte") wurde gelöscht. Um den gelegentliche Ausreißer zu ermöglichen die **maximale** Zeit zwischen der weiteren fünf ausgeführt wird, wurde ebenfalls gelöscht. Der Durchschnitt der vier verbleibenden Ausführungen wurde verwendet, um die durchschnittliche verstrichene Laufzeit jedes Tests zu berechnen.
5. Die Tests ausgeführt wurden, mithilfe der *ReportProgress* Parameter mit dem Wert 3 (= Berichts Zeitangaben und Status). Jede Ausgabedatei enthält Informationen über die Zeit im e/a-Zeit bis Übergang und Rechenzeit. Diese Zeiten sind nützlich für die Problembehandlung und Diagnose.
6. Die Konsolenausgabe wurde auch in eine Datei in das Ausgabeverzeichnis weitergeleitet.
7. Die Testskripts verarbeitet die Zeiten in diesen Dateien, um die durchschnittliche Zeit Läufen zu berechnen.

Die folgenden Ergebnisse sind beispielsweise die Zeiten aus einem einzelnen Test. Die wichtigsten Zeiten sind **Gesamte Lesezeit** (E/A-Zeit) und **Übergangszeit** (Aufwand für das Einrichten von Prozessen für die Berechnung).

**Beispiel-Zeitangaben**

```
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

Es wird empfohlen, dass Sie herunterladen, und ändern Sie die Testskripts, die Sie behandeln von Problemen mit R-Services oder RevoScaleR-Funktionen unterstützen.

### <a name="test-results-all"></a>Testergebnisse (alle)

In diesem Abschnitt werden vor und nach der Ergebnisse aller Tests vergleicht.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Größe der Daten mit Komprimierung und eine einspaltige Tabelle speichern

Der erste Test verglichen, die Verwendung von Komprimierung und eine einspaltige Tabelle zum Verringern der Größe der Daten.

| Tabellenname            | Zeilen     | Reserviert.   | data       | index_size | Nicht verwendet  | % Gespeichert (reserviert) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2.978.816 KB | 2.972.160 KB | 6.128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625.784 KB  | 623.744 KB  | 1.352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1.262.520 KB | 1.258.880 KB | 2.552 KB    | 1.088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201.992 KB  | 201.624 KB  | –        | 368 KB  | 93%                 |

**Schlussfolgerungen**

Die größte Reduzierung der Größe der Daten wurde erreicht, indem ein columnstore-Index, gefolgt von Page-Komprimierung anwenden.

#### <a name="effects-of-compression"></a>Auswirkungen der Komprimierung

Dieser Test verglichen, die Vorteile der zeilenkomprimierung, seitenkomprimierung und keine Komprimierung. Ein Modell trainiert wurde, mithilfe von `rxLinMod` auf Daten aus drei verschiedenen Datentabellen. Für alle Tabellen wurde dieselbe Formel und Abfrage verwendet.

| Tabellenname            | Testname       | numTasks | Durchschnittliche Zeit |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | "Nocompression" - parallel| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - parallel  | 4        | 5.2375       |

**Schlussfolgerungen**

Komprimierung allein scheint nicht zu helfen. In diesem Beispiel wird kompensiert die Abnahme der e/a-Zeit die Erhöhung der CPU aus, um die Komprimierung zu behandeln.

Wenn der Test jedoch parallel ausgeführt wird, indem *numTasks* auf 4 festgelegt wird, verringert sich die durchschnittliche Zeit.

Bei größeren Datasets kann die Auswirkung der Komprimierung deutlicher bemerkbar sein. Die Komprimierung hängt ab von Dataset und Werten, sodass möglicherweise durch Ausprobieren festgestellt werden muss, welche Auswirkung die Komprimierung auf Ihr Dataset hat.

### <a name="effect-of-windows-power-plan-options"></a>Auswirkungen der Windows-Energieoptionen plan

In diesem Experiment wurde `rxLinMod` mit der *airlineWithIntCol*-Tabelle verwendet. Die Windows-Power-Plan wurde festgelegt, entweder **ausgeglichen** oder **hohe Leistung**. Für alle Tests wurde *numTasks* auf 1 festgelegt. Der Test sechs Mal ausgeführt wurde und unter beiden Energieoptionen untersuchen Sie die Variabilität des Ergebnisse zweimal ausgeführt wurde.

**Hohe Leistung** Option schalten:

| Testname | Ausführen von \# | Verstrichene Zeit | Durchschnittliche Zeit |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,57 Sekunden |              |
|           | 2      | 3,45 Sekunden |              |
|           | 3      | 3,45 Sekunden |              |
|           | 4      | 3,55 Sekunden |              |
|           | 5      | 3,55 Sekunden |              |
|           | 6      | 3,45 Sekunden |              |
|           |        |              | 3.475        |
|           | 1      | 3,45 Sekunden |              |
|           | 2      | 3,53 Sekunden |              |
|           | 3      | 3,63 Sekunden |              |
|           | 4      | 3,49 Sekunden |              |
|           | 5      | 3,54 Sekunden |              |
|           | 6      | 3,47 Sekunden |              |
|           |        |              | 3.5075       |

Energiesparoption **Ausgeglichen**:

| Testname | Ausführen von \# | Verstrichene Zeit | Durchschnittliche Zeit |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,89 Sekunden |              |
|           | 2      | 4,15 Sekunden |              |
|           | 3      | 3,77 Sekunden |              |
|           | 4      | 5 Sekunden    |              |
|           | 5      | 3,92 Sekunden |              |
|           | 6      | 3,8 Sekunden  |              |
|           |        |              | 3.91         |
|           | 1      | 3,82 Sekunden |              |
|           | 2      | 3,84 Sekunden |              |
|           | 3      | 3,86 Sekunden |              |
|           | 4      | 4,07 Sekunden |              |
|           | 5      | 4,86 Sekunden |              |
|           | 6      | 3,75 Sekunden |              |
|           |        |              | 3.88         |

**Schlussfolgerungen**

Die Ausführungszeit konsistentere und schneller ist, bei Verwendung der Windows **hohe Leistung** Energiesparplan Priorität.

#### <a name="using-integer-vs-strings-in-formulas"></a>Ganze Zahl im Vergleich zu Zeichenfolgen verwenden in Formeln

Dieser Test bewertet die Auswirkungen der Änderung des R-Codes, um ein häufiges Problem mit der Zeichenfolge Faktoren zu vermeiden. Insbesondere wurde ein Modell mithilfe trainiert `rxLinMod` mithilfe von zwei Tabellen: in der ersten Faktoren als Zeichenfolgen gespeichert werden; in der zweiten Tabelle werden die Faktoren als ganze Zahlen gespeichert.

+ Für die *Fluggesellschaft* Tabelle, für die Spalte [DayOfWeek] Zeichenfolgen enthält. Die _ColInfo_ -Parameter wurde verwendet, um den Faktor Ebenen (Montag, Dienstag,...) angeben

+  Für die *AirlineWithIndex* [DayOfWeek]-Tabelle ist eine ganze Zahl. Die _ColInfo_ Parameter wurde nicht angegeben.

+ In beiden Fällen wurde dieselbe Formel `ArrDelay ~ CRSDepTime + DayOfWeek` verwendet.

| Tabellenname          | Testname   | Durchschnittliche Zeit |
|---------------------|-------------|--------------|
| *Airline-Aktivität*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Schlussfolgerungen**

Bietet ein entscheidenden Vorteil wird für Faktoren vor Ganzzahlen anstelle von Zeichenfolgen verwenden.

### <a name="avoiding-transformation-functions"></a>Vermeiden von Funktionen der transformation

In diesem Test wurde ein Modell trainiert, mit `rxLinMod`, aber der Code zwischen den zwei Testläufen geändert wurde:

+ Eine Transformationsfunktion wurde in der ersten Ausführung im Rahmen der Modellerstellung angewendet. 
+ In der zweiten Ausführung waren die Funktionswerte vorausberechnete und verfügbar ist, so, dass keine Transformationsfunktion erforderlich war.

| Testname             | Durchschnittliche Zeit |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Schlussfolgerungen**

Die Trainingszeit wurde kürzer When **nicht** mithilfe einer Transformationsfunktion. Das Modell wurde also schneller trainiert, bei Verwendung von Spalten, die vorab berechnet und persistent in der Tabelle gespeichert sind.

Die einsparungen muss größer sein, wenn es viele weitere Transformationen wurden und das DataSet größere (\> 100 Millionen).

### <a name="using-columnar-store"></a>Verwenden des spaltenbasierten-Speichers

Dieser Test bewertet die Leistungsvorteile von mithilfe eines spaltenbasierten Datenspeicher und Index. Das gleiche Modell trainiert wurde, mithilfe von `rxLinMod` und keine Datentransformationen.

+ In der ersten Ausführung verwendet die Tabelle einen Zeilenspeicher standard.
+ In der zweiten Ausführung wurde ein spaltenspeicher verwendet.

| Tabellenname         | Testname | Durchschnittliche Zeit |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Schlussfolgerungen**

Leistung ist besser mit den Einspaltig Speicher als mit der standardmäßigen Zeilenspeicher. Ein deutlicher Unterschied in der Leistung bei größeren Datasets erwartet werden kann (\> 100 Millionen).

### <a name="effect-of-using-the-cube-parameter"></a>Auswirkungen der mit dem cubeparameter

Der Zweck des Tests wurde, um zu bestimmen, ob die Option im "revoscaler" für die Verwendung der vorausberechnete **Cube** Parameter kann die Leistung verbessern. Ein Modell trainiert wurde, mithilfe von `rxLinMod`, folgende Formel:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

In der Tabelle, die Faktoren *DayOfWeek* als Zeichenfolge gespeichert ist.

| Testname     | Cube-Parameter | numTasks | Durchschnittliche Zeit | Einzeiliges Vorhersagen (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Schlussfolgerungen**

Die Verwendung des Arguments Parameter Cube deutlich verbessert.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Auswirkung die Änderung MaxDepth für der RxDTree-Modelle

In diesem Experiment der `rxDTree` -Algorithmus verwendet wurde, zum Erstellen eines Modells auf die *AirlineColumnar* Tabelle. Für diesen Test wurde *numTasks* auf 4 festgelegt. Mehrere verschiedene Werte für *MaxDepth* verwendet wurden, um zu veranschaulichen, wie Strukturtiefe ändern zur Laufzeit auswirkt.

| Testname       | maxDepth | Durchschnittliche Zeit |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**Schlussfolgerungen**

Mit zunehmender die Tiefe des Baums, der die Gesamtzahl der Knoten exponentiell erhöht. Die verstrichene Zeit zum Erstellen des Modells auch erheblich erhöht.

### <a name="prediction-on-a-stored-model"></a>Vorhersagen für eine gespeicherte Modell

Der Zweck dieses Tests wurde, um zu bestimmen, die Auswirkungen auf die Leistung für die Bewertung des trainierten Modells eine SQL Server-Tabelle gespeichert ist und nicht als Teil der aktuell ausgeführten Code generiert. Für die Bewertung, wird das gespeicherte Modell aus der Datenbank geladen und Vorhersagen werden mit einem Datenrahmen mit einer Zeile im Arbeitsspeicher (lokalen computekontext) erstellt.

Die Testergebnisse anzeigen, die Zeit für das Modell speichern, und die Zeit zum Laden des Modells und vorherzusagen.

| Tabellenname | Testname | Durchschnittliche Zeit (Trainieren des Modells) | Zeit zum Speichern/Laden des Modells|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (einschließlich Zeit für Vorhersagen) |

**Schlussfolgerungen**

Laden eines trainierten Modells aus einer Tabelle ist deutlich schneller tun Vorhersageabfragen aus. Es wird empfohlen, dass Sie das Modell erstellen und ausführen, alle in einem Skript Bewertung vermeiden.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Fallstudie: Optimierung für den Task Resume-Abgleich

Das Modell Resume-Abgleich wurde entwickelt, von Microsoft Data scientists Ke Huang zum Testen der Leistung von R-Code in SQL Server, und auf diese Weise dies der Fall ist Hilfe Data Scientists skalierbarer erstellen, Lösungen auf Unternehmensebene.

### <a name="methods"></a>Methoden

Die "revoscaler" und die MicrosoftML Pakete wurden zum Trainieren eines Vorhersagemodells in einer komplexen R-Lösung, die im Zusammenhang mit großen Datasets verwendet. SQL-Abfragen und R-Code wurden in den Tests identisch. Tests wurden auf einer einzelnen Azure-VM mit SQL Server-Installation ausgeführt. Der Autor verglichen dann bewerteten Zeiten mit und ohne die folgenden Optimierungen, die von SQL Server bereitgestellt wird:

- In-Memory-Tabellen
- Soft-NUMA
- Resource Governor

Um die Auswirkung von Soft-NUMA auf R-skriptausführung zu bewerten, getestet, die Data Science-Team die Lösung auf virtuellen Azure-Computer mit 20 physischen Kernen. Auf diese physische Kerne wurden vier Soft-NUMA-Knoten automatisch erstellt, dass jeder Knoten fünf Kerne enthalten sind.

CPU-Affinitization wurde im Szenario fortsetzen übereinstimmende zum Bewerten der Auswirkungen auf R-Aufträge erzwungen. Vier **SQL Ressourcenpools** und vier **externen Ressourcenpools** erstellt wurden, und die CPU-Affinität wurde angegeben, um sicherzustellen, dass dieselbe Gruppe von CPUs in den einzelnen Knoten verwendet werden würde.

Jede der Ressourcenpools wurde zur Optimierung der Auslastung der Hardware eine andere Arbeitsauslastungsgruppe zugewiesen. Der Grund hierfür ist, Soft-NUMA und CPU-Affinität physischen Speicher in der physischen NUMA-Knoten kann nicht geteilt werden. aus diesem Grund müssen alle soft NUMA-Knoten, die auf dem gleichen physischen NUMA-Knoten basieren definitionsgemäß Arbeitsspeicher in demselben Betriebssystem-Speicherblock verwenden. Das heißt, ist es keine Speicher-Prozessor-Affinität.

Der folgende Prozess wurde verwendet, um diese Konfiguration zu erstellen:

1. Reduzieren Sie die Arbeitsspeichermenge, die mit SQL Server standardmäßig zugewiesen.

2. Erstellen Sie die vier neuen Pools für die R-Aufträge parallel ausgeführt wird.

3. Erstellen Sie vier Arbeitsauslastungsgruppen, sodass jede Arbeitsauslastungsgruppe einen Ressourcenpool zugeordnet ist.

4. Starten der Ressourcenkontrolle mit dem neuen Arbeitsauslastungsgruppen und Zuweisungen.

5. Erstellen Sie eine benutzerdefinierte Klassifizierungsfunktion-Funktion (UDF) verschiedene Aufgaben auf anderen Arbeitsauslastungsgruppen zuweisen.

6. Aktualisieren Sie die Konfiguration der Ressourcenkontrolle, um die Funktion für die entsprechenden Arbeitsauslastungsgruppen zu verwenden.

### <a name="results"></a>Ergebnisse

Die Konfiguration, die die beste Leistung im Resume-übereinstimmenden zu untersuchen, mussten wurde wie folgt aus:

-   Vier interne Ressourcenpools (für SQL Server)

-   Vier externen Ressourcenpools (für externe Skripts für Aufträge)

-   Jeder Ressourcenpool ist einer bestimmten Arbeitsauslastungsgruppe zugeordnet

-   Unterschiedliche CPUs wird jedem Ressourcenpool zugewiesen.

-   Maximale interne speicherauslastung (für SQL Server) = 30 %

-   Maximaler Arbeitsspeicher für die Verwendung von R-Sitzungen = 70 %

Für das Modell fortsetzen übereinstimmende externes Skript Verwendung starker wurde und gibt es keine andere Datenbank Datenbankmoduldienste ausgeführt wurden. Aus diesem Grund wurden für externe Skripts reservierten Ressourcen auf 70 % erhöht, die die beste Konfiguration bereit skriptleistung erwiesen.

Diese Konfiguration wurde auf eingetroffen sind, indem Sie mit unterschiedlichen Werten experimentieren. Wenn Sie unterschiedliche Hardware- oder einer anderen Projektmappe verwenden, kann die optimale Konfiguration unterscheiden. Probieren Sie immer die beste Konfiguration für Ihren Fall gefunden!

In der Projektmappe optimiert wurden 1.1 Millionen Datenzeilen (mit 100 Funktionen) in weniger als 8,5 Sekunden auf einem Computer von 20 Kernen bewertet. Optimierungen wird die Leistung im Hinblick auf bewerteten Zeit erheblich verbessert.

Die Ergebnisse vorgeschlagen, die auch die **Anzahl von Funktionen** hatte einen entscheidenden Einfluss auf die bewerteten Zeit. Die Verbesserung wurde auch einen wichtigeren, wenn weitere Funktionen in das Vorhersagemodell verwendet wurden.

Es wird empfohlen, dass Sie in diesem Blog-Artikel und die zugehörigen Lernprogramm ausführliche Informationen zu lesen.

-   [Optimierung Tipps und Tricks für Machine Learning in SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Viele Benutzer haben bereits erwähnt, ergibt sich eine kleine Pause während die Laufzeit von R (oder Python) zum ersten Mal geladen wird. Aus diesem Grund wie bei diesen Tests beschrieben die Zeit für die erste Ausführung ist häufig gemessen, aber später verworfen. Nachfolgende zwischenspeicherungen möglicherweise wichtige Leistungsunterschiede zwischen dem ersten und zweiten ausgeführt. Es gibt auch ein gewisser Aufwand Wenn Daten zwischen SQL Server und die externe Runtime verschoben werden vor allem, wenn Daten über das Netzwerk, anstatt direkt aus SQL Server geladen wird übergeben werden.

Aus diesen Gründen ist keine einfache Lösung zur Vermeidung derartiger diesmal erstmalige Laden mit Auswirkungen auf die Leistung erheblich abhängig von der Aufgabe. Zwischenspeichern wird z. B. für einzeiliges Bewertung in Batches ausgeführt. Daher aufeinander folgende bewerteten Operationen sind wesentlich schneller, und weder das Modell noch der R-Laufzeit wird erneut geladen. Sie können auch [native Bewertung](../sql-native-scoring.md) zu vermeiden, dass die R-Laufzeitversion vollständig geladen.

Für große Modelle trainieren oder bewerten in großen Batches, möglicherweise der Aufwand im Vergleich zu die Gewinne aus datenverschiebungen zu vermeiden oder streaming und parallele Verarbeitung minimal. Finden Sie in dieser letzten Blogs und Beispiele für zusätzliche Leistungsleitfaden:

+ [Loan Klassifizierung mithilfe von SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [Frühe kundenmeinungen mit R-Services](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [Mithilfe von R um 1 Million Transaktionen pro Sekunde Betrug zu erkennen](http://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Ressourcen

Im folgenden finden Links zu Informationen, Tools und Skripts, die in die Entwicklung von Tests verwendet.

+ Leistungstest erfolgt, Skripts und Links zu den Daten: [-Beispieldaten und -Skripts für SQL Server-Optimierungen Überprüfung kennzeichnen](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artikel beschreiben die Projektmappe fortsetzen übereinstimmende: [Optimierung Tipps und Tricks für SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Skripts, die in der SQL-Optimierung für Resume übereinstimmende Projektmappe verwendet: [GitHub-Repository](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Erfahren Sie mehr über Windows Server-Verwaltung

+ [Vorgehensweise: Bestimmen der geeigneten Auslagerungsdateigröße für 64-Bit-Versionen von Windows](https://support.microsoft.com/kb/2860880)

+ [Grundlegendes zu NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Wie unterstützt SQL Server NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Erfahren Sie mehr über SQL Server-Optimierungen

+ [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [Einführung in Speicheroptimierte Tabellen](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demo: Leistungsverbesserungen von in-Memory OLTP](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)

+ [Aktivieren der Komprimierung für eine Tabelle oder einen Index](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Deaktivieren der Komprimierung für eine Tabelle oder einen Index](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Informationen Sie zum Verwalten von SQL Server

+ [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)

+ [Einführung in die Ressourcenkontrolle](https://technet.microsoft.com/library/bb895232.aspx)

+ [Ressourcenkontrolle für R Services](resource-governance-for-r-services.md)

+ [Vorgehensweise: erstellen ein Ressourcenpools für R](how-to-create-a-resource-pool-for-r.md)

+ [Ein Beispiel zum Konfigurieren der Ressourcenkontrolle](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Tools

+ [DISKSPD storage load generator/performance test tool (DISKSPD-Speicherladungsgenerator/Leistungstesttool)](https://github.com/microsoft/diskspd)

+ [Referenz zum Hilfsprogramm FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Andere Artikel in dieser Serie

[Leistung optimieren für R – Einführung](sql-server-r-services-performance-tuning.md)

[Optimieren der Leistung für R - SQL Server-Konfiguration](sql-server-configuration-r-services.md)

[Optimieren der Leistung für R - R Optimierung von Code und Daten](r-and-data-optimization-r-services.md)

[Performance Tuning - Fallstudien](performance-case-study-r-services.md)
