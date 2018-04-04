---
title: Leistung für R Services – datenoptimierung | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 6b320357d8978a97878d31943b48accee8898f9f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="performance-for-r-services---data-optimization"></a>Leistung für R Services – Data-Optimierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist die dritte in einer Reihe, die zur leistungsoptimierung für R-Dienste basierend auf zwei Fallstudien beschreibt. Dieser Artikel beschreibt die leistungsoptimierungen für R oder Python-Skripts, die in SQL Server ausgeführt. Es beschreibt auch Methoden, die Sie verwenden können, aktualisieren Sie Ihre R-Code, zur Verbesserung der Leistung und bekannte Probleme zu vermeiden.

## <a name="choosing-a-compute-context"></a>Wählen einen computekontext.

In SQL Server 2016 und 2017, verwenden Sie entweder die **lokale** oder **SQL** Kontext beim Ausführen von R oder Python-Skript zu berechnen.

Bei Verwendung der **lokale** computekontext, Analyse wird ausgeführt, auf dem Computer und nicht auf dem Server. Wenn Sie Daten aus SQL Server in Ihrem Code verwendet werden, müssen daher die Daten über das Netzwerk abgerufen werden. Die Leistungseinbußen für diesen Netzwerkübertragung hängen von der Größe der übertragenen Daten, dem Geschwindigkeit des Netzwerks und anderen Netzwerkübertragungen ab, die zur gleichen Zeit auftreten.

Bei Verwendung der **SQL Server-computekontext**, der Code auf dem Server ausgeführt wird. Wenn Sie Daten aus SQL Server abrufen, die Daten lokal auf dem Server, der die Analyse ausgeführt werden sollen, und aus diesem Grund wird kein Netzwerkaufwand eingeführt. Wenn Sie Daten aus anderen Quellen importieren müssen, sollten Sie ETL im Vorfeld anordnen.

Bei der Arbeit mit großen Datenmengen sollten Sie immer den SQL Compute Context verwenden.

## <a name="factors"></a>Faktoren

Die Sprache "R" wurde das Konzept der "Faktoren", die spezielle Variable für Kategoriedaten sind. Datenanalysten häufig Faktor Variablen in ihrer Formel verwenden, da Behandlung von kategorievariablen als Faktoren, die die Daten wird sichergestellt, dass ordnungsgemäß von Machine Learning-Funktionen verarbeitet wird. Weitere Informationen finden Sie unter [R für Anfänger: Faktor Variablen] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

Programmbedingt können Faktor Variablen in ganze Zahlen und zurück erneut zur Speicherung oder die Verarbeitung von Zeichenfolgen konvertiert werden. R `data.frame` Funktion als Faktor Variablen, alle Zeichenfolgen behandelt, es sei denn, das Argument *StringsAsFactors* festgelegt ist, um **"false"**. Was bedeutet dies, dass die Zeichenfolgen werden automatisch konvertiert in eine ganze Zahl für die Verarbeitung, und klicken Sie dann zurück an die ursprüngliche Zeichenfolge zugeordnet.

Wenn die Quelldaten für Faktoren vor, als eine ganze Zahl gespeichert werden, kann die Leistung beeinträchtigt, da R Faktor ganzen Zahlen in Zeichenfolgen, zur Laufzeit konvertiert, und dann eine eigene interne Konvertierung der Zeichenfolge in Ganzzahlwerte führt.

Um solche Konvertierungen zur Laufzeit zu vermeiden, sollten Sie die Werte als ganze Zahlen in der SQL Server-Tabelle zu speichern und Verwenden der _ColInfo_ Argument, um die Ebenen für die Spalte Faktor verwendet anzugeben. Die meisten Datenquellenobjekte im "revoscaler" akzeptieren Sie den Parameter _ColInfo_. Verwenden Sie diesen Parameter zum Benennen von Variablen, die von der Datenquelle verwendet, geben Sie ihre und definieren die Variablen Ebenen oder Transformationen auf die Spaltenwerte aus.

Z. B. die folgende R-Funktionsaufruf Ruft die ganzen Zahlen 1, 2 und 3 aus einer Tabelle, jedoch ordnet die Werte auf den Faktor mit Ebenen "Apple", "Orange" und "Banane".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Wenn die Quellspalte Zeichenfolgen enthält, es ist immer mehr effizient, geben Sie die Ebenen im Voraus den _ColInfo_ Parameter. Der folgende R-Code behandelt z. B. die Zeichenfolgen als Faktoren, wie sie gelesen werden.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Ist keine semantische Unterschiede in der modellgenerierung, kann der zweite Ansatz eine bessere Leistung führen.

## <a name="data-transformations"></a>Datentransformationen

