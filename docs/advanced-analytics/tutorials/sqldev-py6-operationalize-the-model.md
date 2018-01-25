---
title: 'Schritt 6: Operationalisieren die Python-Modell mithilfe von SQL Server | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 7613115f014ff2c53ce63ef883798b06f2e5d270
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>Schritt 6: Operationalisieren Sie die Python-Modell mithilfe von SQL Server

Dieser Artikel ist Teil eines Lernprogramms [In Datenbank-Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md). 

In diesem Schritt erfahren Sie, wie *operationalisieren* die Modelle, die Sie trainiert und im vorherigen Schritt gespeichert.

In diesem Szenario bedeutet operationalisierung Bereitstellung des Modells bis hin zur Produktion zur Bewertung. Die Integration mit SQL Server macht diese relativ einfach, da Sie Python-Code in einer gespeicherten Prozedur einbetten können. Um Vorhersagen aus dem Modell basierend auf neue Eingaben zu erhalten, rufen Sie die gespeicherte Prozedur von einer Anwendung, und übergeben Sie die neuen Daten.

In dieser Lektion veranschaulicht zwei Methoden zum Erstellen von Vorhersagen auf Grundlage eines Modells Python: batch-Bewertung und Bewertung zeilenweise.

- **Batchbewertung:** um mehrere Zeilen mit Eingabedaten bereitzustellen, übergeben Sie eine SELECT-Abfrage als Argument an die gespeicherte Prozedur. Das Ergebnis ist eine Tabelle mit Beobachtungen eingabefälle entspricht.
- **Einzelne Bewertung:** als Eingabe einen Satz von Werten der einzelnen Parameter zu übergeben.  Die gespeicherte Prozedur gibt eine einzelne Zeile oder einen Wert zurück.

Alle Python-Code, die erforderlich sind, für die Bewertung wird im Rahmen der gespeicherten Prozeduren bereitgestellt.

| Name der gespeicherten Prozedur | Batch oder einzelne | Modell-Quelle|
|----|----|----|
|PredictTipRxPy|Batch| Revoscalepy-Modell|
|PredictTipSciKitPy|Batch |Scikit-Modells lernen|
|PredictTipSingleModeRxPy|einzelne Zeile| Revoscalepy-Modell|
|PredictTipSingleModeSciKitPy|einzelne Zeile| Scikit-Modells lernen|

## <a name="batch-scoring"></a>Batchbewertung

Die ersten beiden gespeicherten Prozeduren veranschaulichen die grundlegende Syntax für einen Aufruf der Python-Vorhersage in einer gespeicherten Prozedur umschließen. Sowohl gespeicherten Prozeduren erfordern eine Tabelle mit Daten als Eingaben.

- Der Name des Modells mit genauen wird als Eingabeparameter für die gespeicherte Prozedur bereitgestellt. Die gespeicherte Prozedur das serialisierte Modell aus der Datenbanktabelle lädt `nyc_taxi_models`.table, verwenden die SELECT-Anweisung in der gespeicherten Prozedur.
- Das serialisierte Modell in der Python-Variablen gespeichert ist `mod` zur weiteren Verarbeitung mithilfe von Python.
- Die neue Fälle, die bewertet werden müssen erhalten Sie vom der [!INCLUDE[tsql](../../includes/tsql-md.md)] in angegebene Abfrage `@input_data_1`. Wenn die Abfragedaten gelesen werden, werden die Zeilen im Standard-Datenrahmen, `InputDataSet`, gespeichert.
- Sowohl gespeicherte Prozedur aus Funktionen verwenden `sklearn` um eine Metrik Genauigkeit AUC (Bereich unter der Kurve) zu berechnen. Genauigkeitsmetriken, z. B. AUC können nur generiert, wenn Sie auch die Ziel-Bezeichnung angeben (die _Geneigter_ Spalte). Vorhersagen ist nicht erforderlich, die Ziel-Bezeichnung (Variable `y`), jedoch die Genauigkeit Metrik Berechnung.

    Aus diesem Grund Wenn Sie nicht über die Ziel-Bezeichnungen für die Daten zu bewertendes verfügen, Sie können ändern Sie die gespeicherte Prozedur, um die AUC Berechnungen zu entfernen und nur die Wahrscheinlichkeiten im Tipp aus Funktionen zurückgeben (Variable `X` in der gespeicherten Prozedur).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Die gespeicherte Prozedur sollte bereits für Sie erstellt haben. Wenn Sie es nicht finden, führen Sie die folgenden T-SQL-Anweisungen, um die gespeicherten Prozeduren zu erstellen.

