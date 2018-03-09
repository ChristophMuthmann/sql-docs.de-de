---
title: Statistik | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: statistics
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ed0124e677f79bd25b11a4ac994f60e65f8fe82
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="statistics"></a>Statistik
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Der Abfrageoptimierer verwendet Statistiken zum Erstellen von Abfrageplänen, die die Abfrageleistung verbessern. Bei den meisten Abfragen generiert der Abfrageoptimierer automatisch die notwendigen Statistiken für einen hochwertigen Abfrageplan. In einigen Fällen müssen Sie weitere Statistiken erstellen oder den Abfrageentwurf ändern, um optimale Ergebnisse zu erzielen. Dieses Thema enthält eine Erläuterung von Statistikkonzepten sowie Richtlinien zur effektiven Verwendung von Abfrageoptimierungsstatistiken.  
  
##  <a name="DefinitionQOStatistics"></a> Komponenten und Konzepte  
### <a name="statistics"></a>Statistik  
 Statistiken zur Abfrageoptimierung sind Blobs (Binary Large Objects), die statistische Informationen über die Verteilung von Werten in Spalten einer Tabelle oder indizierten Sicht enthalten. Der Abfrageoptimierer verwendet diese Statistiken, um die *Kardinalität* oder Anzahl von Zeilen im Abfrageergebnis zu schätzen. Diese *Kardinalitätsschätzungen* ermöglichen es dem Abfrageoptimierer, einen hochwertigen Abfrageplan zu erstellen. Beispielsweise kann der Abfrageoptimierer Kardinalitätsschätzungen verwenden, um statt des ressourcenintensiveren Index Scan-Operators den Index Seek-Operator auszuwählen und auf diese Weise die Abfrageleistung zu verbessern.  
  
 Jedes Statistikobjekt wird für eine Liste mit mindestens einer Tabellenspalte erstellt und enthält ein *Histogramm*, das die Verteilung von Werten in der ersten Spalte anzeigt. Statistikobjekte, die sich auf mehrere Spalten beziehen, enthalten außerdem statistische Informationen über die spaltenübergreifende Korrelation von Werten. Diese Korrelationsstatistiken oder *Dichten*werden von der Anzahl unterschiedlicher Zeilen mit Spaltenwerten abgeleitet. 

#### <a name="histogram"></a> Histogramm  
Ein **Histogramm** misst die Häufigkeit des Vorkommens für jeden unterschiedlichen Wert in einem Dataset. Der Abfrageoptimierer berechnet ein Histogramm für die Spaltenwerte in der ersten Schlüsselspalte des Statistikobjekts und wählt die Spaltenwerte aus, indem statistische Zeilenstichproben entnommen werden oder indem ein vollständiger Scan aller Zeilen in der Tabelle oder Sicht ausgeführt wird. Wenn das Histogramm anhand einer Gruppe von Zeilenstichproben erstellt wird, handelt es sich bei der gespeicherten Gesamtzahl von Zeilen und unterschiedlichen Werten um Schätzungen, die keine ganzen Zahlen sein müssen.

> [!NOTE]
> Histogramme werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur für eine einzige Spalte erstellt, nämlich für die erste der Schlüsselspalten des Statistikobjekts.
  
Zum Erstellen des Histogramms sortiert der Abfrageoptimierer die Spaltenwerte, berechnet die Anzahl der Werte, die den einzelnen unterschiedlichen Spaltenwerten entsprechen, und aggregiert die Spaltenwerte dann in maximal 200 zusammenhängenden Histogrammschritten. Jeder Histogrammschritt umfasst einen Bereich von Spaltenwerten gefolgt von einem oberen Spaltengrenzwert. Der Bereich enthält alle möglichen Spaltenwerte zwischen den Begrenzungswerten, ohne die Begrenzungswerte selbst. Der niedrigste der sortierten Spaltenwerte ist der obere Grenzwert für den ersten Histogrammschritt.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt das **Histogramm** aus den sortierten Spaltenwerten in drei Schritten:

- **Initialisierung des Histogramms:** Im ersten Schritt wird eine Wertesequenz verarbeitet, die am Anfang der sortierten Menge beginnt, und bis zu 200 Werte von *range_high_key*, *equal_rows*, *range_rows*, und *distinct_range_rows* werden erfasst (*range_rows* und *distinct_range_rows* sind während dieses Schritts immer 0). Der erste Schritt ist abgeschlossen, wenn alle Eingaben erschöpft sind oder 200 Werte gefunden wurden. 
- **Scannen mit Bucketzusammenführung:** Jeder zusätzliche Wert aus der führenden Spalte des Statistikschlüssels wird im zweiten Schritt in sortierter Reihenfolge verarbeitet. Jeder nachfolgende Wert wird entweder zum letzten Bereich hinzugefügt, oder es wird am Ende ein neuer Bereich erstellt (dies ist möglich, da die Eingabewerte sortiert sind). Wenn ein neuer Bereich erstellt wird, wird ein Paar der vorhandenen benachbarten Bereiche zu einem einzelnen Bereich reduziert. Dieses Bereichspaar wird ausgewählt, um den Verlust von Informationen zu minimieren. Diese Methode verwendet einen Algorithmus für die *maximale Differenz*, um die Anzahl von Schritten im Histogramm zu minimieren und gleichzeitig die Differenz zwischen den Begrenzungswerten zu maximieren. Die Anzahl von Schritten nach dem Reduzieren von Bereichen bleibt in diesem Schritt bei 200.
- **Konsolidierung des Histogramms:** Im dritten Schritt können weitere Bereiche reduziert werden, wenn keine erhebliche Menge an Informationen verloren geht. Die Anzahl von Histogrammschritten kann geringer sein als die Anzahl unterschiedlicher Werte, auch bei Spalten mit weniger als 200 Grenzpunkten. Wenn jede Spalte mehr als 200 eindeutige Werte enthält, kann das Histogramm daher weniger als 200 Schritte enthalten. Für eine Spalte, die nur aus eindeutigen Werten besteht, enthält das konsolidierte Histogramm mindestens drei Schritte.

