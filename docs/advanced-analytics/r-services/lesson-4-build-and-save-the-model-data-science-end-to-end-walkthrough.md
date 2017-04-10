---
title: "Lektion 4: Erstellen und Speichern des Modells (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lektion 4: Erstellen und Speichern des Modells (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
In dieser Lektion erfahren Sie, wie Sie ein Machine Learning-Modell erstellen und das Modell in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]speichern.  
  
## <a name="creating-a-classification-model"></a>Erstellen eines Klassifizierungsmodells  
Das Modell, das Sie erstellen, ist eine binäre Klassifizierung, die vorhersagt, ob der Taxifahrer eher ein Trinkgeld für eine bestimmte Fahrt erhält oder nicht. Verwenden Sie die Datenquelle `featureDataSource,` , die Sie in der vorherigen Lektion erstellt haben, um die Trinkgeld-Klassifizierung mithilfe der logistischen Regression zu trainieren.  
  
Hier sind die Funktionen, die Sie im Modell verwenden:  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>Erstellen des Modells mithilfe von „rxLogit“  
1.  Rufen Sie die *rxLogit*-Funktion auf, die im **RevoScaleR**-Paket enthalten ist, um ein logistisches Regressionsmodell zu erstellen.  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
  
2.  Nachdem Sie das Modell erstellt haben, möchten Sie es wahrscheinlich mithilfe der `summary` -Funktion untersuchen und die Koeffizienten anzeigen.  
  
    ```  
    summary(logitObj)  
    ```  

     *Ergebnisse*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
     *Data: featureDataSource (RxSqlServerData Data Source)*  
     *Dependent variable(s): tipped*  
     *Total independent variables: 5*   
     *Number of valid observations: 17068*  
     *Number of missing observations: 0*   
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*  
     *Coefficients:*  
     *Estimate Std. Error z value Pr(>|z|)*   
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*   
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**  
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**   
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**  
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**   
     *---*  
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*  
     *Condition number of final variance-covariance matrix: 48.3933*   
     *Number of iterations: 4*  
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>Verwenden des logistischen Regressionsmodells für die Bewertung  
Da das Modell bereits erstellt wurde, können Sie es verwenden, um vorherzusagen, ob der Fahrer eher eine Trinkgeld für eine bestimmte Fahrt erhält oder nicht.  
  
1.  Definieren Sie zuerst das Datenobjekt zum Speichern der Bewertungsergebnisse  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + Um dieses Beispiel zu vereinfachen, ist die Eingabe für das logistische Regressionsmodell die gleiche `featureDataSource` , die Sie zum Trainieren des Modells verwendet haben.  Es wird in der Regel vorkommen, dass Sie neue Daten bewerten müssen oder andere Daten für das Testen oder Trainieren beiseite gestellt haben.  
  
    + Die Vorhersageergebnisse werden in der Tabelle _taxiscoreOutput_gespeichert. Beachten Sie, dass das Schema für diese Tabelle bei der Erstellung mit `rxSqlServerData`nicht definiert ist, es aber aus der Objektausgabe *scoredOutput* aus `rxPredict`abgerufen wird.  
  
    + Um die Tabelle zu erstellen, die die vorhergesagten Werte speichert, muss der SQL-Login, der die Datenfunktion `rxSqlServer` ausführt, über DDL-Berechtigungen in der Datenbank verfügen. Wenn dieser Anmeldename keine Tabellen erstellen kann, schlägt die Anweisung fehl.  
  
