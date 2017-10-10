---
title: Ein R-Modell zu erstellen und speichern in SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 281f5026bc3aa7dc67cff418eb0868eeb81bc80a
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="build-an-r-model-and-save-to-sql-server"></a>Ein R-Modell zu erstellen und speichern in SQL Server

In diesem Schritt erfahren Sie, wie Sie ein Machine Learning-Modells erstellen und speichern Sie das Modell in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="create-a-classification-model-using-rxlogit"></a>Erstellen eines klassifizierungsmodells mit rxLogit

Das Modell erstellen ist eine binäre Klassifizierung, die vorhersagt, ob der Treiber Taxi wahrscheinlich einen Hinweis für einen bestimmten fuhr oder nicht abgerufen wird. Verwenden Sie die Datenquelle in der vorherigen Lektion zum Trainieren des Klassifizierers Tipp erstellten verwenden der logistischen Regression.

1. Rufen Sie die [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) -Funktion auf, die im **RevoScaleR** -Paket enthalten ist, um ein logistisches Regressionsmodell zu erstellen. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    Der Aufruf, der das Modell erstellt, wird in der system.time-Funktion eingeschlossen. Dadurch können Sie die erforderliche Zeit zum Erstellen des Modells abrufen.

2. Nachdem Sie das Modell erstellt haben, können Sie überprüfen, mit der `summary` -Funktion, und zeigen Sie die Koeffizienten.

    ```R
    summary(logitObj);
    ```

     *Ergebnisse*

     *Die logistische Regression Ergebnisse für: Geneigter ~ Passenger_count Trip_distance + Trip_time_in_secs +*
     <br/>*direct_distance*
     <br/>*Daten: FeatureDataSource (RxSqlServerData-Datenquelle)*
     <br/>*Dependent Variable(s): Geneigter*
     <br/>*Gesamtanzahl der unabhängigen Variablen: 5*
     <br/>*Anzahl der gültigen Beobachtungen: 17068*
     <br/>*Anzahl der fehlenden Beobachtungen: 0*
     <br/>*-2\*LogLikelihood: 23540.0602 (Residual basiert auf 17063 Freiheitsgrade)*
     <br/>*Koeffizienten:*
     <br/>*Estimate Std. Fehlerwert Z Pr (> | Z |)*
     <br/>*(Intercept) - 2.509e-03 3.223e-02-0.078 0.93793*
     <br/>*Passenger_count-5.753e-02 1.088e-02-5.289 1.23e-07\*\*\**
     <br/>*Trip_distance-3.896e-02 1.466e-02-2.658 0.00786\*\**
     <br/>*Trip_time_in_secs 2.115e-4.336e 04-05 4.878 1.07e-06\*\*\**
     <br/>*Direct_distance 6.156e-02 2.076e-02 2.966 0.00302\*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     <br/>*Anzahl der endgültigen Varianz-kovarianzmatrix Bedingung: 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>Verwenden des logistischen Regressionsmodells für die Bewertung

Da das Modell bereits erstellt wurde, können Sie es verwenden, um vorherzusagen, ob der Fahrer eher eine Trinkgeld für eine bestimmte Fahrt erhält oder nicht.

1. Verwenden Sie zuerst die [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) Funktion, um ein Datenquellenobjekt für das Speichern von bewerteten Resul definieren

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Um dieses Beispiel zu vereinfachen, wird die Eingabe für das logistische Regressionsmodell verwendet die gleiche Funktion-Datenquelle (`sql_feature_ds`), dass Sie zum Trainieren des Modells verwendet.  Es wird in der Regel vorkommen, dass Sie neue Daten bewerten müssen oder andere Daten für das Testen oder Trainieren beiseite gestellt haben.
  
    + Die Ergebnisse werden in der Tabelle gespeichert werden _TaxiscoreOutput_. Beachten Sie, dass das Schema für diese Tabelle nicht definiert wird, wenn Sie mithilfe von RxSqlServerData erstellen. Das Schema wird aus der Ausgabe RxPredict abgerufen.
  
    + Zum Erstellen der Tabelle, die die vorhergesagten Werte speichert, muss die SQL-Anmeldung RxSqlServer Data-Funktion mit DDL-Administratorrechte in der Datenbank verfügen. Wenn die Anmeldung Tabellen erstellen kann, schlägt die Anweisung fehl.

2. Rufen Sie die Funktion [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) auf, um Ergebnisse zu generieren.

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Wenn die Anweisung erfolgreich ausgeführt wird, sollte es auszuführende etwas dauern. Nach Abschluss des Vorgangs können SQL Server Management Studio öffnen und stellen Sie sicher, dass die Tabelle erstellt wurde und enthält die Ergebnisspalte und andere Ausgabe erwartete.

## <a name="plot-model-accuracy"></a>Zeichnen Sie die Genauigkeit von Miningmodellen

Um eine Vorstellung von der Genauigkeit des Modells zu erhalten, können Sie die [RxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) Funktion, um die Empfänger Betrieb Kurve zu zeichnen. Da RxRoc zu den neuen Funktionen, die von der "revoscaler"-Paket bereitgestellte ist, unterstützt remote rechenkontexte, stehen Ihnen zwei Optionen zur Verfügung:

+ Sie können die RxRoc-Funktion und zum erneuten Ausführen des Diagramms in der remote-computekontext des Diagramms auf den lokalen Client verwenden.

+ Sie können die Daten auch in Ihren Clientcomputer importieren und andere Zeichenfunktionen von R verwenden, um das Leistungsdiagramm zu erstellen.

In diesem Abschnitt experimentieren Sie mit beiden Techniken.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Erstellen eines Diagramms im Remotecomputekontext (SQL Server)