Datenanalysten verwenden häufig Transformationsfunktionen, die als Teil der Analyse in R geschrieben werden. Die Transformation wird auf jede Zeile aus der Tabelle abgerufen angewendet. In SQL Server werden solche Transformationen angewendet, auf alle Zeilen abgerufen, die in einem Batch, der Kommunikation zwischen R-Interpreter und das Modul erforderlich ist. Zum Ausführen der Umwandlungen werden die Daten von SQL an das Datenanalysemodul und dann an den Prozess der R-Interpreter verschoben und zurück.

Aus diesem Grund kann mithilfe von Transformationen als Teil des Codes R erhebliche negative Auswirkungen auf die Leistung des Algorithmus, der abhängig vom Umfang der zu verarbeitenden Daten haben.

Es ist effizienter, alle erforderliche Spalten in der Tabelle oder Sicht, die vor dem Ausführen der Analyse haben, und vermeiden Transformationen während der Berechnung. Wenn es nicht möglich ist, zusätzliche Spalten zu vorhandenen Tabellen hinzuzufügen, können Sie eine andere Tabelle oder Ansicht mit den transformierten Spalten erstellen und eine entsprechende Abfrage zum Abrufen der Daten verwenden.

## <a name="batch-row-reads"></a>Batch-Zeile liest.

Bei Verwendung eine SQL Server-Datenquelle (`RxSqlServerData`) in Ihrem Code wird empfohlen, dass Sie versuchen, mithilfe des Parameters _RowsPerRead_ Batchgröße angeben. Dieser Parameter definiert die Anzahl der Zeilen, die abgefragt, und klicken Sie dann zur Verarbeitung an das externe Skript gesendet. Zur Laufzeit erkennt der Algorithmus nur die angegebene Anzahl von Zeilen in jedem Batch an.

Die Möglichkeit, den Umfang der Daten steuern, die gleichzeitig verarbeitet werden können Sie lösen oder Probleme zu vermeiden. Wenn die Eingabedatasets sehr breit ist beispielsweise (verfügt über viele Spalten), oder wenn das Dataset über wenige große Spalten (z. B. von freiem Text) enthält, reduzieren Sie die Batchgröße zum Auslagern von Daten aus dem Arbeitsspeicher zu vermeiden.

Standardmäßig ist der Wert dieses Parameters auf 50000 festgelegt, um ordentliche Leistung auch auf Computern mit wenig Arbeitsspeicher sicherzustellen. Wenn der Server über genügend Speicherplatz verfügt, kann durch Erhöhen dieses Werts auf 500.000 oder sogar einer Million eine bessere Leistung, insbesondere bei großen Tabellen ergeben.

Die Vorteile des zu erhöhenden Batchgröße, die offensichtlich werden, auf ein großes DataSet, und klicken Sie in eine Aufgabe, die auf mehrere Prozesse ausgeführt werden kann. Allerdings ist das Erhöhen des Werts nicht immer den besten Ergebnissen führen. Es wird empfohlen, dass Sie experimentieren Sie mit Ihren Daten und den Algorithmus, um den optimalen Wert zu bestimmen.

## <a name="parallel-processing"></a>Parallele Verarbeitung

Zum Verbessern der Leistung von **Rx** analytische Funktionen können Sie die Möglichkeit von SQL Server zum Ausführen von Tasks mithilfe der verfügbaren Kerne auf dem Servercomputer parallel nutzen.

Es gibt zwei Möglichkeiten, um die Parallelisierung mit R in SQL Server zu erreichen:

