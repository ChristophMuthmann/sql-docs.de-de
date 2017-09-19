---
title: Anzeigen und Zusammenfassen von Daten mithilfe von R (Exemplarische Vorgehensweise) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/08/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 22
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4d2da018be494691ff67b9b200a24b7c615fbbad
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="view-and-summarize-data-using-r"></a>Anzeigen und Zusammenfassen von Daten mithilfe von R

Jetzt sehen wir arbeiten mit derselben Daten mithilfe von R-Code. In dieser Lektion erfahren Sie, wie Sie die Funktionen in der **"revoscaler"** Paket.

Es wird ein R-Skript mit dieser exemplarischen Vorgehensweise bereitgestellt, das den gesamten Code enthält, der für die Erstellung des Datenobjekts, die Generierung von Zusammenfassungen und die Erstellung von Modellen erforderlich ist. Die R-Skriptdatei **RSQL_RWalkthrough.R**befindet sich an dem Speicherort, an dem Sie die Skriptdateien gespeichert haben.

+ Wenn Sie bereits über Erfahrung mit R verfügen, können Sie das Skript komplett auf einmal ausführen.
+ Für Personen, die lernen, wie Sie "revoscaler" verwenden wird das Skript zeilenweise in diesem Lernprogramm durchläuft.
+ Um einzelne Zeilen des Skripts auszuführen, können Sie eine oder mehrere Zeilen in der Datei markieren und dann STRG+EINGABETASTE drücken.

> [!TIP]
> Speichern Sie Ihren R-Arbeitsbereich im Falle, dass Sie die restliche exemplarische Vorgehensweise später abschließen möchten.  Auf diese Weise sind die Datenobjekte und andere Variablen für die erneute Verwendung bereit.

## <a name="define-a-sql-server-compute-context"></a>Definieren Sie einen SQL Server-computekontext.

Microsoft R erleichtert das Abrufen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R-Code verwenden. Der Prozess sieht folgendermaßen aus:
  
- Stellen Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz her.
- Definieren Sie eine Abfrage mit den Daten, die Sie benötigen, oder geben Sie eine Tabelle oder Sicht an.
- Definieren von einem oder mehreren Computekontexten, die beim Ausführen von R-Code verwendet werden sollen
- Definieren Sie wahlweise die Transformationen, die mit der Datenquelle angewendet werden, während es aus der Quelle gelesen werden

Die folgenden Schritte sind alle Teil der R-Code und sollte in einer R-Umgebung ausgeführt werden. Wir verwendet Microsoft R-Client, da er alle "revoscaler"-Pakete als auch einen grundlegenden, einfachen Satz von R-Tools enthält.

1. Wenn die **"revoscaler"** Paket nicht bereits geladen wird, führen Sie diese Zeile von R-Code:

    ```R
    library("RevoScaleR")
    ```

     Die Anführungszeichen sind in diesem Fall optional, jedoch empfohlen.
     
     Wenn Sie eine Fehlermeldung erhalten, stellen Sie sicher, dass Ihre R-Entwicklungsumgebung eine Bibliothek verwendet wird, die die RevoScaleR-Paket enthält. Verwenden Sie einen Befehl wie `.libPaths()` zum Anzeigen des Pfades der aktuellen Bibliothek.