> [!NOTE]
> Wenn das Histogramm mithilfe eines Beispiels statt mit der Option „Fullscan“ erstellt wurde, werden die Werte von *equal_rows*, *range_rows*, *distinct_range_rows* und *average_range_rows* geschätzt und müssen keine ganzen Zahlen sein.

Das folgende Diagramm zeigt ein Histogramm mit sechs Schritten. Der Bereich links vom ersten oberen Grenzwert ist der erste Schritt.
  
![](../../relational-databases/system-dynamic-management-views/media/histogram_2.gif "Histogramm") 
  
Für jeden der vorherigen Histogrammschritt gilt:
-   Eine fett formatierte Zeile stellt den oberen Grenzwert (*range_high_key*) und die Häufigkeit des Vorkommens (*equal_rows*) dar.  
  
-   Der einfarbige Bereich links von *range_high_key* stellt den Bereich der Spaltenwerte und die durchschnittliche Häufigkeit des Vorkommens der einzelnen Spaltenwerte (*average_range_rows*) dar. *average_range_rows* ist für den ersten Histogrammschritt immer 0.  
  
-   Gepunktete Linien stellen die als Stichprobe entnommenen Werte dar, die zum Schätzen der Gesamtanzahl der unterschiedlichen Werte im Bereich (*distinct_range_rows*) verwendet werden, sowie die Gesamtanzahl der Werte im Bereich (*range_rows*). Der Abfrageoptimierer verwendet *range_rows* und *distinct_range_rows*, um *average_range_rows* zu berechnen. Die als Stichprobe entnommenen Werte werden nicht gespeichert.   
  
#### <a name="density"></a>Dichtevektor  
Die **Dichte** enthält Informationen zur Anzahl von Duplikaten in einer bestimmten Spalte oder Spaltekombination und wird als 1/(Anzahl der unterschiedlichen Werte) berechnet. Der Abfrageoptimierer verwendet Dichten, um Kardinalitätsschätzungen für Abfragen zu erweitern, die mehrere Spalten aus derselben Tabelle oder indizierten Sicht zurückgeben. Der Dichtevektor enthält eine Dichte für jedes Präfix von Spalten im Statistikobjekt. 

> [!NOTE]
> Die Häufigkeit enthält Informationen über das Auftreten der einzelnen unterschiedlichen Werte in der ersten Schlüsselspalte des Statistikobjekts und wird als Zeilenanzahl · Dichte berechnet. In Spalten mit eindeutigen Werten kann eine maximale Häufigkeit von 1 gefunden werden.

Wenn ein Statistikobjekt beispielsweise die Schlüsselspalten `CustomerId`, `ItemId` und `Price` enthält, wird die Dichte für jedes der folgenden Spaltenpräfixe berechnet:
  
|Spaltenpräfix|Dichte berechnet für|  
|---|---|
|(CustomerId)|Zeilen mit übereinstimmenden Werten für CustomerId|  
|(CustomerId, ItemId)|Zeilen mit übereinstimmenden Werten für CustomerId und ItemId|  
|(CustomerId, ItemId, Price)|Zeilen mit übereinstimmenden Werten für CustomerId, ItemId und Price| 

