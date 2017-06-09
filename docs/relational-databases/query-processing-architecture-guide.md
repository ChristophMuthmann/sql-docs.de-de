---
title: Handbuch zur Architektur der Abfrageverarbeitung | Microsoft-Dokumentation
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, query processing architecture
- query processing architecture guide
ms.assetid: 44fadbee-b5fe-40c0-af8a-11a1eecf6cb5
caps.latest.revision: 5
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: ceddddafe0c052d0477e218955949012818e9a73
ms.openlocfilehash: bb13d94c5ef1eb36c3d50d3217f259a09c39e832
ms.contentlocale: de-de
ms.lasthandoff: 06/05/2017

---
# <a name="query-processing-architecture-guide"></a>Handbuch zur Architektur der Abfrageverarbeitung
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] verarbeitet Abfragen für verschiedene Datenspeicherungsarchitekturen, z. B. lokale Tabellen, partitionierte Tabellen und serverübergreifend verteilte Tabellen. In den folgenden Themen wird erläutert, wie mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Abfragen verarbeitet werden und die Wiederverwendung von Abfragen mithilfe des Zwischenspeicherns von Ausführungsplänen optimiert wird.

## <a name="sql-statement-processing"></a>Verarbeiten von SQL-Anweisungen

Die Verarbeitung einer einzelnen SQL-Anweisung ist das grundlegendste Verfahren, nach dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SQL-Anweisungen ausführt. Die Schritte, die zur Verarbeitung einer einzelnen `SELECT` -Anweisung verwendet werden, die nur auf lokale Basistabellen verweist (keine Sichten oder Remotetabellen), sollen das zugrunde liegende Verfahren veranschaulichen.

#### <a name="optimizing-select-statements"></a>Optimieren von SELECT-Anweisungen

Eine `SELECT` -Anweisung ist nicht prozedural; sie gibt nicht die genauen Schritte vor, die der Datenbankserver verwenden soll, um die angeforderten Daten abzurufen. Dies bedeutet, dass der Datenbankserver die Anweisung analysieren muss, um das effizienteste Verfahren zum Extrahieren der angeforderten Daten zu ermitteln. Dieser Vorgang wird als Optimieren der `SELECT` -Anweisung bezeichnet. Die Komponente, die ihn durchführt, wird als Abfrageoptimierer bezeichnet. Die Eingaben für den Abfrageoptimierer bestehen aus der Abfrage, dem Datenbankschema (Tabellen- und Indexdefinitionen) und den Datenbankstatistiken. Die Ausgabe des Abfrageoptimierers ist ein Abfrageausführungsplan, der manchmal auch als Abfrageplan oder einfach nur als Plan bezeichnet wird. Der Inhalt eines Abfrageplans wird ausführlicher an späterer Stelle in diesem Thema beschrieben.

Die Ein- und Ausgaben des Abfrageoptimierers während der Optimierung einer einzelnen `SELECT`-Anweisung werden in der folgenden Abbildung gezeigt: ![query_processor_io](../relational-databases/media/query-processor-io.gif)

Eine `SELECT` -Anweisung definiert lediglich Folgendes:  
* Das Format des Resultsets. Dieses wird meistens in der Auswahlliste angegeben. Das endgültige Format des Resultsets wird jedoch auch von anderen Klauseln, wie z.B. `ORDER BY` und `GROUP BY` , beeinflusst.
* Die Tabellen, die die Quelldaten enthalten. Dies wird in der `FROM` -Klausel angegeben.
* Die logischen Beziehungen zwischen den Tabellen, die im Rahmen der `SELECT` -Anweisung relevant sind. Diese werden in den Joinspezifikationen definiert, die in der `WHERE` -Klausel oder in einer `ON` -Klausel, die auf `FROM`folgt, auftreten können.
* Die Bedingungen, die die Zeilen in den Quelltabellen erfüllen müssen, um für die `SELECT` -Anweisung qualifiziert zu sein. Diese werden in den `WHERE` - und `HAVING` -Klauseln angegeben.


In einem Abfrageausführungsplan wird Folgendes definiert: 

* Die Reihenfolge des Zugriffs auf die Quelltabellen.  
  In der Regel gibt es viele Abfolgen, in denen der Datenbankserver auf die Basistabellen zugreifen kann, um das Resultset zu erstellen. Wenn die `SELECT` -Anweisung z.B. auf drei Tabellen verweist, könnte der Datenbankserver zuerst auf `TableA`zugreifen, dann die Daten aus `TableA` verwenden, um die entsprechenden Zeilen aus `TableB`zu extrahieren, und dann die Daten aus `TableB` verwenden, um Daten aus `TableC`zu extrahieren. Die anderen Abfolgen, in denen der Datenbankserver auf die Tabellen zugreifen kann, lauten:  
  `TableC`, `TableB`, `TableA`oder  
  `TableB`, `TableA`, `TableC`oder  
  `TableB`, `TableC`, `TableA`oder  
  `TableC`, `TableA`, `TableB`  

* Die Methoden, die verwendet werden, um Daten aus den einzelnen Tabellen zu extrahieren.  
  Für den Zugriff auf die Daten in den einzelnen Tabellen gibt es in der Regel unterschiedliche Methoden. Wenn nur wenige Zeilen mit bestimmten Schlüsselwerten erforderlich sind, kann der Datenbankserver einen Index verwenden. Wenn alle Zeilen der Tabelle erforderlich sind, kann der Datenbankserver die Indizes übergehen und einen Tabellenscan ausführen. Wenn alle Zeilen einer Tabelle erforderlich sind, die Tabelle jedoch über einen Index verfügt, dessen Schlüsselspalten in einer `ORDER BY`-Klausel verwendet werden, kann durch die Durchführung eines Indexscans anstelle eines Tabellenscans eine andere Sortierung des Resultsets gespeichert werden. Wenn es sich um eine sehr kleine Tabelle handelt, können Tabellenscans die effizienteste Methode für fast alle Zugriffe auf die Tabelle darstellen.

Der Vorgang, in dessen Verlauf ein bestimmter Ausführungsplan aus einer Anzahl möglicher Ausführungspläne ausgewählt wird, wird Optimierung genannt. Der Abfrageoptimierer stellt eine der wichtigsten Komponenten eines SQL-Datenbanksystems dar. Der Abfrageoptimierer erzeugt zwar den zusätzlichen Aufwand, um die Abfrage analysieren und einen Plan auswählen zu können, ein Vielfaches dieses Aufwands wird jedoch normalerweise dadurch eingespart, dass der Abfrageoptimierer einen effizienten Ausführungsplan auswählt. Nehmen Sie z. B. an, zwei Bauunternehmer erhalten dieselben Konstruktionszeichnungen für ein Haus. Wenn nun das eine Unternehmen zunächst einige Tage darauf verwendet, den Bau des Hauses detailliert zu planen, das andere Unternehmen jedoch sofort und ohne weitere Planung mit dem Bau des Hauses beginnt, ist es mehr als wahrscheinlich, dass das erste Unternehmen, das sich Zeit für die Planung des Projekts nimmt, den Bau des Hauses zuerst abschließen wird.

Der Abfrageoptimierer von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] arbeitet kostenorientiert. Jeder denkbare Ausführungsplan verfügt über zugeordnete Kosten hinsichtlich des Umfangs der benötigten Verarbeitungsressourcen. Der Abfrageoptimierer muss die möglichen Pläne analysieren und den Plan auswählen, der die geringsten geschätzten Kosten verursacht. Einige komplexe `SELECT` -Anweisungen verfügen über mehrere Tausend mögliche Ausführungspläne. In einem solchen Fall werden nicht alle denkbaren Kombinationen vom Abfrageoptimierer analysiert. Stattdessen werden komplexe Algorithmen verwendet, um einen Ausführungsplan zu ermitteln, dessen Kosten sich in vernünftigem Rahmen an die möglichen Mindestkosten annähern.

Der Abfrageoptimierer von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wählt nicht nur den Ausführungsplan aus, der die geringsten Kosten bezüglich der benötigten Ressourcen verursacht. Stattdessen wird der Plan ausgewählt, der die Ergebnisse so schnell wie möglich an den Benutzer zurückgibt und dabei Kosten für Ressourcen in vertretbarem Maß verursacht. Für die parallele Verarbeitung einer Abfrage werden in der Regel mehr Ressourcen verwendet als für die serielle Verarbeitung, die Abfrageausführung wird jedoch schneller beendet. Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer verwendet einen Plan mit paralleler Ausführung, um Ergebnisse zurückzugeben, wenn sich dies nicht negativ auf die Serverlast auswirkt.

Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer stützt sich bei der Schätzung der Ressourcenkosten, die durch unterschiedliche Methoden zum Extrahieren von Informationen aus einer Tabelle oder einem Index verursacht werden, auf Verteilungsstatistiken. Die Verteilungsstatistiken werden für Spalten und Indizes erstellt. Sie kennzeichnen die Selektivität der Werte in einem bestimmten Index oder einer bestimmten Spalte. In einer Tabelle für Autos stammen z. B. viele Autos von demselben Hersteller, jedes Auto verfügt jedoch über eine eindeutige Fahrzeugnummer. Ein Index, der die Fahrzeugnummer verwendet, weist eine höhere Selektivität auf als ein Index, der den Hersteller einsetzt. Wenn die Indexstatistiken nicht auf dem aktuellen Stand sind, wählt der Abfrageoptimierer möglicherweise nicht den Plan aus, der für den aktuellen Status der Tabelle am besten geeignet ist. Weitere Informationen zur Aktualisierung von Indexstatistiken finden Sie unter „Verwenden von Statistiken zum Verbessern der Abfrageleistung“. 

Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer ist deshalb so wichtig, weil er es dem Datenbankserver ermöglicht, dynamische Anpassungen an geänderte Bedingungen in der Datenbank vorzunehmen, ohne dass eine Eingabe durch einen Programmierer oder Datenbankadministrator erforderlich ist. Programmierer können sich somit darauf konzentrieren, das endgültige Ergebnis der Abfrage zu beschreiben. Sie können sich darauf verlassen, dass der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer bei jeder Ausführung der Anweisung einen effizienten Ausführungsplan auf der Basis des aktuellen Status der Datenbank erstellt.

#### <a name="processing-a-select-statement"></a>Verarbeiten einer SELECT-Anweisung

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] führt zur Verarbeitung einer einzelnen SELECT-Anweisung die folgenden grundlegenden Schritte aus: 

1. Der Parser scannt die `SELECT` -Anweisung und spaltet sie in ihre logischen Einheiten auf, wie z.B. Schlüsselwörter, Ausdrücke, Operatoren und Bezeichner.
2. Eine Abfragestruktur, manchmal auch Sequenzstruktur genannt, wird erstellt, die die logischen Schritte beschreibt, die für die Transformation der Quelldaten in das für das Resultset benötigte Format erforderlich sind.
3. Der Abfrageoptimierer analysiert verschiedene Arten des Zugriffs auf die Quelltabellen. Anschließend wählt er die Reihenfolge der Schritte aus, mit denen die Ergebnisse am schnellsten mithilfe möglichst weniger Ressourcen zurückgegeben werden. Die Abfragestruktur wird aktualisiert, um diese genaue Reihenfolge von Schritten aufzuzeichnen. Die endgültige, optimierte Version der Abfragestruktur wird als Ausführungsplan bezeichnet.
4. Das relationale Modul beginnt mit der Ausführung des Ausführungsplans. Während der Verarbeitung von Schritten, für die Daten aus den Basistabellen erforderlich sind, fordert das relationale Modul an, dass das Speichermodul die Daten aus den Rowsets übergibt, die durch das relationale Modul angefordert wurden.
5. Das relationale Modul transformiert die Daten, die von dem Speichermodul zurückgegeben werden, in das für das Resultset definierte Format und gibt das Resultset an den Client zurück.

#### <a name="processing-other-statements"></a>Verarbeiten anderer Anweisungen

Die zuvor beschriebenen grundlegenden Schritte für die Verarbeitung einer `SELECT` -Anweisung gelten ebenfalls für andere SQL-Anweisungen, wie z.B. `INSERT`, `UPDATE`und `DELETE`. `UPDATE` - und `DELETE` -Anweisungen müssen sich auf die Gruppe von Zeilen beziehen, die geändert bzw. gelöscht werden soll. Der Vorgang zum Identifizieren dieser Zeilen ist der gleiche Vorgang, der zum Identifizieren der Quellzeilen verwendet wird, die einen Beitrag zum Resultset einer `SELECT` -Anweisung leisten. `UPDATE` - und `INSERT` -Anweisungen können eingebettete SELECT-Anweisungen enthalten, die die Datenwerte bereitstellen, die aktualisiert oder eingefügt werden sollen.

Sogar DDL-Anweisungen (Data Definition Language, Datendefinitionssprache), wie z.B. `CREATE PROCEDURE` oder `ALTER TABL`E, werden letztendlich in eine Folge relationaler Operationen aufgelöst, die für die Systemkatalogtabellen und manchmal (wie bei `ALTER TABLE ADD COLUMN`) auch für die Datentabellen ausgeführt werden.

### <a name="worktables"></a>Arbeitstabellen

Um eine logische Operation ausführen zu können, die in einer SQL-Anweisung angegeben wurde, muss das relationale Modul ggf. eine Arbeitstabelle erstellen. Arbeitstabellen sind interne Tabellen, die zum Speichern von Zwischenergebnissen verwendet werden. Arbeitstabellen werden für bestimmte `GROUP BY`-, `ORDER BY`- oder `UNION` -Abfragen generiert. Wenn z.B. eine `ORDER BY` -Klausel auf Spalten verweist, die nicht durch Indizes erfasst werden, muss das relationale Modul eventuell eine Arbeitstabelle generieren, um das Resultset in der angeforderten Reihenfolge sortieren zu können. Arbeitstabellen werden mitunter auch als Spool-Speicher verwendet, die vorübergehend das Ergebnis der Ausführung eines Teils eines Abfrageplans aufnehmen. Arbeitstabellen werden in `tempdb` erstellt und automatisch wieder gelöscht, sobald sie nicht mehr benötigt werden.

### <a name="view-resolution"></a>Sichtauflösung

Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageprozessor behandelt indizierte und nicht indizierte Sichten unterschiedlich: 

* Die Zeilen einer indizierten Sicht werden in der Datenbank in demselben Format wie eine Tabelle gespeichert. Wenn sich der Abfrageoptimierer entscheidet, eine indizierte Sicht in einem Abfrageplan zu verwenden, wird die indizierte Sicht auf die gleiche Weise wie eine Basistabelle behandelt.
* Nur die Definition einer nicht indizierten Sicht wird gespeichert, nicht die Zeilen der Sicht. Der Abfrageoptimierer nimmt die Logik aus der Sichtdefinition in den Ausführungsplan auf, den er für die SQL-Anweisung erstellt, die auf die nicht indizierte Sicht verweist. 

Die Logik, anhand derer der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer entscheidet, wann eine indizierte Sicht verwendet werden soll, ist mit der Logik vergleichbar, anhand derer ermittelt wird, wann ein Index für eine Tabelle verwendet wird. Wenn die Daten in der indizierten Sicht die gesamte oder einen Teil der SQL-Anweisung erfüllen und der Abfrageoptimierer ermittelt, dass ein Index für die Sicht der Zugriffspfad mit den geringsten Kosten ist, wählt der Abfrageoptimierer den Index unabhängig davon aus, ob im Namen der Abfrage auf die Sicht verwiesen wird.

Wenn eine SQL-Anweisung auf eine nicht indizierte Sicht verweist, analysieren der Parser und der Abfrageoptimierer die Quelle sowohl der SQL-Anweisung als auch der Sicht und lösen sie dann zu einem einzigen Ausführungsplan auf. Es gibt nicht einen Plan für die SQL-Anweisung und einen weiteren Plan für die Sicht.

Nehmen Sie z. B. an, dass die folgende Sicht verwendet wird:

```tsql
USE AdventureWorks2014;
GO
CREATE VIEW EmployeeName AS
SELECT h.BusinessEntityID, p.LastName, p.FirstName
FROM HumanResources.Employee AS h 
JOIN Person.Person AS p
ON h.BusinessEntityID = p.BusinessEntityID;
GO
```

Von dieser Sicht ausgehend führen die beiden folgenden SQL-Anweisungen die gleichen Vorgänge für die Basistabellen aus und erzeugen identische Ergebnisse:

