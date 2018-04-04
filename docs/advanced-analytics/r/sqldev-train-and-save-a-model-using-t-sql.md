---
title: 'Lektion 5: Trainieren, und speichern Sie ein Modell mithilfe des T-SQL | Microsoft Docs'
ms.custom: ''
ms.date: 07/26/2016
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7684ee7d8135b00a02cae6c1fdbe9c74da3a041c
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>Lektion 5: Trainieren Sie, und speichern Sie ein Modell mithilfe des T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil eines Lernprogramms für SQL-Entwicklern zum Verwenden von R in SQL Server.

In dieser Lektion erfahren Sie, wie Sie ein Machine Learning-Modell zu trainieren, mithilfe von r Sie Trainieren des Modells mithilfe der Data-Features, die Sie gerade erstellt haben, und speichern Sie dann das trainierte Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. In diesem Fall werden die R-Pakete mit bereits installiert [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], sodass alle Funktionen von SQL erfolgen kann.

## <a name="create-the-stored-procedure"></a>Erstellen Sie die gespeicherte Prozedur

Beim Aufrufen von R in T-SQL, verwenden Sie die gespeicherte Systemprozedur, [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Für Prozesse, die Sie häufig wiederholt, wie z. B. ein Modell Umschulung es ist jedoch einfacher, den Aufruf von kapseln `sp_execute_exernal_script` in einer anderen gespeicherten Prozedur.

1.  Erstellen Sie zunächst eine gespeicherte Prozedur, die den R-Code zum Erstellen des Vorhersagemodells QuickInfo enthält. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], öffnen Sie ein neues **Abfrage** Fenster und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModel_. Diese gespeicherte Prozedur definiert die Eingabedaten und verwendet ein R-Paket, um ein logistisches Regressionsmodell zu erstellen.

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - Allerdings werden um sicherzustellen, dass einige Daten übrig geblieben, zum Testen des Modells, 70 % der Daten nach dem Zufallsprinzip aus der Datentabelle Taxi ausgewählt.
    
    - Die SELECT-Abfrage verwendet die benutzerdefinierte Skalarfunktion _fnCalculateDistance_ zum Berechnen der direkten Entfernung zwischen den Abhol- und Zielorten.  die Ergebnisse der Abfrage werden in der Standardeingabevariable von R, `InputDataset`, gespeichert.
  
    - Ruft das R-Skript die `rxLogit` -Funktion, die eine verbesserte R-Funktionen ist in enthaltenen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], um das logistische Regressionsmodell zu erstellen.
  
        Die binäre Variable _tipped_ dient als die Spalte *label* oder „outcome“, und das Modell wird mithilfe folgender Funktionsspalten angepasst:  _passenger_count_, _trip_distance_, _trip_time_in_secs_und _direct_distance_.
  
    -   Das trainierte Modell, das in der R-Variable `logitObj`gespeichert ist, wird serialisiert und in einen Datenrahmen für die Ausgabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geladen. Diese Ausgabe wird in die Datenbanktabelle _nyc_taxi_models_eingefügt, sodass Sie diese für zukünftige Vorhersagen verwenden können.
  
2.  Führen Sie die Anweisung aus, um die gespeicherte Prozedur erstellt, wenn er nicht bereits vorhanden.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>Generieren Sie das R-Modell mithilfe der gespeicherten Prozedur

Da die gespeicherte Prozedur, die bereits eine Definition der Eingabedaten enthält, müssen Sie eine Eingabeabfrage bereitstellen.

1. Um das R-Modell zu generieren, rufen Sie die gespeicherte Prozedur ohne weitere Parameter:

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. Überwachen der **Nachrichten** Zeitfenster [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] für Nachrichten, die an der R weitergeleitet werden würde **"stdout"** Stream, wie diese Messaage: 

    "Stdout-Meldung(en) aus dem externen Skript: Gelesene Zeilen: 1193025, insgesamt Zeilen verarbeitet: 1193025, Segment Gesamtzeit: 0.093 Sekunden"

    Darüber hinaus möglicherweise Nachrichten, die spezifisch für der jeweiligen Funktion `rxLogit`, die Variablen anzeigen und Testen von Metriken, die als Teil der Modellerstellung generiert.

3.  Wenn die Anweisung abgeschlossen wurde, öffnen Sie die Tabelle *Nyc_taxi_models*. Verarbeitung der Daten und Anpassen des Modells können eine Weile dauern.

    Sie können sehen, dass eine neue Zeile hinzugefügt wurde, die das serialisierte Modell in der Spalte _model_enthält.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

Im nächsten Schritt verwenden Sie das trainierte Modell zum Erstellen von Vorhersagen.

## <a name="next-lesson"></a>Nächste Lektion

[Lektion 6: Operationalisieren des Modells](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Lektion 4: Erstellen von Data-Funktionen, die mithilfe des T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

