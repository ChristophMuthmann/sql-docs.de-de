---
title: 'Schritt 5: Trainieren und Speichern eines Modells mit T-SQL | Microsoft-Dokumentation'
ms.custom: 
ms.date: 07/26/2017
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
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>Schritt 5: Trainieren Sie, und speichern Sie ein Modell mithilfe des T-SQL

In diesem Schritt erfahren Sie, wie zum Trainieren eines Machine Learning-Modells mithilfe der Python-Pakete **Scikit-Informationen** und **Revoscalepy**. Diese Python-Bibliotheken sind mit SQL Server Machine Learning Services bereits installiert, dadurch können Sie die Module zu laden, und rufen Sie die erforderlichen Funktionen von innerhalb einer gespeicherten Prozedur. Sie trainieren dieses Modell mithilfe der zuvor von Ihnen erstellten Datenfunktionen und speichern das trainierte Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle.

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Teilen Sie die Beispieldaten in Trainings- und Testsätze auf

1. Führen Sie die folgenden T-SQL-Befehle zum Erstellen einer gespeicherten Prozedur, die die Daten in der Nyctaxi dividiert\_Beispieltabelle in zwei Teile: Nyctaxi\_Beispiel\_Trainings- und Nyctaxi\_Beispiel\_testen.

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

2. Führen Sie die gespeicherte Prozedur, und geben Sie eine ganze Zahl, die den Prozentsatz der Daten, die in das Trainingsdataset darstellt. Die folgende Anweisung würde z. B. 60 % der Daten in das Trainingsdataset zuordnen. Trainings- und Testdaten werden in zwei separaten Tabellen gespeichert.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>Erstellen ein logistischen Regressionsmodells mit Scikit-Informationen

In diesem Abschnitt erstellen Sie eine gespeicherte Prozedur, die zum Trainieren eines Modells mit den Trainingsdaten, die Sie soeben vorbereitet verwendet werden kann. Diese gespeicherte Prozedur die Eingabedaten definiert und verwendet eine **Scikit-Informationen** Funktion, um ein Logistisches Regressionsmodell zu trainieren. Rufen Sie die Python-Laufzeit, die mit SQL Server installiert ist, mithilfe der gespeicherten Systemprozedur, [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Zum Trainieren des Modells zu erleichtern, können Sie den Aufruf von Sp_execute_exernal_script in einer anderen gespeicherten Prozedur umschließen und in den neuen Trainingsdaten als Parameter übergeben. In diesem Abschnitt begleiten Sie durch diesen Prozess.

1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], öffnen Sie ein neues **Abfrage** Fenster und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModelSciKitPy_.  Beachten Sie, dass die gespeicherte Prozedur eine Definition der Eingabedaten, enthält daher brauchen Sie eine Eingabeabfrage bereitzustellen.

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
      import pandas
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

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>Erstellen eines logistischen Modells mit dem _Revoscalepy_ Paket

Erstellen Sie eine andere gespeicherte Prozedur, die die neue verwendet jetzt **Revoscalepy** Paket um ein Logistisches Regressionsmodell zu trainieren. Die **Revoscalepy** Python enthält Objekte, Transformation und Algorithmen wie für der Sprache R-Paket **"revoscaler"** Paket. Mit dieser Bibliothek können Sie einen computekontext erstellen, Verschieben von Daten zwischen remotecomputekontexten, Transformieren von Daten und Vorhersagemodellen mit gängigen Algorithmen wie z. B. logistische und lineare Regression und Entscheidungsstrukturen zu trainieren. Weitere Informationen finden Sie unter [was Revoscalepy ist?](../python/what-is-revoscalepy.md)

1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], öffnen Sie ein neues **Abfrage** Fenster und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModelRxPy_.  Dieses Modell verwendet auch die Trainingsdaten, die Sie soeben vorbereitet. Da die gespeicherte Prozedur, die bereits eine Definition der Eingabedaten enthält, müssen Sie eine Eingabeabfrage bereitstellen.

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
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - Trainieren ein logistischen Regressionsmodells mithilfe von Revoscalepy-Pakets auf Nyctaxi\_Beispiel\_Trainingsdaten.
    - Die SELECT-Abfrage verwendet die benutzerdefinierte Skalarfunktion _fnCalculateDistance_ zum Berechnen der direkten Entfernung zwischen den Abhol- und Zielorten. Die Ergebnisse der Abfrage werden in der Standardeinstellung Python input-Variable gespeichert `InputDataset`.
    - Python-Skript die Revoscalepy LogisticRegression Funktion aufruft, der Bestandteil von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], um das logistische Regressionsmodell zu erstellen.
    - Die binäre Variable _tipped_ dient als die Spalte *label* oder „outcome“, und das Modell wird mithilfe folgender Funktionsspalten angepasst:  _passenger_count_, _trip_distance_, _trip_time_in_secs_und _direct_distance_.
    - Das trainierte Modell, in der Python-Variablen enthaltenen `logitObj`, serialisiert und als Output-Parameter put [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ausgabe in die Datenbanktabelle eingefügt werden _Nyc_taxi_models_, zusammen mit den Namen, wie eine neue Zeile, damit Sie abgerufen und für zukünftige Vorhersagen verwenden können.

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

[Schritt 6: Operationalisieren des Modells](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Schritt 4: Erstellen von Data-Funktionen, die mithilfe des T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