```tsql
/* SELECT referencing the EmployeeName view. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.Sales.SalesOrderHeader AS soh
JOIN AdventureWorks2014.dbo.EmployeeName AS EmpN
ON (soh.SalesPersonID = EmpN.BusinessEntityID)
WHERE OrderDate > '20020531';

/* SELECT referencing the Person and Employee tables directly. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.HumanResources.Employee AS e 
JOIN AdventureWorks2014.Sales.SalesOrderHeader AS soh
ON soh.SalesPersonID = e.BusinessEntityID
JOIN AdventureWorks2014.Person.Person AS p
ON e.BusinessEntityID =p.BusinessEntityID
WHERE OrderDate > '20020531';
```

Durch die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio-Showplanfunktion wird deutlich, dass das relationale Modul für beide `SELECT`-Anweisungen denselben Ausführungsplan erstellt.

#### <a name="using-hints-with-views"></a>Verwenden von Hinweisen mit Sichten

Hinweise, die für Sichten in einer Abfrage gespeichert werden, können zu Konflikten mit anderen Hinweisen führen, die beim Erweitern der Sicht für den Zugriff auf ihre Basistabellen erkannt werden. Wenn das passiert, gibt die Abfrage einen Fehler zurück. Angenommen, die folgende Sicht enthält einen Tabellenhinweis in ihrer Definition:

```tsql
USE AdventureWorks2014;
GO
CREATE VIEW Person.AddrState WITH SCHEMABINDING AS
SELECT a.AddressID, a.AddressLine1, 
    s.StateProvinceCode, s.CountryRegionCode
FROM Person.Address a WITH (NOLOCK), Person.StateProvince s
WHERE a.StateProvinceID = s.StateProvinceID;
```

Nehmen Sie nun an, dass die folgende Abfrage eingegeben wird:

```tsql
SELECT AddressID, AddressLine1, StateProvinceCode, CountryRegionCode
FROM Person.AddrState WITH (SERIALIZABLE)
WHERE StateProvinceCode = 'WA';
```

Die Abfrage erzeugt einen Fehler, weil der `SERIALIZABLE` -Hinweis, der für die `Person.AddrState` -Sicht in der Abfrage angewendet wird, an die beiden Tabellen `Person.Address` und `Person.StateProvince` in der Sicht weitergegeben wird, wenn diese erweitert wird. Das Erweitern der Sicht legt jedoch außerdem den `NOLOCK` -Hinweis für `Person.Address`offen. Da die `SERIALIZABLE` - und `NOLOCK` -Hinweise einen Konflikt verursachen, ist die sich ergebende Abfrage falsch. 

Die `PAGLOCK`-, `NOLOCK`-, `ROWLOCK`-, `TABLOCK`- oder `TABLOCKX` -Tabellenhinweise verursachen Konflikte miteinander, genau wie die `HOLDLOCK`-, `NOLOCK`-, `READCOMMITTED`-, `REPEATABLEREAD`-, `SERIALIZABLE` -Tabellenhinweise.

Hinweise können über die Ebenen geschachtelter Sichten weitergegeben werden. Angenommen, eine Abfrage wendet den `HOLDLOCK` -Hinweis auf eine `v1`-Sicht an. Wenn `v1` erweitert wird, wird erkennbar, dass die Sicht `v2` Teil ihrer Definition ist. Die Definition von`v2`enthält einen `NOLOCK` -Hinweis für eine der Basistabellen der Sicht. Diese Tabelle erbt jedoch außerdem den `HOLDLOCK` -Hinweis für die Sicht `v1`von der Abfrage. Da die `NOLOCK` - und `HOLDLOCK` -Hinweise einen Konflikt verursachen, führt die Abfrage zu einem Fehler.

Wenn der `FORCE ORDER` -Hinweis in einer Abfrage verwendet wird, die eine Sicht enthält, wird die Joinreihenfolge der Tabellen innerhalb der Sicht durch die Position der Sicht im sortierten Konstrukt festgelegt. Die folgende Abfrage trifft z. B. eine Auswahl aus drei Tabellen und einer Sicht:

```tsql
SELECT * FROM Table1, Table2, View1, Table3
WHERE Table1.Col1 = Table2.Col1 
    AND Table2.Col1 = View1.Col1
    AND View1.Col2 = Table3.Col2;
OPTION (FORCE ORDER);
```

Außerdem ist `View1` wie im folgenden Beispiel gezeigt definiert:

```tsql
CREATE VIEW View1 AS
SELECT Colx, Coly FROM TableA, TableB
WHERE TableA.ColZ = TableB.Colz;
```

Die Joinreihenfolge im Abfrageplan lautet `Table1`, `Table2`, `TableA`, `TableB`, `Table3`.

### <a name="resolving-indexes-on-views"></a>Auflösen von Indizes für Sichten

Wie bei jedem Index entscheidet sich [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nur dann für die Verwendung einer indizierten Sicht in seinem Abfrageplan, wenn der Abfrageoptimierer feststellt, dass dies vorteilhaft ist.

Indizierte Sichten können in jeder Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erstellt werden. In einigen Editionen einiger Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] berücksichtigt der Abfrageoptimierer die indizierte Sicht automatisch. In einigen Editionen einiger Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muss der `NOEXPAND`-Tabellenhinweis verwendet werden, um eine indizierte Sicht zu verwenden. Erläuterungen finden Sie in der Dokumentation der Versionen.

Der Abfrageoptimierer von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet eine indizierte Sicht, wenn die folgenden Bedingungen erfüllt sind: 

* Die folgenden Sitzungsoptionen sind auf `ON`festgelegt: 
  * `ANSI_NULLS`
  * `ANSI_PADDING`
  * `ANSI_WARNINGS`
  * `ARITHABORT`
  * `CONCAT_NULL_YIELDS_NULL`
  * `QUOTED_IDENTIFIER` 
  * Die `NUMERIC_ROUNDABORT` -Sitzungsoption ist auf OFF festgelegt.
* Der Abfrageoptimierer findet eine Übereinstimmung zwischen den Indexspalten der Sicht und Abfrageelementen, wie z.B.: 
  * Suchbedingungsprädikate in der WHERE-Klausel
  * Joinvorgänge
  * Aggregatfunktionen
  * `GROUP BY` -Klauseln
  * Tabellenverweise
* Die geschätzten Kosten für das Verwenden des Indexes sind die niedrigsten Kosten aller durch den Abfrageoptimierer berücksichtigten Zugriffsmechanismen. 
* Für jede Tabelle, auf die in der Abfrage verwiesen wird (entweder direkt oder durch Erweitern einer Sicht zum Zugriff auf die zugrunde liegenden Tabellen), die einem Tabellenverweis in der indizierten Sicht entspricht, muss derselbe Satz von Hinweisen in der Abfrage angewendet werden.

> [!NOTE] 
> Die `READCOMMITTED` - und `READCOMMITTEDLOCK` -Hinweise werden in diesem Kontext immer als unterschiedliche Hinweise angesehen, unabhängig von der aktuellen Transaktionsisolationsstufe.
 
Abweichend von den Anforderungen für die `SET`-Optionen und Tabellenhinweise verwendet der Abfrageoptimierer hier dieselben Regeln, mit denen er ermittelt, ob ein Tabellenindex eine Abfrage erfüllt. In der zu verwendenden Abfrage für eine indizierte Sicht muss nichts weiter angegeben werden.

Eine Abfrage muss nicht explizit in der `FROM`-Klausel auf eine indizierte Sicht verweisen, damit der Abfrageoptimierer die indizierte Sicht verwendet. Falls die Abfrage Verweise auf Spalten in den Basistabellen enthält, die auch in der indizierten Sicht vorhanden sind, und der Abfrageoptimierer schätzt, dass das Verwenden der indizierten Sicht den kostengünstigsten Zugriffsmechanismus darstellt, wählt der Abfrageoptimierer die indizierte Sicht aus. Die Vorgehensweise ist dabei ähnlich wie bei der Auswahl von Basistabellenindizes, wenn in einer Abfrage nicht direkt auf diese verwiesen wird. Der Abfrageoptimierer kann die Sicht auswählen, wenn sie Spalten enthält, auf die die Abfrage nicht verweist, vorausgesetzt die Sicht bietet die kostengünstigste Möglichkeit zum Abdecken einer oder mehrerer Spalten, die in der Abfrage angegeben sind.

Der Abfrageoptimierer behandelt eine indizierte Sicht, auf die in der `FROM`-Klausel verwiesen wird, als Standardsicht. Der Abfrageoptimierer erweitert am Beginn des Optimierungsprozesses die Definition der Sicht in die Abfrage. Dann erfolgt der Abgleich der indizierten Sicht. Die indizierte Sicht kann im endgültigen Ausführungsplan verwendet werden, der vom Abfrageoptimierer ausgewählt wird, oder stattdessen kann der Plan die erforderlichen Daten aus der Sicht materialisieren, indem auf die Basistabellen zugegriffen wird, auf die durch die Sicht verwiesen wird. Der Abfrageoptimierer wählt die kostengünstigste Alternative aus.

#### <a name="using-hints-with-indexed-views"></a>Verwenden von Hinweisen mit indizierten Sichten

Sie können verhindern, dass Sichtindizes für eine Abfrage verwendet werden, indem Sie den `EXPAND VIEWS` -Abfragehinweis verwenden oder indem Sie mit dem `NOEXPAND` -Tabellenhinweis die Verwendung eines Indexes für eine indizierte Sicht erzwingen, die in der `FROM` -Klausel einer Abfrage angegeben ist. Sie sollten jedoch den Abfrageoptimierer für jede Abfrage dynamisch ermitteln lassen, welches die besten Zugriffsmethoden sind. Verwenden Sie `EXPAND` und `NOEXPAND` nur in bestimmten Fällen, wenn Tests gezeigt haben, dass durch sie die Leistung deutlich gesteigert wird.

Die Option `EXPAND VIEWS` gibt an, dass der Abfrageoptimierer für die gesamte Abfrage keine Sichtindizes verwendet. 

Wenn `NOEXPAND` für eine Sicht angegeben wird, zieht der Abfrageoptimierer die Verwendung sämtlicher Indizes in Erwägung, die für die Sicht definiert sind. `NOEXPAND` mit der optionalen `INDEX()`-Klausel zwingt den Abfrageoptimierer, die angegebenen Indizes zu verwenden. `NOEXPAND` kann nur für eine indizierte Sicht angegeben werden, nicht für eine nicht indizierte Sicht.

Wenn weder `NOEXPAND` noch `EXPAND VIEWS` in einer Abfrage angegeben ist, die eine Sicht enthält, wird die Sicht erweitert, um auf die zugrunde liegenden Tabellen zuzugreifen. Wenn die Abfrage, die die Sicht bildet, irgendwelche Tabellenhinweise enthält, werden diese Hinweise auch an die zugrunde liegenden Tabellen weitergegeben. (Detaillierte Informationen zu diesem Vorgang finden Sie unter „Sichtauflösung“.) Solange die der Sicht zugrunde liegenden Tabellen identische Sätze von Hinweisen besitzen, kommt die Abfrage für den Abgleich mit einer indizierten Sicht infrage. Zumeist stimmen diese Hinweise miteinander überein, da sie direkt aus der Sicht vererbt werden. Wenn die Abfrage jedoch auf Tabellen und nicht auf Sichten verweist und die direkt auf diese Tabellen angewendeten Hinweise nicht identisch sind, so kommt eine solche Abfrage nicht für den Abgleich mit einer indizierten Sicht infrage. Wenn die Hinweise `INDEX`, `PAGLOCK`, `ROWLOCK`, `TABLOCKX`, `UPDLOCK`oder `XLOCK` auf die Tabellen angewendet werden, auf die die Abfrage nach der Sichterweiterung verweist, kommt die Abfrage nicht für den Abgleich mit einer indizierten Sicht infrage.

Wenn ein Tabellenhinweis in Form von `INDEX (index_val[ ,...n] )` auf eine Sicht in einer Abfrage verweist und Sie nicht gleichzeitig den `NOEXPAND` -Hinweis angeben, wird der Indexhinweis ignoriert. Zum Angeben eines bestimmten Indexes verwenden Sie `NOEXPAND`. 

Allgemein gilt: Wenn der Abfrageoptimierer eine indizierte Sicht mit einer Abfrage abgleicht, werden alle für die Tabellen oder Sichten in der Abfrage angegebenen Hinweise direkt auf die indizierte Sicht angewendet. Wenn der Abfrageoptimierer sich entscheidet, keine indizierte Sicht zu verwenden, werden alle Hinweise direkt zu den Tabellen weitergegeben, auf die in der Sicht verwiesen wird. Weitere Informationen finden Sie unter „Sichtauflösung“. Diese Weitergabe gilt nicht für die Joinhinweise. Diese werden ausschließlich an ihrer ursprünglichen Position in der Abfrage angewendet. Joinhinweise werden vom Abfrageoptimierer beim Abgleich von Abfragen zu indizierten Sichten nicht berücksichtigt. Wenn ein Abfrageplan eine indizierte Sicht verwendet, die mit einem Teil einer Abfrage übereinstimmt, der einen Joinhinweis enthält, wird der Joinhinweis im Plan nicht verwendet.

In den Definitionen von indizierten Sichten sind Hinweise nicht zulässig. In den Kompatibilitätsmodi 80 und höher ignoriert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die in den Definitionen indizierter Sichten enthaltenen Hinweise, wenn diese verwaltet werden oder wenn Abfragen ausgeführt werden, in denen indizierte Sichten verwendet werden. Obwohl die Verwendung von Hinweisen in den Definitionen indizierter Sichten im Kompatibilitätsmodus 80 nicht zu einem Syntaxfehler führt, werden sie ignoriert.

### <a name="resolving-distributed-partitioned-views"></a>Auflösen verteilter partitionierter Sichten

Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageprozessor optimiert die Leistung von verteilten partitionierten Sichten. Der wichtigste Aspekt bei der Leistung von verteilten partitionierten Sichten ist das Minimieren der Datenmenge, die zwischen den Mitgliedsservern übertragen wird.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erstellt intelligente, dynamische Pläne, in denen verteilte Abfragen effizient für den Zugriff auf Daten in Remotemitgliedstabellen verwendet werden: 

* Zunächst verwendet der Abfrageprozessor OLE DB, um die Definitionen der CHECK-Einschränkungen aus jeder Mitgliedstabelle abzurufen. Dadurch kann der Abfrageprozessor die Verteilung der Schlüsselwerte auf die Mitgliedstabellen zuordnen.
* Der Abfrageprozessor vergleicht die in der `WHERE`-Klausel einer SQL-Anweisung angegebenen Schlüsselbereiche mit der Zuordnung, die die Verteilung der Zeilen in den Mitgliedstabellen anzeigt. Anschließend erstellt der Abfrageprozessor einen Abfrageausführungsplan, der mithilfe von verteilten Abfragen nur die Remotezeilen abruft, die zum Ausführen der SQL-Anweisung erforderlich sind. Darüber hinaus wird der Ausführungsplan so erstellt, dass alle Zugriffe auf Remotemitgliedstabellen, entweder für Daten oder Metadaten, so lange verzögert werden, bis die Informationen benötigt werden.

Stellen Sie sich z.B. ein System vor, in dem eine Kundentabelle über Server1 (`CustomerID` von 1 bis 3299999), Server2 (`CustomerID` von 3300000 bis 6599999) und Server3 (`CustomerID` von 6600000 bis 9999999) partitioniert ist.

Stellen Sie sich den Ausführungsplan vor, der für diese auf Server1 ausgeführte Abfrage erstellt wird:

```tsql
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID BETWEEN 3200000 AND 3400000;
```

Der Ausführungsplan für diese Abfrage extrahiert die Zeilen mit `CustomerID` -Schlüsselwerten von 3200000 bis 3299999 aus der lokalen Mitgliedstabelle und gibt eine verteilte Abfrage aus, um die Zeilen mit Schlüsselwerten von 3300000 bis 3400000 von Server2 abzurufen.

Der Abfrageprozessor von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann zudem eine dynamische Logik in die Abfrageausführungspläne für SQL-Anweisungen integrieren, bei denen die Schlüsselwerte nicht bekannt sind, wenn der Plan erstellt werden muss. Sehen Sie sich z.B. diese gespeicherte Prozedur an:

