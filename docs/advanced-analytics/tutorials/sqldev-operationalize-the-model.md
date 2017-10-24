---
title: 'Lektion 6: Operationalisieren von R-Modell | Microsoft Docs'
ms.custom: 
ms.date: 08/23/2016
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
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0fbdebc582650b0bd524d583d936848ae42e5f6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-operationalize-the-r-model"></a>Lektion 6: Operationalisieren von R-Modell

Dieser Artikel ist Teil eines Lernprogramms für SQL-Entwicklern zum Verwenden von R in SQL Server.

In diesem Schritt erfahren Sie, wie *operationalisieren* das Modell mithilfe einer gespeicherten Prozedur. Diese gespeicherte Prozedur kann direkt von anderen Anwendungen aufgerufen werden, um Vorhersagen für neue Beobachtungen zu treffen. Die exemplarische Vorgehensweise veranschaulicht zwei Möglichkeiten zum Ausführen von Bewertungen eines R-Modells in einer gespeicherten Prozedur mit:

- **Batch scoring-Modus**: verwenden eine SELECT-Abfrage als Eingabe für die gespeicherte Prozedur. Die gespeicherte Prozedur gibt eine Tabelle mit Beobachtungen zurück, die mit den Eingabefällen übereinstimmen.

- **Einzelbewertungsmodus**: Übergeben Sie einen Satz von einzelnen Parameterwerten als Eingabe.  Die gespeicherte Prozedur gibt eine einzelne Zeile oder einen Wert zurück.

Sehen wir uns zuerst einmal an, wie die Bewertung im Allgemeinen abläuft.

## <a name="basic-scoring"></a>Grundlegende Bewertung

Die gespeicherte Prozedur _PredictTip_ beschreibt die grundlegende Syntax für das Umschließen eines Vorhersageaufrufs in einer gespeicherten Prozedur.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
str(OutputDataSet)  
print(OutputDataSet)  
',  
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2  
  WITH RESULT SETS ((Score float));  
  
END  
  
GO
```

- Die SELECT-Anweisung ruft das serialisierte Modell aus der Datenbank ab und speichert das Modell in der R-Variable `mod` zur weiteren Verarbeitung mit R.

- Die neue Fälle für die Bewertung erhalten Sie vom der [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage, die im angegebenen `@inquery`, der erste Parameter der gespeicherten Prozedur. Wenn die Abfragedaten gelesen werden, werden die Zeilen im Standard-Datenrahmen, `InputDataSet`, gespeichert. Dieser Datenrahmen wird der `rxPredict` -Funktion in R übergeben, die die Bewertungen generiert.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Da ein data.frame eine einzelne Zeile enthalten kann, können Sie den gleichen Code für die Batchbewertung und die Einzelbewertung verwenden.
  
-   Der zurückgegebene Wert der `rxPredict` Funktion ist ein **"float"** , die die Wahrscheinlichkeit, dass der Treiber einen Betrag-Tipp ruft darstellt.

## <a name="batch-scoring"></a>Batchbewertung

Jetzt sehen wir uns an, wie die Batchbewertung funktioniert.

1.  Zunächst rufen wir einen kleineren Satz von Eingabedaten ab, mit denen wir arbeiten werden. Diese Abfrage erstellt eine „Top 10“-Liste der Fahrten mit Reisenden sowie anderen Funktionen, die benötigt werden, um eine Vorhersage zu erstellen.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count,
        a.trip_time_in_secs AS trip_time_in_secs, 
        a.trip_distance AS trip_distance, 
        a.dropoff_datetime AS dropoff_datetime, 
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    FROM
    (
        SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
         dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a
    LEFT OUTERJOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion IS NULL
    ```

    **Beispielergebnisse**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    Diese Abfrage dient als Eingabe für die gespeicherte Prozedur _PredictTipBatchMode_, der als Teil des Downloads.

2. Nehmen Sie sich an den Code der gespeicherten Prozedur überprüfen _PredictTipBatchMode_ in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model
      FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
        @script = N'
          mod <- unserialize(as.raw(model));
          print(summary(mod))
          OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
          str(OutputDataSet)
          print(OutputDataSet)
        ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  Geben Sie den Abfragetext in einer Variablen, und übergeben Sie ihn als Parameter an die gespeicherte Prozedur:

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='
    select top 10 a.passenger_count as passenger_count,
        a.trip_time_in_secs as trip_time_in_secs,
        a.trip_distance as trip_distance,
        a.dropoff_datetime as dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance
    from
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
        from nyctaxi_sample
    )a  
    LEFT OUTER JOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample  
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b 
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. Die gespeicherte Prozedur gibt eine Reihe von Werten, die die Vorhersage für jeden der zehn wichtigsten Roundtrips darstellt. Die oberste Roundtrips sind jedoch auch einzelne Reisenden Reisen mit einer relativ kurzen Reise Entfernung, für die der Treiber einen Tipp abzurufenden unwahrscheinlich ist.
  

