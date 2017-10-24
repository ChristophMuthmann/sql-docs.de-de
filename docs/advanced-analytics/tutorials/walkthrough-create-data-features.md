---
title: Erstellen von Data-Features, die mit R und SQL (Exemplarische Vorgehensweise) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: 4f3f5463e6a0117780add65feb9916ff78dad68d
ms.contentlocale: de-de
ms.lasthandoff: 10/07/2017

---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>Erstellen von Data-Features, die mit R und SQL (Exemplarische Vorgehensweise)

Data Engineering ist ein wichtiger Teil des maschinellen Lernens. Daten erfordern oft Transformation aus, bevor Sie es zur vorhersagemodellierung verwenden können. Wenn die Daten nicht über die Features verfügen, die Sie benötigen, können Sie diese aus vorhandenen Werten erstellen.

Sie möchten für diesen Modellierungstask möglicherweise lieber die Entfernung in Meilen zwischen zwei Orten haben anstatt die ungefähren Werte für den Breiten- und Längengrad des Abhol- und Zielorts. Um dieses Feature zu erstellen, berechnen Sie die direkte lineare Abstand zwischen zwei Punkten, mit der [semiversus Formel](https://en.wikipedia.org/wiki/Haversine_formula).

In diesem Schritt Vergleichen wir zwei verschiedene Installationsmethoden für eine Funktion mit Daten zu erstellen:

- Verwenden eine benutzerdefinierte R-Funktion
- Verwenden in eine benutzerdefinierte T-SQL-Funktion[!INCLUDE[tsql](../../includes/tsql-md.md)]

Das Ziel ist es zum Erstellen eines neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Satz von Daten, die die ursprünglichen Spalten und die neue numerische Funktion enthält *Direct_distance*.

## <a name="featurization-using-r"></a>Merkmalbereitstellung mithilfe von R

Die Sprache R ist bekannt für ihre großen und vielseitigen statistischen Bibliotheken, doch Sie müssen ggf. weiterhin benutzerdefinierte Datentransformationen erstellen.

Zuerst führen wir ihn der Möglichkeit R-Benutzer sind daran gewöhnt,: Rufen Sie die Daten auf Ihrem Laptop, und führen Sie eine benutzerdefinierte R-Funktion *ComputeDist*, berechnet die lineare Abstand zwischen zwei Punkten, die Breiten- und Längengraden angegeben.

1. Denken Sie daran, dass das Datenquellenobjekt, das Sie zuvor erstellt haben, nur die Top 1000 Zeilen erhält. Wir also definieren Sie eine Abfrage, die alle Daten abruft.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Erstellen Sie eine neue SQL Server-Datenquelle, die mit der Abfrage.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) können entweder eine Abfrage, bestehend aus einer gültigen SELECT-Abfrage, als das Argument bereitgestellt werden die _SqlQuery_ Parameter oder den Namen eines Table-Objekts, als die _Tabelle_ Parameter.
    
    - Wenn Sie Beispieldaten aus einer Tabelle möchten, müssen Sie verwenden die _SqlQuery_ Parameter Samplingparameter, die mit der T-SQL-TABLESAMPLE-Klausel definieren und Festlegen der _RowBuffering_ Argument auf "false".

3. Führen Sie den folgenden Code zum Erstellen von benutzerdefinierten R-Funktion. ComputeDist nimmt zwei Wertepaaren Breiten- und Längengrad und berechnet die lineare Entfernung zwischen ihnen, den Abstand in Meilen zurückgeben.

    ```R
    env <- new.env();
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){
      R <- 6371/1.609344 #radius in mile
      delta_lat <- dropoff_lat - pickup_lat
      delta_long <- dropoff_long - pickup_long
      degrees_to_radians = pi/180.0
      a1 <- sin(delta_lat/2*degrees_to_radians)
      a2 <- as.numeric(a1)^2
      a3 <- cos(pickup_lat*degrees_to_radians)
      a4 <- cos(dropoff_lat*degrees_to_radians)
      a5 <- sin(delta_long/2*degrees_to_radians)
      a6 <- as.numeric(a5)^2
      a <- a2+a3*a4*a6
      c <- 2*atan2(sqrt(a),sqrt(1-a))
      d <- R*c
      return (d)
    }
    ```
  
    + Die erste Zeile definiert eine neue Umgebung. In R kann eine Umgebung verwendet werden, um Namespaces z.B. in Paketen einzuschließen.  Sie können die `search()` -Funktion verwenden, um die Umgebungen in Ihrem Arbeitsbereich anzuzeigen. Um die Objekte in einer bestimmten Umgebung anzuzeigen, geben Sie `ls(<envname>)`ein.
    + Die Zeilen, die mit `$env.ComputeDistance` beginnen, enthalten den Code, der die Haversine-Formel definiert, die die *Großkreisentfernung* zwischen zwei Punkten auf einer Kugel berechnet.