```tsql
CREATE PROCEDURE GetCustomer @CustomerIDParameter INT
AS
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID = @CustomerIDParameter;
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann nicht vorhersagen, welcher Schlüsselwert jeweils bei der Ausführung der Prozedur durch den `@CustomerIDParameter`-Parameter zurückgegeben wird. Da der Schlüsselwert nicht vorhergesagt werden kann, kann der Abfrageprozessor auch nicht vorhersagen, auf welche Mitgliedstabelle zugegriffen werden muss. Wegen dieses Aspekts erstellt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] einen Ausführungsplan mit Bedingungslogik (so genannte dynamische Filter), um zu steuern, auf welche Mitgliedstabelle basierend auf den Eingabeparameterwerten zugegriffen wird. Angenommen die gespeicherte Prozedur `GetCustomer` wurde für Server1 ausgeführt, dann kann die Logik des Ausführungsplans wie folgt dargestellt werden:

```tsql
IF @CustomerIDParameter BETWEEN 1 and 3299999
   Retrieve row from local table CustomerData.dbo.Customer_33
ELSE IF @CustomerIDParameter BETWEEN 3300000 and 6599999
   Retrieve row from linked table Server2.CustomerData.dbo.Customer_66
ELSE IF @CustomerIDParameter BETWEEN 6600000 and 9999999
   Retrieve row from linked table Server3.CustomerData.dbo.Customer_99
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erstellt diese dynamischen Ausführungspläne manchmal sogar für nicht parametrisierte Abfragen. Der Abfrageoptimierer kann eine Abfrage parametrisieren, sodass der Ausführungsplan wieder verwendet werden kann. Falls der Abfrageoptimierer eine Abfrage parametrisiert, die auf eine partitionierte Sicht verweist, kann der Abfrageoptimierer nicht mehr davon ausgehen, dass die erforderlichen Zeilen aus einer bestimmten Basistabelle stammen. In diesem Fall muss der Optimierer dynamische Filter im Ausführungsplan verwenden.

## <a name="stored-procedure-and-trigger-execution"></a>Ausführung von gespeicherten Prozeduren und Triggern

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] speichert nur die Quelle für gespeicherte Prozeduren und Trigger. Wenn eine gespeicherte Prozedur oder ein Trigger das erste Mal ausgeführt wird, wird die Quelle zu einem Ausführungsplan kompiliert. Wenn die gespeicherte Prozedur oder der Trigger erneut ausgeführt wird, bevor der Ausführungsplan aus dem Arbeitsspeicher entfernt wurde, erkennt das relationale Modul den vorhandenen Plan und verwendet ihn erneut. Wenn der Plan aus dem Arbeitsspeicher entfernt wurde, wird ein neuer Plan erstellt. Dieser Vorgang ist mit dem Verfahren vergleichbar, das [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für alle SQL-Anweisungen anwendet. Der wesentliche Leistungsvorteil, den gespeicherte Prozeduren und Trigger in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] im Vergleich zu Batch- oder dynamischem SQL besitzen, besteht darin, dass ihre SQL-Anweisungen immer identisch sind. Aus diesem Grund können sie durch das relationale Modul auf einfache Weise vorhandenen Ausführungsplänen zugeordnet werden. Pläne für gespeicherte Prozeduren und Trigger können einfach erneut verwendet werden.

Der Ausführungsplan für gespeicherte Prozeduren und Trigger wird getrennt von dem Ausführungsplan für den Batch ausgeführt, der die gespeicherte Prozedur aufruft oder den Trigger auslöst. Dadurch können die Ausführungspläne für gespeicherte Prozeduren und Trigger mehrmals erneut verwendet werden.

## <a name="execution-plan-caching-and-reuse"></a>Zwischenspeichern und Wiederverwenden von Ausführungsplänen

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verfügt über einen Arbeitsspeicherpool, der zum Speichern von Ausführungsplänen und von Datenpuffern verwendet wird. Der Prozentsatz des Pools, der entweder für Ausführungspläne oder für Datenpuffer zugeordnet wird, verändert sich dynamisch in Abhängigkeit vom Status des Systems. Der Teil des Arbeitsspeicherpools, der zum Speichern von Ausführungsplänen verwendet wird, wird Plancache genannt.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Ausführungspläne weisen die folgenden Hauptkomponenten auf: 

* Abfrageausführungsplan: Bei dem größten Teil des Ausführungsplans handelt es sich um eine eintrittsinvariante, schreibgeschützte Datenstruktur, die von einer beliebigen Anzahl von Benutzern verwendet werden kann. Man bezeichnet diesen Teil als Abfrageplan. Im Abfrageplan wird kein Benutzerkontext gespeichert. Im Arbeitsspeicher befinden sich immer nur eine oder zwei Kopien des Abfrageplans: eine Kopie für alle seriellen Ausführungen und eine weitere für alle parallelen Ausführungen. Die parallele Kopie deckt alle parallelen Ausführungen ab, und zwar unabhängig von ihrem Grad an Parallelität. 
* Ausführungskontext: Jeder Benutzer, der die Abfrage zurzeit ausführt, verfügt über eine Datenstruktur mit den Daten, die für diese Ausführung spezifisch sind, z.B. Parameterwerte. Diese Datenstruktur wird als Ausführungskontext bezeichnet. Die Datenstrukturen des Ausführungskontexts werden wiederverwendet. Wenn ein Benutzer eine Abfrage ausführt und eine der Strukturen nicht verwendet wird, wird diese Struktur erneut initialisiert, und zwar diesmal mit dem Kontext für den neuen Benutzer. 

![execution_context](../relational-databases/media/execution-context.gif)

Wenn eine SQL-Anweisung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird, durchsucht das relationale Modul zunächst den Plancache, um zu überprüfen, ob ein vorhandener Ausführungsplan für die SQL-Anweisung vorhanden ist. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet sämtliche vorhandenen Pläne, die hierbei gefunden werden, wieder und spart somit den Aufwand für das erneute Kompilieren der SQL-Anweisung ein. Wenn kein Ausführungsplan vorhanden ist, generiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] einen neuen Ausführungsplan für die Abfrage.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet einen effizienten Algorithmus, um vorhandene Ausführungspläne für bestimmte SQL-Anweisungen zu suchen. In den meisten Systemen können durch das erneute Verwenden vorhandener Pläne anstelle des erneuten Kompilierens jeder SQL-Anweisung mehr Ressourcen eingespart werden, als für den Scan nach vorhandenen Plänen benötigt werden.

Die Algorithmen, die SQL-Anweisungen mit vorhandenen, nicht verwendeten Ausführungsplänen im Cache vergleichen, erfordern, dass alle Objektverweise vollqualifiziert sind. Die erste der folgenden `SELECT` -Anweisungen wird z. B. nicht mit vorhandenen Plänen verglichen. Für die zweite Anweisung wird jedoch ein Vergleich vorgenommen:

```tsql
SELECT * FROM Person;

SELECT * FROM Person.Person;
```

### <a name="removing-execution-plans-from-the-plan-cache"></a>Entfernen von Ausführungsplänen aus dem Plancache

Ausführungspläne verbleiben im Plancache, solange ausreichend Speicherplatz für deren Speicherung zur Verfügung steht. Wenn nicht ausreichend Speicherplatz zur Verfügung steht, ermittelt [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] kostenbasiert, welche Ausführungspläne aus dem Plancache entfernt werden. Für die kostenbasierte Entscheidung erhöht und senkt [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] die aktuelle Kostenvariable für sämtliche Ausführungspläne anhand der im Folgenden aufgeführten Faktoren.

Wenn ein Benutzerprozess einen Ausführungsplan in den Cache einfügt, werden die aktuellen Kosten auf die Kosten der ursprünglichen Abfragekompilierung festgelegt. Für Ad-hoc-Ausführungspläne legt der Benutzerprozess die aktuellen Kosten auf 0 (null) fest. Jedes Mal, wenn danach ein Benutzerprozess auf einen Ausführungsplan verweist, werden die aktuellen Kosten auf die ursprünglich kompilierten Kosten zurückgesetzt. Für Ad-hoc-Ausführungspläne erhöht der Benutzerprozess die aktuellen Kosten. Für alle Pläne entspricht der maximale Wert für die aktuellen Kosten den Kosten der ursprünglichen Kompilierung.

Wenn nicht ausreichend Speicherplatz zur Verfügung steht, werden von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] Ausführungspläne aus dem Plancache gelöscht. Um zu ermitteln, welche Pläne entfernt werden sollen, überprüft [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] wiederholt den Status sämtlicher Ausführungspläne. Die Pläne, deren aktuelle Kosten 0 (null) betragen, werden entfernt. Ein Ausführungsplan, dessen aktuelle Kosten 0 (null) betragen, wird bei unzureichendem Speicher nicht automatisch entfernt. Der Ausführungsplan wird nur bei einer Überprüfung durch [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] entfernt, wenn die aktuellen Kosten 0 (null) betragen. Wird ein Ausführungsplan derzeit nicht von einer Abfrage verwendet, werden bei der Überprüfung des Plans die aktuellen Kosten von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] durch Reduzieren dieser Kosten gegen 0 (null) gesenkt.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] überprüft die Ausführungspläne wiederholt, bis genügend Ausführungspläne entfernt wurden, um die Speicheranforderungen zu erfüllen. Wenn nicht ausreichend Speicher zur Verfügung steht, können die Kosten eines Ausführungsplans mehrmals erhöht und gesenkt werden. Sobald wieder ausreichend Speicher zur Verfügung steht, werden die aktuellen Kosten nicht verwendeter Ausführungspläne von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] nicht mehr gesenkt. Alle Ausführungspläne verbleiben im Plancache, auch wenn die Kosten 0 (null) betragen.

Wenn nicht ausreichend Speicher zur Verfügung steht, verwendet [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] den Ressourcenmonitor und Benutzerarbeitsthreads, um Speicherplatz im Prozedurcache freizugeben. Vom Ressourcenmonitor und von den Benutzerarbeitsthreads können gleichzeitig ausgeführte Pläne überprüft werden, um die Kosten für die nicht verwendeten Ausführungspläne zu senken. Wenn nicht ausreichend globaler Speicher zur Verfügung steht, werden durch den Ressourcenmonitor Ausführungspläne aus dem Plancache gelöscht. Dadurch wird die Einhaltung von Richtlinien für den Systemspeicher, Prozessspeicher, Ressourcenpoolspeicher und die maximale Größe aller Caches erzwungen. 

Die maximale Größe für alle Caches ist eine Funktion der Pufferpoolgröße und kann den maximalen Serverarbeitsspeicher nicht überschreiten. Weitere Informationen zum Konfigurieren des maximalen Serverarbeitsspeichers finden Sie in den Details zur Einstellung `max server memory` von `sp_configure`. 

Wenn nicht ausreichend Einzelcachespeicher zur Verfügung steht, werden durch die Benutzerarbeitsthreads Ausführungspläne aus dem Plancache gelöscht. Dadurch wird die Einhaltung der Richtlinien für die maximale Einzelcachegröße und die maximale Anzahl von Einzelcacheeinträgen erzwungen. 

In den folgenden Beispielen wird erläutert, welche Ausführungspläne aus dem Plancache entfernt werden:

* Auf einen Ausführungsplan wird regelmäßig verwiesen, sodass seine Kosten nie den Wert 0 (null) erreichen. Der Plan verbleibt im Plancache und wird nur dann entfernt, wenn nicht genügend Arbeitsspeicher vorhanden ist und die aktuellen Kosten 0 (null) sind.
* Ein Ad-hoc-Ausführungsplan wird eingefügt. Auf diesen wird erst wieder verwiesen, wenn nicht ausreichend Speicherplatz zur Verfügung steht. Ad-hoc-Pläne werden mit einem Wert für die aktuellen Kosten von 0 (null) initialisiert. Daher wird der Plan aus dem Plancache entfernt, wenn der Ausführungsplan vom [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] überprüft wird und die aktuellen Kosten 0 (null) betragen. Der Ad-hoc-Ausführungsplan verbleibt im Plancache mit aktuellen Kosten vom Wert 0 (null), wenn genügend Arbeitsspeicher vorhanden ist.

Um einen einzelnen Plan oder alle Pläne manuell aus dem Cache zu entfernen, verwenden Sie [DBCC FREEPROCCACHE](../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md).

### <a name="recompiling-execution-plans"></a>Erneutes Kompilieren von Ausführungsplänen

Bestimmte Änderungen in einer Datenbank können dazu führen, dass ein Ausführungsplan basierend auf dem neuen Status der Datenbank ineffizient oder ungültig ist. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erkennt die Änderungen, die einen Ausführungsplan ungültig machen, und kennzeichnet den Plan als ungültig. Für die nächste Verbindung, die die Abfrage ausführt, muss dann ein neuer Plan kompiliert werden. Folgende Bedingungen können dazu führen, dass ein Plan ungültig wird: 

* Änderungen, die an einer Tabelle oder einer Sicht vorgenommen werden, auf die in der Abfrage verwiesen wird (`ALTER TABLE` und `ALTER VIEW`).
* Änderungen, die an einer einzigen Prozedur vorgenommen werden, durch die alle Pläne für die Prozedur aus dem Cache gelöscht werden (`ALTER PROCEDURE`).
* Änderungen an Indizes, die vom Ausführungsplan verwendet werden.
* Updates der vom Ausführungsplan verwendeten Statistiken, die entweder explizit durch eine Anweisung, wie beispielsweise `UPDATE STATISTICS`, oder automatisch generiert werden.
* Löschen eines Indexes, der von dem Ausführungsplan verwendet wird.
* Ein expliziter Aufruf von `sp_recompile`.
* Eine große Anzahl von Änderungen an Schlüsseln (generiert durch `INSERT` - oder `DELETE` -Anweisungen von anderen Benutzern, die eine Tabelle ändern, auf die in der Abfrage verwiesen wird).
* Bei Tabellen mit Triggern eine deutliche Erhöhung der Zeilenanzahl in der eingefügten oder gelöschten Tabelle.
* Ausführen einer gespeicherten Prozedur mithilfe der Option `WITH RECOMPILE` .

Die meisten Neukompilierungen sind erforderlich, um die Richtigkeit der Anweisungen sicherzustellen oder um möglicherweise schnellere Abfrageausführungspläne zu erhalten.

Jedes Mal, wenn in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 eine in einem Batch vorhandene Anweisung eine Neukompilierung auslöst, wird der gesamte durch eine gespeicherte Prozedur, einen Trigger, einen Ad-hoc-Batch oder eine vorbereitete Anweisung übermittelte Batch neu kompiliert. Ab [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] wird nur die Anweisung innerhalb des Batches, der die Neukompilierung auslöst, erneut kompiliert. Aufgrund dieses Unterschieds kann die Anzahl der Neukompilierungen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 und späteren Versionen nicht für die Anzahl der Neukompilierungen als Vergleich herangezogen werden. Des Weiteren gibt es in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] und höheren Versionen aufgrund der erweiterten Funktionsgruppe mehr Neukompilierungstypen.

Die Neukompilierung auf Anweisungsebene wirkt sich positiv auf die Leistung aus, da in den meisten Fällen wenige Anweisungen Neukompilierungen und die damit verbundenen Sanktionen in Bezug auf die CPU-Zeit und die Sperren verursachen. Diese Sanktionen werden daher für die anderen Anweisungen innerhalb des Batchs vermieden, für die keine Neukompilierung erforderlich ist.

Das erweiterte `sql_statement_recompile`-Ereignis (xEvent) meldet Neukompilierungen auf Anweisungsebene. Dieses xEvent erscheint, wenn ein beliebiger Batch eine Neukompilierung auf Anweisungsebene erfordert. Dazu gehören gespeicherte Prozeduren, Trigger, Ad-hoc-Batches und Abfragen. Batches können möglicherweise über mehrere Schnittstellen, einschließlich sp_executesql, dynamische SQL-Anweisungen, Prepare-Methoden oder Execute-Methoden gesendet werden.
Die `recompile_cause`-Spalte von `sql_statement_recompile` xEvent enthält einen ganzzahligen Code, der den Grund für die Neukompilierung angibt. Die folgende Tabelle enthält die möglichen Gründe:

|||
|----|----|  
|Schema geändert|Statistiken geändert|  
|Verzögerte Kompilierung|SET-Option geändert|  
|Temporäre Tabelle geändert|Remote-Rowset geändert|  
|`FOR BROWSE`-Berechtigung geändert|Abfragebenachrichtigungsumgebung geändert|  
|Partitionierte Sicht geändert|Cursoroptionen geändert|  
|`OPTION (RECOMPILE)` angefordert.|Parametrisierter Plan geleert|  
|Plan geändert, der die Datenbankversion betrifft|Erzwingende Richtlinie des Abfragespeicherplans geändert|  
|Erzwingende Richtlinie des Abfragespeicherplans fehlgeschlagen|Plan des Abfragespeichers fehlt|

