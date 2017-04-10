---
title: "Lektion 5: Bereitstellen und Verwenden des Modells (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Lektion 5: Bereitstellen und Verwenden des Modells (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
In dieser Lektion werden Sie R-Modelle in einer Produktionsumgebung verwenden, indem Sie das persistente Modell in einer gespeicherten Prozedur einschließen. Sie können anschließend die gespeicherte Prozedur aus R oder jeder beliebigen Anwendungsprogrammiersprache aufrufen, die [!INCLUDE[tsql](../../includes/tsql-md.md)] (z.B. C#, Java, Python usw) unterstützt, um das Modell zum Treffen von Vorhersagen für neue Beobachtungen zu verwenden.  
  
Es gibt zwei Möglichkeiten, ein Modell für die Bewertung aufzurufen:  
  
-   Mit dem**Batchbewertungsmodus** können Sie mehrere Vorhersagen auf Grundlage von Eingaben einer SELECT-Abfrage erstellen.  
  
-   Mit dem**Einzelbewertungsmodus** können Sie eine Vorhersage nach der anderen erstellen, indem Sie einen Satz von Funktionswerten für einen individuellen Fall an die gespeicherte Prozedur übermitteln, die eine einzige Vorhersage oder andere Werte als Ergebnis zurückgibt.  
  
Sie erfahren, wie Sie Vorhersagen mithilfe der Einzelbewertung und der Batchbewertung erstellen.  
  
## <a name="batch-scoring"></a>Batchbewertung  
Der Einfachheit halber können Sie eine gespeicherte Prozedur verwenden, die erstellt wurde, als Sie das PowerShell-Skript erstmalig in Lektion 1 ausgeführt haben. Diese gespeicherte Prozedur führt folgende Aktionen aus:  
  
-   Ruft einen Satz von Eingabedaten als SQL-Abfrage ab    
-   Ruft das trainierte logistische Regressionsmodell auf, das Sie in der vorherigen Lektion gespeichert haben    
-   Sagt die Möglichkeit voraus, dass der Fahrer ein Trinkgeld bekommt  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>Verwenden der gespeicherten Prozedur „PredictTipBatchMode“

1. Betrachten Sie kurz das Skript, das die gespeicherte Prozedur *PredictTipBatchMode* definiert. Es veranschaulicht verschiedene Aspekte wie ein Modell mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]operationalisiert werden kann.  
  
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

    + Beachten Sie die SELECT-Anweisung, die das gespeicherte Modell aufruft. Sie können jedes beliebige trainierte Modell in einer SQL-Tabelle speichern, indem Sie eine Spalte des Typs **varbinary(max)**verwenden. In diesem Code wird das Modell aus der Tabelle abgerufen, die in der SQL-Variable _@lmodel2_ gespeichert ist, und als Parameter *mod* an die gespeicherte Systemprozedur [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) übergeben.
    + Die Eingabedaten, die für die Bewertung verwendet werden, werden als Zeichenfolge an die gespeicherte Prozedur übergeben.  
  
        Um die Eingabedaten für dieses bestimmte Modell zu definieren, erstellen Sie eine Abfrage, die gültige Daten zurückgibt. Wenn Daten aus der Datenbank abgerufen werden, befinden sich diese in einem Datenrahmen namens *InputDataSet*. Alle Zeilen in diesem Datenrahmen werden für die Batchbewertung verwendet.
        + *InputDataSet* ist der Standardname für die Eingabedaten der Prozedur [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sie können bei Bedarf einen anderen Variablennamen definieren.
        + Die gespeicherte Prozedur ruft die *rxPredict*-Funktion aus der **RevoScaleR**-Bibliothek auf, um die Bewertung zu generieren.
    + Der Rückgabewert für die gespeicherte Prozedur, *Score*, ist eine vorhergesagte Wahrscheinlichkeit, dass der Fahrer ein Trinkgeld bekommen wird.  
  
2.  (Optional) Sie können einfach eine Art Filter auf die zurückgegebenen Werten anwenden, um die Rückgabewerte in Gruppen wie „Ja, Trinkgeld“ oder „Kein Trinkgeld“ zu kategorisieren.  Eine Wahrscheinlichkeit von weniger als 0,5 würde beispielsweise bedeuten, dass eher kein Trinkgeld gegeben wird.  
  
3.  Aufrufen der gespeicherten Prozedur im Batchmodus:  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>Einzelzeilenbewertung  

Anstatt eine Abfrage zu verwenden, um die Eingabewerte an das gespeicherte R-Modell zu übermitteln, möchten Sie möglicherweise die Funktionen als Argumente in der gespeicherten Prozedur angeben.  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>Verwenden der gespeicherten Prozedur „PredictTipSingleMode“
1.  Nehmen Sie sich eine Minute zum Untersuchen des folgenden Codes für die gespeicherte Prozedur *PredictTipSingleMode*, die bereits in Ihrer Datenbank erstellt worden sein sollte.  
  
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
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, 
            @trip_distance,  
            @trip_time_in_secs,  
            @pickup_latitude,  
            @pickup_longitude,  
            @dropoff_latitude,  
            @dropoff_longitude)  
        '  
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
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
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
    ```  
  
    Diese gespeicherte Prozedur nimmt Funktionswerte als Eingabe, z.B. die Anzahl der Reisenden und die Wegstrecke, bewertet diese Funktionen mithilfe des gespeicherten R-Modells und gibt eine Bewertung aus.  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>Aufrufen der gespeicherten Prozedur und Übergeben von Parametern

1. In SQL Server Management Studio können Sie über [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** die gespeicherte Prozedur aufrufen und an sie die erforderlichen Eingaben übergeben. .  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    Die hier übergebenen Werte stehen für _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_und _dropoff_longitude_(in dieser Reihenfolge).  
  
2.  Um diesen gleichen Aufruf von R-Code ausführen zu können, definieren Sie einfach eine R-Variable, die den gesamten Aufruf der gespeicherten Prozedur enthält. 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    Die hier übergebenen Werte stehen für _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_und _dropoff_longitude_(in dieser Reihenfolge).  
  
### <a name="generate-scores"></a>Generieren von Bewertungen

1. Rufen Sie die *sqlQuery*-Funktion des **RODBC**-Pakets auf, und übergeben Sie die Verbindungszeichenfolge und Zeichenfolgenvariable mit dem Aufruf der gespeicherten Prozedur.  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    Weitere Informationen zu **RODBC** finden Sie unter [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery).  
  
## <a name="conclusion"></a>Fazit  
Da Sie nun gelernt haben, mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten zu arbeiten und trainierte R-Modelle dauerhaft in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu speichern, sollte es relativ einfach für Sie sein, einige zusätzliche Modelle auf Grundlage dieses Datasets zu erstellen. Beispielsweise möchten Sie versuchen, Modelle wie diese zu erstellen:  
  
-   Ein Regressionsmodell, das die Höhe des Trinkgelds vorhersagt    
-   Ein klassenübergreifendes Klassifizierungsmodell, dass vorhersagt, ob das Trinkgeld hoch, nicht so hoch oder wenig sein wird.  

Wir empfehlen außerdem, dass Sie sich einige dieser Beispiele und Ressourcen anschauen: 
+ [Szenarien für Data Science und Lösungsvorlagen](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [Datenbankinterne Advanced Analytics](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R: Eintauchen in die Datenanalyse](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [Zusätzliche Ressourcen](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lektion 4: Erstellen und Speichern des Modells&#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