2.  Rufen Sie die Funktion *rxPredict* auf, um Ergebnisse zu generieren.  
  
    ```R  
    rxPredict(modelObject = logitObj, data = featureDataSource, outData = scoredOutput,   
                       predVarNames = "Score", type = "response",   
                       writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>Zeichnen der Modellgenauigkeit  
Um eine Vorstellung von der Genauigkeit des Modells zu erhalten, können Sie die Funktion *rxRocCurve* verwenden, um die ROC-Kurve (Receiver Operating Characteristics Curve, Grenzwertoptimierungskurve) zu zeichnen. Da *rxRocCurve* eine der neuen Funktionen ist, die vom „RevoScaleR“-Paket bereitgestellt wurden und Remotecomputekontexte unterstützt, haben Sie zwei Möglichkeiten:  
  
+ Sie können die Funktion `rxRocCurve` verwenden, um das Diagramm im Remotecomputekontext auszuführen und anschließend das Diagramm an Ihren lokalen Client zurückgeben.
+ Sie können die Daten auch in Ihren Clientcomputer importieren und andere Zeichenfunktionen von R verwenden, um das Leistungsdiagramm zu erstellen.  
  
In diesem Abschnitt verwenden Sie beide Techniken.  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Erstellen eines Diagramms im Remotecomputekontext (SQL Server)  
  
1.  Rufen Sie die Funktion *rxRocCurve* auf, und stellen Sie die Daten bereit, die zuvor als Eingabe definiert wurden.  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    Beachten Sie, dass Sie auch die Bezeichnungsspalte „tipped“ (die Variable, die Sie zu vorhersagen versuchen) angeben müssen sowie den Namen der Spalte, in der die Vorhersage (_Score_) gespeichert ist.  
  
2.  Sie können das Diagramm anzeigen, indem Sie das Grafikgerät von R öffnen, oder indem Sie in RStudio auf das Fenster **Zeichnung** klicken.  
  
    ![ROC plot for the model](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "ROC plot for the model")  

    Das Diagramm wird im Remotecomputekontext erstellt und anschließend an Ihre R-Umgebung zurückgegeben.   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Erstellen der Zeichnungen im lokalen Computekontext mithilfe von Daten aus SQL Server  
  
1.  Verwenden Sie die Funktion *rxImport*, um die angegebenen Daten in Ihre lokale R-Umgebung zu verschieben.  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  Nachdem Sie die Daten in den lokalen Arbeitsspeicher geladen haben, können Sie anschließend die **ROCR**-Bibliothek öffnen, um einige Vorhersagen zu erstellen und die Zeichnung zu generieren.  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  Das folgende Diagramm wird in beiden Fällen erstellt.  
  
    ![plotting model performance using R](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "plotting model performance using R")  
  
## <a name="deploying-a-model"></a>Bereitstellen eines Modells  

Nachdem Sie ein Modell erstellt und festgestellt haben, dass es ordnungsgemäß ausgeführt wird, möchten Sie möglicherweise das Modell *operationalisieren*. Da Sie mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ein R-Modell mithilfe einer gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur aufrufen können, ist es wirklich einfach, R in einer Clientanwendung zu verwenden.  
  
Bevor Sie jedoch das Modell aus einer externen Anwendung aufrufen können, müssen Sie das Modell in der Datenbank speichern, die für Produktion verwendet wird. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]werden trainierte Modelle im Binärformat in einer einzelnen Spalte des Typs **varibnary(max)** gespeichert.

Daher umfasst das Verschieben eines trainierten Modells aus R in SQL Server diese Schritte:  
  
+ Serialisieren des Modells in eine hexadezimale Zeichenfolge
+ Übertragen des serialisierten Objekts in die Datenbank
+ Speichern des Modells in einer varbinary(max)-Spalte  
  
In diesem Abschnitt erfahren Sie, wie Sie das Modell dauerhaft speichern und wie es zum Treffen von Vorhersagen aufgerufen wird.  
  
### <a name="serialize-the-model"></a>Serialisieren des Modells  
  
+  Serialisieren Sie das Modell in Ihrer lokalen R-Umgebung, und speichern Sie es in einer Variablen.  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    Die Funktion *serialize* ist im R-Paket **base** enthalten und stellt eine einfache Schnittstelle auf niedriger Ebene für die Serialisierung für Verbindungen bereit. Weitere Informationen finden Sie unter [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize).  
  
### <a name="move-the-model-to-sql-server"></a>Verschieben des Modells in SQL Server

+ Öffnen Sie eine ODBC-Verbindung, und rufen Sie eine gespeicherte Prozedur auf, um die binäre Darstellung des Modells in einer Spalte in der Datenbank zu speichern. 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

Das Speichern eines Modells in einer Tabelle erfordert nur eine INSERT-Anweisung. Um es jedoch einfacher zu machen, haben wir hier die gespeicherte Prozedur _PersistModel_ verwendet. 
 
Hier finden Sie den vollständigen Code der gespeicherten Prozedur als Referenz:  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP] Es empfiehlt sich, Hilfsfunktionen wie diese gespeicherte Prozedur zu erstellen, um die Verwaltung und die Aktualisierung Ihrer R-Modelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu vereinfachen.  
  
  
### <a name="invoke-the-saved-model"></a>Aufrufen des gespeicherten Modells  
Nachdem Sie das Modell in der Datenbank gespeichert haben, können Sie es direkt aus dem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code mithilfe der gespeicherten Prozedur [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) aufrufen.  
  
Um z.B. Vorhersagen zu generieren, stellen Sie einfach eine Verbindung mit der Datenbank her, und führen Sie eine gespeicherte Prozedur aus, die zusammen mit einigen Eingabedaten das gespeicherte Modell als Eingabe verwendet.  
  
Wenn Sie jedoch ein Modell besitzen, das Sie häufig verwenden, ist es einfacher, die Eingabeabfrage und den Aufruf an das Modell sowie andere Parameter in einer benutzerdefinierten gespeicherten Prozedur einzubinden.  
  
In der nächsten Lektion erfahren Sie, wie Sie eine Bewertung anhand des gespeicherten Modells mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]ausführen.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 5: Bereitstellen und Verwenden des Modells &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lektion 3: Erstellen der Datenfunktionen &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