> [!NOTE]
> In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Versionen, in denen xEvents nicht verfügbar sind, kann die [SP:Recompile](../relational-databases/event-classes/sp-recompile-event-class.md)-Ablaufverfolgung des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Profiler auch zur Berichterstellung von Neukompilierungen auf Anweisungsebene verwendet werden.
> Das Ablaufereignis [SQL:StmtRecompile](../relational-databases/event-classes/sql-stmtrecompile-event-class.md) meldet ebenfalls Neukompilierungen, und dieses Ablaufereignis kann auch zum Nachverfolgen und Debuggen von Neukompilierungen verwendet werden. Während „SP:Recompile“ nur für gespeicherte Prozeduren und Trigger generiert wird, wird „SQL:StmtRecompile“ für gespeicherte Prozeduren, Trigger, Ad-hoc-Batches, Batches, die mithilfe von `sp_executesql` ausgeführt werden, vorbereitete Abfragen sowie für die dynamische SQL generiert.
> Die *EventSubClass*-Spalte von „SP:Recompile“ und „SQL:StmtRecompile“ enthält einen ganzzahligen Code, der den Grund für die Neukompilierung angibt. Die Codes sind [hier](../relational-databases/event-classes/sql-stmtrecompile-event-class.md) beschrieben.

> [!NOTE]
> Wenn die Datenbankoption `AUTO_UPDATE_STATISTICS` auf `ON` festgelegt wird, werden Abfragen neu kompiliert, wenn sie Tabellen oder indizierte Sichten betreffen, deren Statistiken aktualisiert wurden oder deren Kardinalitäten sich seit der letzten Ausführung signifikant geändert haben. Dieses Verhalten gilt für standardmäßige benutzerdefinierte Tabellen, temporäre Tabellen und die durch DML-Trigger erstellten eingefügten und gelöschten Tabellen. Wenn sich sehr viele Neukompilierungen auf die Abfrageleistung auswirken, können Sie diese Einstellung in `OFF`ändern. Wenn die `AUTO_UPDATE_STATISTICS`-Datenbankoption auf `OFF` festgelegt wird, werden auf der Grundlage von Statistiken oder wegen Änderungen der Kardinalität keine Neukompilierungen durchgeführt, mit Ausnahme der durch DML `INSTEAD OF`-Trigger erstellten eingefügten und gelöschten Tabellen. Da diese Tabellen in „tempdb“ erstellt wurden, hängt die Neukompilierung von Abfragen, die auf diese Tabellen zugreifen, von der `AUTO_UPDATE_STATISTICS` -Einstellung in „tempdb“ ab. Beachten Sie, dass, auch wenn diese Einstellung auf `OFF` festgelegt ist, Abfragen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 weiterhin auf der Grundlage der Kardinalitätsänderungen in den durch DML-Trigger eingefügten und gelöschten Tabellen erneut kompiliert werden.

### <a name="parameters-and-execution-plan-reuse"></a>Parameter und Wiederverwendung von Ausführungsplänen

Durch die Verwendung von Parametern, einschließlich der Parametermarkierungen in ADO-, OLE DB- und ODBC-Anwendungen, kann die Wiederverwendbarkeit von Ausführungsplänen erhöht werden. 

> [!WARNING] 
> Es ist sicherer, Parameter oder Parametermarkierungen zu verwenden, die vom Endbenutzer eingegebene Werte enthalten, als die Werte in einer Zeichenfolge zu verketten, die dann mithilfe einer API-Datenzugriffsmethode, einer `EXECUTE` -Anweisung oder einer gespeicherten `sp_executesql` -Prozedur ausgeführt werden.
 
Die zwei folgenden `SELECT` -Anweisungen unterscheiden sich lediglich im Hinblick auf die Werte, die in der `WHERE` -Klausel verglichen werden:

```tsql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```
```tsql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

Die Ausführungspläne für diese Abfragen unterscheiden sich lediglich hinsichtlich des Werts, der für den Vergleich mit der `ProductSubcategoryID` -Spalte gespeichert wird. Das Ziel von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], stets zu erkennen, wenn Anweisungen im Prinzip den gleichen Plan generieren, und diesen Plan dann wiederzuverwenden, kann von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in komplexen SQL-Anweisungen manchmal nicht erfüllt werden.

Wenn Sie Konstanten mithilfe von Parametern von den SQL-Anweisungen trennen, unterstützen Sie das relationale Modul dabei, doppelte Pläne zu erkennen. Es gibt folgende Möglichkeiten, um Parameter zu verwenden: 

* Verwenden Sie in Transact-SQL `sp_executesql`: 

   ```tsql
   DECLARE @MyIntParm INT
   SET @MyIntParm = 1
   EXEC sp_executesql
     N'SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = @Parm',
     N'@Parm INT',
     @MyIntParm
   ```

   Diese Methode wird für Transact-SQL-Skripts, gespeicherte Prozeduren oder Trigger empfohlen, die SQL-Anweisungen dynamisch generieren. 

* ADO, OLE DB und ODBC verwenden Parametermarkierungen. Parametermarkierungen sind Fragezeichen (?), die eine Konstante in einer SQL-Anweisung ersetzen und an eine Programmvariable gebunden sind. Beispielsweise können Sie in einer ODBC-Anwendung folgende Aktionen ausführen: 

   * Verwenden Sie `SQLBindParameter` , um eine ganzzahlige Variable an die erste Parametermarkierung in einer SQL-Anweisung zu binden.
   * Speichern Sie den ganzzahligen Wert in der Variablen.
   * Führen Sie die Anweisung aus, und geben Sie dabei die Parametermarkierung (?) an: 

   ```
   SQLExecDirect(hstmt, 
     "SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = ?",
     SQL_NTS);
   ```

   Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter und der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber, die beide mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zur Verfügung gestellt werden, verwenden `sp_executesql`, um Anweisungen an [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu senden, wenn Parametermarkierungen in Anwendungen verwendet werden. 

* Zum Entwerfen von gespeicherten Prozeduren mit vorprogrammierter Parameterverwendung

Wenn Sie beim Entwerfen ihrer Anwendungen nicht explizit Parameter in diese einbauen, können Sie auch den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer heranziehen, um bestimmte Abfragen mithilfe des Standardverhaltens der einfachen Parametrisierung automatisch zu parametrisieren. Alternativ können Sie erzwingen, dass der Abfrageoptimierer die Parametrisierung aller Abfragen in der Datenbank in Betracht zieht, indem Sie die `PARAMETERIZATION`-Option der `ALTER DATABASE`-Anweisung auf `FORCED` festlegen.

Auch wenn die erzwungene Parametrisierung aktiviert ist, kann die einfache Parametrisierung erfolgen. Die folgende Abfrage kann beispielsweise gemäß den Regeln der erzwungenen Parametrisierung nicht parametrisiert werden:

```tsql
SELECT * FROM Person.Address
WHERE AddressID = 1 + 2;
```

Sie kann jedoch nach den Regeln der einfachen Parametrisierung parametrisiert werden. Wenn die erzwungene Parametrisierung einen Fehler erzeugt, wird anschließend die einfache Parametrisierung versucht.

### <a name="simple-parameterization"></a>Einfache Parametrisierung

In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird durch das Verwenden von Parametern oder Parametermarkierungen in Transact-SQL-Anweisungen die Fähigkeit des relationalen Moduls verbessert, neue SQL-Anweisungen vorhandenen, zuvor kompilierten Ausführungsplänen zuzuordnen.

> [!WARNING] 
> Es ist sicherer, Parameter oder Parametermarkierungen zu verwenden, die vom Endbenutzer eingegebene Werte enthalten, als die Werte in einer Zeichenfolge zu verketten, die dann mithilfe einer API-Datenzugriffsmethode, einer `EXECUTE` -Anweisung oder einer gespeicherten `sp_executesql` -Prozedur ausgeführt werden.

Wenn eine SQL-Anweisung ohne Parameter ausgeführt wird, parametrisiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Anweisung intern, um die Wahrscheinlichkeit zu erhöhen, dass ein übereinstimmender Ausführungsplan gefunden wird. Dieser Prozess wird als einfache Parametrisierung bezeichnet. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 wurde dieser Prozess als Auto-Parametrisierung bezeichnet.

Angenommen, die folgende Anweisung wird ausgeführt:

```tsql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```

Der Wert 1 am Ende der Anweisung kann als Parameter angegeben werden. Das relationale Modul erstellt den Ausführungsplan für diesen Batch so, als ob anstelle des Werts 1 ein Parameter angegeben worden wäre. Aufgrund dieser einfachen Parametrisierung erkennt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], dass die folgenden beiden Anweisungen im Prinzip den gleichen Ausführungsplan generieren, und verwendet den ersten Plan auch für die zweite Anweisung:

```tsql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```
```tsql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

Bei der Verarbeitung komplexer SQL-Anweisungen können für das relationale Modul eventuell Schwierigkeiten bei der Bestimmung der Ausdrücke auftreten, die parametrisiert werden können. Um die Wahrscheinlichkeit zu erhöhen, dass das relationale Modul Übereinstimmungen zwischen komplexen SQL-Anweisungen und vorhandenen, nicht verwendeten Ausführungsplänen erkennt, sollten Sie die Parameter explizit mithilfe von „sp_executesql“ oder Parametermarkierungen angeben. 

> [!NOTE]
> Wenn die arithmetischen Operatoren +, -, *, / oder % zur impliziten oder expliziten Konvertierung von Konstantenwerten der Datentypen „int“, „smallint“, „tinyint“ oder „bigint“ in die Datentypen „float“, „real“, „decimal“ oder „numeric“ verwendet werden, wendet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] spezielle Regeln an, um den Typ und die Genauigkeit der Ausdrucksergebnisse zu berechnen. Allerdings unterscheiden sich diese Regeln in Abhängigkeit davon, ob die Abfrage parametrisiert ist oder nicht. Daher können gleiche Ausdrücke in Abfragen in einigen Fällen zu unterschiedlichen Ergebnissen führen.

Beim Standardverhalten der einfachen Parametrisierung parametrisiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eine relativ kleine Klasse von Abfragen. Allerdings können Sie angeben, dass mit bestimmten Einschränkungen alle Abfragen in einer Datenbank parametrisiert werden, indem Sie die `PARAMETERIZATION` -Option des Befehls `ALTER DATABASE` auf `FORCED`festlegen. Damit kann die Leistung von Datenbanken verbessert werden, bei denen sehr viele gleichzeitige Abfragen auftreten, indem die Häufigkeit der Abfragekompilierungen verringert wird.

Alternativ können Sie angeben, dass eine einzelne Abfrage und alle anderen Abfragen, die in ihrer Syntax gleichwertig sind, und lediglich in ihren Parameterwerten abweichen, parametrisiert werden. 

### <a name="forced-parameterization"></a>Erzwungene Parametrisierung

Sie können das standardmäßige Parametrisierungsverhalten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], die einfache Parametrisierung, überschreiben, indem Sie angeben, dass alle `SELECT`-, `INSERT`-, `UPDATE`- und `DELETE`-Anweisungen in einer Datenbank mit bestimmten Einschränkungen parametrisiert werden sollen. Die erzwungene Parametrisierung wird aktiviert, indem die `PARAMETERIZATION` -Option in der `FORCED` -Anweisung auf `ALTER DATABASE` festgelegt wird. Indem sie die Frequenz von Anweisungskompilierungen und -neukompilierungen verringert, kann die erzwungene Parametrisierung die Leistungsfähigkeit bestimmter Datenbanken erhöhen. Dabei handelt es sich im Allgemeinen um Datenbanken, die einer großen Anzahl gleichzeitiger Abfragen ausgesetzt sind, wie z. B. Point-of-Sale-Anwendungen.

Wenn die `PARAMETERIZATION` -Option auf `FORCED`festgelegt ist, werden während der Kompilierung der Abfrage alle Literalwerte in `SELECT`-, `INSERT`-, `UPDATE`- oder `DELETE` -Anweisungen, ungeachtet der Form, in der sie übergeben wurden, in Parameter konvertiert. Ausnahmen bilden Literalwerte in folgenden Abfragekonstruktionen: 

* `INSERT...EXECUTE` -Anweisungen.
* Anweisungen innerhalb des Hauptteils von gespeicherten Prozeduren, Triggern oder benutzerdefinierten Funktionen. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] werden bereits Abfragepläne für diese Routinen wiederverwendet.
* Vorbereitete Anweisungen, die bereits in der clientbasierten Anwendung parametrisiert wurden.
* Anweisungen, die XQuery-Methodenaufrufe enthalten, wo die Methode in einem Kontext angezeigt wird, in dem ihre Argumente normalerweise parametrisiert werden, wie beispielsweise die `WHERE` -Klausel. Wenn die Methode in einem Kontext angezeigt wird, in dem ihre Argumente normalerweise nicht parametrisiert werden, wird der Rest der Anweisung parametrisiert.
* Anweisungen in einem Transact-SQL-Cursor. (`SELECT` -Anweisungen innerhalb von API-Cursorn werden parametrisiert.)
* Als veraltet markierte Abfragekonstrukte.
* Eine Anweisung, die im Kontext von `ANSI_PADDING` oder `ANSI_NULLS` mit der Einstellung `OFF`ausgeführt wird.
* Anweisungen mit mehr als 2.097 parametrisierbaren Literalwerten.
* Anweisungen, die auf Variablen verweisen, wie beispielsweise `WHERE T.col2 >= @bb`.
* Anweisungen mit `RECOMPILE` -Abfragehinweis.
* Anweisungen mit `COMPUTE` -Klauseln.
* Anweisungen mit `WHERE CURRENT OF` -Klauseln.

Außerdem werden die folgenden Abfrageklauseln nicht parametrisiert. Beachten Sie, dass in diesen Fällen nur die Klauseln nicht parametrisiert werden. Andere Klauseln in derselben Abfrage können für eine erzwungene Parametrisierung in Frage kommen.

* <select_list> in `SELECT`-Anweisungen. Dies trifft ebenfalls auf `SELECT`-Listen von Unterabfragen sowie `SELECT`-Listen innerhalb von `INSERT`-Anweisungen zu.
* Unterabfragen mit `SELECT` -Anweisungen innerhalb von `IF` -Anweisungen.
* Die Abfrageklauseln `TOP`, `TABLESAMPLE`, `HAVING`, `GROUP BY`, `ORDER BY`, `OUTPUT...INTO`und `FOR XM`L.
* Direkte oder als Teilausdrücke formulierte Argumente der Operatoren `OPENROWSET`, `OPENQUERY`, `OPENDATASOURCE`, `OPENXML`sowie aller `FULLTEXT` -Operatoren.
* Das pattern-Argument und das escape_character-Argument einer `LIKE` -Klausel.
* Das style-Argument einer `CONVERT` -Klausel.
* Integer-Konstanten innerhalb einer `IDENTITY` -Klausel.
* Über die ODBC-Erweiterungssyntax angegebene Konstanten.
* Vor der Kompilierzeit auf eine Konstante reduzierbar Ausdrücke, die Argumente der Operatoren +, -, *, / und % sind. Um zu ermitteln, ob die erzwungene Parametrisierung in Frage kommt, betrachtet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] einen Ausdruck als vor der Kompilierzeit auf eine Konstante reduzierbar, wenn die beiden folgenden Bedingungen erfüllt sind:  
  * Der Ausdruck enthält keine Spalten, Variablen oder Unterabfragen.  
  * Der Ausdruck enthält eine `CASE` -Klausel.  
* Argumente von Abfragehinweisklauseln. Zu diesen gehören das `number_of_rows` -Argument des `FAST` -Abfragehinweises, das `number_of_processors` -Argument des `MAXDOP` -Abfragehinweises sowie das number-Argument des `MAXRECURSION` -Abfragehinweises.

