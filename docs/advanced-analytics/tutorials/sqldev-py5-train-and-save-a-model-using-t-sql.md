---
title: 'Schritt 5: Trainieren, und speichern Sie ein Python-Modell mithilfe des T-SQL | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
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
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 11fa031229d8bc08a9091c3fa6f85e81468d7379
ms.contentlocale: de-de
ms.lasthandoff: 10/18/2017

---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>Schritt 5: Trainieren Sie, und speichern Sie ein Python-Modell mithilfe des T-SQL

Dieser Artikel ist Teil eines Lernprogramms [In Datenbank-Python-Analyse für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md). 

In diesem Schritt erfahren Sie, wie zum Trainieren eines Machine Learning-Modells mithilfe der Python-Pakete **Scikit-Informationen** und **Revoscalepy**. Diese Python-Bibliotheken sind mit SQL Server-Machine Learning-Services bereits installiert.

Die Module geladen und die erforderlichen Funktionen zum Erstellen und Trainieren des Modells mithilfe einer gespeicherten SQL Server-Prozedur aufrufen. Das Modell erfordert die Data-Funktionen, die Sie in den früheren Lektionen entwickelt. Speichern Sie Sie abschließend das trainierte Modell an eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.

> [!IMPORTANT]
> Es wurden einige Änderungen hinsichtlich der **Revoscalepy** Paket, d. h. kleinen Änderungen in den Code für dieses Lernprogramm erforderlich. Finden Sie unter der [Änderungsliste](sqldev-py6-operationalize-the-model.md#changes) am Ende dieses Lernprogramms. 
> 
> Wenn Sie Python-Diensten, die mit einer Vorabversion von SQL Server-2017 installiert haben, wird empfohlen, auf die neueste Version zu aktualisieren. 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Teilen Sie die Beispieldaten in Trainings- und Testsätze auf

1. Können Sie die gespeicherte Prozedur **TrainTestSplit** für die Daten in der Nyctaxi\_Beispieltabelle in zwei Teile: Nyctaxi\_Beispiel\_Trainings- und Nyctaxi\_Beispiel\_testen. 

    Diese gespeicherte Prozedur sollte bereits für Sie erstellt werden, jedoch können, führen Sie den folgenden Code aus, um ihn zu erstellen:

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Um Ihre Daten mithilfe einer benutzerdefinierten unterteilten Teilen kann, führen Sie die gespeicherte Prozedur aus, und geben Sie eine ganze Zahl, die den Prozentsatz der Daten, die in das Trainingsdataset darstellt. Die folgende Anweisung würde z. B. 60 % der Daten in das Trainingsdataset zuordnen.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Erstellen eines logistischen Regressionsmodells

Nach der Vorbereitung der Daten können Sie es verwenden, um ein Modell zu trainieren. Dazu rufen eine gespeicherte Prozedur, die einige Python-Code, der als ausführt Eingabe die Datentabelle Training. In diesem Lernprogramm erstellen Sie zwei Modelle, die beide binärer klassifizierungsmodelle:

+ Die gespeicherte Prozedur **TrainTipPredictionModelRxPy** erstellt ein Modell mit Tipp Vorhersage der **Revoscalepy** Paket.
+ Die gespeicherte Prozedur **TrainTipPredictionModelSciKitPy** erstellt ein Modell mit Tipp Vorhersage der **Scikit-Informationen** Paket.

Jede gespeicherte Prozedur verwendet die Eingabedaten Sie zum Erstellen und Trainieren Sie ein Logistisches Regressionsmodell bereitstellen. Alle Python-Code wird in der gespeicherten Systemprozedur umschlossen [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Zum Trainieren des Modells auf neue Daten zu vereinfachen, wird den Aufruf von Sp_execute_exernal_script in einer anderen gespeicherten Prozedur umschließen und in den neuen Trainingsdaten als Parameter übergeben. In diesem Abschnitt begleiten Sie durch diesen Prozess.

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], öffnen Sie ein neues **Abfrage** Fenster und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModelSciKitPy_.  Die gespeicherte Prozedur enthält eine Definition der Eingabedaten, daher brauchen Sie eine Eingabeabfrage bereitzustellen.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
      EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
      import numpy
      import pickle
      from sklearn.linear_model import LogisticRegression
      
      ##Create SciKit-Learn logistic regression model
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      SKLalgo = LogisticRegression()
      logitObj = SKLalgo.fit(X, y)
      
      ##Serialize model
      trained_model = pickle.dumps(logitObj)
      ',
      @input_data_1 = N'
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_training
      ',
      @input_data_1_name = N'InputDataSet',
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT;
      ;
    END;
    GO
    ```

2. Führen Sie die folgende SQL-Anweisungen in das trainierte Modell einzufügende Tabelle nyc\_Taxi_models.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Verarbeitung der Daten und Anpassen des Modells können ein paar Minuten dauern. Nachrichten, die an Python weitergeleitet werden würde **"stdout"** Stream werden angezeigt, der **Nachrichten** Fenster [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Beispiel:

    *Stdout-Meldung(en) aus dem externen Skript:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Öffnen Sie die Tabelle *nyc\_Taxi_models*. Sie können sehen, dass eine neue Zeile hinzugefügt wurde, die das serialisierte Modell in der Spalte _model_enthält.

    *Linear_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Diese gespeicherte Prozedur verwendet die neue **Revoscalepy** Paket, d. h. ein neues Paket für Python. Sie enthält Objekte, Transformation und Algorithmen wie für der Sprache R **"revoscaler"** Paket. 

Mithilfe von **Revoscalepy**, können Sie remote rechenkontexte erstellen, Verschieben von Daten zwischen Kontexte, Transformieren von Daten und Train Vorhersagemodellen mit gängigen Algorithmen wie z. B. logistische und lineare Regression, Entscheidungsstrukturen zu berechnen und Weitere. Weitere Informationen finden Sie unter [was Revoscalepy ist?](../python/what-is-revoscalepy.md)

1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], öffnen Sie ein neues **Abfrage** Fenster und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModelRxPy_.  Da die gespeicherte Prozedur, die bereits eine Definition der Eingabedaten enthält, müssen Sie eine Eingabeabfrage bereitstellen.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    Diese gespeicherte Prozedur führt die folgenden Schritte im Rahmen des modelltrainings:

    - Die SELECT-Abfrage angewendet wird, die benutzerdefinierte Skalarfunktion _FnCalculateDistance_ auf den direkten Abstand zwischen den Standorten übernommen und Ladengeschäft zu berechnen. Die Ergebnisse der Abfrage werden in der Standardeinstellung Python input-Variable gespeichert `InputDataset`.
    - Die binäre Variable _Geneigter_ dient als die *Bezeichnung* oder Ergebnisspalte angezeigt, und das Modell ist zu groß sind folgende Feature Spalten: _Passenger_count_, _Trip_ Abstand_, _Trip_time_in_secs_, und _Direct_distance_.
    - Das trainierte Modell wird serialisiert und in der Python-Variable gespeicherte `logitObj`. Durch das T-SQL-Schlüsselwort Ausgabe hinzufügen, können Sie die Variable als Ausgabe der gespeicherten Prozedur hinzufügen. Im nächsten Schritt diese Variable verwendet, um binären Code des Modells in eine Datenbanktabelle einzufügen _Nyc_taxi_models_. Dieser Mechanismus ermöglicht es leicht zu speichern und Modelle erneut verwenden.

2. Führen Sie die gespeicherte Prozedur wie folgt, um die trainierten einfügen **Revoscalepy** Modell in der Tabelle _nyc\_Taxi\_Modelle.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Verarbeitung der Daten und Anpassen des Modells können eine Weile dauern. Nachrichten, die an Python weitergeleitet werden würde **"stdout"** Stream werden angezeigt, der **Nachrichten** Fenster [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Beispiel:

    *Stdout-Meldung(en) aus dem externen Skript:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Öffnen Sie die Tabelle *nyc_taxi_models*. Sie können sehen, dass eine neue Zeile hinzugefügt wurde, die das serialisierte Modell in der Spalte _model_enthält.

    *Rx_model* *0x8003637265766F7363616c...*

Im nächsten Schritt verwenden Sie die trainierten Modelle Vorhersagen erstellen.

## <a name="next-step"></a>Nächster Schritt

[Schritt 6: Operationalisieren Sie die Python-Modell mithilfe von SQL Server](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

