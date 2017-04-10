---
title: "Leistung Case Study (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# Leistung Case Study (R Services)

Um die Auswirkung der Anleitung in den vorherigen Abschnitten veranschaulichen, wurden die Tests mithilfe der Tabellen aus dem Fluggesellschaft ausgeführt. 

## Tests und Beispieldaten

Es gibt sechs Tabellen mit 10M Zeilen in jeder Tabelle:

| Tabellenname | Description |
| ---------- | ----------- |
| _Fluggesellschaft_ | Daten aus der ursprünglichen Xdf mit konvertiert *RxDataStep*. |
| _airlineWithIntCol_ | *DayOfWeek* in eine ganze Zahl anstelle einer Zeichenfolge konvertiert. Fügt auch eine *RowNum* Spalte. |
| _airlineWithIndex_ | Die gleichen Daten wie die *AirlineWithIntCol* Tabelle, jedoch mit einem einzelnen gruppierten Index mithilfe der *RowNum* Spalte. |
| _airlineWithPageComp_ | Die gleichen Daten wie die *AirlineWithIndex* Tabelle, jedoch mit der Page-Komprimierung aktiviert. Außerdem fügt zwei Spalten, *CRSDepHour* und *späte*, werden die aus berechnet *ID* und *ArrDelay*. |
| _airlineWithRowComp_ | Die gleichen Daten wie die *AirlineWithIndex* Tabelle, jedoch mit Row-Komprimierung aktiviert. Außerdem fügt zwei Spalten, *CRSDepHour* und *späte* werden die aus berechnet *ID* und *ArrDelay*. 
| _airlineColumnar_ | Ein Einspaltig Speicher mit einem einzelnen gruppierten Index. Diese Tabelle wird aufgefüllt, mit Daten aus einer Aufräumarbeiten Csv Datei. |