Die Parametrisierung wird auf der Ebene der einzelnen Transact-SQL-Anweisungen ausgeführt, d. h. die Anweisungen werden nacheinander batchweise parametrisiert. Nach dem Kompilieren wird eine parametrisierte Abfrage ausgeführt – in dem Kontext des Batches, in dem die Abfrage ursprünglich übermittelt wurde. Wenn ein Ausführungsplan für eine Abfrage zwischengespeichert wird, können Sie anhand der sql-Spalte der dynamischen Verwaltungssicht sys.syscacheobjects ermitteln, ob die Abfrage parametrisiert wurde. Wenn eine Abfrage parametrisiert wird, stehen die Namen und Datentypen der Parameter vor dem Text des übergebenen Batches in dieser Spalte, wie beispielsweise (@1 tinyint).

> [!NOTE]
> Parameternamen sind willkürlich. Benutzer bzw. Anwendungen sollten sich nicht auf eine bestimmte Namensreihenfolge verlassen. Darüber hinaus kann sich zwischen verschiedenen Versionen und Service Pack-Upgrades von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Folgendes ändern: Parameternamen, die Auswahl der parametrisierten Literale und der Abstand im parametrisierten Text.

#### <a name="data-types-of-parameters"></a>Parameterdatentypen

Beim Parametrisieren von Literalwerten konvertiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Parameter in folgende Datentypen:

* Integer-Literale, die von der Größe her in den int-Datentyp passen, werden beim Parametrisieren in int-Werte konvertiert. Größere Integer-Literale, die Teil von Prädikaten mit Vergleichsoperatoren sind (unter anderem <, \<=, =, !=, >, >=, , !\<, !>, <>, `ALL`, `ANY`, `SOME`, `BETWEEN`, and `IN`) werden beim Parametrisieren in numeric(38,0)-Werte konvertiert. Größere Literale, die nicht Teil von Prädikaten mit Vergleichsoperatoren sind, werden bei der Parametrisierung in numerische Werte mit ausreichenden Ziffern (precision) für ihre Größe und einem Dezimalstellenwert (scale) von 0 konvertiert.
* Numerische Festkommaliterale, die Teil von Prädikaten mit Vergleichsoperatoren sind, werden bei der Parametrisierung in numerische Werte mit 38 Ziffern (precision) und einem für ihre Größe ausreichenden Dezimalstellenwert (scale) konvertiert. Numerische Festkommaliterale, die nicht Teil von Prädikaten mit Vergleichsoperatoren sind, werden bei der Parametrisierung in numerische Werte mit ausreichenden Ziffern (precision) und einem ausreichenden Dezimalstellenwert (scale) für ihre Größe konvertiert.
* Numerische Fließkommaliterale werden bei der Parametrisierung in float(53)-Werte konvertiert.
* Nicht-Unicode-Zeichenfolgenliterale werden bei der Parametrisierung in varchar(8000)-Werte konvertiert, wenn das Literal 8.000 Zeichen nicht überschreitet, und in varchar(max)-Werte, wenn es 8.000 Zeichen überschreitet.
* Unicode-Zeichenfolgenliterale werden bei der Parametrisierung in nvarchar(4000)-Werte konvertiert, wenn das Literal 4.000 Zeichen nicht überschreitet, und in nvarchar(max)-Werte, wenn es 4.000 Zeichen überschreitet.
* Binäre Literale werden bei der Parametrisierung in varbinary(8000)-Werte konvertiert, wenn das Literal 8.000 Bytes nicht überschreitet. Wenn es 8.000 Bytes überschreitet, wird es in einen varbinary(max)-Wert konvertiert.
* Literale vom Typ „money“ werden bei der Parametrisierung in money-Werte konvertiert.

#### <a name="guidelines-for-using-forced-parameterization"></a>Richtlinien für die Verwendung der erzwungenen Parametrisierung

Berücksichtigen Sie Folgendes, wenn Sie die `PARAMETERIZATION` -Option auf FORCED festlegen:

* Die erzwungene Parametrisierung konvertiert die literalen Konstanten einer Abfrage, sobald diese kompiliert wird, tatsächlich in Parameter. Daher ist es möglich, dass der Abfrageoptimierer nicht die optimalen Abfragepläne auswählt. Insbesondere verringert sich die Wahrscheinlichkeit, dass der Abfrageoptimierer eine Übereinstimmung zwischen der Abfrage und der richtigen indizierten Sicht oder dem Index für eine berechnete Spalte findet. Außerdem wählt der Abfrageoptimierer möglicherweise auch für Abfragen für partitionierte Tabellen und verteilte partitionierte Sichten nicht optimale Abfragepläne aus. Die erzwungene Parametrisierung sollte deshalb nicht in Umgebungen verwendet werden, die sich stark auf indexierte Sichten oder Indizes für berechnete Spalten stützen. Im Allgemeinen sollte die `PARAMETERIZATION FORCED` -Option nur von erfahrenen Datenbankadministratoren verwendet werden, und auch dann nur, wenn diese sichergestellt haben, dass die erzwungene Parametrisierung die Leistung der Datenbank nicht beeinträchtigt.
* Verteilte Abfragen, die auf mehrere Datenbanken verweisen, sind für die erzwungene Parametrisierung geeignet, solange die `PARAMETERIZATION` -Option in der Datenbank auf `FORCED` festgelegt wird, in deren Kontext die Abfrage ausgeführt wird.
* Wenn die `PARAMETERIZATION` -Option auf `FORCED` festgelegt wird, werden alle Abfragepläne aus dem Plancache der Datenbank geleert, mit Ausnahme derer, die gerade kompiliert, erneut kompiliert oder ausgeführt werden. Die Pläne der Abfragen, die während der Einstellungsänderung kompiliert, erneut kompiliert oder ausgeführt werden, werden beim nächsten Ausführen der Abfrage parametrisiert.
* Das Festlegen der `PARAMETERIZATION` -Option ist ein Onlinevorgang, d.h., es sind keine exklusiven Sperren auf Datenbankebene erforderlich.
* Die aktuelle Einstellung der `PARAMETERIZATION` -Option wird beim erneuten Anfügen oder Wiederherstellen einer Datenbank beibehalten.

Sie können das Verhalten der erzwungenen Parametrisierung überschreiben, indem Sie angeben, dass für eine einzelne Abfrage und für alle anderen Abfragen, die syntaktisch äquivalent sind und sich nur in ihren Parameterwerten unterscheiden, die einfache Parametrisierung versucht werden soll. Im Gegensatz dazu können Sie angeben, dass die erzwungene Parametrisierung nur für einen Satz von syntaktisch äquivalenten Abfragen versucht werden soll, selbst wenn die erzwungene Parametrisierung in der Datenbank deaktiviert ist. Zu diesem Zweck werden[Planhinweislisten](../relational-databases/performance/plan-guides.md) verwendet.

> [!NOTE]
> Wird die `PARAMETERIZATION` -Option auf `FORCED`festgelegt, werden Fehlermeldungen möglicherweise nicht auf die gleiche Weise wie bei der einfachen Parametrisierung gemeldet: Eventuell werden mehr Fehlermeldungen als bei der einfachen Parametrisierung ausgegeben, und die Zeilennummern, in denen die Fehler aufgetreten sind, werden möglicherweise falsch gemeldet.

### <a name="preparing-sql-statements"></a>Vorbereiten von SQL-Anweisungen

Das relationale Modul von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bietet vollständige Unterstützung für die Vorbereitung von SQL-Anweisungen vor ihrer Ausführung. Wenn eine Anwendung eine SQL-Anweisung mehrfach ausführen muss, kann mithilfe der Datenbank-API Folgendes erreicht werden: 

* Einmaliges Vorbereiten der Anweisung. Mit diesem Schritt wird die SQL-Anweisung zu einem Ausführungsplan kompiliert.
* Ausführen des vorkompilierten Ausführungsplans immer dann, wenn die Anweisung ausgeführt werden muss. Auf diese Weise muss die SQL-Anweisung nach der ersten Ausführung nicht jedes Mal erneut kompiliert werden.   
  Das Vorbereiten und Ausführen von Anweisungen wird durch API-Funktionen und -Methoden gesteuert. Es ist nicht Teil der Transact-SQL-Sprache. Das Vorbereiten/Ausführen-Modell für die Ausführung von SQL-Anweisungen wird von dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter und dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber unterstützt. Bei einer Vorbereitungsanforderung sendet der Anbieter oder der Treiber die Anweisung zusammen mit der Anforderung zur Vorbereitung der Anweisung an [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird ein Ausführungsplan kompiliert und ein Handle für diesen Plan an den Anbieter oder Treiber zurückgegeben. Bei einer Ausführungsanforderung sendet der Anbieter bzw. Treiber eine Anforderung an den Server, den dem Handle zugeordneten Plan auszuführen. 

Vorbereitete Anweisungen können nicht zum Erstellen von temporären Objekten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet werden. Vorbereitete Anweisungen können nicht auf gespeicherte Systemprozeduren verweisen, die temporäre Objekte, wie z. B. temporäre Tabellen, erstellen. Diese Prozeduren müssen direkt ausgeführt werden.

Durch übermäßige Verwendung des Vorbereiten/Ausführen-Modells kann die Leistung beeinträchtigt werden. Wenn eine Anweisung nur ein Mal ausgeführt wird, wird durch eine direkte Ausführung nur ein Netzwerkroundtrip zum Server benötigt. Das Vorbereiten und Ausführen einer SQL-Anweisung, die nur ein Mal ausgeführt wird, erfordert einen zusätzlichen Netzwerkroundtrip: einen Trip zur Vorbereitung und einen Trip zur Ausführung der Anweisung.

Das Vorbereiten einer Anweisung ist effizienter, wenn Parametermarkierungen verwendet werden. Nehmen Sie z.B. an, eine Anwendung soll gelegentlich Produktinformationen aus der `AdventureWorks` -Beispieldatenbank abrufen. Es gibt zwei Möglichkeiten, wie die Anwendung diese Aufgabe ausführen kann. 

Die erste Möglichkeit besteht darin, dass die Anwendung für jedes angeforderte Produkt eine eigene Abfrage ausführt:

```tsql
SELECT * FROM AdventureWorks2014.Production.Product
WHERE ProductID = 63;
```

Die zweite Möglichkeit umfasst folgende Schritte: 

1. Die Anwendung bereitet eine Anweisung vor, die die Parametermarkierung (?) enthält:  
   ```tsql
   SELECT * FROM AdventureWorks2014.Production.Product  
   WHERE ProductID = ?;
   ```
2. Die Anwendung bindet eine Programmvariable an die Parametermarkierung.
3. Die Anwendung füllt die gebundene Variable mit dem Schlüsselwert und führt die Anweisung aus, sobald die Produktinformationen benötigt werden.

Die zweite Methode ist effizienter, sobald die Anweisung mehr als drei Mal ausgeführt wird.

In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bietet das Vorbereiten/Ausführen-Modell aufgrund der Art und Weise, wie Ausführungspläne von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wiederverwendet werden, keine erheblichen Leistungsvorteile gegenüber der direkten Ausführung. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] besitzt effiziente Algorithmen zur Ermittlung von Übereinstimmungen zwischen aktuellen SQL-Anweisungen und Ausführungsplänen, die für vorhergehende Ausführungen derselben SQL-Anweisung generiert wurden. Wenn eine Anwendung eine SQL-Anweisung mit Parametermarkierungen mehrfach ausführt, verwendet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] den Ausführungsplan der ersten Ausführung für die zweite und alle folgenden Ausführungen erneut (es sei denn, der Plan wird aus dem Plancache entfernt). Das Vorbereiten/Ausführen-Modell bietet jedoch weiterhin die folgenden Vorteile: 

* Das Suchen eines Ausführungsplans anhand eines identifizierenden Handles ist effizienter als die Algorithmen, die für das Ermitteln einer übereinstimmenden SQL-Anweisung mit vorhandenen Ausführungsplänen verwendet werden.
* Die Anwendung kann steuern, wann der Ausführungsplan erstellt, und wann er wiederverwendet werden soll.
* Das Vorbereiten/Ausführen-Modell kann auf andere Datenbanken portiert werden, einschließlich früherer Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

 
### <a name="parameter-sniffing"></a>Parameterermittlung
Die „Parameterermittlung“ bezieht sich auf einen Prozess, wobei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die aktuellen Parameter während der Kompilierung oder Neukompilierung ermittelt und diese an den Abfrageoptimierer übermittelt, sodass sie zum Generieren potenziell effizienter Abfrageausführungspläne verwendet werden können.

Parameterwerte werden während der Kompilierung oder Neukompilierung für die folgenden Batchtypen ermittelt:

-  Gespeicherte Prozeduren
-  Abfragen, die über „sp_executesql“ übermittelt werden 
-  Vorbereitete Abfragen

> [!NOTE]
> Für Abfragen, die den `RECOMPILE`-Hinweis verwenden, werden jeweils die Parameterwerte und aktuellen Werte der lokalen Variablen ermittelt. Die ermittelten Werte (der Parameter und lokalen Variablen) sind die, die an dem Ort direkt vor der Anweisung mit dem `RECOMPILE`-Hinweis vorhanden sind. Im Gegensatz dazu werden bei Parametern die Werte, die innerhalb des Batchaufrufs übermittelt werden, nicht geprüft.

## <a name="parallel-query-processing"></a>Parallele Abfrageverarbeitung

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ermöglicht parallele Abfragen, um die Abfrageausführung und Indexvorgänge für Computer zu optimieren, die über mehrere Mikroprozessoren (CPUs) verfügen. Da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mehrere Betriebssystem-Arbeitsthreads verwenden kann, um eine Abfrage oder einen Indexvorgang parallel auszuführen, kann der betreffende Vorgang schnell und effizient ausgeführt werden.

