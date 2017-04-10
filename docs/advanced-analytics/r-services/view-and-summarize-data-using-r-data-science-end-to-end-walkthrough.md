---
title: "Anzeigen und Zusammenfassen von Daten mithilfe von R (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Anzeigen und Zusammenfassen von Daten mithilfe von R (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
Nun arbeiten Sie mit denselben Daten mithilfe von R-Code. Sie erfahren auch, wie Sie die Funktionen im **RevoScaleR**-Paket verwenden, das in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten ist, um Zusammenfassungen von Daten im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Servers zu generieren und die Ergebnisse zurück an Ihre R-Umgebung zu senden.  

Es wird ein R-Skript mit dieser exemplarischen Vorgehensweise bereitgestellt, das den gesamten Code enthält, der für die Erstellung des Datenobjekts, die Generierung von Zusammenfassungen und die Erstellung von Modellen erforderlich ist. Die R-Skriptdatei **RSQL_RWalkthrough.R** befindet sich an dem Speicherort, an dem Sie die Skriptdateien gespeichert haben.  
+ Wenn Sie bereits über Erfahrung mit R verfügen, können Sie das Skript komplett auf einmal ausführen.
+ Für Entwickler, die RevoScaleR gerade erlernen, wird das Skript in diesem Tutorial Zeile für Zeile durchlaufen.
+ Um einzelne Zeilen des Skripts auszuführen, können Sie eine oder mehrere Zeilen in der Datei markieren und dann STRG+EINGABETASTE drücken.    
  
> [!TIP]  Speichern Sie Ihren R-Arbeitsbereich im Falle, dass Sie die restliche exemplarische Vorgehensweise später abschließen möchten.  Auf diese Weise stehen die Datenobjekte und andere Variablen für die Wiederverwendung bereit.   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>Definieren von SQL Server-Datenquellen und Computekontexten
Zum Abrufen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Verwendung in Ihrem R-Code müssen Sie diese Aufgaben ausführen:  
  
- Stellen Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz her.  
- Definieren Sie eine Abfrage mit den Daten, die Sie benötigen, oder geben Sie eine Tabelle oder Sicht an.    
- Definieren Sie einen oder mehrere Computekontexte, die beim Ausführen von R-Code verwendet werden sollen.    
-   Definieren Sie wahlweise Funktionen, die auf die Datenquelle angewendet werden können.  
 

### <a name="load-the-revoscaler-library"></a>Laden der RevoScaleR-Bibliothek