Skripte, die zur Durchführung der Tests beschrieben, die in diesem Abschnitt sowie Links zu den Beispieldaten für die Tests verwendete finden Sie unter [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

Jeder einzelne Test ausgeführt wurde bis zu sechs Mal die Zeit der ersten (kalt ausführen) wurde gelöscht. Um den gelegentlichen Ausreißer zu ermöglichen, wurde die maximale Zeit für die verbleibenden fünf ausgeführt wird, ebenfalls gelöscht. Der Durchschnitt der vier verbleibenden Ausführungen wurde berechnet die durchschnittliche verstrichene Laufzeit jedes Tests erstellt. R Garbagecollection wurde vor jedem Test ausgelöst. Der Wert der *RowsPerRead* für jeden Test auf 500000 festgelegt wurde.

## Größe der Daten bei Verwendung von Komprimierung und eine Einspaltig Store-Tabelle

Im folgenden sind die Ergebnisse der Verwendung von Komprimierung und einer einspaltigen Tabelle zum Verringern der Größe der Daten:

| Tabellenname | Zeilen | Reserviert. | Data | index_size | Nicht verwendet | % (Reserviert) speichern |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | 528 KB | 0 |
| airlineWithPageComp | 10000000 | 625784 KB | 623744 KB | 1352 KB | 688 KB | 79% |
| airlineWithRowComp | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| airlineColumnar | 9999999 | 201992 KB | 201624 KB | n/v | 368 KB | 93% |

## Verwenden die ganze Zahl im Vergleich. Zeichenfolge in Formel

In diesem Experiment `rxLinMod` wurde mit der Airline-Tabelle verwendet (wobei *DayOfWeek* ist eine Zeichenfolge) und *AirlineWithIndex* (, in denen *DayOfWeek* ist eine ganze Zahl). Im ersten Fall `colInfo` wurde verwendet, um die Ebenen Factor angeben (`Monday`, `Tuesday`, ...). Für die zweite `colInfo` wurde nicht angegeben. In beiden Fällen wurde die gleiche Formel verwendet. Die verwendete Formel ist `ArrDelay ~ CRSDepTime + DayOfWeek`. Die folgenden Ergebnisse zeigt eindeutig die Vorteile von Integer-Vs-Zeichenfolge:

| Tabellenname | Name des Tests | Die durchschnittliche Zeit |
| ---------- | --------- | ------------ |
| Fluggesellschaft | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## Komprimierung

In diesem Experiment `rxLinMod` verwendet wurde, mit der *AirlineWithIndex*, *AirlineWithPageComp*, und *AirlineWithRowComp* Tabellen. Die gleiche Formel und Abfrage wurde für alle Tabellen verwendet. 

| Tabellenname | Name des Tests | numTasks | Die durchschnittliche Zeit |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | "Nocompression" | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

Beachten Sie, Komprimierung, die allein (*NumTasks* auf 1 festgelegt) scheint nicht dabei helfen, wie die Verringerung der e/a-Zeit der Anstieg der CPU-Komprimierung in der Lage kompensiert. Allerdings bei Ausführung des Tests wird parallel durch Festlegen von *NumTasks* 4 die durchschnittliche Zeit verringert. Bei größeren Datasets möglicherweise der Effekt der Komprimierung deutlicher. Komprimierung hängt von Datasets und Werte, damit experimentieren möglicherweise benötigt werden, um zu bestimmen, dass die Komprimierung Effekt auf das DataSet verfügt.

## Vermeiden von Transformationsfunktion

In diesem Experiment `rxLinMod` mit der AirlineWithIndex-Tabelle mit und ohne Verwendung einer Transformationsfunktion verwendet wird.  

| Name des Tests | Die durchschnittliche Zeit |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

Beachten Sie, dass es zur Verbesserung der Zeitpunkt, wenn eine Transformationsfunktion (in Spalten, die bereits berechnet und in der Tabelle beibehalten) nicht verwenden. Die Zeitersparnis werden viel größer, wenn es viele weitere Transformationen und das Dataset ist größer (> 100M).

## Einspaltig Store verwenden

In diesem Experiment `rxLinMod` wurde ohne eine Transformation mit den Tabellen AirlineWithIndex und AirlineColumnar verwendet. Die Ergebnisse zeigen, dass der einspaltige Speicher besser als Zeile Store ausführen kann. Es ist ein deutlicher Unterschied bei der Leistung auf größeren DataSet (> 100 M).  

| Tabellenname | Name des Tests |Die durchschnittliche Zeit |
| ---------- | --------- | ------------ |
| airlineWithIndex | RowStore | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## Auswirkungen des Cube-Parameters

In diesem Experiment `rxLinMod` mit der Airline-Tabelle verwendet wird, in dem `DayOfWeek` wird als Zeichenfolge gespeichert. Die verwendete Formel ist `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`. Die Ergebnisse verdeutlichen, die die Verwendung von `cube` Parameter hilft bei der Leistung. 

| Name des Tests | Cubeparameter | numTasks | Die durchschnittliche Zeit | Eine Zeile Vorhersagen (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## Auswirkung der MaxDepth für rxDTree

In diesem Experiment `rxDTree` mit der AirlineColumnar-Tabelle verwendet wird. Mehrere verschiedene Werte für *MaxDepth* verwendet wurden, um zu veranschaulichen, wie sie die Komplexität der Laufzeit beeinflusst. Mit zunehmender Tiefe die die Gesamtzahl der Knoten exponentiell erhöhen, und die verstrichene Zeit erheblich erhöhen. Für diesen Test *NumTasks* auf 4 festgelegt wurde.

| Name des Tests | maxDepth | Die durchschnittliche Zeit |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## Auswirkung der Power-Optionen

In diesem Experiment `rxLinMod` wurde mit der AirlineWithIntCol-Tabelle verwendet, während Windows sowohl ausgeglichen als auch hohe Leistung Energieoptionen festgelegt wurde. Für alle Tests *NumTasks* auf 1 festgelegt wurde. Der Test 6-Mal ausgeführt wurde und unter beide Optionen die Variabilität der Ergebnisse veranschaulicht, wenn mit der Option Ausbalanciert zweimal ausgeführt wurde. Die Ergebnisse zeigen, dass die Zahlen konsistentere und schnellere für die Power-Option für hohe Leistung. 

__Hohe Leistung__ power Option:

| Name des Tests | Ausführen # | Verstrichene Zeit | Die durchschnittliche Zeit |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3,57 Sekunden | &nbsp; |
| &nbsp; | 2 | 3,45 Sekunden | &nbsp; |
| &nbsp; | 3 | 3,45 Sekunden | &nbsp; |
| &nbsp; | 4 | 3.55 Sekunden | &nbsp; |
| &nbsp; | 5 | 3.55 Sekunden | &nbsp; |
| &nbsp; | 6 | 3,45 Sekunden | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3,45 Sekunden | &nbsp; |
| &nbsp; | 2 | 3.53 Sekunden | &nbsp; |
| &nbsp; | 3 | 3,63 Sekunden | &nbsp; |
| &nbsp; | 4 | 3.49 Sekunden | &nbsp; |
| &nbsp; | 5 | 3.54 Sekunden | &nbsp; |
| &nbsp; | 6 | 3.47 Sekunden | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__Ausgeglichene__ power Option:

| Name des Tests | Ausführen # | Verstrichene Zeit | Die durchschnittliche Zeit |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 Sekunden | &nbsp; |
| &nbsp; | 2 | 4.15 Sekunden | &nbsp; |
| &nbsp; | 3 | 3.77 Sekunden | &nbsp; |
| &nbsp; | 4 | 5 Sekunden | &nbsp; |
| &nbsp; | 5 | 3.92 Sekunden | &nbsp; |
| &nbsp; | 6 | 3.8 Sekunden | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3,82 Sekunden | &nbsp; |
| &nbsp; | 2 | 3,84 Sekunden | &nbsp; |
| &nbsp; | 3 | 3,86 Sekunden | &nbsp; |
| &nbsp; | 4 | 4.07 Sekunden | &nbsp; |
| &nbsp; | 5 | 4.86 Sekunden | &nbsp; |
| &nbsp; | 6 | 3,75 Sekunden | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## Vorhersage mit einem gespeicherten Modell

In diesem Experiment ein Modell erstellt und in einer Datenbank gespeichert. Anschließend wird das gespeicherte Modell aus der Datenbank und die Vorhersagen mit einem Datenrahmen eine Zeile im Arbeitsspeicher (lokale Compute-Kontext) geladen. Die Zeit zum Trainieren, zu speichern, und das Modell geladen und Vorhersagen ist unten dargestellt. Dies ist deutlich schneller vorhersagen möchten. Die Testergebnisse zeigen die Zeit für das Modell zu speichern und die benötigte Zeit für das Modell geladen und vorherzusagen. 

| Tabellenname | Name des Tests | Die durchschnittliche Zeit (zum Trainieren) | Zeit zum Speichern/Modell laden |
| ---------- | --------- | ----- | ----- |
| Fluggesellschaft | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09. (einschließlich der Zeit für Vorhersagen) |


## Behandeln von Leistungsproblemen

In diesem Abschnitt verwendeten Tests erzeugen Ausgabedateien für jede Ausführung durch Verwendung der *ReportProgress* -Parameter, der an die Tests mit dem Wert `3`. Die Konsolenausgabe wird in eine Datei im Ausgabeverzeichnis geleitet. Die Ausgabedatei enthält Informationen über die e/a-Übergangszeit und Rechenzeit verbrachte Zeit. Diese Zeiten sind nützlich für die Problembehandlung und Diagnose. Die Testskripts verarbeiten diese Zeiten für die verschiedenen ausgeführt wird, mit der durchschnittlichen Zeit über ausgeführt wird. Diese Skripts testen und Techniken können auch nützlich sein, in der Fehlerbehebung für Probleme, bei der Verwendung von Rx-Analysefunktionen für Ihre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Das folgende zeigt z. B. die Beispiel-Zeiten für eine Ausführung. Die wichtigsten Anzeigedauer von Interesse sind insgesamt lesen (e/a-Zeit) und den Übergang Zeit (in Einrichten von Prozessen für die Berechnung).

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 ## Siehe auch
 [SQL Server-R Services Performance Tuning Guide](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [SQL Server-Konfiguration für R-Dienste](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R und Datenoptimierung](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)