2. Erstellen Sie die Verbindungszeichenfolge für SQL Server, und speichern Sie sie in einer Variablen R _ConnStr_.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=Your_Database_Name;Uid=Your_User_Name;Pwd=Your_Password"
    ```

    Für den Servernamen möglicherweise nur den Instanznamen verwenden können, oder müssen Sie möglicherweise den Namen, abhängig von Ihrem Netzwerk vollständig zu qualifizieren.

    Für Windows-Authentifizierung ist die Syntax etwas anders:
    
    ```R
    connStrWin <- "Driver=SQL Server;Server=SQL_instance_name;Database=database_name;Trusted_Connection=Yes"
    ```

    Das für den Download verfügbare R-Skript verwendet ausschließlich SQL-Anmeldungen. Im Allgemeinen wird empfohlen, dass die Windows-Authentifizierung verwenden, wenn möglich, um zu vermeiden, Speichern von Kennwörtern in Ihrem R-Code. Um sicherzustellen, dass der Code in diesem Lernprogramm den Code von Github heruntergeladen übereinstimmt, müssen wir jedoch, eine SQL-Anmeldung für den Rest der exemplarischen Vorgehensweise verwenden.

3. Definieren Sie Variablen verwenden, die beim Erstellen eines neuen _computekontext_. Nach der Erstellung des Compute Context-Objekts können Sie es verwenden, um R-Code für die SQL Server-Instanz ausgeführt.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R nutzt ein temporäres Verzeichnis, das bei der Serialisierung von R-Objekten zwischen Ihrer Arbeitsstation und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer verwendet wird. Sie können das lokale Verzeichnis angeben, das als *SqlShareDir*verwendet wird, oder den Standardnamen übernehmen.
  
    - Verwendung *SqlWait* , um anzugeben, ob Sie R, um die Ergebnisse vom Server gewartet werden soll.  Eine Erläuterung der wartenden im Vergleich zu nicht wartenden Aufträge, finden Sie unter [verteilt und die parallele Berechnung mit ScaleR in Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Verwenden Sie das Argument *SqlConsoleOutput* , um anzugeben, dass Sie nicht Ausgabe der R-Konsole anzeigen möchten.


4. Rufen Sie die [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) Konstruktor zum Erstellen von Compute Context-Objekt mit der Variablen und die Verbindungszeichenfolgen, die bereits definiert, und speichern das neue Objekt in der R-Variablen *Sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. Standardmäßig computekontext ist lokal, daher Sie explizit festlegen müssen der *active* computekontext.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` gibt den zuvor aktiven Computekontext im Hintergrund zurück, sodass Sie ihn verwenden können.
    + `rxGetComputeContext` gibt den aktiven Computekontext zurück.
    
    Beachten Sie, dass das Festlegen des Computekontexts nur Vorgänge betrifft, die Funktionen im **RevoScaleR** -Paket nutzen. Der Computekontext wirkt sich nicht darauf aus, wie Open-Source-R-Vorgänge erfolgen.

## <a name="create-a-data-source-using-rxsqlserver"></a>Erstellen einer Datenquelle mit RxSqlServer