-   **Verwendung \@parallel.** Bei Verwendung der `sp_execute_external_script` gespeicherten Prozedur zur Ausführung eines R-Skripts legen Sie den `@parallel`-Parameter auf `1` fest. Dies ist die beste Methode, wenn Ihre R-Skript führt **nicht** verwenden RevoScaleR-Funktionen, die andere Mechanismen für die Verarbeitung haben. Wenn Ihr Skript verwendet die RevoScaleR-Funktionen (in der Regel mit dem Präfix "Rx"), parallele Verarbeitung automatisch ausgeführt wird und Sie nicht explizit festgelegt müssen `@parallel` auf `1`.

    Wenn das R-Skript parallelisiert werden kann, und die SQL-Abfrage parallelisiert werden kann, erstellt das Datenbankmodul mehrere parallele Prozesse. Die maximale Anzahl von Prozessen, die erstellt werden können, ist gleich der **Max. Grad an Parallelität** (MAXDOP)-Einstellung für die Instanz. Alle Prozesse dann führen Sie das gleiche Skript, sondern nur einen Teil der Daten erhalten.
    
    Diese Methode ist daher nicht nützlich sein, die Skripts, die alle Daten, z. B. Wenn Sie müssen die Trainieren eines Modells. Es ist jedoch nützlich, wenn Tasks wie die Batchvorhersage parallel ausgeführt werden. Weitere Informationen zur Verwendung von Parallelität mit `sp_execute_external_script`, finden Sie unter der **erweiterte Tipps: parallele Verarbeitung** Abschnitt [mithilfe von R-Code in Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Verwenden Sie NumTasks = 1.** Bei Verwendung **Rx** Funktionen in einer SQL Server-computekontext, legen Sie den Wert von der _NumTasks_ Parameter, um die Anzahl der Prozesse, die Sie erstellen möchten. Die Anzahl von Prozessen erstellt kann niemals mehr als **MAXDOP**; allerdings wird die tatsächliche Anzahl von Prozessen erstellt vom Datenbankmodul bestimmt und kleiner als die angefordert werden.

    Wenn das R-Skript parallelisiert werden kann, und die SQL-Abfrage parallelisiert werden kann, erstellt SQL Server mehrere parallele Prozesse, wenn die Rx-Funktionen ausgeführt. Die tatsächliche Anzahl von Prozessen, die erstellt werden, hängt von einer Vielzahl von Faktoren wie die Ressourcenkontrolle, aktuelle Verwendung von Ressourcen, die anderen Sitzungen und der Abfrageausführungsplan für die Abfrage mit dem R-Skript, ab.

## <a name="query-parallelization"></a>Parallelisierung der Abfragen

In Microsoft-R können Sie mit SQL Server-Datenquellen arbeiten, indem Ihre Daten als ein RxSqlServerData Datenquellenobjekt definieren.

Erstellt eine Datenquelle basierend auf einer gesamten Tabelle oder Sicht an:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Erstellt eine Datenquelle basierend auf einer SQL-Abfrage:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Wenn eine Tabelle in der Datenquelle nicht mit einer Abfrage angegeben ist, verwendet R Services interner Heuristik, um bestimmt die benötigten Spalten aus der Tabelle abgerufen; Dieser Ansatz ist jedoch genügt nicht parallelen Ausführung.

Um sicherzustellen, dass die Daten parallel analysiert werden können, sollten so zum Abrufen der Daten verwendete Abfrage eingeschlossen werden, dass das Datenbankmodul auf einen parallelen Abfrageplan erstellen kann. Wenn der Code oder der Algorithmus große Mengen an Daten verwendet wird, stellen sicher, dass die Abfrage übergeben, um `RxSqlServerData` ist optimiert für die parallele Ausführung. Eine Abfrage, die nicht zu einem parallelen Ausführungsplan führt, kann zu einem einzelnen Prozess für die Berechnung führen.

Wenn Sie mit großen Datasets arbeiten möchten, verwenden Sie Management Studio oder in einer anderen SQL Query Analyzer vor dem Ausführen von R-Code, um den Ausführungsplan zu analysieren. Klicken Sie dann, nehmen Sie alle empfohlenen Schritte zum Verbessern der Leistung der Abfrage. Ein fehlender Index für eine Tabelle kann z.B. die Zeit zum Ausführen einer Abfrage beeinträchtigen. Weitere Informationen finden Sie unter [überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Eine andere häufiger Fehler, der die Leistung beeinträchtigt ist, dass eine Abfrage, mehr Spalten abruft als erforderlich sind. Z. B. wenn eine Formel darauf, dass nur drei Spalten basiert, aber die Quelltabelle über 30 Spalten verfügt, verschieben Sie Daten unnötigerweise.

 + Vermeiden Sie die Verwendung `SELECT *`!
 + Nehmen Sie überprüfen die Spalten im Dataset, und identifizieren Sie nur die für die Analyse benötigt einige Zeit in Anspruch
 + Entfernen Sie aus Ihrer Abfragen keine Spalten mit Datentypen, die mit R-Code, z. B. GUIDS und ROWGUID nicht kompatibel sind
 + Kontrollkästchen für nicht unterstützte Datums- und Zeitformate
 + Anstelle eine Tabelle zu laden, erstellen Sie eine Sicht, die bestimmte Werte aktiviert bzw. deaktiviert das wandelt Spalten, um Fehler bei der Konvertierung zu vermeiden.

## <a name="optimizing-the-machine-learning-algorithm"></a>Optimieren der Machine Learning-Algorithmus

Dieser Abschnitt enthält verschiedene Tipps und Ressourcen, die für "revoscaler" und anderen Optionen im Microsoft R. spezifisch sind

> [!TIP]
> Eine allgemeine Beschreibung der R-Optimierung ist nicht Gegenstand dieses Artikels. Wenn Sie Code schneller vornehmen müssen, wir empfehlen jedoch die beliebten Artikel [der R-Inferno](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Es behandelt Programmierkonstrukten in R und häufige Fehlerquellen in lebendige Sprache und Details, und bietet viele spezifische Beispiele von R Programmierverfahren.

### <a name="optimizations-for-revoscaler"></a>Optimierungen für "revoscaler"

Viele "revoscaler"-Algorithmus unterstützen die Parameter, um zu steuern, wie das trainierte Modell generiert wird. Während die Genauigkeit und Richtigkeit des Modells ist wichtig, könnte die Leistung des Algorithmus gleichermaßen wichtig sein. Um das richtige Gleichgewicht zwischen Genauigkeit und Zeit für das Training zu erhalten, können Sie Parameter für den erhöhen die Geschwindigkeit der Berechnung und in vielen Fällen verbessern, ohne zu reduzieren, die Genauigkeit oder die Korrektheit ändern.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` unterstützt die `maxDepth` -Parameter, der die Tiefe der Entscheidungsstruktur steuert. Als `maxDepth` wird erhöht, Leistung kann beeinträchtigt werden, es ist daher wichtig, um die Vorteile der Erhöhen der Tiefe im Vergleich zu beeinträchtigt die Leistung zu analysieren.

    Sie können auch steuern, das Gleichgewicht zwischen Zeit Komplexität und Vorhersage Genauigkeit durch Anpassen der Parameter wie z. B. `maxNumBins`, `maxDepth`, `maxComplete`, und `maxSurrogate`. Das Erhöhen der Tiefe auf mehr als 10 oder 15 kann die Berechnung sehr teuer machen.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Versuchen Sie es mit der `cube` -Argument an, wenn der erste abhängige Variable in der Formel Faktor ist.
    
    Wenn `cube` festgelegt ist, um `TRUE`, die Regression erfolgt mithilfe einer partitionierte Inverse, in denen möglicherweise schneller ausgeführt und belegen weniger Speicher als standard Regression Berechnung. Wenn die Formel über eine große Anzahl von Variablen verfügt, kann die Leistungssteigerung erheblich sein.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Verwenden der `cube` -Argument an, wenn der erste abhängige Variable Faktor ist.
    
    Wenn `cube` festgelegt ist, um `TRUE`, verwendet der Algorithmus eine partitionierte Inverse, in denen möglicherweise schneller ausgeführt und belegen weniger Speicher. Wenn die Formel über eine große Anzahl von Variablen verfügt, kann die Leistungssteigerung erheblich sein.

Weitere Anleitungen zur Optimierung der "revoscaler" finden Sie in diesen Artikeln:

+ Support-Artikel: [Feineinstellungsoptionen für RxDForest und der RxDTree](https://support.microsoft.com/kb/3104235)

+ Methoden zum Steuern des Modells in einem verstärkten Strukturmodell passen: [schätzen Modelle mithilfe von Stochastic Gradient Boosting](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Überblick über "revoscaler" verschiebt und Verarbeiten von Daten: [benutzerdefinierte Algorithmen, die Aufteilung in ScaleR schreiben](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Programmiermodell für "revoscaler": [Verwalten von Threads im "revoscaler"](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referenz für die Funktion [RxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referenz für die Funktion [RxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Verwenden Sie MicrosoftML

Zudem wird empfohlen, dass Sie in das neue Aussehen **MicrosoftML** Paket, die skalierbare Machine Learning-Algorithmen bereitstellt, die die rechenkontexte und "revoscaler"-Transformationen verwendet werden kann.

+ [Erste Schritte mit MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Gewusst wie: auswählen ein Algorithmus MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Operationalisieren von einer Lösung, die mithilfe von Microsoft R Server

Wenn Ihr Szenario beinhaltet schnelle Vorhersagen mithilfe eines Modells mit gespeicherten oder Integrieren von Machine Learning in einer Anwendung aus, Sie können die [operationalisierung](https://docs.microsoft.com/r-server/what-is-operationalization) Funktionen in Microsoft R Server (ehemals DeployR).

+ Als eine **datenanalyst**, verwenden die [Mrsdeploy Paket](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) Teilen von R-Code mit anderen Computern und R Analytics in Web, Desktop, Mobil und Dashboard Anwendungen integrieren: [veröffentlichen und R-Webdienste in R-Server verwalten](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Als ein **Administrator**, erfahren Sie, wie Pakete verwalten, überwachen Sie Knoten für Web-Serverknoten und Steuern der Sicherheit auf R-Aufträge: [wie zur Interaktion und zum Verarbeiten von Webdiensten in R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artikel in dieser Serie

[Leistung optimieren für R – Einführung](sql-server-r-services-performance-tuning.md)

[Optimieren der Leistung für R - SQL Server-Konfiguration](sql-server-configuration-r-services.md)

[Optimieren der Leistung für R - R Optimierung von Code und Daten](r-and-data-optimization-r-services.md)

[Performance Tuning - Fallstudien](performance-case-study-r-services.md)
