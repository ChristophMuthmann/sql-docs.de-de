---
title: "Schritt 5: Trainieren und Speichern eines Modells mit T-SQL (Tutorial f&#252;r datenbankinterne Advanced Analytics) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Schritt 5: Trainieren und Speichern eines Modells mit T-SQL (Tutorial f&#252;r datenbankinterne Advanced Analytics)
In diesem Schritt erfahren Sie, wie Sie ein Machine Learning-Modell mit R trainieren. Die R-Pakete wurden bereits mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert, Sie können also den Algorithmus von einer gespeicherten Prozedur aufrufen. Sie trainieren dieses Modell mithilfe der zuvor von Ihnen erstellten Datenfunktionen und speichern das trainierte Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle.  
  
## Erstellen eines R-Modells mithilfe gespeicherter Prozeduren  
Alle Aufrufe der R-Laufzeit, die mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert wurde, erfolgen mithilfe der gespeicherten Systemprozedur, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Wenn Sie jedoch ein Modell erneut trainieren müssen, ist es möglicherweise einfacher, den Aufruf von sp_execute_exernal_script in eine andere gespeicherte Prozedur einzuschließen.  
  
In diesem Abschnitt erstellen Sie eine gespeicherte Prozedur, die zum Erstellen eines Modells mithilfe der zuvor von Ihnen vorbereiteten Daten verwendet werden kann. Diese gespeicherte Prozedur definiert die Eingabedaten und verwendet ein R-Paket, um ein logistisches Regressionsmodell zu erstellen.  
  
#### So erstellen Sie die gespeicherte Prozedur  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ein neues Abfragefenster, und führen Sie die folgende Anweisung aus, um die gespeicherte Prozedur _TrainTipPredictionModel_ zu erstellen.  
  
    Da die gespeicherte Prozedur schon eine Definition der Eingabedaten enthält, beachten Sie, dass Sie keine Eingabeabfrage bereitstellen müssen.  
  
    ```  
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
  
    Diese gespeicherte Prozedur führt diese Aktivitäten als Teil des Modelltrainings aus:  
  
    -   Um sicherzustellen, dass einige Daten zum Testen des Modells übrig bleiben, werden 70 % der Daten aus der Datentabelle „Taxi“ nach dem Zufallsprinzip ausgewählt.  
  
    -   Die SELECT-Abfrage verwendet die benutzerdefinierte Skalarfunktion _fnCalculateDistance_ zum Berechnen der direkten Entfernung zwischen den Abhol- und Zielorten.  die Ergebnisse der Abfrage werden in der Standardeingabevariable von R, `InputDataset`, gespeichert.  
  
    -   das R-Skript ruft die `rxLogit`-Funktion auf, die Teil der erweiterten R-Funktionen ist, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten sind, um das logistische Regressionsmodell zu erstellen.  
  
        Die binäre Variable _tipped_ dient als die Spalte *label* oder „outcome“, und das Modell wird mithilfe folgender Funktionsspalten angepasst: _passenger_count_, _trip_distance_, _trip_time_in_secs_ und _direct_distance_.  
  
    -   Das trainierte Modell, das in der R-Variable `logitObj` gespeichert ist, wird serialisiert und in einen Datenrahmen für die Ausgabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen. Diese Ausgabe wird in die Datenbanktabelle _nyc_taxi_models_ eingefügt, sodass Sie diese für zukünftige Vorhersagen verwenden können.  
  
2.  Führen Sie die Anweisung aus, um die gespeicherte Prozedur zu erstellen.  
  
#### So erstellen Sie die das R-Modell mithilfe der gespeicherten Prozedur  
  
1.  Führen Sie diese Anweisung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] aus:  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    Die Verarbeitung der Daten und die Anpassung des Modells könnte eine Weile dauern. Nachrichten, die an den **stdout**-Stream von R weitergeleitet werden würden, werden im Fenster **Meldungen** von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] angezeigt. Beispiel:  
  
  
*STDOUT message(s) from external script: Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds*       
  
Aufeinanderfolgende Datenabschnitte werden gelesen und verarbeitet. Darüber hinaus werden möglicherweise Meldungen angezeigt, die für die individuelle Funktion `rxLogit` spezifisch sind und die Variable und Testmetriken angeben.  
  
2.  Öffnen Sie die Tabelle *nyc_taxi_models*. Sie können sehen, dass eine neue Zeile hinzugefügt wurde, die das serialisierte Modell in der Spalte _model_ enthält.  
  
  
  
*Modell*  
*0x580A00000002000302020....*  
  
Im nächsten Schritt verwenden Sie das trainierte Modell zum Erstellen von Vorhersagen.  
  
## Nächster Schritt  
[Schritt 6: Operationalisieren des Modells](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## Vorheriger Schritt  
[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Siehe auch  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Datenbankinterne Advanced-Analytics für SQL-Entwickler (Tutorial))](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