Diese gespeicherte Prozedur erfordert ein Modell basierend auf den Scikit-Paket, erfahren Sie, weil für das Paket bestimmte Funktionen verwendet:

+ Die Eingaben mit Datenrahmen übergeben der `predict_proba` Funktion des logistischen Regressionsmodells `mod`. Die `predict_proba` Funktion (`probArray = mod.predict_proba(X)`) gibt eine **"float"** , die die Wahrscheinlichkeit, die gewährt wird, Tipps und Tricks (beliebige Anzahl) darstellt.

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

### <a name="predicttiprxpy"></a>PredictTipRxPy

Diese gespeicherte Prozedur verwendet die gleichen Eingaben und den gleichen Typ von Faktoren wie der vorherigen Prozedur erstellt, aber Funktionen aus der **Revoscalepy** Paket mit SQL Server-Machine Learning bereitgestellt.

> [!NOTE] 
> Der Code für diese gespeicherte Prozedur hat sich leicht zwischen frühen Versionen und die RTM-Version, um Änderungen an das Paket Revoscalepy widerzuspiegeln geändert. Finden Sie unter der [Änderungen](#changes) Tabelle Details.

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
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
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

## <a name="run-batch-scoring-using-a-select-query"></a>Führen Sie die batchbewertung mithilfe einer SELECT-Abfrage

Die gespeicherten Prozeduren **PredictTipSciKitPy** und **PredictTipRxPy** zwei Eingabeparameter erfordern: 

- Die Abfrage, die die Daten für die Bewertung abruft
- Der Name eines trainierten Modells

Durch diese Argumente werden an die gespeicherte Prozedur übergeben, können Sie wählen Sie ein bestimmtes Modell oder ändern Sie die Daten für die Bewertung verwendet.

1. Verwenden der **Scikit-Informationen** für die Bewertung zu modellieren, rufen Sie die gespeicherte Prozedur **PredictTipSciKitPy**, übergeben Sie den Modellnamen und Abfragezeichenfolge als Eingaben.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    Die gespeicherte Prozedur liefert vorhergesagte Wahrscheinlichkeiten für jede Reise, die als Teil der Eingabeabfrage übergeben wurde. 
    
    Wenn Sie SSMS (SQL Server Management Studio) zum Ausführen von Abfragen verwenden, erscheint die Wahrscheinlichkeiten als Tabelle in der **Ergebnisse** Bereich. Die **Nachrichten** Bereich gibt die Genauigkeit Metrik (AUC oder Bereich unter der Kurve) mit einem Wert von ca. 0.56.

2. Verwenden der **Revoscalepy** für die Bewertung zu modellieren, rufen Sie die gespeicherte Prozedur **PredictTipRxPy**, übergeben Sie den Modellnamen und Abfragezeichenfolge als Eingaben.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Einzeiliges Bewertung

In manchen Fällen können anstelle von batchbewertungs, Sie in einem einzigen Gehäuse übergeben möchten Abrufen von Werten aus einer Anwendung, und ein einzelnes Ergebnis basierend auf diesen Werten zurückgegeben. Beispielsweise könnten Sie einrichten eine Excel-Arbeitsblatt, Webanwendung, oder einen Bericht zum Aufrufen der gespeicherten Prozedur, und übergeben Sie sie Eingaben die eingegebenen oder ausgewählten Benutzer.

In diesem Abschnitt erfahren Sie, wie einzelne Vorhersagen zu erstellen, indem zwei gespeicherten Prozeduren aufrufen:

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) dient für die einzelnen Zeile Bewertung mithilfe der Scikit-Modell zu erfahren.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) für die einzelnen Zeile Bewertung unter Verwendung des Modells Revoscalepy dient.
+ Wenn Sie noch nicht geschehen ein Modell trainiert, wiederherstellen, [Schritt 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Beide Modelle werden als Eingabe eine Reihe von einzelnen Werten, z. B. Reisenden Count, Reise Abstand usw. Eine Funktion mit Tabellenrückgabe `fnEngineerFeatures`, wird verwendet, um Breiten-und Längengrade der Eingaben in ein neues Feature konvertieren, direkte Abstand. [Lektion 4](sqldev-py4-create-data-features-using-t-sql.md) enthält eine Beschreibung dieser Funktion mit Tabellenrückgabe.

Sowohl gespeicherten Prozeduren erstellen Sie eine Bewertung auf der Grundlage der Python-Modells.

> [!NOTE]
> 
> Es ist wichtig, dass Sie alle Eingabe-Funktionen, die vom Modell Python erforderlich sind, wenn Sie die gespeicherte Prozedur aus einer externen Anwendung aufrufen bereitstellen. Um Fehler zu vermeiden, müssen Sie umgewandelt oder konvertieren Sie die Eingabedaten in einen Datentyp Python zusätzlich zum Überprüfen von Datentypen und Datenlänge.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Nehmen Sie sich den Code der gespeicherten Prozedur zu überprüfen, die mit Bewertung führt die **Scikit-Informationen** Modell.

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

Die folgende gespeicherte Prozedur führt mit Bewertung der **Revoscalepy** Modell.

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
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
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

### <a name="generate-scores-from-models"></a>Generieren von Bewertungen aus Modellen

Nachdem Sie die gespeicherten Prozeduren erstellt wurden, ist es einfach, eine Bewertung, die basierend auf einem Modell zu generieren. Öffnen Sie einfach ein neues **Abfrage** Fenster und eingeben oder Einfügen von Parametern für jede der merkmalspalten. Die sieben erforderlichen Werte für diese Funktion Spalten, in Reihenfolge sind:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Generieren Sie eine Vorhersage mithilfe von der **Revoscalepy** Modell, die diese Anweisung ausführen:
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Generieren Sie ein Ergebnis mithilfe von der **Scikit-Informationen** Modell, die diese Anweisung ausführen:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

Die Ausgabe von beiden Verfahren ist die Wahrscheinlichkeit eines Tipps für die Reise Taxi mit den angegebenen Parametern oder Funktionen bezahlt wird.

### <a name="changes"></a>Änderungen

In diesem Abschnitt werden Änderungen an den Code in diesem Lernprogramm verwendete aufgelistet. Diese Änderungen vorgenommen wurden, entsprechend die neuesten **Revoscalepy** Version. API-Hilfe finden Sie unter [Python-Funktion Bibliotheksverweis](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference).

| Ändern von details | Hinweise|
| ----|----|
| Gelöschte `import pandas` in alle Beispiele| Pandas jetzt standardmäßig geladen.|
| Funktion `rx_predict_ex` geändert`rx_predict`| RTM und Vorabversion Versionen erforderlich sind`rx_predict_ex`|
| Funktion `rx_logit_ex` geändert`rx_logit`| RTM und Vorabversion Versionen erforderlich sind`rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])`in geändert`prob_list = prob_array["tipped_Pred"].values`| Updates API|

Wenn Sie Python-Diensten, die mit einer Vorabversion von SQL Server-2017 installiert haben, wird empfohlen, zu aktualisieren. Sie können auch nur die Python- und R-Komponenten aktualisieren, mit der neuesten Version von Machine Learning-Server. Weitere Informationen finden Sie unter [mithilfe von Bindung zum Aktualisieren einer Instanz von SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="conclusions"></a>Schlussfolgerungen

In diesem Lernprogramm haben Sie gelernt, wie mit Python-Code eingebettet in gespeicherten Prozeduren arbeiten wird. Die Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] kann es viel einfacher, zum Bereitstellen von Python-Modellen zur Vorhersage und Modell Umschulung als Teil einer Enterprise Data-Workflow einzubeziehen.

## <a name="previous-step"></a>Vorherigen Schritt

[Schritt 5: Trainieren Sie, und speichern Sie ein Python-Modell](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Dienste mit Python](../python/sql-server-python-services.md)