1. Rufen Sie die Funktion RxRoc, und geben Sie die Daten, die zuvor definierten als Eingabe.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Dieser Aufruf gibt die Werte, die beim Berechnen des Diagramms ROC verwendet. Die Bezeichnungsspalte ist _Geneigter_, verfügt über die tatsächlichen Ergebnisse vorhersagen möchten, während die _Score_ Spalte hat die Vorhersage.

2. Um tatsächlich das Diagramm zu zeichnen, können Sie speichern die ROC-Objekt und zeichnen Sie dann mit der `plot` Funktion. Das Diagramm auf die remote-computekontext erstellt, und an Ihre R-Umgebung zurückgegeben.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Zeigen Sie das Diagramm aus, öffnen Sie das R-Grafikgerät oder durch Klicken auf die **zeichnen** Fenster in RStudio.

    ![ROC-Zeichnung für das Modell](media/rsql-e2e-rocplot.png "ROC plot for the model")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Erstellen der Zeichnungen im lokalen Computekontext mithilfe von Daten aus SQL Server

1. Für den lokalen computekontext ist der Prozess nahezu identisch. Verwenden Sie die [RxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) Funktion, um die angegebenen Daten in Ihrer lokalen R-Umgebung einzubinden.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Die Daten im lokalen Speicher verwenden, laden Sie die **ROCR** Verpacken und die Vorhersagefunktion aus diesem Paket verwenden, um einige neuen Vorhersagen zu erstellen.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generieren Sie eine lokale Darstellung, basierend auf den Werten in der Output-Variable gespeicherten `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![Zeichnen der Modellleistung mithilfe von R](media/rsql-e2e-performanceplot.png "plotting model performance using R")

> [!NOTE]
> Die Diagramme möglicherweise Workflowklasse, je nach Anzahl der Datenpunkte unterschiedlich aussehen, die Sie verwendet.

## <a name="deploy-the-model"></a>Bereitstellen des Modells

Nachdem Sie ein Modell erstellt und ermittelt, dass sie gut funktioniert haben, möchten Sie möglicherweise für einen Standort bereitstellen, in dem Benutzer oder Personen in Ihrer Organisation vornehmen können, Verwenden des Modells oder vielleicht trainieren und kalibrieren Sie das Modell in regelmäßigen Abständen neu. Dieser Vorgang wird manchmal als *operationalisieren* eines Modells.

Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können Sie die aufrufen ein R-Modell mithilfe einer [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur ist leicht mit R in einer Clientanwendung verwenden.

Bevor Sie jedoch das Modell aus einer externen Anwendung aufrufen können, müssen Sie das Modell in der Datenbank speichern, die für Produktion verwendet wird. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]werden trainierte Modelle im Binärformat in einer einzelnen Spalte des Typs **varibnary(max)**gespeichert.

Daher umfasst das Verschieben eines trainierten Modells aus R in SQL Server diese Schritte:

+ Serialisieren des Modells in eine hexadezimale Zeichenfolge

+ Übertragen des serialisierten Objekts in die Datenbank

+ Speichern des Modells in einer varbinary(max)-Spalte

In diesem Abschnitt erfahren Sie, wie das Modell beibehalten und zum Aufrufen, um vorhersagen zu treffen.

1. Wechseln Sie zu Ihrer lokalen R-Umgebung zurück, wenn Sie nicht bereits verwenden, serialisieren Sie des Modells und in einer Variablen zu speichern.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Öffnen Sie eine ODBC-Verbindung mit **RODBC**.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    Sie können den Aufruf von RODBC weglassen, wenn Sie bereits das Paket geladen haben.

3. Rufen Sie die gespeicherte Prozedur erstellt, indem das PowerShell-Skript, um die binäre Darstellung des Modells in einer Spalte in der Datenbank zu speichern.

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    Das Speichern eines Modells in einer Tabelle erfordert nur eine INSERT-Anweisung. Allerdings ist es einfacher, wenn in einer gespeicherten Prozedur, z. B. umschlossen _PersistModel_.

    > [!NOTE]
    > Wenn Sie eine Fehlermeldung wie z. B. "die EXECUTE-Berechtigung wurde verweigert auf das Objekt PersistModel" Stellen Sie sicher, dass es sich bei Ihrer Anmeldung über die Berechtigung verfügt. Sie können explizite Berechtigungen für nur die gespeicherte Prozedur erteilen, indem Sie eine T-SQL-Anweisung wie folgt ausführen:`GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. Nachdem Sie ein Modell erstellt haben und in einer Datenbank gespeichert, Sie können diese aufrufen direkt aus [!INCLUDE[tsql](../../includes/tsql-md.md)] code mithilfe der gespeicherten Systemprozedur, [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    Mit jedem Modell, die Sie häufig verwenden, ist es jedoch einfacher Eingabeabfrage und der Aufruf an das Modell sowie anderen Parametern in einer benutzerdefinierten gespeicherten Prozedur umschließen.

    Hier ist der vollständige Code für eine gespeicherte Prozedur. Es wird empfohlen, damit sie leichter verwalten und Aktualisieren der R-Modelle in wie diese gespeicherte Prozedur erstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > Verwenden der **SET NOCOUNT ON** -Klausel, um zu verhindern, dass zusätzliche Ergebnis legt websiteisolation SELECT-Anweisungen.


In der nächsten und letzten Lektion erfahren Sie, wie zum Ausführen der Bewertung anhand der gespeicherten Modells mit [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="next-lesson"></a>Nächste Lektion

[Das R-Modell bereitstellen und dort in SQL nutzen](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Erstellen Sie mithilfe von R und SQL Data-Funktionen](walkthrough-create-data-features.md)


