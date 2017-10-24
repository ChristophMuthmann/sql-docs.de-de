---
title: Das R-Modell bereitstellen und deren Verwendung in SQL (Exemplarische Vorgehensweise) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
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
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: 5d37c9150d19c3e39ea76b48fb0453d159ca0f44
ms.contentlocale: de-de
ms.lasthandoff: 10/07/2017

---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>Das R-Modell bereitstellen und deren Verwendung in SQL

In dieser Lektion verwenden Sie die R-Modelle in einer produktionsumgebung durch Aufrufen eines trainierten Modells aus einer gespeicherten Prozedur. Rufen Sie dann die gespeicherte Prozedur von R oder eine beliebige Anwendung-Programmiersprache, unterstützt [!INCLUDE[tsql](../../includes/tsql-md.md)] (z. B. c#, Java, Python usw.), um das Modell zum Vorhersagen für neue Beobachtungen verwenden.

Dieses Beispiel zeigt die beiden häufigsten Verwendungsmöglichkeiten für ein Modell in die Bewertung verwenden:

- **Batch scoring-Modus** wird verwendet, wenn Sie sehr schnell mehrere Vorhersagen erstellen, durch Übergeben einer SQL abzufragen oder Tabelle als Eingabe benötigen. Eine Tabelle der Ergebnisse wird zurückgegeben, die Sie möglicherweise direkt in eine Tabelle einfügen, oder in eine Datei schreiben.

- **Einzelne bewerteten Modus** wird verwendet, wenn Sie einzelne Vorhersagen zu einem Zeitpunkt erstellen müssen. Sie haben einen Satz von einzelnen Werten an die gespeicherte Prozedur übergeben. Die Werte entsprechen den Funktionen im Modell, das Modell, die zum Erstellen einer Vorhersage verwendet werden, oder ein anderes Ergebnis, wie z. B. ein Wahrscheinlichkeitswert zu generieren. Sie können diesen Wert dann an die Anwendung oder der Benutzer zurückgeben.

## <a name="batch-scoring"></a>Batchbewertung

Eine gespeicherte Prozedur für die batchbewertung wurde erstellt, wenn Sie zunächst das PowerShell-Skript ausgeführt haben. Diese gespeicherte Prozedur, *PredictTipBatchMode*, bewirkt Folgendes:

- Ruft einen Satz von Eingabedaten als SQL-Abfrage ab
- Ruft das trainierte logistische Regressionsmodell auf, das Sie in der vorherigen Lektion gespeichert haben
- Sagt die Wahrscheinlichkeit, dass der Treiber Ruft alle Tipp ungleich 0 (null) ab

1. Nehmen Sie sich über das Skript für die gespeicherte Prozedur aussehen *PredictTipBatchMode*. Es veranschaulicht verschiedene Aspekte wie ein Modell mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]operationalisiert werden kann.
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + Sie verwenden eine SELECT-Anweisung, um das gespeicherte Modell aus einer SQL-Tabelle aufzurufen. Das Modell wird abgerufen, aus der Tabelle als **varbinary(max)** Daten, die in der SQL-Variablen gespeichert  _@lmodel2_ , und als Parameter übergeben *mod* an das System gespeichert Prozedur [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Die Daten, die als Eingaben verwendet werden, für die Bewertung als eine SQL-Abfrage definiert und als Zeichenfolge in der SQL-Variablen gespeicherten  _@input_ . Wie Daten aus der Datenbank abgerufen werden, wird es in einem Datenrahmen aufgerufen gespeichert *InputDataSet*, also nur der Standardnamen für die Eingabedaten für die [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Prozedur können Sie definieren einen anderen Variablennamen an, die bei Bedarf mithilfe des Parameters  _@input \_Daten\_1\_Namen_.

    + Die gespeicherte Prozedur ruft die `rxPredict` -Funktion aus der **RevoScaleR** -Bibliothek auf, um die Bewertung zu generieren.

    + Der Rückgabewert *Score*, ist die Wahrscheinlichkeit angesichts des Modells, diesen Treiber Ruft einen Tipp. Optional, könnten Sie die zurückgegebenen Werte auf die Rückgabewerte in "QuickInfo" und "kein Tipp" Gruppen unterteilen einfach eine Art von Filter anwenden.  Beispielsweise würde eine Wahrscheinlichkeit von weniger als 0,5 bedeuten, dass ein Tipp unwahrscheinlich ist.
  
2.  Zum Aufrufen der gespeicherten Prozedur im Batchmodus definieren Sie die Abfrage als Eingabe für die gespeicherte Prozedur erforderlich. Hier ist die SQL-Abfrage. Führen sie in SSMS, um sicherzustellen, dass er funktioniert.

    ```SQL
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. Verwenden Sie diese R-Code, um die Eingabezeichenfolge aus der SQL-Abfrage zu erstellen:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Rufen Sie zum Ausführen der gespeicherten Prozedur von R der **SqlQuery** Methode der **RODBC** packen sowie die Verwendung der SQL-Verbindungs `conn` , die Sie zuvor definiert:

    ```R
    sqlQuery (conn, q);
    ```

    Wenn Sie einen ODBC-Fehler erhalten, überprüfen Sie die Abfragesyntax, sowie davon, ob Sie die richtige Anzahl von Anführungszeichen. 
    
    Wenn Sie einen Berechtigungsfehler erhalten haben, stellen Sie sicher, dass die Anmeldung die gespeicherte Prozedur ausführen kann.

## <a name="single-row-scoring"></a>Einzelne Zeile Bewertung

Wenn das Modell für Vorhersagen auf Basis der Zeile für Zeile aufrufen, übergeben Sie einen Satz von Werten, die Features für jeden einzelnen Fall darstellen. Die gespeicherte Prozedur gibt einen einzelnen Vorhersage oder die Wahrscheinlichkeit zurück. 

Die gespeicherte Prozedur *PredictTipSingleMode* veranschaulicht diesen Ansatz. Sie nimmt als Eingabe mehrere Parameter, die Funktion Werte (z. B. Reisenden Count und Reise Abstand) darstellen, Bewertungen dieser Funktionen mit dem gespeicherten R-Modell und gibt die Wahrscheinlichkeit Tipp.

1. Wenn die gespeicherte Prozedur *PredictTipSingleMode* wurde nicht erstellt vom ersten PowerShell-Skript können Sie die folgenden Transact-SQL-Anweisung aus, um ihn jetzt erstellen ausführen.

    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. In SQL Server Management Studio können Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** Prozedur (oder **EXECUTE**) rufen Sie die gespeicherte Prozedur, und übergeben sie die erforderlichen Eingaben. Beispielsweise führen Sie diese Anweisung in Management Studio:

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Der hier übergebene Werte werden bzw. für die Variablen _Reisenden\_Anzahl_, _Trip_distance_, _Reise\_Zeit\_in\_Sek._, _Abholung\_Breitengrad_, _Abholung\_Längengrad_, _Dropoff\_Breitengrad_, und _Dropoff\_Längengrad_.

3. Um dieses Aufrufs von R-Code ausführen zu können, definieren Sie einfach eine R-Variable, die den gesamten gespeicherten Prozeduraufruf, wie diese enthält:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Der hier übergebene Werte werden bzw. für die Variablen _Reisenden\_Anzahl_, _Reise\_Abstand_, _Reise\_Zeit\_in\_Sekunden_, _Abholung\_Breitengrad_, _Abholung\_Längengrad_, _Dropoff\_ Breitengrad_, und _Dropoff\_Längengrad_.

4. Rufen Sie `sqlQuery` (aus der **RODBC** Paket), und übergeben Sie die Verbindungszeichenfolge sowie die Zeichenfolgenvariable, die den Aufruf der gespeicherten Prozedur enthält.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R-Tools für Visual Studio (RTVS) bietet eine hervorragende Integration mit SQL Server und r angezeigt. Finden Sie in diesem Artikel finden Sie weitere Beispiele für die Verwendung von RODBC mit einer SQL Server-Verbindung: [arbeiten mit SQL Server und R](https://docs.microsoft.com/en-us/visualstudio/rtvs/sql-server)

## <a name="summary"></a>Zusammenfassung

Nun, da Sie zum Arbeiten mit gelernt haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten und die persist trainierte R-Modelle, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es sollte Ihnen die Erstellung neuer Modelle basierend auf diesem DataSet relativ einfach sein. Beispielsweise können Sie versuchen, diese zusätzliche Modelle zu erstellen:

- Ein Regressionsmodell, das die Höhe des Trinkgelds vorhersagt

- Ein mehrklassiges klassifizierungsmodell, das vorhersagt, ob die QuickInfo groß, Mittel oder klein ist.

Wir empfehlen außerdem, dass Sie sich einige dieser Beispiele und Ressourcen anschauen:

+ [Szenarien für Data Science und Lösungsvorlagen](data-science-scenarios-and-solution-templates.md)

+ [Datenbankinterne Advanced Analytics](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R: Eintauchen in die Datenanalyse](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [Zusätzliche Ressourcen](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>Vorherige Lektion

[Erstellen Sie ein R-Modell zu und speichern Sie sie in SQL Server](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>Nächste Schritte

[SQL Server-R-Lernprogramme](sql-server-r-tutorials.md)

[Vorgehensweise: erstellen eine gespeicherte Prozedur mithilfe von sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)

