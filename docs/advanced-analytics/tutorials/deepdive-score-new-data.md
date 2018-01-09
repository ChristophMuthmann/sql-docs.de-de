---
title: Bewerten von neuen Daten (SQL und R deep Dive) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9b4192252edff42275acff6902677e3dadd3122e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>Bewerten von neuen Daten (SQL und R deep Dive)

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In diesem Schritt verwenden Sie das logistische Regressionsmodell, das Sie zuvor erstellt haben, um Bewertungen für ein anderes DataSet zu erstellen, die die gleichen unabhängigen Variablen als Eingaben verwendet.

> [!NOTE]
> Sie benötigen Administratorberechtigungen, DDL für einige der folgenden Schritte aus.

## <a name="generate-and-save-scores"></a>Erstellen und Speichern der Ergebnisse
  
1. Aktualisiert die Datenquelle, die Sie zuvor eingerichtet `sqlScoreDS`, um die erforderliche Spalteninformationen hinzuzufügen.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Stellen Sie sicher, dass Sie die Ergebnisse nicht verlieren, erstellen Sie ein neues Datenquellenobjekt. Verwenden Sie dann zum Auffüllen einer neuen Tabelle in das neue Datenquellenobjekt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    Zu diesem Zeitpunkt ist die Tabelle noch nicht erstellt worden. Diese Anweisung definiert lediglich einen Datencontainer.
     
3. Überprüfen Sie den aktuellen Computekontext, und legen Sie ihn bei Bedarf auf den Server fest.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Vor der Ausführung der Vorhersagefunktion, die die Ergebnisse generiert, müssen Sie prüfen, ob eine Ausgabetabelle vorhanden ist. Andernfalls würden Sie eine Fehlermeldung beim Versuch, die neue Tabelle zu schreiben.
  
    Rufen Sie dazu die Funktionen **rxSqlServerTableExists** und **rxSqlServerDropTable**auf, und übergeben Sie den Tabellennamen als Eingabe.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  Die Funktion **rxSqlServerTableExists** fragt den ODBC-Treiber ab und gibt TRUE zurück, wenn die Tabelle existiert, und FALSE, wenn dem nicht so ist.
    -  Die Funktion **RxSqlServerDropTable** führt die DDL-Anweisungen aus, und gibt true zurück, wenn die Tabelle erfolgreich gelöscht, "false" andernfalls.
    - -Verweis auf beide Funktionen Sie hier finden: [RxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. Nun können Sie mithilfe der [RxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) Funktion, um die Ergebnisse zu erstellen, und speichern Sie sie in der neuen Tabelle in der Datenquelle definierten `sqlScoreDS`.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    Die Funktion **rxPredict** ist eine weitere Funktion, die die Ausführung in Remotecomputekontexten unterstützt. Sie können die Funktion **rxPredict** zum Erstellen von Bewertungen aus Modellen verwenden, die mithilfe von [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)oder [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)erstellt wurden.
  
    - Der Parameter *writeModelVars* wurde in diesem Beispiel auf **TRUE** festgelegt. Dies bedeutet, dass die Variablen, die für die Schätzung verwendet wurden, in die neue Tabelle aufgenommen werden.
  
    - Der Parameter *predVarNames* gibt die Variable an, in der Ergebnisse gespeichert werden. Hier werden Sie eine neue Variable bestanden `ccFraudLogitScore`.
  
    - Der *type* -Parameter für **rxPredict** definiert, wie die Vorhersagen berechnet werden sollen. Geben Sie das Schlüsselwort **Antwort** zum Generieren von Bewertungen, die basierend auf der Skala die antwortvariable. Oder verwenden Sie das Schlüsselwort **Link** zum Generieren von Bewertungen, die basierend auf den zugrunde liegenden Link-Funktion in diesem Fall werden Vorhersagen erstellt, mithilfe einer logistischen Skala.

6. Nach einer Weile können Sie die Tabellenliste in Management Studio aktualisieren, um die neue Tabelle und deren Daten anzuzeigen.

7. Verwenden Sie zum Hinzufügen von zusätzlichen Variablen zu den Ausgabevorhersagen das *extraVarsToWrite*-Argument.  Z. B. im folgenden Code wird die Variable `custID` wird in der Ausgabetabelle von Vorhersagen aus den bewerteten Datentabelle hinzugefügt.
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>Anzeigen der Ergebnisse in einem Histogramm

Nachdem die neue Tabelle erstellt wurde, können zu berechnen und ein Histogramm mit der 10.000 vorhergesagten Bewertungen anzeigen. Berechnung ist schneller, wenn Sie niedrigen und hohen Werte angeben, also, die aus der Datenbank abrufen und Ihre Arbeitsdaten werden hinzugefügt.

1. Erstellen Sie eine neue Datenquelle `sqlMinMax`, Abfragen, bei denen die Datenbank auf den niedrigen und hohen Werte zu erhalten.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     In diesem Beispiel wird veranschaulicht, wie einfach die Verwendung von **RxSqlServerData** -Datenquellobjekten ist, um beliebige Datasets auf Grundlage von SQL-Abfragen, Funktionen oder gespeicherten Prozeduren zu definieren und diese anschließend in Ihrem R-Code zu verwenden. Die Variable speichert nicht die eigentlichen Werte, sondern lediglich die Datenquellendefinition. Die Abfrage wird ausgeführt, um die Werte nur dann zu generieren, wenn sie in einer Funktion wie **rxImport**verwendet wird.
      
2. Rufen Sie die [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) Funktion die Werte in einem Datenrahmen, die gemeinsam genutzt werden kann über rechenkontexte versetzt.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **Ergebnisse**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. Die maximalen und minimalen Werte verfügbar sind, verwenden Sie die Werte zum Erstellen einer anderen Datenquelle für die generierten Ergebnisse.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Verwenden Sie das Datenquellenobjekt `sqlOutScoreDS` erhalten die Ergebnisse zu berechnen und ein Histogramm angezeigt. Fügen Sie bei Bedarf den Code hinzu, um den Computekontext festzulegen.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Ergebnisse**
  
    ![Komplexes von R erstelltes Histogramm](media/rsql-sue-complex-histogram.png "complex histogram created by R")
  
## <a name="next-step"></a>Nächster Schritt

[Umwandeln von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Erstellen von Modellen](../../advanced-analytics/tutorials/deepdive-create-models.md)