4. Die Funktion definieren, Sie wenden Sie es auf die Daten so erstellen eine neue merkmalspalte *Direct_distance*. jedoch vor dem Ausführen der Transformations des computekontexts ändern, in ein lokales.

    ```R
    rxSetComputeContext("local");
    ```

5. Rufen Sie die [RxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) Funktion, um das Feature engineering-Daten abzurufen, und wenden Sie die `env$ComputeDist` Funktion, um die Daten im Arbeitsspeicher.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + Die Funktion RxDataStep unterstützt verschiedene Methoden zum Ändern von Daten erfüllt. Weitere Informationen finden Sie im Artikel: [Transformation und Teilmenge von Daten in Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Allerdings eine Reihe von Punkten erwähnenswerte bezüglich RxDataStep: 
    
    In anderen Datenquellen können Sie die Argumente *VarsToKeep* und *VarsToDrop*, aber diese werden für SQL Server-Datenquellen nicht unterstützt. Aus diesem Grund in diesem Beispiel haben wird die _transformiert_ Argument, um die Pass-Through-Spalten und die transformierten Spalten anzugeben. Darüber hinaus bei Ausführung in einer SQL Server computekontext, die _InData_ Argumente können nur eine SQL Server-Datenquelle.

    Der vorhergehende Code kann außerdem eine Warnmeldung angezeigt, die bei Ausführung auf größeren Datasets erstellen. Wenn die Anzahl der Zeilen erreicht wird die Anzahl von Spalten erstellt wird (der Standardwert ist 3.000.000) festgelegten Wert überschreitet, RxDataStep eine Warnung zurückgibt, und die Anzahl der Zeilen im Frame zurückgegebenen Daten werden abgeschnitten. Um die Warnung zu entfernen, ändern Sie die _MaxRowsByCols_ Argument in der RxDataStep-Funktion. Jedoch wenn _MaxRowsByCols_ ist zu groß, könnten Probleme auftreten, wenn die Datenrahmen in den Speicher geladen.

7. Sie können optional Aufrufen [von RxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) , das Schema der Quelle transformierten Daten zu überprüfen.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Featurebereitstellung mit Transact-SQL

Erstellen Sie eine benutzerdefinierte SQL-Funktion nun *ComputeDist*, für die gleiche Aufgabe wie die benutzerdefinierten R-Funktion.

1. Definieren Sie eine neue benutzerdefinierte SQL-Funktion mit dem Namen *fnCalculateDistance*. Der Code für diese benutzerdefinierte SQL-Funktion wird als Teil des PowerShell-Skripts bereitgestellt, das Sie zur Erstellung und Konfiguration der Datenbank ausgeführt haben.  Die Funktion sollte bereits in Ihrer Datenbank vorhanden sein.

    Falls nicht, generieren Sie die Funktion mit SQL Server Management Studio in der gleichen Datenbank, in der die Taxidaten gespeichert sind.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
    AS
    BEGIN
      DECLARE @distance decimal(28, 10)
      -- Convert to radians
      SET @Lat1 = @Lat1 / 57.2958
      SET @Long1 = @Long1 / 57.2958
      SET @Lat2 = @Lat2 / 57.2958
      SET @Long2 = @Long2 / 57.2958
      -- Calculate distance
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
      --Convert to miles
      IF @distance <> 0
      BEGIN
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
      END
      RETURN @distance
    END
    ```

2. Führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung von einer beliebigen Anwendung aus, die [!INCLUDE[tsql](../../includes/tsql-md.md)] unterstützt, um zu sehen, wie die Funktion arbeitet.

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. Diese Funktion definieren, fehlschlagen erstellen die Funktionen aus, indem Sie mithilfe von SQL, und klicken Sie dann die Werte direkt in eine neue Tabelle einfügen es kann leicht:

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. Allerdings sehen wie die benutzerdefinierte SQL-Funktion aus R-Code aufrufen. Speichern Sie zuerst merkmalbereitstellung SQL-Abfrage in ein R-Variable.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Diese Abfrage wurde geändert, um eine kleinere Stichprobe von Daten, zum Beschleunigen der in dieser exemplarischen Vorgehensweise zu erhalten. Sie können die TABLESAMPLE-Klausel entfernen, wenn alle Daten abgerufen werden soll. möglicherweise möglich, das vollständige Datset in R, eine Fehlermeldung zu laden sie je nach Ihrer Umgebung nicht aus.
  
5. Verwenden Sie die folgenden Codezeilen, um die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion aus Ihrer R-Umgebung aufzurufen und sie auf die Daten anzuwenden, die in *featureEngineeringQuery* definiert sind.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Nun, dass die neue Funktion erstellt wurde, rufen **RxGetVarsInfo** So erstellen Sie eine Zusammenfassung der Daten in der Feature-Tabelle.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *Ergebnisse*

    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > In einigen Fällen erhalten Sie möglicherweise eine Fehlermeldung wie diesen: *die EXECUTE-Berechtigung wurde für das Objekt "FnCalculateDistance" verweigert* Wenn dies der Fall ist, stellen Sie sicher, dass die Anmeldung Sie verwenden verfügt über Berechtigungen zum Ausführen von Skripts und Objekte in der Datenbank erstellen nicht nur auf die Instanz.
    > Überprüfen Sie das Schema für das Objekt FnCalculateDistance. Wenn das Objekt vom Datenbankbesitzer erstellt wurde, und Ihre Anmeldung, zu der Rolle "db_datareader gehört", müssen Sie den Anmeldenamen explizite Berechtigungen zum Ausführen des Skripts erhalten.

## <a name="comparing-r-functions-and-sql-functions"></a>Vergleichen von R und SQL-Funktionen

Erinnern Sie sich diesem Codeabschnitt, die zum Zeitpunkt des R-Codes verwendet?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Sie können versuchen, mit diesem mit der SQL-Beispiel für benutzerdefinierte Funktionen, um festzustellen, wie lange dauert die Datentransformation, wenn eine SQL-Funktion aufgerufen wird. Darüber hinaus versuchen Sie rechenkontexte mit RxSetComputeContext zu wechseln, und vergleichen Sie die Zeitangaben.

Die Zeiten variieren beträchtlich, je nach Geschwindigkeit des Netzwerks ab, und der Hardwarekonfiguration. In den Konfigurationen, die wir getestet, die [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktion schneller als die Verwendung einer benutzerdefinierten R-Funktion wurde. Daher verwenden wir die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktion für diese Berechnungen in den folgenden Schritten.

> [!TIP]
> Sehr häufig feature engineering mit [!INCLUDE[tsql](../../includes/tsql-md.md)] schneller erfolgt als R. T-SQL enthält beispielsweise schnell Windowing und Rangfolgefunktionen, die auf allgemeine Data Science Berechnungen wie gleitende Durchschnitte parallelen angewendet werden können und  *n* -Kacheln. Wählen Sie je nach Daten und Aufgabe die effizienteste Methode.

## <a name="next-lesson"></a>Nächste Lektion

[Erstellen Sie ein R-Modell zu und speichern Sie in SQL](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Anzeigen und Zusammenfassen von Daten mithilfe von R](walkthrough-view-and-summarize-data-using-r.md)