In Microsoft R eine *Datenquelle* ist ein Objekt, das Sie mithilfe von RevoScaleR-Funktionen erstellen. Das Datenquellenobjekt gibt einen Satz mit Daten, die Sie für einen Task, z. B. Modell trainieren oder Feature Extraction verwenden möchten. Sie können Daten aus einer Vielzahl von Quellen abrufen; die Liste der derzeit unterstützten Datenquellen finden Sie unter [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Früher eine Verbindungszeichenfolge definiert und diese Informationen in einer R-Variablen gespeichert. Sie können erneut verwenden, Verbindungsinformationen, um die Daten anzugeben, dass Sie abrufen möchten.

1. Speichern Sie eine SQL-Abfrage als Zeichenfolgenvariable. Die Abfrage definiert die Daten zum Trainieren des Modells.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

2. Übergeben Sie die Abfragedefinition als Argument an die [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)-Funktion.

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + Das Argument  *colClasses* gibt die zu verwendenden Spaltentypen an, wenn die Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R verschoben werden. Das ist wichtig, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] andere und mehr Datentypen als R verwendet. Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](../r/r-libraries-and-data-types.md).
  
    + Das Argument *RowsPerRead* ist wichtig für die Verwaltung von speicherauslastung und effiziente Berechnungen.  Die meisten analytischen Funktionen in[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verarbeiten Daten in Segmenten und sammeln Zwischenergebnisse an, die die endgültigen Berechnungen zurückgeben, nachdem alle Daten gelesen wurden.  Durch Hinzufügen der *RowsPerRead* Parameter, Sie können steuern, wie viele Zeilen mit Daten in jeder Block für die Verarbeitung gelesen werden.  Wenn der Wert dieses Parameters zu groß ist, könnte der Datenzugriff möglicherweise langsam sein, da Sie nicht über genügen Speicher verfügen, um einen solch großen Datenblock effizient zu verarbeiten.  Auf einige Systeme, Festlegen von *RowsPerRead* auf einen sehr kleinen Wert kann auch bereitstellen Rückgang der Leistung.

3. An diesem Punkt haben Sie erstellt die *InDataSource* -Objekt, aber es enthält keinen Daten. Die Daten nicht per Pull abgerufen werden aus der SQL-Abfrage in der lokalen Umgebung, bis Sie eine Funktion, z. B. ausführen [RxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) oder [RxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    Nun, dass Sie die Datenobjekte definiert haben, können Sie es als Argument für andere Funktionen verwenden.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Verwenden Sie die SQL Server-Daten in R-Zusammenfassungen

In diesem Abschnitt, probieren Sie mehrere Funktionen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] , Support-remoterechenkontexte. R-Funktionen auf die Datenquelle anwenden, untersuchen, zusammenfassen und Diagramm die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten.

1. Rufen Sie die Funktion [von RxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) um eine Liste der Variablen in der Datenquelle und deren Datentypen abzurufen.

    **von RxGetVarInfo** ist eine praktische Funktion; können Sie es auf alle Datenrahmen aufrufen oder auf einem Satz von Daten in einem remote-Datenobjekt, beim Abrufen von Informationen, z. B. die maximalen und minimalen Werte, den Datentyp und die Anzahl der Ebenen in Faktor Spalten.
    
    Ziehen Sie es in Erwägung, diese Funktion nach jeder Art von Dateneingabe, Funktionstransformation oder Featureentwicklung auszuführen. Auf diese Weise können Sie sicherstellen, dass alle Funktionen, die Sie verwenden, in Ihrem Modell möchten erwarteten Daten eingeben und Fehler vermeiden.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **Ergebnisse**
    
    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. Rufen Sie jetzt die Funktion "revoscaler" [RxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) ausführlichere Statistiken zur einzelne Variablen abrufen.

    RxSummary basiert auf dem R `summary` funktionsfähig, jedoch verfügt über einige zusätzliche Funktionen und Vorteile. RxSummary funktioniert in mehreren Kontexten für Compute und Segmentierung unterstützt.  Sie können auch RxSummary zum Transformieren von Werten oder zusammenfassen basierend auf Faktor.
    
    In diesem Beispiel werden Sie die Fahrpreis Menge basierend auf der Anzahl der Fahrgäste zusammengefasst.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + Das erste Argument RxSummary gibt die Formel oder gleich nach zusammenzufassen. Hier wird die `F()` Funktion dient zum Konvertieren der Werte in _Reisenden\_Anzahl_ in Faktoren vor dem zusammenfassen. Außerdem müssen Sie den Mindestwert (1) und den Maximalwert (6) Geben Sie für die _Reisenden\_Anzahl_ Faktor-Variable.
    + Wenn Sie die Statistik zur Ausgabe nicht angeben, gibt standardmäßig RxSummary Mittelwert, StDev, Min, Max und die Anzahl der gültigen und fehlende Beobachtungen.
    + Dieses Beispiel enthält Code, um zu messen, wie viel Zeit zwischen dem Start der Funktion und dem Abschluss der Funktion vergangen ist, sodass Sie die Leistung vergleichen können.
  
    **Ergebnisse**

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    Name  Mean    StdDev   Min Max ValidObs MissingObs
    fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0
    Statistics by category (6 categories):*
    Category                             F_passenger_count Means    StdDev    Min
    fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5
    fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0
    fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5
    fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5
    fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5
    fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0
    Max ValidObs
    55  666
    52  206
    52   51
    39   21
    64   55
    12    1
    "It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."
    ```

Erhalten Sie unterschiedliche Ergebnisse? Ist, dass die kleinere Abfrage, die mithilfe der TOP-Schlüsselwort nicht unbedingt die gleichen Ergebnisse jedes Mal wiederherzustellen.

### <a name="bonus-exercise-on-big-data"></a>Bonus Übung über big data

Versuchen Sie, definieren eine neue Abfragezeichenfolge für die alle Zeilen. Es wird empfohlen, dass Sie ein neues Datenquellenobjekt für diesen Versuch eingerichtet. Sie können auch versuchen, Ändern der *RowsToRead* Parameter zu sehen, wie sie den Durchsatz auswirkt.

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> Während dieser ausgeführt wird, können Sie ein Tool wie [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) oder SQL Profiler, um festzustellen, wie die Verbindung hergestellt wird und der R-Code mithilfe von SQL Server-Dienste ausgeführt wird.
> 
> Eine weitere Möglichkeit besteht, zum Überwachen von R-Aufträge, die unter SQL Server, die mit diesen [benutzerdefinierte Berichte](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-lesson"></a>Nächste Lektion

[Erstellen von Diagrammen und mithilfe von R-plots](/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Untersuchen Sie die Daten mit SQL](/walkthrough-view-and-explore-the-data.md)

