---
title: "Schritt 6: Operationalisieren des Modells (Tutorial f&#252;r datenbankinterne Advanced Analytics) | Microsoft Docs"
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
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Schritt 6: Operationalisieren des Modells (Tutorial f&#252;r datenbankinterne Advanced Analytics)
In diesem Schritt erfahren Sie, wie Sie das Modell mithilfe einer gespeicherten Prozedur *operationalisieren*. Diese gespeicherte Prozedur kann direkt von anderen Anwendungen aufgerufen werden, um Vorhersagen für neue Beobachtungen zu treffen.  
  
In diesem Schritt lernen Sie zwei Methoden zum Aufrufen eines R-Modells aus einer gespeicherten Prozedur kennen:  
  
-   **Batchbewertungsmodus**: Verwenden Sie eine SELECT-Abfrage, um mehrere Datenzeilen bereitzustellen. Die gespeicherte Prozedur gibt eine Tabelle mit Beobachtungen zurück, die mit den Eingabefällen übereinstimmen.  
  
-   **Einzelbewertungsmodus**: Übergeben Sie einen Satz von einzelnen Parameterwerten als Eingabe.  Die gespeicherte Prozedur gibt eine einzelne Zeile oder einen Wert zurück.  
  
Sehen wir uns zuerst einmal an, wie die Bewertung im Allgemeinen abläuft.  
  
## Grundlegende Bewertung  
Die gespeicherte Prozedur _PredictTip_ beschreibt die grundlegende Syntax für das Umschließen eines Vorhersageaufrufs in einer gespeicherten Prozedur.  
  
```  
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
  
-   Die SELECT-Anweisung ruft das serialisierte Modell aus der Datenbank ab und speichert das Modell in der R-Variable `mod` zur weiteren Verarbeitung mit R.  
  
-   Die neuen Fälle, die bewertet werden, werden aus der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage abgerufen, die in `@inquery` festgelegt ist, dem ersten Parameter für die gespeicherte Prozedur. Wenn die Abfragedaten gelesen werden, werden die Zeilen im Standard-Datenrahmen, `InputDataSet`, gespeichert. Dieser Datenrahmen wird der `rxPredict`-Funktion in R übergeben, die die Bewertungen generiert.  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    Da ein data.frame eine einzelne Zeile enthalten kann, können Sie den gleichen Code für die Batchbewertung und die Einzelbewertung verwenden.  
  
-   Der von der `rxPredict`-Funktion zurückgegebene Wert ist ein **float**-Wert, der die Wahrscheinlichkeit darstellt, dass ein Trinkgeld (beliebige Höhe) gegeben wird.  
  
## Batchbewertung mithilfe einer SELECT-Abfrage  
Jetzt sehen wir uns an, wie die Batchbewertung funktioniert.  
  
1.  Zunächst rufen wir einen kleineren Satz von Eingabedaten ab, mit denen wir arbeiten werden.  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    Diese Abfrage erstellt eine „Top 10“-Liste der Fahrten mit Reisenden sowie anderen Funktionen, die benötigt werden, um eine Vorhersage zu erstellen.  
  
 **Ergebnisse**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
Sie verwenden diese Abfrage als Eingabe für die gespeicherte Prozedur _PredictTipBatchMode_, die als Teil des Downloads bereitgestellt wurde.  
  
2.  Nehmen Sie sich zunächst eine Minute Zeit, um den Code der gespeicherten Prozedur _PredictTipBatchMode_ in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zu überprüfen.  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
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
    ```  
  
3.  Zum Erstellen von Vorhersagen stellen Sie den Text der Abfrage in einer Variable bereit, und übergeben Sie diese mithilfe einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage als Parameter an die gespeicherte Prozedur, so wie hier dargestellt.  
  
    ```  
    -- Specify input query  
  
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
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  Die gespeicherte Prozedur gibt eine Reihe von Werten zurück, die die Vorhersage für jede Fahrt der „Top 10 Fahrten“ darstellt. Wenn wir uns noch einmal die Eingabewerte ansehen, sehen wir, dass alle „Top 10 Fahrten“ mit nur einem Reisenden und einem relativ kurzen Fahrtweg sind. Auf Grundlage dieser Daten lässt sich erkennen, dass der Fahrer für solche Fahrten wohl eher kein Trinkgeld bekommen wird.  
  
    Anstatt nur die „Trinkgeld/ Kein Trinkgeld“-Ergebnisse zurückzugeben, könnten Sie auch den Wahrscheinlichkeitswert für die Vorhersage zurückgeben und anschließend auf die Spalte _Score_ eine WHERE-Klausel anwenden, um die Bewertung als „Trinkgeld“, „Kein Trinkgeld“ zu kategorisieren und dabei einen Schwellenwert wie z.B. 0,5 oder 0,7 verwenden. Dieser Schritt ist nicht in der gespeicherten Prozedur enthalten, aber es wäre leicht, ihn zu implementieren.  
  
## Bewerten einzelner Zeilen  
Gelegentlich möchten Sie einzelne Werte aus einer Anwendung übergeben und ein einzelnes Ergebnis basierend auf diesen Werten erhalten. Beispielsweise könnten Sie ein Excel-Arbeitsblatt, eine Webanwendung oder einen Reporting Services-Bericht einrichten, um die gespeicherte Prozedur aufzurufen und Eingaben bereitzustellen, die von Benutzern eingegeben oder ausgewählt wurden.  
  
In diesem Abschnitt erfahren Sie, wie Sie einzelne Vorhersagen mithilfe einer gespeicherten Prozedur erstellen.  
  
1.  Überprüfen Sie kurz den Code der gespeicherten Prozedur _PredictTipSingleMode_, die als Teil des Downloads enthalten war.  
  
    ```  
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
  
    -   Diese gespeicherte Prozedur besitzt mehrerer einzelner Werte als Eingabe, wie die Anzahl der Reisende, Fahrstrecke usw.  
  
        Wenn Sie die gespeicherte Prozedur aus einer externen Anwendung aufrufen, überprüfen Sie, dass die Daten mit den Anforderungen des R-Modells übereinstimmen. Sie müssen möglicherweise sicherstellen, dass die Eingabedaten in einen R-Datentyp umgewandelt oder konvertiert werden können oder den Datentyp und die Datenlänge überprüfen. Weitere Informationen finden Sie unter [Arbeiten mit R-Datentypen](https://msdn.microsoft.com/library/mt590948.aspx).  
  
    -   Die gespeicherte Prozedur erstellt eine Bewertung auf Grundlage des gespeicherten R-Modells.  
  
2.  Probieren Sie es einfach aus, indem Sie die Werte manuell bereitstellen.  
  
    Öffnen Sie ein neues **Abfrage**-Fenster, rufen Sie die gespeicherte Prozedur auf, und geben Sie dabei noch Parameter für jede Funktionsspalte ein.  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    Die Werte für diese Funktionsspalten sind der Reihe nach hier angeordnet:  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  Die Ergebnisse geben an, dass die Wahrscheinlichkeit, ein Trinkgeld zu erhalten, für diese „Top 10 Fahrten“ sehr niedrig ist, da bei diesen nur ein Reisender über eine relativ kurze Entfernung mitgefahren ist.  
  
## Schlussfolgerungen  
In diesem Tutorial haben Sie erfahren, wie Sie mit R-Code arbeiten, der in gespeicherten Prozeduren eingebettet ist. Die Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] macht es viel einfacher, R-Modelle für Vorhersagen bereitzustellen und das erneute Trainieren von Modellen im Rahmen eines Unternehmensdatenworkflows zu integrieren.  
  
  
## Vorheriger Schritt  
[Schritt 4: Erstellen von Datenfunktionen mit T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Siehe auch  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Datenbankinterne Advanced-Analytics für SQL-Entwickler (Tutorial))](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
