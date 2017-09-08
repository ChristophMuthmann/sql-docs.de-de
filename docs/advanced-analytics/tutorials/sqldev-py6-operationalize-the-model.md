---
title: 'Schritt 6: Operationalisieren Modell | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>Schritt 6: Operationalisieren des Modells

In diesem Schritt erfahren Sie *operationalisieren* die Modelle, die Sie trainiert und im vorherigen Schritt gespeichert. Operationalisieren Sie in diesem Fall "Bereitstellung des Modells bis hin zur Produktion zur Bewertung" bedeutet. Dies ist sehr einfach, wenn Ihrem Python-Code in einer gespeicherten Prozedur enthalten ist. Sie können dann die gespeicherte Prozedur von Anwendungen, um Vorhersagen für neue Beobachtungen aufrufen.

Erfahren Sie zwei Methoden zum Aufrufen von einem Python-Modell aus einer gespeicherten Prozedur an:

- **Batchbewertungsmodus**: Verwenden Sie eine SELECT-Abfrage, um mehrere Datenzeilen bereitzustellen. Die gespeicherte Prozedur gibt eine Tabelle mit Beobachtungen zurück, die mit den Eingabefällen übereinstimmen.
- **Einzelbewertungsmodus**: Übergeben Sie einen Satz von einzelnen Parameterwerten als Eingabe.  Die gespeicherte Prozedur gibt eine einzelne Zeile oder einen Wert zurück.

## <a name="scoring-using-the-scikit-learn-model"></a>Bewerten von mit der Scikit-Modells lernen

Die gespeicherte Prozedur _PredictTipSciKitPy_ verwendet die Scikit-Modell zu erfahren. Diese gespeicherte Prozedur veranschaulicht die grundlegende Syntax für einen Aufruf der Python-Vorhersage in einer gespeicherten Prozedur umschließen.

- Der Name des Modells verwenden, wird als Eingabeparameter an die gespeicherte Prozedur bereitgestellt. 
- Die gespeicherte Prozedur wird anschließend Laden Sie das serialisierte Modell aus der Datenbanktabelle `nyc_taxi_models`.table, verwenden die SELECT-Anweisung in der gespeicherten Prozedur.
- Das serialisierte Modell in der Python-Variablen gespeichert ist `mod` zur weiteren Verarbeitung mithilfe von Python.
- Die neue Fälle, die bewertet werden müssen erhalten Sie vom der [!INCLUDE[tsql](../../includes/tsql-md.md)] in angegebene Abfrage `@input_data_1`. Wenn die Abfragedaten gelesen werden, werden die Zeilen im Standard-Datenrahmen, `InputDataSet`, gespeichert.
- Dieser Datenrahmen übergeben wird die `predict_proba` Funktion des logistischen Regressionsmodells `mod`, die mit Scikit erstellt wurde-Modell erfahren. 
- Die `predict_proba` Funktion (`probArray = mod.predict_proba(X)`) gibt eine **"float"** , die die Wahrscheinlichkeit, die gewährt wird, Tipps und Tricks (beliebige Anzahl) darstellt.
- Außerdem wird die gespeicherte Prozedur eine Genauigkeit-Metrik AUC (Bereich unter der Kurve) berechnet. Genauigkeitsmetriken, z. B. AUC können nur generiert werden, wenn Sie auch die Ziel-Bezeichnung (d. h. die Geneigter Spalte) angeben. Vorhersagen ist nicht erforderlich, die Ziel-Bezeichnung (Variable `y`), jedoch die Genauigkeit Metrik Berechnung.

  Aus diesem Grund Wenn Sie nicht über die Ziel-Bezeichnungen für die Daten zu bewertendes verfügen, Sie können ändern Sie die gespeicherte Prozedur, um die AUC Berechnungen zu entfernen und einfach die Wahrscheinlichkeiten im Tipp aus Funktionen zurückgeben (Variable `X` in der gespeicherten Prozedur).

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        import pandas;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="scoring-using-the-revoscalepy-model"></a>Bewerten von mit dem Modell revoscalepy

Die gespeicherte Prozedur _PredictTipRxPy_ verwendet ein Modell, das erstellt wurde, mithilfe der **Revoscalepy** Bibliothek. Es funktioniert ähnlich wie die _PredictTipSciKitPy_ Prozedur, jedoch mit einigen Änderungen für die **Revoscalepy** Funktionen.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="batch-scoring-using-a-select-query"></a>Batchbewertung mithilfe einer SELECT-Abfrage

Die gespeicherten Prozeduren **PredictTipSciKitPy** und **PredictTipRxPy** zwei Eingabeparameter erfordern: 

- Die Abfrage, die die Daten für die Bewertung abruft
- Der Name eines trainierten Modells