Während der Abfrageoptimierung sucht [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nach Abfragen oder Indexvorgängen, für die eine parallele Ausführung vorteilhaft ist. Für diese Abfragen fügt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Verteilungsoperatoren in den Abfrageausführungsplan ein, um die Abfrage für die parallele Ausführung vorzubereiten. Ein Verteilungsoperator ist ein Operator in einem Plan für die Abfrageausführung, der die Prozessverwaltung, die Neuverteilung der Daten und die Ablaufsteuerung ermöglicht. Der Verteilungsoperator schließt die logischen Operatoren `Distribute Streams`, `Repartition Streams`und `Gather Streams` als Untertypen ein. Einer oder mehrere dieser Operatoren können in der Showplanausgabe eines Abfrageplans für eine parallele Abfrage enthalten sein. 

Nach dem Einfügen eines Verteilungsoperators ist das Ergebnis ein Plan für eine parallele Abfrageausführung. Ein Plan für die parallele Abfrageausführung kann mehrere Arbeitsthreads verwenden. Ein serieller Ausführungsplan, der von einer nicht parallelen Abfrage verwendet wird, verwendet nur einen Arbeitsthread bei seiner Ausführung. Die tatsächliche Anzahl der Arbeitsthreads, die von einer parallelen Abfrage verwendet werden, wird während der Initialisierung der Abfrageplanausführung bestimmt und durch die Komplexität des Plans und den Grad der Parallelität bestimmt. Der Grad der Parallelität bestimmt die maximal verwendete Anzahl von CPUs; er bezieht sich nicht auf die Anzahl der verwendeten Arbeitsthreads. Der Wert für den Grad der Parallelität wird auf Serverebene festgelegt und kann mithilfe der gespeicherten Systemprozedur „sp_configure“ geändert werden. Sie können diesen Wert für einzelne Abfrage- oder Indexanweisungen überschreiben, indem Sie den `MAXDOP` -Abfragehinweis oder die `MAXDOP` -Indexoption angeben. 

Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer verwendet keinen parallelen Ausführungsplan für eine Abfrage, wenn eine der folgenden Bedingungen zutrifft:

* Die Kosten für die serielle Ausführung der Abfrage sind nicht hoch genug, um einen parallelen Ausführungsplan zu rechtfertigen. 
* Ein serieller Ausführungsplan wird für die betreffende Abfrage als schneller erachtet als jeder mögliche parallele Ausführungsplan.
* Die Abfrage enthält skalare oder relationale Operatoren, die nicht parallel ausgeführt werden können. Bestimmte Operatoren können verursachen, dass ein Abschnitt des Ausführungsplans oder der gesamte Plan im seriellen Modus ausgeführt wird.

### <a name="degree-of-parallelism"></a>Grad der Parallelität

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erkennt automatisch den am besten geeigneten Grad an Parallelität für jede Instanz einer parallelen Abfrageausführung oder eines DDL-Indizierungsvorgangs (Data Definition Language). Dazu werden die folgenden Kriterien untersucht: 

1. Wird [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Computer mit mehreren Mikroprozessoren (oder CPUs) ausgeführt wie z. B. auf einem symmetrischen Multiprozessorcomputer (Symmetric Multiprocessing, SMP)?  
  Nur Computer mit mehreren CPUs können parallele Abfragen verwenden. 

2. Sind ausreichend Arbeitsthreads verfügbar?  
  Jeder Abfrage- oder Indexvorgang setzt zu seiner Ausführung eine bestimmte Anzahl von Arbeitsthreads voraus. Das Ausführen eines parallelen Plans erfordert mehr Arbeitsthreads als ein serieller Plan, und die Anzahl der erforderlichen Arbeitsthreads steigt mit dem Grad der Parallelität. Wenn die Arbeitsthreadanforderung des parallelen Plans für einen bestimmten Grad der Parallelität nicht erfüllt werden kann, reduziert [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] den Grad an Parallelität automatisch oder verwirft den parallelen Plan in dem angegebenen Arbeitsauslastungskontext. Stattdessen wird der serielle Plan (ein Arbeitsthread) ausgeführt. 

3. Welcher Abfragetyp oder Indexvorgangstyp soll ausgeführt werden?  
  Indexvorgänge, die einen Index erstellen oder neu erstellen oder einen gruppierten Index löschen, sowie Abfragen, die sehr viele CPU-Zyklen beanspruchen, eignen sich am besten für einen parallelen Plan. So sind z. B. Joins großer Tabellen, umfassende Aggregationen und Sortierungen großer Resultsets gut geeignet. Für einfache Abfragen, die häufig in transaktionsverarbeitenden Anwendungen eingesetzt werden, wird der zusätzliche Aufwand, der für die Koordinierung einer parallelen Abfrageausführung erforderlich ist, durch die erwartete Leistungssteigerung in der Regel nicht gerechtfertigt. Um zu ermitteln, für welche Abfragen die parallele Ausführung sinnvoll ist und für welche dies nicht gilt, vergleicht [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] die geschätzten Kosten für die Ausführung der Abfrage oder des Indexvorgangs mithilfe des [cost threshold for parallelism](../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)-Werts. Mithilfe von [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)können Benutzer den Standardwert 5 ändern; dies wird jedoch nicht empfohlen. 

4. Gibt es eine ausreichende Anzahl von zu verarbeitenden Zeilen?  
  Wenn der Abfrageoptimierer ermittelt, dass die Anzahl der Zeilen zu niedrig ist, werden keine Verteilungsoperatoren eingesetzt, um die Zeilen zu verteilen. Demzufolge werden die Operatoren seriell ausgeführt. Durch das Ausführen der Operatoren in einem seriellen Plan werden Situationen vermieden, in denen die Kosten für Start, Verteilung und Koordinierung den Nutzen übersteigen, der durch die parallele Ausführung der Operatoren erzielt würde.

5. Sind aktuelle Verteilungsstatistiken verfügbar?  
  Wenn der höchste Grad der Parallelität nicht möglich ist, werden zunächst niedrigere Grade in Betracht gezogen, bevor der parallele Plan verworfen wird.  
  Wenn Sie z. B. einen gruppierten Index für eine Sicht erstellen, können die Statistiken nicht ausgewertet werden, weil der gruppierte Index noch nicht vorhanden ist. In diesem Fall kann [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] nicht den höchsten Grad der Parallelität für den Indexvorgang bereitstellen. Allerdings können einige Vorgänge, wie z. B. das Sortieren und Scannen, von der parallelen Ausführung profitieren.

> [!NOTE]
> Parallele Indexvorgänge sind nur in den Editionen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise, Developer und Evaluation verfügbar.
 
Zur Ausführungszeit ermittelt [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], ob die aktuelle Systemlast und die oben beschriebenen Konfigurationsinformationen die parallele Ausführung zulassen. Wenn die parallele Ausführung gerechtfertigt ist, ermittelt [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] die optimale Anzahl von Arbeitsthreads und verteilt dann die Ausführung des parallelen Plans auf diese Arbeitsthreads. Wenn die parallele Ausführung eines Abfrage- oder Indexvorgangs mit mehreren Arbeitsthreads gestartet wird, wird dieselbe Anzahl an Arbeitsthreads bis zur Beendigung des Vorgangs verwendet. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] bestimmt die optimale Anzahl von Arbeitsthreads jedes Mal neu, wenn ein Ausführungsplan aus dem Plancache abgerufen wird. Bei einer Ausführung einer Abfrage könnte z. B. ein serieller Plan verwendet werden, bei einer späteren Ausführung derselben Abfrage ein paralleler Plan, der drei Arbeitsthreads verwendet, und bei der dritten Ausführung dieser Abfrage ein paralleler Plan, der vier Arbeitsthreads verwendet.

In einem parallelen Abfrageausführungsplan werden die Vorgänge zum Einfügen, Aktualisieren und Löschen seriell ausgeführt. Jedoch können die WHERE-Klausel einer UPDATE- oder einer DELETE-Anweisung oder der SELECT-Teil einer INSERT-Anweisung parallel ausgeführt werden. Die eigentlichen Datenänderungen werden anschließend seriell auf die Datenbank angewendet.

Statische Cursor und keysetgesteuerte Cursor können durch parallele Ausführungspläne aufgefüllt werden. Das spezifische Verhalten dynamischer Cursor kann jedoch nur durch die serielle Ausführung gewährleistet werden. Für eine Abfrage, die Teil eines dynamischen Cursors ist, generiert der Abfrageoptimierer immer einen seriellen Ausführungsplan.

#### <a name="overriding-degrees-of-parallelism"></a>Überschreiben der Grade der Parallelität

Mithilfe der Serverkonfigurationsoption [Max. Grad an Parallelität](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (MAXDOP) ([ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) in [!INCLUDE[ssSDS_md](../includes/sssds-md.md)] ) kann die Anzahl der Prozessoren beschränkt werden, die bei der Ausführung paralleler Pläne verwendet werden. Die Option „Max. Grad an Parallelität“ kann jedoch für einzelne Abfrage- und Indexvorgangsanweisungen überschrieben werden, indem der MAXDOP-Abfragehinweis oder die MAXDOP-Indexoption angegeben wird. MAXDOP bietet mehr Kontrolle über einzelne Abfrage- und Indexvorgänge. Sie können z.B. die MAXDOP-Option verwenden, um durch Erhöhen oder Reduzieren eine Steuerung der Anzahl der einem Onlineindexvorgang zugewiesenen Prozessoren zu bewirken. Auf diese Weise können Sie die Ressourcen, die von dem Indexvorgang verwendet werden, mit den Ressourcen gleichzeitiger Benutzer ausgleichen. 

Wenn die Option „Max. Grad an Parallelität“ auf 0 (Standard) festgelegt wurde, kann [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alle verfügbaren Prozessoren (maximal 64) zur Ausführung paralleler Pläne verwenden. Obwohl [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ein Laufzeitziel von 64 logischen Prozessoren festlegt, wenn MAXDOP auf 0 festgelegt ist, kann falls nötig ein anderer Wert manuell festgelegt werden. Wenn MAXDOP für Abfragen und Indizes auf 0 (null) festgelegt wurde, kann [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alle verfügbaren Prozessoren (maximal 64) zur Ausführung paralleler Pläne für die jeweiligen Abfragen oder Indizes verwenden. MAXDOP ist kein erzwungener Wert für alle parallelen Abfragen, sondern eher ein Ziel mit Vorbehalt für alle Abfragen, die für die Parallelität qualifiziert sind. Das bedeutet, dass wenn nicht genügend Arbeitsthreads zur Laufzeit vorhanden sind, eine Abfrage möglicherweise mit einem niedrigeren Grad der Parallelität als die MAXDOP-Serverkonfigurationsoption ausgeführt wird.

Bewährte Methoden zum Konfigurieren von MAXDOP finden Sie im [Microsoft Support-Artikel](https://support.microsoft.com/en-us/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-configuration-option-in-sql-server).

### <a name="parallel-query-example"></a>Beispiel für eine parallele Abfrage

In der folgenden Abfrage wird die Anzahl der Bestellungen gezählt, die in einem bestimmten Quartal, beginnend mit dem 1. April 2000, aufgegeben wurden und in denen mindestens ein Artikel der Bestellung vom Kunden erst nach dem angekündigten Datum empfangen wurde. Die Abfrage listet die Anzahl dieser Bestellungen gruppiert nach Priorität der Bestellung und in aufsteigender Reihenfolge der Priorität auf. 

In diesem Beispiel werden erfundene Tabellen- und Spaltennamen verwendet.

```tsql
SELECT o_orderpriority, COUNT(*) AS Order_Count
FROM orders
WHERE o_orderdate >= '2000/04/01'
   AND o_orderdate < DATEADD (mm, 3, '2000/04/01')
   AND EXISTS
         (
          SELECT *
            FROM    lineitem
            WHERE l_orderkey = o_orderkey
               AND l_commitdate < l_receiptdate
         )
   GROUP BY o_orderpriority
   ORDER BY o_orderpriority
```

Nehmen Sie an, dass die folgenden Indizes für die lineitem- und die orders-Tabelle definiert werden:

```tsql
CREATE INDEX l_order_dates_idx 
   ON lineitem
      (l_orderkey, l_receiptdate, l_commitdate, l_shipdate)

CREATE UNIQUE INDEX o_datkeyopr_idx
   ON ORDERS
      (o_orderdate, o_orderkey, o_custkey, o_orderpriority)
```

Im Folgenden sehen Sie einen möglichen parallelen Plan, der für die zuvor beschriebene Abfrage generiert wurde:

```
|--Stream Aggregate(GROUP BY:([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=COUNT(*)))
    |--Parallelism(Gather Streams, ORDER BY:
                  ([ORDERS].[o_orderpriority] ASC))
         |--Stream Aggregate(GROUP BY:
                  ([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=Count(*)))
              |--Sort(ORDER BY:([ORDERS].[o_orderpriority] ASC))
                   |--Merge Join(Left Semi Join, MERGE:
                  ([ORDERS].[o_orderkey])=
                        ([LINEITEM].[l_orderkey]),
                  RESIDUAL:([ORDERS].[o_orderkey]=
                        [LINEITEM].[l_orderkey]))
                        |--Sort(ORDER BY:([ORDERS].[o_orderkey] ASC))
                        |    |--Parallelism(Repartition Streams,
                           PARTITION COLUMNS:
                           ([ORDERS].[o_orderkey]))
                        |         |--Index Seek(OBJECT:
                     ([tpcd1G].[dbo].[ORDERS].[O_DATKEYOPR_IDX]),
                     SEEK:([ORDERS].[o_orderdate] >=
                           Apr  1 2000 12:00AM AND
                           [ORDERS].[o_orderdate] <
                           Jul  1 2000 12:00AM) ORDERED)
                        |--Parallelism(Repartition Streams,
                     PARTITION COLUMNS:
                     ([LINEITEM].[l_orderkey]),
                     ORDER BY:([LINEITEM].[l_orderkey] ASC))
                             |--Filter(WHERE:
                           ([LINEITEM].[l_commitdate]<
                           [LINEITEM].[l_receiptdate]))
                                  |--Index Scan(OBJECT:
         ([tpcd1G].[dbo].[LINEITEM].[L_ORDER_DATES_IDX]), ORDERED)
```

![parallel_plan](../relational-databases/media/parallel-plan.gif) Abfrageplan mit DOP 4, enthält einen Join zweier Tabellen

Die Abbildung zeigt einen Abfrageoptimiererplan, der mit einem Parallelitätsgrad von 4 ausgeführt wird und ein Join von zwei Tabellen einschließt.

Der parallele Plan enthält drei Parallelism-Operatoren. Sowohl der „Index Seek“-Operator des `o_datkey_ptr`-Indexes als auch der „Index Scan“-Operator des `l_order_dates_idx`-Indexes werden parallel ausgeführt. Dadurch werden mehrere exklusive Datenströme erzeugt. Dies kann mithilfe der nächsten Parallelism-Operatoren oberhalb der Operatoren „Index Scan“ und „Index Seek“ bestimmt werden. Beide Operatoren nehmen einfach eine Umverteilung der Daten auf die Datenströme vor, sodass dieselbe Anzahl von Datenströmen als Ausgabe erzeugt wird, wie als Eingabe vorlag. Diese Anzahl der Datenströme entspricht dem Grad an Parallelität.

Der „Parallelism“-Operator oberhalb des `l_order_dates_idx` Index Scan-Operators nimmt mithilfe des Werts für `L_ORDERKEY` als Schlüssel eine Neueinteilung der Eingabedatenströme vor. Auf diese Weise gelangen identische Werte für `L_ORDERKEY` in dieselben Ausgabedatenströme. Gleichzeitig behalten die Ausgabedatenströme die Reihenfolge für die `L_ORDERKEY`-Spalte bei, sodass die Eingabeanforderungen des „Merge Join“-Operators erfüllt sind.

Der „Parallelism“-Operator oberhalb des „Index Seek“-Operators nimmt mithilfe des Werts für `O_ORDERKEY` eine Neueinteilung der Eingabedatenströme vor. Da die Eingabe nicht anhand der Werte der `O_ORDERKEY`-Spalte sortiert wird, es sich hierbei aber um die Joinspalte des `Merge Join`-Operators handelt, stellt der „Sort“-Operator zwischen dem „Parallelism“- und dem „Merge Join“-Operator sicher, dass die Eingabe für den `Merge Join`-Operator auf der Basis der Joinspalten sortiert wird. Der `Sort`-Operator wird wie der „Merge Join“-Operator parallel ausgeführt.

Der oberste „Parallelism“-Operator fasst die Ergebnisse von mehreren Datenströmen in einem einzigen Datenstrom zusammen. Teilaggregationen, die vom „Stream Aggregate“-Operator unterhalb des „Parallelism“-Operators vorgenommen werden, werden dann in dem „Stream Aggregate“-Operator oberhalb des „Parallelism“-Operators zu einem einzigen `SUM`-Wert für jeden Wert von `O_ORDERPRIORITY` aufsummiert. Dieser Plan verwendet acht Arbeisthreads, da er zwei Austauschsegmente mit einem Parallelitätsgrad von 4 besitzt.

### <a name="parallel-index-operations"></a>Parallele Indexvorgänge

Die für das Erstellen oder Neuerstellen eines Indexes bzw. für das Löschen eines gruppierten Indexes erstellten Abfragepläne ermöglichen parallele Threadvorgänge mit mehreren Workern auf Computern, die über mehrere Mikroprozessoren verfügen.

> [!NOTE]
> Parallele Indexvorgänge sind nur in Enterprise Edition ab [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] verfügbar.
 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet die gleichen Algorithmen wie bei anderen Abfragen, um den Grad an Parallelität (die Gesamtzahl der separaten Arbeitsthreads, die ausgeführt werden sollen) für Indexvorgänge zu ermitteln. Der maximale Grad an Parallelität für einen Indexvorgang hängt von der Serverkonfigurationsoption [Max. Grad an Parallelität](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) ab. Der Wert „Max. Grad an Parallelität“ kann für einzelne Indexvorgänge überschrieben werden; legen Sie hierzu die MAXDOP-Indexoption in den Anweisungen CREATE INDEX, ALTER INDEX, DROP INDEX und ALTER TABLE fest.

Wenn [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] einen Indexausführungsplan erstellt, wird die Anzahl der parallelen Vorgänge auf den niedrigsten der folgenden Werte festgelegt: 

* Die Anzahl der Mikroprozessoren (oder CPUs) des Computers.
* Die in der Serverkonfigurationsoption „Max. Grad an Parallelität“ angegebene Anzahl.
* Die Anzahl der CPUs, die nicht bereits einen Schwellenwert an Arbeit überschritten haben, die für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Arbeitsthreads durchgeführt wird.

Auf einem Computer mit acht CPUs und einem Wert für „Max. Grad an Parallelität“ in Höhe von 6 werden z.B. maximal sechs parallele Arbeitsthreads für einen Indexvorgang generiert. Falls fünf der CPUs in dem Computer bereits den Schwellenwert von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Arbeit überschritten haben, wenn ein Indexausführungsplan erstellt wird, legt der Ausführungsplan nur drei parallele Arbeitsthreads fest.

Die Hauptphasen eines parallelen Indexvorgangs umfassen Folgendes: 

* Ein koordinierender Arbeitsthread scannt die Tabelle schnell und nach dem Zufallsprinzip, um die Verteilung der Indexschlüssel einzuschätzen. Der koordinierende Arbeitsthread legt die Schlüsselgrenzen fest, die eine Reihe von Schlüsselbereichen erstellen, die dem Grad an parallelen Vorgängen entsprechen, wobei jeder Schlüsselbereich so geschätzt wird, dass eine ähnlich große Anzahl von Zeilen abgedeckt ist. Wenn z.B. vier Millionen Zeilen in einer Tabelle vorhanden sind und der Grad an Parallelität 4 beträgt, bestimmt der koordinierende Arbeitsthread die Schlüsselwerte, die vier Zeilengruppen mit je einer Million Zeilen in jeder Gruppe trennen. Wenn nicht genügend Schlüsselbereiche für die Verwendung aller CPUs eingerichtet werden können, wird der Grad an Parallelität entsprechend verringert.  
* Der koordinierende Arbeitsthread verteilt eine Reihe von Arbeitsthreads, die dem Grad an parallelen Vorgängen entsprechen, und wartet, dass diese Arbeitsthreads ihre Arbeit beenden. Jeder Arbeitsthread scannt die Basistabelle mithilfe eines Filters, der nur Zeilen mit Schlüsselwerten in dem Bereich abruft, der dem Arbeitsthread zugewiesen ist. Jeder Arbeitsthread erstellt eine Indexstruktur für die Zeilen in seinem Schlüsselbereich. Bei einem partitionierten Index erstellt jeder Arbeitsthread eine angegebene Anzahl an Partitionen. Partitionen werden nicht für Arbeitsthreads freigegeben.  
* Nachdem alle parallelen Arbeitsthreads abgeschlossen sind, verbindet der koordinierende Arbeitsthread die Untereinheiten des Indexes zu einem einzelnen Index. Diese Phase gilt nur für Offline-Indexvorgänge.

Einzelne `CREATE TABLE` - oder `ALTER TABLE` -Anweisungen können über mehrere Einschränkungen verfügen, die die Erstellung eines Indexes erforderlich machen. Diese mehrfachen Indexerstellungsvorgänge werden seriell durchgeführt, obwohl jeder einzelne Indexerstellungsvorgang auf einem Computer mit mehreren CPUs als paralleler Vorgang ausgeführt werden kann.

## <a name="distributted-query-architecture"></a>Architektur verteilter Abfragen

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt zwei Methoden, um auf heterogene OLE DB-Datenquellen in Transact-SQL-Anweisungen zu verweisen:

* Verbindungsservernamen  
  Mithilfe der gespeicherten Systemprozeduren `sp_addlinkedserver` und `sp_addlinkedsrvlogin` kann einer OLE DB-Datenquelle ein Servername zugewiesen werden. Auf Objekte in diesen Verbindungsservern kann in Transact-SQL-Anweisungen mithilfe von aus vier Teilen bestehenden Namen verwiesen werden. Wenn z.B. der Verbindungsservername `DeptSQLSrvr` für eine andere Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] definiert wird, verweist die folgende Anweisung auf eine Tabelle auf diesem Server: 
  
  ```tsql
  SELECT JobTitle, HireDate 
  FROM DeptSQLSrvr.AdventureWorks2014.HumanResources.Employee;
  ```

   Der Verbindungsservername kann auch in einer `OPENQUERY` -Anweisung angegeben werden, um ein Rowset aus einer OLE DB-Datenquelle zu öffnen. In Transact-SQL-Anweisungen kann dann auf dieses Rowset wie auf eine Tabelle verwiesen werden. 

* Ad-hoc-Konnektornamen  
  Für seltene Verweise auf eine Datenquelle wird die `OPENROWSET` - oder `OPENDATASOURCE` -Funktion zusammen mit den Informationen angegeben, die zum Herstellen einer Verbindung mit dem Verbindungsserver erforderlich sind. Auf das Rowset kann dann auf die gleiche Weise verwiesen werden, wie auf eine Tabelle in Transact-SQL-Anweisungen verwiesen wird: 
  
  ```tsql
  SELECT *
  FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',
        'c:\MSOffice\Access\Samples\Northwind.mdb';'Admin';'';
        Employees);
  ```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet OLE DB für die Kommunikation zwischen dem relationalen Modul und dem Speichermodul. Das relationale Modul zerlegt jede Transact-SQL-Anweisung in eine Reihe von Vorgängen für einfache OLE DB-Rowsets, die durch das Speichermodul aus den Basistabellen geöffnet werden. Dies bedeutet, dass das relationale Modul einfache OLE DB-Rowsets auch für jede OLE DB-Datenquelle öffnen kann.  
![oledb_storage](../relational-databases/media/oledb-storage.gif)  
Das relationale Modul verwendet die OLE DB-API (Application Programming Interface), um die Rowsets auf Verbindungsservern zu öffnen, die Zeilen abzurufen und Transaktionen zu verwalten.

Auf dem Server, auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird, muss für jede OLE DB-Datenquelle, auf die als Verbindungsserver zugegriffen wird, ein OLE DB-Anbieter vorhanden sein. Die Reihe von Transact-SQL-Vorgängen, die für eine bestimmte OLE DB-Datenquelle angewendet werden können, wird durch die Funktionalität des OLE DB-Anbieters bestimmt.

Mitglieder der festen Serverrolle `sysadmin` können mithilfe der `DisallowAdhocAccess`-Eigenschaft in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Ad-hoc-Konnektornamen für einen OLE DB-Anbieter in jeder Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aktivieren oder deaktivieren. Bei aktiviertem Ad-hoc-Zugriff kann ein beliebiger Benutzer, der bei der Instanz angemeldet ist, SQL-Anweisungen mit Ad-hoc-Konnektornamen ausführen, die auf eine beliebige Datenquelle im Netzwerk verweisen, und mithilfe dieses OLE DB-Anbieters auf diese Datenquellen zugreifen. Mitglieder der `sysadmin` -Rolle können zum Steuern des Zugriffs auf Datenquellen den Ad-hoc-Zugriff auf diesen OLE DB-Anbieter deaktivieren. Auf diese Weise können Benutzer lediglich auf diejenigen Datenquellen zugreifen, auf die mit den von den Administratoren definierten Verbindungsservernamen verwiesen wird. Standardmäßig ist der Ad-hoc-Zugriff für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-OLE DB-Anbieter aktiviert und für alle anderen OLE DB-Anbieter deaktiviert.

Mithilfe von verteilten Abfragen kann Benutzern der Zugriff auf andere Datenquellen gewährt werden (z.B. auf Dateien, nicht relationale Datenquellen wie Active Directory usw.). Dies geschieht innerhalb des Sicherheitskontexts des Microsoft Windows-Kontos, mit dem der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Dienst ausgeführt wird. Bei Windows-Anmeldungen nimmt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Identität der Anmeldung ordnungsgemäß an; dies ist jedoch bei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Anmeldungen nicht möglich. Auf diese Weise ist es einem Benutzer, der verteilte Abfragen ausführt, potenziell möglich, auf eine andere Datenquelle zuzugreifen, für die er selbst keine Berechtigungen hat, wohl aber das Konto, unter dem der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Dienst ausgeführt wird. Verwenden Sie `sp_addlinkedsrvlogin` , um spezifische Anmeldungen mit Zugriffsrechten für die entsprechenden Verbindungsserver zu definieren. Diese Steuerung ist nicht für Ad-hoc-Namen verfügbar. Sie sollten daher sehr sorgfältig beim Aktivieren eines OLE DB-Anbieters für den Ad-hoc-Zugriff sein.

Wenn möglich, verlagert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] relationale Vorgänge wie Joins, Einschränkungen, Projektionen, Sortierungen und Gruppierungen auf die OLE DB-Datenquelle. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] liest die Basistabellen nicht standardmäßig in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ein, um die relationalen Vorgänge selbst durchzuführen. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fragt den OLE DB-Anbieter ab, um zu ermitteln, welche Ebene der SQL-Grammatik er unterstützt, und sendet auf der Grundlage dieser Informationen so viele relationale Vorgänge wie möglich an den Anbieter. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gibt einen Mechanismus an, mit dem ein OLE DB-Anbieter Statistiken zur Verteilung von Schlüsselwerten innerhalb der OLE DB-Datenquelle zurückgibt. So kann der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Abfrageoptimierer das Datenmuster in der Datenquelle im Hinblick auf die Anforderungen jeder SQL-Anweisung besser analysieren, wodurch der Abfrageoptimierer besser in der Lage ist, optimale Ausführungspläne zu generieren. 

## <a name="query-processing-enhancements-on-partitioned-tables-and-indexes"></a>Verbesserte Abfrageverarbeitung bei partitionierten Tabellen und Indizes

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2008 hat für viele parallele Pläne eine bessere Leistung bei der Verarbeitung von Abfragen in partitionierten Tabellen, eine geänderte Art der Darstellung paralleler und serieller Pläne und bessere Partitionierungsinformationen in Kompilierzeit- und Laufzeitausführungsplänen ermöglicht. In diesem Thema werden diese Verbesserungen vorgestellt. Außerdem erhalten Sie Hinweise zur Interpretation der Abfrageausführungspläne für partitionierte Tabellen und Indizes sowie zu bewährten Methoden zur Verbesserung der Abfrageleistung bei partitionierten Objekten. 

> [!NOTE]
> Partitionierte Tabellen und Indizes werden nur in der Enterprise Edition, Developer Edition und Evaluation Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt.

### <a name="new-partition-aware-seek-operation"></a>Neuer partitionsgerichteter Suchvorgang (SEEK)

In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird die interne Darstellung einer partitionierten Tabelle so geändert, dass der Abfrageprozessor die Tabelle für einen mehrspaltigen Index mit `PartitionID` als führender Spalte hält. `PartitionID` ist eine verborgene berechnete Spalte, die intern die `ID` der Partition, die eine bestimmte Zeile enthält, repräsentiert. Beispiel: Die Tabelle T, die als `T(a, b, c)`definiert ist, wird in Spalte a partitioniert und enthält in Spalte b einen gruppierten Index. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird diese partitionierte Tabelle intern als nicht partitionierte Tabelle mit dem Schema `T(PartitionID, a, b, c)` und einem gruppierten Index im zusammengesetzten Schlüssel `(PartitionID, b)` behandelt. Auf diese Weise kann der Abfrageoptimierer Suchvorgänge basierend auf `PartitionID` in allen partitionierten Tabellen und Indizes durchführen. 

Die Partitionsentfernung wird jetzt im Suchvorgang vorgenommen.

Außerdem wurde der Abfrageoptimierer so erweitert, dass jetzt zunächst ein Such- oder Scanvorgang mit einer Bedingung für `PartitionID` (als logischer führender Spalte) und ggf. für weitere Indexschlüsselspalten durchgeführt werden kann. Anschließend wird dann für jeden eindeutigen Wert, der die Kriterien des Suchvorgangs der ersten Ebene erfüllt hat, ein Suchvorgang der zweiten Ebene mit einer anderen Bedingung in einer oder mehreren zusätzlichen Spalten durchgeführt. Dies bedeutet, dass mit diesem Vorgang, der Skip-Scan genannt wird, der Abfrageoptimierer basierend auf einer Bedingung zunächst einen Such- bzw. Scanvorgang durchführen kann, mit dem die Partitionen ermittelt werden, auf die zugegriffen werden muss, und dann innerhalb dieses Operators einen Indexsuchvorgang der zweiten Ebene, durch den Zeilen in diesen Partitionen zurückgegeben werden, die eine andere Bedingung erfüllen. Sehen Sie sich zum Beispiel die folgende Abfrage an:

```tsql
SELECT * FROM T WHERE a < 10 and b = 2;
```

Gehen Sie nun davon aus, dass die Tabelle T, die als `T(a, b, c)`definiert ist, in Spalte a partitioniert wird und in Spalte b einen gruppierten Index enthält. Die Partitionsgrenzen für Tabelle T werden mit der folgenden Partitionsfunktion definiert:

```tsql
CREATE PARTITION FUNCTION myRangePF1 (int) AS RANGE LEFT FOR VALUES (3, 7, 10);
```

Zur Auflösung der Abfrage führt der Abfrageprozessor zunächst einen Suchvorgang der ersten Ebene durch, in dem alle Partitionen mit Zeilen, die die Bedingung `T.a < 10`erfüllen, gesucht werden. Hierdurch werden die Partitionen identifiziert, auf die zugegriffen werden muss. In diesen identifizierten Partitionen führt der Prozessor dann einen Suchvorgang der zweiten Ebene im gruppierten Index der Spalte b durch, um die Zeilen zu suchen, die die Bedingung `T.b = 2` und `T.a < 10`erfüllen. 

Die folgende Abbildung ist eine logische Darstellung des Skip-Scan-Vorgangs. Sie zeigt die Tabelle T mit Daten in den Spalten a und b. Die Partitionen sind mit 1 bis 4 nummeriert, wobei die Partitionsgrenzen durch gestrichelte vertikale Linien angezeigt werden. Durch einen Suchvorgang der ersten Ebene in den Partitionen (nicht abgebildet) wurde ermittelt, dass die Partitionen 1, 2 und 3 die Suchbedingung, die durch die für die Tabelle definierte Partitionierung und das Prädikat für Spalte a vorgegeben wurde, erfüllen. Das heißt, sie erfüllen die Bedingung `T.a < 10`. Der vom Suchvorgang der zweiten Ebene innerhalb des Skip-Scan-Vorgangs durchlaufene Pfad ist anhand der Kurve zu erkennen. Im Wesentlichen wird beim Skip-Scan-Vorgang in diesen Partitionen nach Zeilen gesucht, die die Bedingung `b = 2`erfüllen. Die Gesamtkosten für den Skip-Scan-Vorgang entsprechen den Kosten, die durch drei separate Indexsuchvorgänge entstehen würden.   

![skip_scan](../relational-databases/media/skip-scan.gif)

### <a name="displaying-partitioning-information-in-query-execution-plans"></a>Anzeigen von Partitionierungsinformationen in Abfrageausführungsplänen

Sie können die Ausführungspläne für Abfragen in partitionierten Tabellen und Indizes überprüfen, indem Sie die Transact-SQL `SET`-Anweisung `SET SHOWPLAN_XML` bzw. `SET STATISTICS XML` ausführen oder den in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio ausgegebenen grafischen Ausführungsplan verwenden. So können Sie zum Beispiel den Ausführungsplan für die Kompilierzeit anzeigen, indem Sie auf der Abfrage-Editor-Symbolleiste auf *Geschätzten Ausführungsplan anzeigen* klicken, und den Laufzeitplan, indem Sie auf *Tatsächlichen Ausführungsplan einschließen*klicken. 

Mit diesen Tools können Sie die folgenden Informationen abrufen:

* Die Vorgänge, wie z.B. `scans`, `seeks`, `inserts`, `updates`, `merges`und `deletes` , bei denen auf partitionierte Tabellen oder Indizes zugegriffen wird.
* Die Partitionen, auf die durch die Abfrage zugegriffen wird. So finden sich zum Beispiel in Ausführungsplänen für die Laufzeit Informationen zur Gesamtanzahl der Partitionen sowie zu den Bereichen angrenzender Partitionen, auf die zugegriffen wird.
* Wann Skip-Scan in einem Such- bzw. Scanvorgang verwendet wird, um Daten aus einer oder mehreren Partitionen abzurufen.

#### <a name="partition-information-enhancements"></a>Bessere Partitionierungsinformationen

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] stellt verbesserte Partitionierungsinformationen sowohl für Kompilierzeit- als auch für Laufzeitausführungspläne bereit. Die Ausführungspläne enthalten jetzt die folgenden Informationen:

* Ein optionales `Partitioned` -Attribut, das anzeigt, dass für eine partitionierte Tabelle ein Operator wie `seek`, `scan`, `insert`, `update`, `merge`oder `delete`ausgeführt wird.  
* Ein neues `SeekPredicateNew` -Element mit einem `SeekKeys` -Unterelement, das `PartitionID` als führende Indexschlüsselspalte sowie Filterbedingungen enthält, mit denen Bereichssuchen für `PartitionID`festgelegt werden. Das Vorhandensein von zwei `SeekKeys` -Unterelementen zeigt an, dass für `PartitionID` ein Skip-Scan-Vorgang verwendet wird.   
* Zusammenfassende Informationen mit der Gesamtanzahl der Partitionen, auf die zugegriffen wird. Diese Informationen sind nur in Laufzeitplänen verfügbar. 

Nehmen Sie die folgende Abfrage für die partitionierte Tabelle `fact_sales`als Beispiel zur Veranschaulichung, wie diese Informationen im grafischen Ausführungsplan und in der XML-Showplanausgabe angezeigt werden. Durch diese Abfrage werden Daten in zwei Partitionen aktualisiert. 

```tsql
UPDATE fact_sales
SET quantity = quantity * 2
WHERE date_id BETWEEN 20080802 AND 20080902;
```

Die folgende Abbildung zeigt die Eigenschaften des `Clustered Index Seek` -Operators im Kompilierzeitausführungsplan für diese Abfrage. Die Definition der Tabelle `fact_sales` und die Partitionsdefinition finden Sie in diesem Thema im Abschnitt „Beispiel“.  

![clustered_index_seek](../relational-databases/media/clustered-index-seek.gif)

#### <a name="partitioned-attribute"></a>Das Partitioned-Attribut

Wenn ein Operator wie `Index Seek` für eine partitionierte Tabelle oder einen partitionierten Index ausgeführt wird, enthalten der Kompilierzeit- und der Laufzeitausführungsplan das Attribut `Partitioned` , das auf `True` (1) festgelegt wird. Das Attribut wird nicht angezeigt, wenn es auf `False` (0) gesetzt ist.

Das `Partitioned` -Attribut kann in den folgenden physischen und logischen Operatoren erscheinen:  
* `Table Scan`  
* `Index Scan`  
* `Index Seek`  
* `Insert`  
* `Update`  
* `Delete`  
* `Merge`  

Wie in der obigen Abbildung zu sehen, wird das Attribut in den Eigenschaften des Operators, in dem es definiert ist, angezeigt. In der XML-Showplanausgabe erscheint das Attribut als `Partitioned="1"` im `RelOp` -Knoten des Operators, in dem es definiert ist.

#### <a name="new-seek-predicate"></a>Neues Suchprädikat (SEEK-Prädikat)

In der XML-Showplanausgabe wird das `SeekPredicateNew` -Element in dem Operator angezeigt, in dem es definiert ist. Das Element kann maximal zwei Instanzen des `SeekKeys` -Unterelements enthalten. Durch das erste `SeekKeys` -Element wird der Suchvorgang (SEEK) auf erster Ebene für die Partitions-ID des logischen Index angegeben. In diesem Suchvorgang werden die Partitionen ermittelt, auf die zugegriffen werden muss, damit die Bedingungen der Abfrage erfüllt werden können. Durch das zweite `SeekKeys` -Element wird der Suchvorgang auf zweiter Ebene innerhalb des Skip-Scan-Vorgangs festgelegt, der in allen Partitionen durchgeführt wird, die im ersten Suchvorgang identifiziert wurden. 

#### <a name="partition-summary-information"></a>Zusammenfassende Partitionsinformationen

In Laufzeitausführungsplänen geben die zusammenfassenden Partitionsinformationen Auskunft darüber, auf wie viele und auf welche Partitionen zugegriffen wird. Anhand dieser Informationen können Sie überprüfen, ob in der Abfrage auf die richtigen Partitionen zugegriffen wird und ob alle anderen Partitionen vom Zugriff ausgenommen werden.

Die folgenden Informationen werden bereitgestellt: `Actual Partition Count`und `Partitions Accessed`. 

`Actual Partition Count` ist die Gesamtzahl der Partitionen, auf die durch die Abfrage zugegriffen wird.

`Partitions Accessed`ist in der XML-Showplanausgabe die Übersichtsinformation zur Partition, die im neuen `RuntimePartitionSummary` -Element im `RelOp` -Knoten des Operators, in dem sie definiert ist, erscheint. Das folgende Beispiel zeigt den Inhalt des `RuntimePartitionSummary` -Elements, durch den angegeben wird, dass auf insgesamt zwei Partitionen (Partition 2 und 3) zugegriffen wird.
```
<RunTimePartitionSummary>

    <PartitionsAccessed PartitionCount="2" >

        <PartitionRange Start="2" End="3" />

    </PartitionsAccessed>

</RunTimePartitionSummary>
```

#### <a name="displaying-partition-information-by-using-other-showplan-methods"></a>Anzeigen von Partitionsinformationen mittels anderer Showplan-Methoden

Die Showplanmethoden `SHOWPLAN_ALL`, `SHOWPLAN_TEXT`und `STATISTICS PROFILE` stellen keine der in diesem Thema beschriebenen Partitionsinformationen bereit, mit der folgenden Ausnahme. Als Teil des `SEEK` -Prädikats werden die Partitionen, auf die zugegriffen werden muss, durch ein Bereichsprädikat für die berechnete Spalte, die die Partitions-ID repräsentiert, identifiziert. Das folgende Beispiel zeigt das `SEEK` -Prädikat für einen `Clustered Index Seek` -Operator. Es wird auf die Partitionen 2 und 3 zugegriffen, und der SEEK-Operator filtert die Zeilen heraus, die die Bedingung `date_id BETWEEN 20080802 AND 20080902`erfüllen.
```
|--Clustered Index Seek(OBJECT:([db_sales_test].[dbo].[fact_sales].[ci]), 

        SEEK:([PtnId1000] >= (2) AND [PtnId1000] \<= (3) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] >= (20080802) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] <= (20080902)) 

                ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-partitioned-heaps"></a>Interpretieren von Ausführungsplänen für partitionierte Heaps

Ein partitionierter Heap wird als logischer Index für die Partitions-ID behandelt. Die Partitionsentfernung für einen partitionierten Heap wird in einem Ausführungsplan als `Table Scan` -Operator mit einem `SEEK` -Prädikat für die Partitions-ID dargestellt. Das folgende Beispiel zeigt die bereitgestellten Showplan-Informationen:
```
|-- Table Scan (OBJECT: ([db].[dbo].[T]), SEEK: ([PtnId1001]=[Expr1011]) ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-collocated-joins"></a>Interpretieren von Ausführungsplänen für angeordnete Joins

Eine Anordnung von Joins kann eintreten, wenn zwei Tabellen mit derselben oder einer ähnlichen Partitionsfunktion partitioniert und die Partitionierungsspalten auf beiden Seiten des Joins in der Join-Bedingung der Abfrage angegeben werden. Der Abfrageoptimierer kann einen Plan erzeugen, in dem die Partitionen aller Tabellen mit identischer Partitions-ID separat verknüpft werden. Angeordnete Joins sind jedoch möglicherweise schneller als nicht angeordnete, da sie ggf. weniger Arbeitsspeicher und weniger Verarbeitungszeit benötigen. Die Entscheidung, ob ein Plan für nicht angeordnete oder angeordnete Joins erzeugt wird, fällt auf Grundlage der geschätzten Kosten.

Bei einem Plan für angeordnete Joins liest der `Nested Loops` -Join eine oder mehrere zusammengefasste Tabellen- oder Indexpartitionen auf der Innenseite. Die Zahlen in den `Constant Scan` -Operatoren repräsentieren die Partitionsnummern. 

Wenn parallele Pläne für angeordnete Joins für partitionierte Tabellen oder Indizes erzeugt werden, wird ein Parallelism-Operator zwischen dem `Constant Scan` -Joinoperator und dem `Nested Loops` -Joinoperator eingefügt. In diesem Fall lesen und bearbeiten mehrere Arbeitsthreads auf der Außenseite des Joins jeweils eine andere Partition. 

Die folgende Abbildung zeigt einen parallelen Abfrageplan für einen angeordneten Join.   
![colocated_join](../relational-databases/media/colocated-join.gif)


#### <a name="parallel-query-execution-strategy-for-partitioned-objects"></a>Parallele Ausführungsstrategie für Abfragen bei partitionierten Objekten

Der Abfrageprozessor verwendet eine parallele Ausführungsstrategie für Abfragen bei partitionierten Objekten. Im Rahmen dieser Ausführungsstrategie ermittelt der Abfrageprozessor die für die Abfrage erforderlichen Tabellenpartitionen und die den einzelnen Partitionen zugewiesenen Arbeitsthreadanteile. In den meisten Fällen ordnet der Abfrageprozessor den einzelnen Partitionen eine etwa gleich große Anzahl an Arbeitsthreads zu und führt anschließend die Abfrage partitionsübergreifend parallel aus. In den folgenden Absätzen wird die Arbeitsthreadzuordnung näher erläutert.  

![arbeisthread1](../relational-databases/media/thread1.gif)

Wenn die Arbeitsthreadanzahl kleiner ist als die Partitionsanzahl, ordnet der Abfrageprozessor jeden Arbeitsthread einer anderen Partition zu, und zunächst verbleiben eine oder mehrere Partitionen ohne Arbeitsthreadzuordnung. Wenn die Ausführung eines Arbeitsthreads für eine Partition abgeschlossen ist, weist der Abfrageprozessor diesen der nächsten Partition zu, bis jeder Partition ein Arbeitsthread zugewiesen wurde. Dies ist der einzige Fall, in dem der Abfrageprozessor Arbeitsthreads anderen Partitionen neu zuordnet.  
Zeigt einen Arbeitsthread, der nach seinem Abschluss erneut zugeordnet wurde Wenn die Anzahl an Arbeitsthreads und an Partitionen gleich ist, wird jeder Partition ein Arbeitsthread zugewiesen. Abgeschlossene Arbeitsthreads werden nicht erneut zugeordnet.  

![arbeitsthread2](../relational-databases/media/thread2.gif)  

Wenn die Arbeitsthreadanzahl größer ist als die Partitionsanzahl, wird jeder Partition dieselbe Anzahl an Arbeitsthreads zugewiesen. Falls es sich bei der Anzahl an Arbeitsthreads nicht um ein Vielfaches der Anzahl an Partitionen handelt, weist der Abfrageprozessor einigen Partitionen einen weiteren Arbeitsthread zu, sodass alle verfügbaren Arbeitsthreads verwendet werden. Wenn nur eine Partition vorhanden ist, werden alle Arbeitsthreads dieser Partition zugewiesen. In der Abbildung unten sind vier Partitionen und 14 Arbeitsthreads verfügbar. Jeder Partition werden drei Arbeitsthreads zugewiesen, und zwei Partitionen wird jeweils ein zusätzlicher Arbeitsthread zugewiesen, sodass alle 14 Arbeitsthreads zugewiesen sind. Abgeschlossene Arbeitsthreads werden nicht erneut zugeordnet.  

![arbeitsthread3](../relational-databases/media/thread3.gif)  

Die oben aufgeführten Beispiele sind einfache Beschreibungen der Arbeitsthreadzuordnung. Die tatsächliche Strategie ist komplexer und umfasst weitere Variablen, die sich während der Abfrageausführung ergeben. Beispiel: Wenn die Tabelle partitioniert ist, in Spalte A einen gruppierten Index aufweist und eine Abfrage mit der Prädikatklausel `WHERE A IN (13, 17, 25)`verwendet wird, weist der Abfrageprozessor jedem dieser drei Suchwerte (A=13, A=17 und A=25) statt jeder Tabellenpartition einen oder mehrere Arbeitsthreads zu. Die Abfrage muss nur für die Partitionen ausgeführt werden, die diese Werte enthalten. Wenn sich alle Suchwerte in derselben Partition befinden, werden alle Arbeitsthreads dieser Partition zugewiesen.

Ein weiteres Beispiel: Die Tabelle weist vier Partitionen in Spalte A mit Grenzpunkten (10, 20, 30) sowie einen Index in Spalte B auf, und für die Abfrage wird folgende Prädikatklausel verwendet: `WHERE B IN (50, 100, 150)`. Da die Tabellenpartitionen auf den A-Werten basieren, können die B-Werte in allen Tabellenpartitionen enthalten sein. Somit sucht der Abfrageprozessor in jeder der vier Tabellenpartitionen nach jedem der drei B-Werte (50, 100, 150). Der Abfrageprozessor weist Arbeitsthreads proportional zu, sodass alle zwölf Abfragesuchläufe parallel ausgeführt werden können.

|Tabellenpartitionen auf Grundlage der Spalte A    |Suche in allen Tabellenpartitionen nach B-Spaltenwerten |
|----|----|
|Tabellenpartition 1: A < 10     |B=50, B=100, B=150 |
|Tabellenpartition 2: A >= 10 AND A < 20     |B=50, B=100, B=150 |
|Tabellenpartition 3: A >= 20 AND A < 30     |B=50, B=100, B=150 |
|Tabellenpartition 4: A >= 30     |B=50, B=100, B=150 |

### <a name="best-practices"></a>Bewährte Methoden

Wir empfehlen die folgenden bewährten Vorgehensweisen, um die Leistung von Abfragen zu verbessern, bei denen in großen partitionierten Tabellen und Indizes auf eine große Menge von Daten zugegriffen wird:

* Verteilen Sie alle Partitionen über viele Datenträger (Datenträgerstriping).
* Verwenden Sie möglichst einen Server mit einem Hauptspeicher, der groß genug ist für Partitionen, auf die häufig zugegriffen wird, bzw. für alle Partitionen, um die E/A-Kosten zu senken.
* Falls die abgefragten Daten nicht in den Arbeitsspeicher passen, komprimieren Sie die Tabellen und Indizes. Dies reduziert die E/A-Kosten.
* Verwenden Sie einen Server mit schnellen und möglichst vielen Prozessoren, um sich die Vorteile der parallelen Abfrageverarbeitung zu Nutze zu machen.
* Stellen Sie sicher, dass der Server über eine ausreichend große E/A-Controllerbandbreite verfügt. 
* Erstellen Sie für jede große partitionierte Tabelle einen gruppierten Index, um den optimierten B-Strukturscan voll nutzen zu können.
* Beachten Sie die Empfehlungen für bewährte Vorgehensweisen im Whitepaper [Loading Bulk Data into a Partitioned Table](http://go.microsoft.com/fwlink/?LinkId=154561)(Laden von Massendaten in eine partitionierte Tabelle), wenn Sie mittels Massenladen Daten in partitionierte Tabellen laden.

### <a name="example"></a>Beispiel

Im folgenden Beispiel wird eine Testdatenbank mit einer Tabelle, die sieben Partitionen aufweist, erstellt. Verwenden Sie die zuvor in diesem Thema vorgestellten Tools, wenn Sie die Abfragen in diesem Beispiel durchführen, um Partitionierungsinformationen für den Kompilierungszeitplan und den Laufzeitplan anzuzeigen. 

> [!NOTE]
> In diesem Beispiel werden über eine Millionen Zeilen in die Tabelle eingefügt. Je nach Hardware kann die Ausführung dieses Beispiels einige Minuten dauern. Stellen Sie vor dem Ausführen dieses Beispiels sicher, dass mehr als 1,5 GB Speicherplatz zur Verfügung stehen. 
 
```tsql
USE master;
GO
IF DB_ID (N'db_sales_test') IS NOT NULL
    DROP DATABASE db_sales_test;
GO
CREATE DATABASE db_sales_test;
GO
USE db_sales_test;
GO
CREATE PARTITION FUNCTION [pf_range_fact](int) AS RANGE RIGHT FOR VALUES 
(20080801, 20080901, 20081001, 20081101, 20081201, 20090101);
GO
CREATE PARTITION SCHEME [ps_fact_sales] AS PARTITION [pf_range_fact] 
ALL TO ([PRIMARY]);
GO
CREATE TABLE fact_sales(date_id int, product_id int, store_id int, 
    quantity int, unit_price numeric(7,2), other_data char(1000))
ON ps_fact_sales(date_id);
GO
CREATE CLUSTERED INDEX ci ON fact_sales(date_id);
GO
PRINT 'Loading...';
SET NOCOUNT ON;
DECLARE @i int;
SET @i = 1;
WHILE (@i<1000000)
BEGIN
    INSERT INTO fact_sales VALUES(20080800 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
GO
DECLARE @i int;
SET @i = 1;
WHILE (@i<10000)
BEGIN
    INSERT INTO fact_sales VALUES(20080900 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
PRINT 'Done.';
GO
-- Two-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080802 AND 20080902
GROUP BY date_id ;
GO
SET STATISTICS XML OFF;
GO
-- Single-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080801 AND 20080831
GROUP BY date_id;
GO
SET STATISTICS XML OFF;
GO
```

##  <a name="Additional_Reading"></a> Zusätzliches Lesematerial  
 [Referenz zu logischen und physischen Showplanoperatoren](../relational-databases/showplan-logical-and-physical-operators-reference.md)  
 [Erweiterte Ereignisse](../relational-databases/extended-events/extended-events.md)

