---
title: "Lektion 3: Erstellen der Datenfunktionen (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
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
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Lektion 3: Erstellen der Datenfunktionen (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
Data Engineering ist ein weiterer wichtiger Teil des maschinellen Lernens. Häufig müssen Daten transformiert werden, bevor Sie sie für die Vorhersagemodellierung verwenden können. Wenn die Daten nicht über die Features verfügen, die Sie benötigen, können Sie diese aus vorhandenen Werten erstellen.  
  
Sie möchten für diesen Modellierungstask möglicherweise lieber die Entfernung in Meilen zwischen zwei Orten haben anstatt die ungefähren Werte für den Breiten- und Längengrad des Abhol- und Zielorts. Zum Erstellen dieser Funktion berechnen Sie die direkte lineare Entfernung zwischen zwei Punkten mit der [Haversine-Formel](https://en.wikipedia.org/wiki/Haversine_formula).  
Sie vergleichen zwei unterschiedliche Methoden zum Erstellen einer Funktion aus Daten:  
  
-   Mithilfe von R und der `rxDataStep` -Funktion    
-   Mithilfe einer benutzerdefinierten Funktion in [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
Bei beiden Methoden ist das Ergebnis des Codes ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquellenobjekt, `featureDataSource`, das die numerische Funktion `direct_distance`enthält.  
  
## <a name="creating-features-using-r"></a>Erstellen von Funktionen mithilfe von R  

Die Sprache R ist bekannt für ihre großen und vielseitigen statistischen Bibliotheken, doch Sie müssen ggf. weiterhin benutzerdefinierte Datentransformationen erstellen. 

+ Sie erstellen eine neue R-Funktion, `ComputeDist`, um die Luftlinie zwischen zwei Punkten zu berechnen, die durch die Werte für Breiten- und Längengrad angegeben sind.  
+ Sie rufen die Funktion zum Transformieren der Daten im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenobjekt auf, das Sie zuvor erstellt haben, und speichern sie in einer neuen Datenquelle, `featureDataSource`.  

### <a name="create-the-transformation-function"></a>Erstellen der Transformationsfunktion  
1.  Erstellen Sie eine benutzerdefinierte R-Funktion, `ComputeDist`. Sie verwendet zwei Paare von Breiten- und Längengradwerten und berechnet die Luftlinie zwischen diesen.  Die Funktion gibt eine Entfernung in Meilen zurück.
  
    ```R  
    env <- new.env()  
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){  
      R <- 6371/1.609344 #radius in mile  
      delta_lat <- dropoff_lat - pickup_lat  
      delta_long <- dropoff_long - pickup_long  
      degrees_to_radians = pi/180.0  
      a1 <- sin(delta_lat/2*degrees_to_radians)  
      a2 <- as.numeric(a1)^2  
      a3 <- cos(pickup_lat*degrees_to_radians)  
      a4 <- cos(dropoff_lat*degrees_to_radians)  
      a5 <- sin(delta_long/2*degrees_to_radians)  
      a6 <- as.numeric(a5)^2  
      a <- a2+a3*a4*a6  
      c <- 2*atan2(sqrt(a),sqrt(1-a))  
      d <- R*c  
      return (d)  
    }  
    ```  
  
    + Die erste Zeile definiert eine neue Umgebung. In R kann eine Umgebung verwendet werden, um Namespaces z.B. in Paketen einzuschließen.
    + Sie können die `search()` -Funktion verwenden, um die Umgebungen in Ihrem Arbeitsbereich anzuzeigen. Um die Objekte in einer bestimmten Umgebung anzuzeigen, geben Sie `ls(<envname>)`ein. 
    + Die Zeilen, die mit `$env.ComputeDistance` beginnen, enthalten den Code, der die Haversine-Formel definiert, die die *Großkreisentfernung* zwischen zwei Punkten auf einer Kugel berechnet.  
 
  
### <a name="apply-the-transformation-function-to-data"></a>Anwenden der Transformationsfunktion auf Daten

Wenn Sie die Funktion definiert haben, wenden Sie sie auf die Daten an, um eine neue Funktionsspalte, *direct_distance*, zu erstellen.

1. Erstellen Sie mithilfe des Konstruktors `RxSqlServerData` eine Datenquelle, mit der Sie arbeiten möchten.  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  Rufen Sie die `rxDataStep`-Funktion zum Anwenden der `env$ComputeDist`-Funktion auf die angegebenen Daten auf.  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + Die `rxDataStep`-Funktion kann Daten direkt ändern. Die Argumente enthalten einen Zeichenvektor mit Spalten, die über (*varsToKeep*) übergeben werden sollen, sowie eine Liste, die die Transformationen definiert.
    + Alle Spalten, die transformiert werden, werden automatisch ausgegeben und müssen daher nicht in das *varsToKeep* -Argument aufgenommen werden.
    + Alternativ können Sie angeben, dass mithilfe des *varsToDrop* -Arguments alle Spalten in der Quelle eingeschlossen werden sollen, mit Ausnahme der angegebenen Variablen.  
  
4.  Rufen Sie zum Schluss `rxGetVarInfo` auf, um das Schema der neuen Datenquelle zu überprüfen:  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *Ergebnisse*
    
    *"It takes CPU Time=0.74 seconds, Elapsed Time=35.75 seconds to generate features."*  
    *Var 1: tipped, Type: integer*   
    *Var 2: fare_amount, Type: numeric*   
    *Var 3: passenger_count, Type: numeric*   
    *Var 4: trip_time_in_secs, Type: numeric*   
    *Var 5: trip_distance, Type: numeric*   
    *Var 6: pickup_datetime, Type: character*   
    *Var 7: dropoff_datetime, Type: character*   
    *Var 8: pickup_longitude, Type: numeric*   
    *Var 9: pickup_latitude, Type: numeric*   
    *Var 10: dropoff_longitude, Type: numeric*   
    *Var 11: dropoff_latitude, Type: numeric*   
    *Var 12: direct_distance, Type: numeric*   
  
## <a name="creating-features-using-transact-sql"></a>Erstellen von Funktionen mithilfe von Transact-SQL  
Da Sie nun gesehen haben, wie eine Funktion mithilfe einer R-Funktion erstellt wird, können Sie eine benutzerdefinierte SQL-Funktion, `ComputeDist`, verwenden, um dasselbe zu tun. Die SQL-Funktion `ComputeDist` wird auf einem vorhandenen `RxSqlServerData` -Datenobjekt ausgeführt, um die neuen Funktionen für die Entfernung aus den vorhandenen Werten des Breiten- und Längengrads zu erstellen.  
  
Die Ergebnisse der Transformation werden in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenobjekt gespeichert ( `featureDataSource`). Dies ist die gleiche Vorgehensweise wie mit R.  
  
Die Featureentwicklung mit [!INCLUDE[tsql](../../includes/tsql-md.md)] ist oft schneller als R. Wählen Sie daher die effizienteste Methode auf Grundlage Ihrer Daten und Ihrem Task.  

### <a name="define-the-t-sql-custom-function"></a>Definieren der benutzerdefinierten T-SQL-Funktion
  
1.  Definieren Sie eine neue SQL-Funktion, `fnCalculateDistance`.  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END  
  
    ```  

    + Der Code für diese *benutzerdefinierte Funktion* für SQL wurde als Teil des PowerShell-Skripts bereitgestellt, das Sie zur Erstellung und Konfiguration der Datenbank ausgeführt haben.  Die Funktion sollte bereits in Ihrer Datenbank vorhanden sein.  Falls nicht, generieren Sie die Funktion in SQL Server Management Studio in der gleichen Datenbank, in der die Taxidaten gespeichert sind.

2.  Führen Sie z.B. für die Verwendung von [!INCLUDE[tsql](../../includes/tsql-md.md)] die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aus, um zu sehen, wie die Funktion arbeitet.   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>Aufrufen der SQL-Funktion in R

1. Speichern Sie die SQL-Anweisung, die die benutzerdefinierte Funktion in einer R-Variablen aufruft.  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] Diese Abfrage weicht geringfügig von der zuvor verwendeten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage ab. Sie wurde geändert, um ein kleineres Datenbeispiel abzurufen, damit diese exemplarische Vorgehensweise schneller durchgearbeitet werden kann.  
  
4.  Verwenden Sie nun die folgenden Codezeilen, um die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion aus Ihrer R-Umgebung abzurufen und sie auf den Daten anzuwenden, die in `featureEngineeringQuery` definiert sind.  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  Nachdem das neue Feature erstellt wurde, rufen Sie `rxGetVarsInfo` auf, um eine Zusammenfassung der Featuretabelle zu erstellen.  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>Vergleich von R- und SQL-Funktionen

Wie sich herausstellt, ist die Vorgehensweise der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktion für diesen bestimmten Task schneller als die benutzerdefinierte R-Funktion. Verwenden Sie daher die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktion für diese Berechnungen in den nachfolgenden Schritten.  

Fahren Sie mit der nächsten Lektion fort, um zu erfahren, wie ein Vorhersagemodell anhand dieser Daten erstellt wird und wie das Modell in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle gespeichert wird.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 4: Erstellen und Speichern des Modells&#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lektion 2: Anzeigen und Durchsuchen der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