### <a name="filtered-statistics"></a>Gefilterte Statistiken  
 Gefilterte Statistiken können die Abfrageleistung für Abfragen verbessern, bei denen aus klar definierten Teilmengen von Daten ausgewählt wird. Gefilterte Statistiken verwenden ein Filterprädikat, um die Teilmenge von Daten auszuwählen, die in der Statistik enthalten ist. Sorgfältig entworfene gefilterte Statistiken können den Abfrageausführungsplan im Vergleich zu Tabellenstatistiken verbessern. Weitere Informationen zum Filterprädikat finden Sie unter [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md). Weitere Informationen zum Zeitpunkt der Erstellung von gefilterten Statistiken finden Sie im Abschnitt [Zeitpunkt der Erstellung von Statistiken](#CreateStatistics) in diesem Thema.  
 
### <a name="statistics-options"></a>Statistikoptionen  
 Anhand von drei Optionen können Sie festlegen, wann und wie Statistiken erstellt und aktualisiert werden. Diese Optionen werden nur auf Datenbankebene festgelegt.  
  
#### <a name="AutoUpdateStats"></a>AUTO_CREATE_STATISTICS (Option)  
 Ist die [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics)-Option zum automatischen Erstellen von Statistiken aktiviert, erstellt der Abfrageoptimierer nach Bedarf Statistiken für einzelne Spalten im Abfrageprädikat, um Kardinalitätsschätzungen für den Abfrageplan zu verbessern. Diese Statistiken für einzelne Spalten werden für Spalten erstellt, die noch nicht über ein [Histogramm](#histogram) in einem vorhandenen Statistikobjekt verfügen. Durch die AUTO_CREATE_STATISTICS-Option wird nicht festgelegt, ob Statistiken für Indizes erstellt werden. Durch diese Option werden auch keine gefilterten Statistiken generiert. Sie gilt ausschließlich für Statistiken für einzelne Spalten der gesamten Tabelle.  
  
 Erstellt der Abfrageoptimierer Statistiken als Ergebnis der Verwendung der AUTO_CREATE_STATISTICS-Option, beginnt der Statistikname mit `_WA`. Mithilfe der folgenden Abfrage können Sie bestimmen, ob der Abfrageoptimierer Statistiken für eine Abfrageprädikatsspalte erstellt hat.  
  
```sql  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s 
INNER JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
#### <a name="autoupdatestatistics-option"></a>AUTO_UPDATE_STATISTICS (Option)  
 Wenn die [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics)-Option zum automatischen Update von Statistiken aktiviert ist, stellt der Abfrageoptimierer fest, wann Statistiken veraltet sein könnten, und aktualisiert diese Statistiken, sobald sie von einer Abfrage verwendet werden. Statistiken sind veraltet, wenn die Datenverteilung in der Tabelle oder indizierten Sicht durch die Vorgänge INSERT, UPDATE, DELETE oder MERGE geändert wurde. Der Abfrageoptimierer stellt fest, wann Statistiken veraltet sein könnten, indem er die Anzahl von Datenänderungen seit der letzten Statistikaktualisierung ermittelt und sie mit einem Schwellenwert vergleicht. Der Schwellenwert basiert auf der Anzahl von Zeilen in der Tabelle oder indizierten Sicht.  
  
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet einen Schwellenwert basierend auf dem Prozentsatz der geänderten Zeilen. Dies ist unabhängig von der Anzahl der Zeilen in der Tabelle. Der Schwellenwert lautet:
    * Wenn die Tabellenkardinalität zum Zeitpunkt der Statistikauswertung 500 oder weniger beträgt, wird nach jeweils 500 Änderungen eine Aktualisierung durchgeführt.
    * Wenn die Tabellenkardinalität zum Zeitpunkt der Statistikauswertung über 500 liegt, wird nach jeweils 500 Änderungen + 20 Prozent eine Aktualisierung durchgeführt.

* Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und bei einem [Kompatibilitätsgrad](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) von unter 130 verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen abnehmenden dynamischen Schwellenwert für das Statistikupdate, der gemäß der Anzahl von Zeilen in der Tabelle angepasst wird. Dieser berechnet sich als Quadratwurzel aus 1.000 multipliziert mit der aktuellen Tabellenkardinalität. Durch diese Änderung werden Statistiken für große Tabellen häufiger aktualisiert. Weist eine Datenbank jedoch einen Kompatibilitätsgrad unter 130 auf, dann gilt der Schwellenwert [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  

> [!IMPORTANT]
> Ab [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] bis [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwenden Sie bei einem [Kompatibilitätsgrad der Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) unter 130 das [Ablaufverfolgungsflag 2371](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet dann einen abnehmenden dynamischen Schwellenwert für das Statistikupdate, der gemäß der Anzahl von Zeilen in der Tabelle angepasst wird.
  
Bevor der Abfrageoptimierer eine Abfrage kompiliert und einen zwischengespeicherten Abfrageplan ausführt, sucht er nach veralteten Statistiken. Vor dem Kompilieren einer Abfrage ermittelt der Abfrageoptimierer anhand der Spalten, Tabellen und indizierten Sichten im Abfrageprädikat, welche Statistiken veraltet sein könnten. Vor dem Ausführen eines zwischengespeicherten Abfrageplans überprüft das [!INCLUDE[ssDE](../../includes/ssde-md.md)] , ob der Abfrageplan auf aktuelle Statistiken verweist.  
  
Die AUTO_UPDATE_STATISTICS-Option gilt für Statistikobjekte, die für Indizes, einzelne Spalten in Abfrageprädikaten und mit der [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) -Anweisung generierte Statistiken erstellt wurden. Diese Option gilt auch für gefilterte Statistiken.  
 
Weitere Informationen zur Steuerung von AUTO_UPDATE_STATISTICS finden Sie unter [Steuern des Verhaltens der automatischen Statistikaktualisierung (AUTO_UPDATE_STATISTICS) in SQL Server](http://support.microsoft.com/help/2754171).
  
#### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC  
 Mit der [AUTO_UPDATE_STATISTICS_ASYNC](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics_async)-Option für das asynchrone Statistikupdate wird festgelegt, ob der Abfrageoptimierer das synchrone oder asynchrone Statistikupdate verwendet. Die Option für das asynchrone Statistikupdate ist standardmäßig deaktiviert, sodass der Abfrageoptimierer Statistiken synchron aktualisiert. Die AUTO_UPDATE_STATISTICS_ASYNC-Option gilt für Statistikobjekte, die für Indizes, einzelne Spalten in Abfrageprädikaten und mit der [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) -Anweisung generierte Statistiken erstellt wurden.  
 
 > [!NOTE]
 > Um die Option für die asynchrone Statistikaktualisierung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf der Seite *Optionen* des Fensters *Datenbankeigenschaften* festzulegen, müssen die beiden Optionen *Statistik automatisch aktualisierenn* und *Statistik automatisch asynchron aktualisieren* auf **True** festgelegt werden.
  
 Statistikaktualisierungen können entweder synchron (Standard) oder asynchron sein. Bei synchronen Statistikaktualisierungen werden Abfragen immer anhand aktueller Statistiken kompiliert und ausgeführt. Wenn Statistiken veraltet sind, wartet der Abfrageoptimierer auf aktualisierte Statistiken, bevor er die Abfrage kompiliert und ausführt. Bei asynchronen Statistikaktualisierungen werden Abfragen anhand vorhandener Statistiken kompiliert, auch wenn diese veraltet sind. Der Abfrageoptimierer könnte einen suboptimalen Abfrageplan auswählen, wenn die Statistiken beim Kompilieren der Abfrage veraltet sind. Wenn Abfragen nach dem Ausführen asynchroner Updates kompiliert werden, hat dies den Vorteil, dass für die Abfragen aktualisierte Statistiken verwendet werden.  
  
 Verwenden Sie ggf. synchrone Statistiken, wenn Sie Vorgänge ausführen, die die Verteilung der Daten ändern, beispielsweise das Kürzen einer Tabelle oder das Ausführen eines Massenupdates für einen großen Zeilenprozentsatz. Wenn Sie nach dem Abschließen des Vorgangs die Statistiken nicht aktualisieren, wird mithilfe von synchronen Statistiken sichergestellt, dass Statistiken vor dem Ausführen von Abfragen über die geänderten Daten aktuell sind.  
  
 In den folgenden Szenarien empfiehlt sich die Verwendung asynchroner Statistiken, um besser vorhersagbare Antwortzeiten für Abfragen zu erzielen:  
  
* Häufig werden von der Anwendung die gleichen Abfragen, ähnliche Abfragen bzw. ähnliche zwischengespeicherte Abfragepläne ausgeführt. Bei Verwendung asynchroner Statistikaktualisierungen können die Antwortzeiten für Abfragen vorhersagbarer sein als bei synchronen Statistikaktualisierungen, weil der Abfrageoptimierer eingehende Abfragen direkt ausführen kann, ohne auf aktuelle Statistiken zu warten. Dadurch wird verhindert, dass sich einige Abfragen verzögern und andere nicht.  
  
* In der Anwendung sind Timeouts bei Clientanforderungen aufgetreten, die dadurch verursacht werden, dass mindestens eine Abfrage auf aktualisierte Statistiken wartet. In einigen Fällen kann das Warten auf synchrone Statistiken dazu führen, dass Anwendungen mit kurzen Timeouts einen Fehler erzeugen.  
  
#### <a name="incremental"></a>INCREMENTAL  
 Wenn die Option INCREMENTAL von CREATE STATISTICS auf ON festgelegt ist, werden die Statistiken pro Partition erstellt. Bei OFF wird die Statistikstruktur gelöscht und die Statistik von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu berechnet. Der Standardwert ist OFF. Diese Einstellung überschreibt die INCREMENTAL-Eigenschaft auf Datenbankebene. Weitere Informationen zum Erstellen von inkrementellen Statistiken finden Sie unter [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md). Weitere Informationen zum automatischen Erstellen von Statistiken pro Partition finden Sie unter [Datenbankeigenschaften (Seite „Optionen“)](../../relational-databases/databases/database-properties-options-page.md#automatic) und [ALTER DATABASE SET Options (Transact-SQL) (Optionen für ALTER DATABASE SET (Transact-SQL))](../../t-sql/statements/alter-database-transact-sql-set-options.md). 
  
 Wenn einer umfangreichen Tabelle neue Partitionen hinzugefügt werden, sollte die Statistik aktualisiert werden, um die neuen Partitionen zu berücksichtigen. Das Scannen der gesamten Tabelle (FULLSCAN- oder SAMPLE-Option) könnte jedoch ziemlich lange dauern. Außerdem ist das Scannen der gesamten Tabelle nicht erforderlich, da ggf. nur die Statistik der neuen Partitionen benötigt wird. Durch die INCREMENTAL-Option werden nur Statistikdaten pro Partition erstellt und gespeichert. Beim Update werden nur die Statistiken der Partitionen aktualisiert, die eine neue Statistik erfordern.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird die Option ignoriert und eine Warnung generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
* Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
* Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
* Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
* Statistiken, die für gefilterte Indizes erstellt wurden.  
* Statistiken, die für Sichten erstellt wurden.  
* Statistiken, die für interne Tabellen erstellt wurden.  
* Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
## <a name="CreateStatistics"></a> Zeitpunkt der Erstellung von Statistiken  
 Der Abfrageoptimierer erstellt bereits Statistiken in der folgenden Weise:  
  
1.  Bei der Indexerstellung berechnet der Abfrageoptimierer Statistiken für Indizes, die sich auf Tabellen oder Sichten beziehen. Diese Statistiken werden für die Schlüsselspalten des Indexes erstellt. Wenn es sich um einen gefilterten Index handelt, erstellt der Abfrageoptimierer gefilterte Statistiken für die gleiche Teilmenge von Zeilen, die für den gefilterten Index angegeben wurden. Weitere Informationen zu gefilterten Indizes finden Sie unter [Erstellen gefilterter Indizes](../../relational-databases/indexes/create-filtered-indexes.md) und [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
2.  Der Abfrageoptimierer erstellt Statistiken für einzelne Spalten in Abfrageprädikaten, wenn [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) aktiviert ist.  
  
Bei den meisten Abfragen werden durch diese beiden Methoden zum Erstellen von Statistiken hochwertige Abfragepläne gewährleistet. In einigen Fällen können Sie Abfragepläne verbessern, indem Sie zusätzliche Statistiken mit der [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) -Anweisung erstellen. In diesen zusätzlichen Statistiken können Sie statistische Korrelationen aufzeichnen, die vom Abfrageoptimierer beim Erstellen von Statistiken für Indizes oder einzelne Spalten nicht berücksichtigt werden. Ihre Anwendung kann über zusätzliche statistische Korrelationen in den Tabellendaten verfügen, durch die der Abfrageoptimierer Abfragepläne verbessern kann, wenn sie für die Berechnung von Statistikobjekten zugrunde gelegt werden. Der Abfrageplan kann beispielsweise optimiert werden, indem gefilterte Statistiken für eine Teilmenge von Datenzeilen oder Statistiken für mehrere Spalten für Abfrageprädikatsspalten ausgeführt werden.  
  
Wenn Statistiken mit der CREATE STATISTICS-Anweisung erstellt werden, empfiehlt es sich, die AUTO_CREATE_STATISTICS-Option aktiviert zu lassen, damit der Abfrageoptimierer weiterhin routinemäßig Statistiken für einzelne Spalten für Abfrageprädikatsspalten erstellt. Weitere Informationen zu Abfrageprädikaten finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
Wenn eine der folgenden Bedingungen zutrifft, können Sie die Erstellung von Statistiken mit der CREATE STATISTICS-Anweisung in Erwägung ziehen:  

* Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber schlägt vor, Statistiken zu erstellen. 
* Das Abfrageprädikat enthält mehrere korrelierende Spalten, die sich noch nicht im gleichen Index befinden.  
* Bei der Abfrageausführung wird aus einer Teilmenge von Daten ausgewählt.  
* Statistiken für eine Abfrage fehlen.  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>Das Abfrageprädikat enthält mehrere korrelierende Spalten  
Wenn ein Abfrageprädikat mehrere Spalten mit spaltenübergreifenden Beziehungen und Abhängigkeiten enthält, könnte der Abfrageplan durch Statistiken für mehrere Spalten optimiert werden. Statistiken für mehrere Spalten enthalten spaltenübergreifende Korrelationsstatistiken, so genannte *Dichten*, die in Statistiken für einzelne Spalten nicht verfügbar sind. Durch Dichten können Kardinalitätsschätzungen verbessert werden, wenn Abfrageergebnisse von Datenbeziehungen zwischen mehreren Spalten abhängig sind.  
  
Wenn sich die Spalten bereits im gleichen Index befinden, ist das Statistikobjekt für mehrere Spalten bereits vorhanden und muss nicht manuell erstellt werden. Wenn sich die Spalten noch nicht im gleichen Index befinden, können Sie Statistiken für mehrere Spalten erstellen, indem Sie einen Index für die Spalten anlegen oder die [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)-Anweisung verwenden. Zur Verwaltung eines Indexes werden mehr Systemressourcen benötigt als zur Verwaltung eines Statistikobjekts. Wenn die Anwendung keinen Index für mehrere Spalten erfordert, können Sie Systemressourcen sparen, indem Sie das Statistikobjekt erstellen, ohne den Index zu generieren.  
  
Wenn Statistiken für mehrere Spalten erstellt werden, wirkt sich die Reihenfolge der Spalten in der Statistikobjektdefinition darauf aus, wie effektiv die Dichten beim Erstellen von Kardinalitätsschätzungen sind. Im Statistikobjekt werden Dichten für jedes Präfix von Schlüsselspalten in der Statistikobjektdefinition gespeichert. Weitere Informationen zu Dichten finden Sie im Abschnitt [Dichte](#density) auf dieser Seite.  
  
Zum Erstellen von Dichten, die für Kardinalitätsschätzungen hilfreich sind, müssen die Spalten im Abfrageprädikat einem der Spaltenpräfixe in der Statistikobjektdefinition entsprechen. Im Folgenden wird beispielsweise aus den Spalten `LastName`, `MiddleName`und `FirstName`ein Objekt für eine Statistik für mehrere Spalten erstellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
In diesem Beispiel verfügt das Statistikobjekt `LastFirst` über Dichten für die folgenden Spaltenpräfixe: `(LastName)`, `(LastName, MiddleName)` und `(LastName, MiddleName, FirstName)`. Für `(LastName, FirstName)` ist keine Dichte verfügbar. Wenn in der Abfrage `LastName` und `FirstName` ohne `MiddleName`verwendet werden, ist die Dichte für Kardinalitätsschätzungen nicht verfügbar.  
  
### <a name="query-selects-from-a-subset-of-data"></a>Abfrage wählt aus einer Teilmenge von Daten aus  
Wenn der Abfrageoptimierer Statistiken für einzelne Spalten und Indizes erstellt, berechnet er Statistiken für die Werte sämtlicher Zeilen. Wenn bei Abfragen aus einer Teilmenge von Zeilen ausgewählt wird und diese Teilmenge über eine eindeutige Datenverteilung verfügt, können Abfragepläne durch gefilterte Statistiken verbessert werden. Sie können gefilterte Statistiken erstellen, indem Sie die [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)-Anweisung mit der [WHERE](../../t-sql/queries/where-transact-sql.md)-Klausel verwenden, um den Filterprädikatausdruck zu definieren.  
  
Durch die Verwendung von [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] beispielsweise gehört jedes Produkt in der `Production.Product`-Tabelle zu einer von vier Kategorien in der `Production.ProductCategory`-Tabelle: Fahrräder, Bauteile, Bekleidung und Zubehör. Jede Kategorie verfügt über eine andere Datenverteilung für das Gewicht: Die Gewichte der Fahrräder reichen von 13,77 bis 30,0, die Gewichte der Bauteile reichen von 2,12 bis 1050,00 mit einigen NULL-Werten, die Gewichte der Bekleidung sind alle NULL, und die Gewichte des Zubehörs sind ebenfalls NULL.  
  
Bei den Fahrrädern liefern gefilterte Statistiken dem Abfrageoptimierer zu allen Fahrradgewichten genauere Statistikdaten und können die Abfrageplanqualität im Vergleich zu Tabellenstatistiken oder nicht vorhandenen Statistiken für die Weight-Spalte verbessern. Die Spalte mit dem Fahrradgewicht eignet sich besonders für gefilterte Statistiken, jedoch weniger für einen gefilterten Index, wenn nur relativ wenige Suchen nach Gewichtsangaben ausgeführt werden. Die Leistungsvorteile, die gefilterte Indizes bei der Suche bieten, können die zusätzlichen Kosten für Wartung und Speicher, die mit der Implementierung eines gefilterten Indexes in der Datenbank verbunden sind, jedoch nicht aufwiegen.  
  
Durch die folgende Anweisung wird die gefilterte `BikeWeights` -Statistik für alle Unterkategorien von Fahrrädern erstellt. Durch den gefilterten Prädikatausdruck werden Fahrräder definiert, indem alle Fahrradunterkategorien mit dem Vergleich `Production.ProductSubcategoryID IN (1,2,3)`aufgelistet werden. Das Prädikat kann den Kategorienamen für Fahrräder nicht verwenden, da er in der Production.ProductCategory-Tabelle gespeichert ist; alle Spalten im Filterausdruck müssen sich in der gleichen Tabelle befinden.  
  
[!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
Der Abfrageoptimierer kann die gefilterte Statistik für `BikeWeights` verwenden, um den Abfrageplan für die folgende Abfrage zu verbessern, bei der alle Fahrräder ausgewählt werden, deren Gewicht größer ist als `25`.  
  
```sql  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>Abfrage identifiziert fehlende Statistiken  
Wenn der Abfrageoptimierer aufgrund eines Fehlers oder eines anderen Ereignisses keine Statistiken erstellen kann, erstellt er den Abfrageplan ohne Verwendung von Statistiken. Der Abfrageoptimierer kennzeichnet die Statistik als nicht vorhanden und versucht beim nächsten Ausführen der Abfrage, die Statistik erneut zu generieren.  
  
Fehlende Statistiken werden als Warnungen angegeben (Tabellenname als rot formatierter Text), wenn der Ausführungsplan einer Abfrage mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]grafisch angezeigt wird. Das Fehlen von Statistiken wird zudem angezeigt, wenn die **Missing Column Statistics**-Ereignisklasse mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] überwacht wird. Weitere Informationen finden Sie unter [Fehler und Warnungen-Ereigniskategorie &#40;Datenbankmodul&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md).  
  
 Wenn Statistiken fehlen, führen Sie die folgenden Schritte aus:  
  
* Überprüfen Sie, ob [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) und [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) aktiviert sind.  
* Stellen Sie sicher, dass die Datenbank nicht schreibgeschützt ist. Wenn die Datenbank schreibgeschützt ist, kann kein neues Statistikobjekt gespeichert werden.  
* Erstellen Sie die fehlende Statistik mithilfe der [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md)-Anweisung.  
  
Wenn Statistiken zu einer schreibgeschützten Momentaufnahme fehlen oder veraltet sind, erstellt und verwaltet das [!INCLUDE[ssDE](../../includes/ssde-md.md)] temporäre Statistiken in **tempdb**. Wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] temporäre Statistiken erstellt, wird dem Statistiknamen das *_readonly_database_statistic*-Suffix angefügt, um die temporären Statistiken von den dauerhaften Statistiken zu unterscheiden. Das Suffix *_readonly_database_statistic* ist für von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generierte Statistiken reserviert. Skripts für die temporären Statistiken können erstellt und auf einer Datenbank mit Lese-/Schreibzugriff reproduziert werden. Bei einer Skripterstellung ändert [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] das Suffix des Statistiknamens von *_readonly_database_statistic* in *_readonly_database_statistic_scripted*.  
  
Nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann temporäre Statistiken erstellen und aktualisieren. Sie können jedoch temporäre Statistiken löschen und Statistikeigenschaften mit den gleichen Tools überwachen, die Sie für dauerhafte Statistiken verwenden:  
  
* Löschen Sie temporäre Statistiken mit der Anweisung [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md).  
* Überwachen Sie Statistiken mit den Katalogsichten **[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)** und **[sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)**. **sys_stats** beinhaltet die Spalte **is_temporary** . Damit wird angegeben, welche Statistiken dauerhaft und welche temporär sind.  
  
 Da temporäre Statistiken in **tempdb**gespeichert werden, werden durch einen Neustart des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensts alle temporären Statistiken entfernt.  
    
## <a name="UpdateStatistics"></a>Zeitpunkt der Statistikaktualisierung  
 Der Abfrageoptimierer stellt fest, wann Statistiken veraltet sein könnten, und aktualisiert sie, sobald sie für einen Abfrageplan benötigt werden. In einigen Fällen können Sie den Abfrageplan und damit die Abfrageleistung verbessern, indem Sie Statistiken häufiger aktualisieren, als dies bei Aktivierung von [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) der Fall ist. Sie können Statistiken mit der UPDATE STATISTICS-Anweisung oder der gespeicherten Prozedur sp_updatestats aktualisieren.  
  
 Durch das Update von Statistiken wird sichergestellt, dass Abfragen anhand aktueller Statistiken kompiliert werden. Dies führt jedoch dazu, dass Abfragen neu kompiliert werden. Es empfiehlt sich, Statistiken nicht zu oft zu aktualisieren und die Vorteile optimierter Abfragepläne gegen den Zeitaufwand für die Neukompilierung von Abfragen abzuwägen. Die Entscheidung hängt von der verwendeten Anwendung ab.  
  
 Beim Aktualisieren von Statistiken mit UPDATE STATISTICS oder sp_updatestats empfiehlt es sich, AUTO_UPDATE_STATISTICS aktiviert zu lassen, damit der Abfrageoptimierer die Statistiken weiterhin routinemäßig aktualisiert. Weitere Informationen zum Aktualisieren von Statistiken für eine Spalte, einen Index, eine Tabelle oder eine indizierte Sicht finden Sie unter [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Informationen zum Aktualisieren von Statistiken für alle benutzerdefinierten und internen Tabellen in der Datenbank finden Sie in der Beschreibung der gespeicherten Prozedur [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md).  
  
 Um zu ermitteln, wann Statistiken zuletzt aktualisiert wurden, verwenden Sie die Funktionen [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) oder [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md).  
  
 Ziehen Sie die Aktualisierung von Statistiken unter folgenden Bedingungen in Betracht:  
  
* Die Ausführungszeiten von Abfragen sind langsam.  
* Es werden INSERT-Vorgänge für aufsteigend oder absteigend sortierte Schlüsselspalten ausgeführt.  
* Eine Wartung wurde durchgeführt.  

### <a name="query-execution-times-are-slow"></a>Lange Ausführungszeiten für Abfragen  
 Wenn die Antwortzeiten von Abfragen langsam oder nicht vorhersagbar sind, sollten Sie sicherstellen, dass Abfragen auf aktuelle Statistiken zugreifen, bevor Sie weitere Schritte zur Problembehandlung ausführen.  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>INSERT-Ausführungen für aufsteigend oder absteigend sortierte Schlüsselspalten  
 Statistiken für aufsteigend oder absteigend sortierte Schlüsselspalten, z.B. IDENTITY-Spalten oder Spalten mit Echtzeit-Zeitstempeln, können häufigere Statistikaktualisierungen erfordern, als sie vom Abfrageoptimierer ausgeführt werden. Durch INSERT-Vorgänge werden neue Werte an aufsteigend oder absteigend sortierte Spalten angefügt. Möglicherweise wurden zu wenige Zeilen hinzugefügt, um ein Statistikupdate auszulösen. Wenn Statistiken nicht aktuell sind und bei der Abfrageausführung aus den zuletzt hinzugefügten Zeilen ausgewählt wird, weisen die aktuellen Statistiken keine Kardinalitätsschätzungen für diese neuen Werte auf. Dies kann zu ungenauen Kardinalitätsschätzungen und einer langsamen Abfrageleistung führen.  
  
 Eine Abfrage, die aus den letzten Bestelldaten auswählt, verfügt z. B. über ungenaue Kardinalitätsschätzungen, wenn die Statistiken nicht aktualisiert werden, um Kardinalitätsschätzungen für die letzten Bestelldaten einzuschließen.  
  
### <a name="after-maintenance-operations"></a>Nach Wartungsvorgängen  
 Die Aktualisierung von Statistiken empfiehlt sich auch nach dem Durchführen von Wartungsvorgängen, durch die die Verteilung der Daten geändert wird; hierzu gehören z. B. das Abschneiden einer Tabelle oder das Ausführen einer Masseneinfügung für einen großen Prozentsatz von Zeilen. Dadurch lassen sich zukünftige Verzögerungen bei der Abfrageverarbeitung vermeiden, d. h., Abfragen müssen nicht auf automatische Statistikupdates warten.  
  
 Vorgänge wie das Neuerstellen, Defragmentieren oder Neuorganisieren eines Indexes wirken sich nicht auf die Verteilung von Daten aus. Folglich müssen Sie keine Statistiken aktualisieren, nachdem Sie die Vorgänge [ALTER INDEX REBUILD](../../t-sql/statements/alter-index-transact-sql.md#rebuilding-indexes), [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md), [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) oder [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md#reorganizing-indexes) ausgeführt haben. Der Abfrageoptimierer aktualisiert Statistiken, wenn mit ALTER INDEX REBUILD oder DBCC DBREINDEX ein Index für eine Tabelle oder Sicht erstellt wird. Diese Statistikaktualisierung tritt jedoch als Nebenprodukt der Indexneuerstellung auf. Der Abfrageoptimierer führt nach einem DBCC INDEXDEFRAG-Vorgang oder ALTER INDEX REORGANIZE-Vorgang keine Statistikaktualisierung durch. 
 
> [!TIP]
> Verwenden Sie ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4 die PERSIST_SAMPLE_PERCENT-Option von [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) oder [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md), um einen bestimmten Prozentsatz für die Stichprobenentnahme für nachfolgende Statistikaktualisierungen festzulegen und beizubehalten, die einen solchen Prozentzsatz nicht explizit angeben.
  
##  <a name="DesignStatistics"></a> Abfragen mit effektiver Verwendung von Statistiken  
 Bestimmte Abfrageimplementierungen, z. B. lokale Variablen und komplexe Ausdrücke im Abfrageprädikat, können zu suboptimalen Abfrageplänen führen. Sie können dies verhindern, indem Sie Abfrageentwurfsrichtlinien für die effektive Verwendung von Statistiken befolgen. Weitere Informationen zu Abfrageprädikaten finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Zur Optimierung von Abfrageplänen können Sie Abfrageentwurfsrichtlinien anwenden, die Statistiken effektiv einsetzen, um *Kardinalitätsschätzungen* für Ausdrücke, Variablen und Funktionen in Abfrageprädikaten zu verbessern. Wenn der Abfrageoptimierer den Wert eines Ausdrucks, einer Variablen oder Funktion nicht kennt, weiß er nicht, welchen Wert er im Histogramm suchen soll. Folglich kann nicht die beste Kardinalitätsschätzung aus dem Histogramm abgerufen werden. Für alle als Stichprobe entnommenen Zeilen im Histogramm verwendet der Abfrageoptimierer stattdessen die durchschnittliche Anzahl von Zeilen pro eindeutigem Wert als Basis für die Kardinalitätsschätzung. Dies führt zu suboptimalen Kardinalitätsschätzungen und kann die Abfrageleistung beeinträchtigen. Weitere Informationen zu Histogrammen finden Sie im Abschnitt [Histogramm](#histogram) auf dieser Seite oder unter [sys.dm_db_stats_histogram](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md).
  
 In den folgenden Richtlinien wird beschrieben, wie Abfragen geschrieben werden müssen, um Abfragepläne durch optimierte Kardinalitätsschätzungen zu verbessern.  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>Verbessern der Kardinalitätsschätzung für Ausdrücke  
Um Kardinalitätsschätzungen für Ausdrücke zu verbessern, beachten Sie die folgenden Richtlinien:  
  
* Vereinfachen Sie nach Möglichkeit Ausdrücke, in denen Konstanten enthalten sind. Der Abfrageoptimierer wertet nicht alle Funktionen und Ausdrücke mit Konstanten aus, bevor er Kardinalitätsschätzungen ermittelt. Vereinfachen Sie z.B. den `ABS(-100)`-Ausdruck in `100`.  
  
* Wenn der Ausdruck mehrere Variablen verwendet, können Sie in Betracht ziehen, eine berechnete Spalte für den Ausdruck und dann Statistiken oder einen Index für die berechnete Spalte zu erstellen. Das Abfrageprädikat `WHERE PRICE + Tax > 100` könnte beispielsweise eine bessere Kardinalitätsschätzung aufweisen, wenn Sie eine berechnete Spalte für den Ausdruck `Price + Tax`erstellen.  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>Verbessern der Kardinalitätsschätzung für Variablen und Funktionen  
Um die Kardinalitätsschätzungen für Variablen und Funktionen zu verbessern, beachten Sie die folgenden Richtlinien:  
  
* Wenn das Abfrageprädikat eine lokale Variable verwendet, könnte das Umschreiben der Abfrage sinnvoll sein, sodass sie statt einer lokalen Variablen einen Parameter verwendet. Der Wert einer lokalen Variablen ist nicht bekannt, wenn der Abfrageoptimierer den Abfrageausführungsplan erstellt. Wenn eine Abfrage auf einem Parameter basiert, verwendet der Abfrageoptimierer die Kardinalitätsschätzung für den ersten tatsächlichen Parameterwert, der an die gespeicherte Prozedur übergeben wird.  
  
* Erwägen Sie die Verwendung einer Standardtabelle oder temporären Tabelle, in der die Ergebnisse der Tabellenwertfunktionen mit mehreren Anweisungen enthalten sind. Der Abfrageoptimierer erstellt keine Statistiken für Tabellenwertfunktionen mit mehreren Anweisungen. Bei diesem Ansatz kann der Abfrageoptimierer Statistiken für die Tabellenspalten erstellen und sie zum Optimieren der Abfragepläne nutzen.  
  
* Standardtabellen oder temporäre Tabelle können auch als Ersatz für Tabellenvariablen verwendet werden. Der Abfrageoptimierer erstellt keine Statistiken für Tabellenvariablen. Bei diesem Ansatz kann der Abfrageoptimierer Statistiken für die Tabellenspalten erstellen und sie zum Optimieren der Abfragepläne nutzen. Die Vorteile von temporären Tabellen und Tabellenvariablen müssen gegeneinander abgewogen werden. Tabellenvariablen, die in gespeicherten Prozeduren verwendet werden, verursachen weniger Neukompilierungen der gespeicherten Prozedur als temporäre Tabellen. Nicht bei allen Anwendungen wird die Leistung optimiert, wenn statt einer Tabellenvariablen eine temporäre Tabelle verwendet wird.  
  
* Wenn eine gespeicherte Prozedur eine Abfrage enthält, die einen übergebenen Parameter verwendet, sollten Sie den Parameterwert innerhalb der gespeicherten Prozedur nicht ändern, bevor Sie ihn in der Abfrage verwenden. Die Kardinalitätsschätzungen für die Abfrage basieren auf dem übergebenen Parameterwert und nicht auf dem aktualisierten Wert. Damit der Parameterwert nicht geändert werden kann, können Sie die Abfrage so umschreiben, dass zwei gespeicherte Prozeduren verwendet werden.  
  
     Durch die folgende gespeicherte Prozedur `Sales.GetRecentSales` wird beispielsweise der Wert des Parameters `@date` geändert, wenn `@date` auf NULL festgelegt ist.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date IS NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     Wenn der erste Aufruf der gespeicherten Prozedur `Sales.GetRecentSales` für den Parameter `@date` NULL übergibt, kompiliert der Abfrageoptimierer die gespeicherte Prozedur mit der Kardinalitätsschätzung für `@date = NULL`, obwohl das Abfrageprädikat nicht mit `@date = NULL`aufgerufen wird. Diese Kardinalitätsschätzung kann deutlich von der Anzahl der Zeilen im tatsächlichen Abfrageergebnis abweichen. Folglich könnte der Abfrageoptimierer einen suboptimalen Abfrageplan auswählen. Um dies zu vermeiden, können Sie die gespeicherte Prozedur wie folgt in zwei Prozeduren unterteilen:  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>Verbessern der Kardinalitätsschätzung mit Abfragehinweisen  
 Um Kardinalitätsschätzungen für lokale Variablen zu verbessern, können Sie den `OPTIMIZE FOR <value>`-Abfragehinweis oder den `OPTIMIZE FOR UNKNOWN`-Abfragehinweis mit RECOMPILE verwenden. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 Bei einigen Anwendungen könnte es zu lange dauern, die Abfrage bei jeder Ausführung neu zu kompilieren. Der `OPTIMIZE FOR`-Abfragehinweis kann selbst dann hilfreich sein, wenn Sie die `RECOMPILE`-Option nicht verwenden. Sie können der gespeicherten Prozedur „Sales.GetRecentSales“ z.B. eine `OPTIMIZE FOR`-Option hinzufügen, um ein bestimmtes Datum anzugeben. Im folgenden Beispiel wird der Prozedur „Sales.GetRecentSales“ `OPTIMIZE FOR`-Option hinzugefügt.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>Verbessern der Kardinalitätsschätzung mit Planhinweislisten  
 Für einige Anwendungen sind die Abfrageentwurfsrichtlinien möglicherweise nicht geeignet, weil Sie die Abfrage nicht ändern können oder die Verwendung des RECOMPILE-Abfragehinweises zu viele Neukompilierungen verursacht. Sie können mithilfe der Planhinweislisten weitere Hinweise (z. B. USE PLAN) angeben, um das Abfrageverhalten zu steuern. Zur gleichen Zeit können Sie mit dem Hersteller klären, ob die Anwendung geändert wurde. Weitere Informationen zu Planhinweislisten finden Sie unter [Planhinweislisten](../../relational-databases/performance/plan-guides.md).  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [Erstellen gefilterter Indizes](../../relational-databases/indexes/create-filtered-indexes.md)   
 [Steuern des Verhaltens des automatischen Statistikupdates (AUTO_UPDATE_STATISTICS) in SQL Server](http://support.microsoft.com/help/2754171)   
 [STATS_DATE (Transact-SQL)](../../t-sql/functions/stats-date-transact-sql.md)   
 [sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)  
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
 [sys.stats_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