+  Wenn das **RevoScaleR**-Paket noch nicht geladen ist, führen Sie Folgendes aus:
    ```R
    library("RevoScaleR")`.  
    ```  
    Wenn Sie eine Fehlermeldung erhalten, stellen Sie sicher, dass Ihre Entwicklungsumgebung von R die Bibliothek verwendet, die das RevoScaleR-Paket enthält. Verwenden Sie einen Befehl wie `.libPaths())` zum Anzeigen des aktuellen Pfads:  

    Wenn Sie das **RevoScaleR**-Paket zum ersten Mal verwendet haben, rufen Sie in der R-Umgebung die Onlinehilfe durch Eingeben von `help("RevoScaleR")` oder `help("RxSqlServerData")` auf.  

### <a name="create-connection-strings"></a>Erstellen von Verbindungszeichenfolgen


1. Definieren Sie Verbindungszeichenfolgen. In dieser exemplarischen Vorgehensweise haben wir Beispiele für SQL-Anmeldungen und die integrierte Windows-Authentifizierung zusammengestellt. Es wird empfohlen, nach Möglichkeit die Windows-Authentifizierung zu verwenden, um das Speichern von Kennwörtern in Ihrem R-Code zu vermeiden.

    Das verwendete Konto muss über Berechtigungen zum Lesen von Daten und zum Erstellen neuer Tabellen in der angegebenen Datenbank verfügen. Informationen zum Hinzufügen von Benutzern zur SQL-Datenbank und zum Zuweisen der erforderlichen Berechtigungen an die Benutzer finden Sie unter [Häufig gestellte Fragen zu Upgrade und Installation &#40;SQL Server R Services&#41;](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md). 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] Stellen Sie sicher, dass Sie den Servernamen, den Datenbanknamen, den Benutzernamen und das Kennwort bei Bedarf ändern. 
      
  
### <a name="define-and-set-a-compute-context"></a>Erstellen und Festlegen eines Computekontexts  

Als Nächstes definieren Sie einen *Computekontext*, der die Ausführung des R-Codes auf dem SQL Server-Computer ermöglicht. Wenn Sie R verwenden, werden in der Regel alle Vorgänge im Arbeitsspeicher auf Ihrem Computer ausgeführt. Wenn jedoch angegeben wird, dass R-Vorgänge in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ausgeführt werden sollen, können Sie einige Aufgaben parallel ausführen und Serverressourcen besser nutzen.  

Der Computekontext ist standardmäßig lokal. Daher müssen Sie ihn abhängig vom Vorgang explizit festlegen.  


1.  Definieren Sie zunächst einige Variablen, die zum Erstellen des Computekontexts verwendet werden.  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   R nutzt ein temporäres Verzeichnis, das bei der Serialisierung von R-Objekten zwischen Ihrer Arbeitsstation und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer verwendet wird. Sie können das lokale Verzeichnis angeben, das als *SqlShareDir* verwendet wird, oder den Standardnamen übernehmen.  
  
    -   Verwenden Sie *SqlWait*, um anzugeben, ob R auf Ergebnisse warten soll oder nicht.  Eine Erläuterung wartender Aufträge im Vergleich zu nicht wartenden Aufträge finden Sie unter [ScaleR: Verteiltes Computing](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).
  
    -   Verwenden Sie das Argument *SqlConsoleOutput*, um anzugeben, dass Sie die Ausgabe der R-Konsole nicht anzeigen möchten.  
  
2.  Erstellen Sie das Computekontextobjekt mit den bereits definierten Variablen und Verbindungszeichenfolgen, und speichern Sie ihn in der R-Variablen *sqlcc*.  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. Legen Sie den Computekontext fest.
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + `rxSetComputeContext` gibt den zuvor aktiven Computekontext im Hintergrund zurück, sodass Sie ihn verwenden können.
   + `rxGetComputeContext` gibt den aktiven Computekontext zurück.  
  
    Beachten Sie, dass das Festlegen des Computekontexts nur Vorgänge betrifft, die Funktionen im **RevoScaleR**-Paket nutzen. Der Computekontext wirkt sich nicht darauf aus, wie Open-Source-R-Vorgänge erfolgen.  
  
### <a name="create-an-rxsqlserver-data-object"></a>Erstellen des Datenobjekts „RxSqlServer“  

Nachdem Sie die gewünschte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindung definiert haben, können Sie das Datenverbindungsobjekt als Grundlage für die Definition verschiedener Datenquellen verwenden. Eine *Datenquelle* gibt verschiedene Daten an, die Sie für eine Aufgabe verwenden möchten, z.B. zum Trainieren, Erkunden, Bewerten oder Generieren von Features.  
    
Sie definieren Gruppen von SQL Server-Daten mithilfe der *RxSqlServer*-Funktion sowie durch Übergeben einer Verbindungszeichenfolge und der Definition der abzurufenden Daten.  
  
1. Speichern Sie die SQL-Anweisung als Zeichenfolgenvariable. Mit dieser Abfrage werden die Daten definiert, die Sie zum Trainieren des Modells nutzen.    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. Übergeben Sie die Abfragedefinition als Argument an die SQL Server-Datenquelle. Das *colClasses*-Argument gibt das Schema der zurückzugebenden Daten durch Zuordnen der SQL an. 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + Das Argument *colClasses* gibt die zu verwendenden Spaltentypen an, wenn die Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und R verschoben werden. Das ist wichtig, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] andere und mehr Datentypen als R verwendet. Weitere Informationen finden Sie unter [Arbeiten mit R-Datentypen](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
    + Das Argument *rowsPerRead* ist wichtig für das Speichermanagement und effiziente Berechnungen.  Die meisten analytischen Funktionen in[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verarbeiten Daten in Segmenten und sammeln Zwischenergebnisse an, die die endgültigen Berechnungen zurückgeben, nachdem alle Daten gelesen wurden.  Durch Hinzufügen des `rowsPerRead` -Parameters können Sie steuern, wie viele Datenzeilen in jedes Segment für die Verarbeitung eingelesen werden.  Wenn der Wert dieses Parameters zu groß ist, könnte der Datenzugriff möglicherweise langsam sein, da Sie nicht über genügen Speicher verfügen, um einen solch großen Datenblock effizient zu verarbeiten.  Auf einigen Systemen kann sich die Leistung auch verringern, wenn `rowsPerRead` auf einen zu kleinen Wert festgelegt wird.  

> [!TIP] Nachdem das *inDataSource*-Objekt erstellt wurde, können Sie dieses Objekt so oft wie nötig wiederverwenden, um die grundlegenden Informationen über die verwendeten Daten und Variablen zu erhalten, die Daten zu manipulieren und zu transformieren oder sie für das Trainieren eines Modells zu verwenden.  Allerdings enthält das *inDataSource*-Objekt selbst noch keine Daten aus der SQL-Abfrage. Die Daten werden erst in die lokale Umgebung abgerufen, nachdem Sie eine Funktion wie *rxImport* oder *rxSummary* ausgeführt haben.          
  
## <a name="using-the-sql-server-data-in-r"></a>Verwenden der SQL Server-Daten in R  
Sie können nun R-Funktionen auf der Datenquelle anwenden, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten zu untersuchen, zusammenzufassen und in einem Diagramm darzustellen. In diesem Abschnitt testen Sie einige der Funktionen, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bereitgestellt sind und Remotecomputekontexte unterstützen.  
  
-   `rxGetVarInfo`: Verwenden Sie diese Funktion mit jedem beliebigen Datenrahmen oder Satz von Daten in einem Remote-Datenobjekt (auch mit einigen Listen und Matrizen), um Informationen wie die Maximal- und Minimalwerte, den Datentyp sowie die Anzahl der Ebenen in Faktorspalten abzurufen.  
  
    Ziehen Sie es in Erwägung, diese Funktion nach jeder Art von Dateneingabe, Funktionstransformation oder Featureentwicklung auszuführen. So können Sie sicherstellen, dass es sich bei allen Funktionen, die Sie in Ihrem Modell verwenden möchten, um den erwarteten Datentyp handelt, und so Fehler vermieden werden können.  
 
  
-   `rxSummary`: Verwenden Sie diese Funktion, um weitere detaillierte Statistiken zu einzelnen Variablen abzurufen. Sie können auch Werte transformieren, Zusammenfassungen mit Faktorebenen berechnen und diese Zusammenfassungen für den späteren Gebrauch speichern.  
  
  
### <a name="inspect-variables-in-the-data-source"></a>Überprüfen von Variablen in der Datenquelle  
    
+ Rufen Sie die Funktion `rxGetVarInfo`mithilfe der Datenquelle  `inDataSource` als ein Argument auf, um eine Liste der Variablen und der dazugehörigen Datentypen in der Datenquelle zu erhalten.  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    *Ergebnisse:*  
    *Var 1: tipped, Type: integer*  
    *Var 2: fare_amount, Type: numeric*  
    *Var 3: passenger_count, Type: integer*  
    *Var 4: trip_time_in_secs, Type: numeric, Storage: int64*  
    *Var 5: trip_distance, Type: numeric*  
    *Var 6: pickup_datetime, Type: character*  
    *Var 7: dropoff_datetime, Type: character*  
    *Var 8: pickup_longitude, Type: numeric*  
    *Var 9: pickup_latitude, Type: numeric*  
    *Var 10: dropoff_longitude, Type: numeric*  
  
### <a name="create-a-summary-using-r"></a>Erstellen einer Übersicht mithilfe von R

+ Rufen Sie die RevoScaleR-Funktion `rxSummary` auf, um den Fahrpreis basierend auf der Anzahl der Fahrgäste zusammenzufassen. 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + Das erste Argument für `rxSummary` gibt die Formel oder den Begriff an, nach der oder dem zusammengefasst wird. Hier wird die Funktion `F()` verwendet, um die Werte in „passenger_count“ vor der Zusammenfassung in Faktoren zu konvertieren.  
    + Wenn Sie die Statistiken, die ausgegeben werden sollen, nicht angeben, gibt `rxSummary` standardmäßig Mean, StDev, Min, Max und die Anzahl der gültigen und nicht vorhandenen Beobachtungen aus.  
    + Dieses Beispiel enthält Code, um zu messen, wie viel Zeit zwischen dem Start der Funktion und dem Abschluss der Funktion vergangen ist, sodass Sie die Leistung vergleichen können.  
  
    *Ergebnisse*  
    *rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)*  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
    *Number of valid observations: 1000*   
    *Name                          Mean    StdDev   Min Max ValidObs MissingObs*  
    *fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0*   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>Nächster Schritt  
[Erstellen von Graphen und Diagrammen mit R &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lektion 1: Vorbereiten der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