> [!TIP]
> 
> Anstatt nur die „Trinkgeld/ Kein Trinkgeld“-Ergebnisse zurückzugeben, könnten Sie auch den Wahrscheinlichkeitswert für die Vorhersage zurückgeben und anschließend auf die Spalte _Score_ eine WHERE-Klausel anwenden, um die Bewertung als „Trinkgeld“, „Kein Trinkgeld“ zu kategorisieren und dabei einen Schwellenwert wie z.B. 0,5 oder 0,7 verwenden. Dieser Schritt ist nicht in der gespeicherten Prozedur enthalten, aber es wäre leicht, ihn zu implementieren.

## <a name="single-row-scoring"></a>Einzeiliges Bewertung

Gelegentlich möchten Sie einzelne Werte aus einer Anwendung übergeben und ein einzelnes Ergebnis basierend auf diesen Werten erhalten. Beispielsweise könnten Sie ein Excel-Arbeitsblatt, eine Webanwendung oder einen Reporting Services-Bericht einrichten, um die gespeicherte Prozedur aufzurufen und Eingaben bereitzustellen, die von Benutzern eingegeben oder ausgewählt wurden.

In diesem Abschnitt erfahren Sie, wie einzelne Vorhersagen mit einer gespeicherten Prozedur erstellt wird.

1. Überprüfen Sie kurz den Code der gespeicherten Prozedur _PredictTipSingleMode_, die als Teil des Downloads enthalten war.
  
    ```SQL
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
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
    @model = @lmodel2,  
    @passenger_count =@passenger_count ,  
    @trip_distance=@trip_distance,  
    @trip_time_in_secs=@trip_time_in_secs,    
    @pickup_latitude=@pickup_latitude,  
    @pickup_longitude=@pickup_longitude,  
    @dropoff_latitude=@dropoff_latitude,  
    @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```
  
    - Diese gespeicherte Prozedur besitzt mehrerer einzelner Werte als Eingabe, wie die Anzahl der Reisende, Fahrstrecke usw.
  
        Wenn Sie die gespeicherte Prozedur aus einer externen Anwendung aufrufen, überprüfen Sie, dass die Daten mit den Anforderungen des R-Modells übereinstimmen. Sie müssen möglicherweise sicherstellen, dass die Eingabedaten in einen R-Datentyp umgewandelt oder konvertiert werden können oder den Datentyp und die Datenlänge überprüfen. Weitere Informationen finden Sie unter [Arbeiten mit R-Datentypen](https://msdn.microsoft.com/library/mt590948.aspx).
  
    -   Die gespeicherte Prozedur erstellt eine Bewertung auf Grundlage des gespeicherten R-Modells.
  
2. Probieren Sie es einfach aus, indem Sie die Werte manuell bereitstellen.
  
    Öffnen Sie ein neues **Abfrage** Fenster, und rufen Sie die gespeicherte Prozedur, und geben Sie Werte für jeden Parameter. Die Parameter vom Modell verwendeten merkmalspalten darstellen und erforderlich sind.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance float = 2.5,
    @trip_time_in_secs int = 631,
    @pickup_latitude float = 40.763958,
    @pickup_longitude float = -73.973373,
    @dropoff_latitude float =  40.782139,
    @dropoff_longitude float = 73.977303
    ```

    Oder verwenden Sie dieses kürzere Form unterstützt für [Parameter an eine gespeicherte Prozedur](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Die Ergebnisse zeigen, dass die Wahrscheinlichkeit für einen Tipp sehr wenig diese Top 10 Schleifen ist, da alle einzelnen Reisenden Zugriffe über einen relativ kurzen Abstand sind.

## <a name="conclusions"></a>Schlussfolgerungen

Dies ist der Abschluss für das Lernprogramm. Nun, da Sie So betten Sie ein R-Code in gespeicherten Prozeduren gelernt haben, können Sie diese Methoden zum Erstellen von Modellen Ihrer Wahl erweitern. Die Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] macht es viel einfacher, R-Modelle für Vorhersagen bereitzustellen und das erneute Trainieren von Modellen im Rahmen eines Unternehmensdatenworkflows zu integrieren.

## <a name="previous-lesson"></a>Vorherige Lektion

[Lektion 5: Trainieren Sie, und speichern Sie ein R-Modell mithilfe des T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