In diesem Abschnitt erfahren Sie, wie diese Argumente an die gespeicherte Prozedur so ändern Sie einfach das Modell und die Daten für die Bewertung verwendete übergeben werden.

1. Definieren Sie die Eingabedaten, und rufen Sie die gespeicherten Prozeduren für die Bewertung wie folgt. Dieses Beispiel verwendet die gespeicherte Prozedur PredictTipSciKitPy für die Bewertung und übergibt im Namen des Modells und der Abfragezeichenfolge

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    Die gespeicherte Prozedur liefert vorhergesagte Wahrscheinlichkeiten für jede Reise, die als Teil der Eingabeabfrage übergeben wurde. Wenn Sie SSMS (SQL Server Management Studio) zum Ausführen von Abfragen verwenden, erscheint die Wahrscheinlichkeiten als Tabelle in der **Ergebnisse** Bereich. Die **Nachrichten** Bereich gibt die Genauigkeit Metrik (AUC oder Bereich unter der Kurve) mit einem Wert von ca. 0.56.

2. Verwenden der **Revoscalepy** für die Bewertung zu modellieren, rufen Sie die gespeicherte Prozedur **PredictTipRxPy**, und übergeben Sie den Servernamen und Modellzeichenfolge.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>Bewerten Sie einzelne Zeilen mithilfe von Scikit-Modells lernen

In manchen Fällen anstelle von batchbewertung, Sie können z. B. Übergabe in einem einzigen Gehäuse Abrufen von Werten aus einer Anwendung, zu erhalten ein einzelnes Ergebnis basierend auf diesen Werten. Beispielsweise könnten Sie ein Excel-Arbeitsblatt, eine Webanwendung oder einen Reporting Services-Bericht einrichten, um die gespeicherte Prozedur aufzurufen und Eingaben bereitzustellen, die von Benutzern eingegeben oder ausgewählt wurden.

In diesem Abschnitt erfahren Sie, wie einzelne Vorhersagen zu erstellen, indem Sie eine gespeicherte Prozedur aufgerufen wird.

1. Nehmen Sie sich an den Code der gespeicherten Prozeduren überprüfen [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) und [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy), die als Teil des Downloads enthalten sind. Diese gespeicherten Prozeduren verwenden die Scikit-Informationen und Revoscalepy Modelle, und führen Sie die Bewertung wie folgt:

  - Dem Modellnamen und mehrere einzelne Werte werden als Eingabe bereitgestellt. Diese Eingaben enthalten Reisenden Count, Reise Abstand und So weiter.
  - Eine Funktion mit Tabellenrückgabe `fnEngineerFeatures`, akzeptiert Eingabewerte und konvertiert die Breiten- und Längengraden Abstand weiterleiten. [Lektion 4](sqldev-py4-create-data-features-using-t-sql.md) enthält eine Beschreibung dieser Funktion mit Tabellenrückgabe.
  - Wenn Sie die gespeicherte Prozedur von einer externen Anwendung aufrufen, stellen Sie sicher, dass die Eingabedaten der erforderlichen Merkmale des Modells Python übereinstimmt. Dazu gehören Umwandlung oder konvertieren die Eingabedaten in eine Python-Datentyp, oder Überprüfen von Datentypen und Datenlänge beispielsweise.
  - Die gespeicherte Prozedur erstellt eine Bewertung auf dem gespeicherten Python-Datenmodell basiert.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Hier ist die Definition der gespeicherten Prozedur, der ausführt, Bewertung mithilfe der **Scikit-erfahren Sie** Modell.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
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
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

Hier ist die Definition der gespeicherten Prozedur, der ausführt, Bewertung mithilfe der **Revoscalepy** Modell.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
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
GO
```

2.  Um es zu testen, öffnen Sie ein neues **Abfrage** Fenster, und rufen Sie die gespeicherte Prozedur Parameter für die Funktionsspalten eingeben.

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    Die sieben Werte sind für diese Funktion Spalten, in der Reihenfolge auf:
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. Die Ausgabe von beiden Verfahren ist die Wahrscheinlichkeit eines Tipps für die Reise Taxi mit den oben aufgeführten Parametern oder Funktionen bezahlt wird.

## <a name="conclusions"></a>Schlussfolgerungen

In diesem Lernprogramm haben Sie gelernt, wie mit Python-Code eingebettet in gespeicherten Prozeduren arbeiten wird. Die Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] kann es viel einfacher, zum Bereitstellen von Python-Modellen zur Vorhersage und Modell Umschulung als Teil einer Enterprise Data-Workflow einzubeziehen.

## <a name="previous-step"></a>Vorheriger Schritt
[Schritt 6: Operationalisieren des Modells](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)

