---
title: Bewerten von neuen Daten | Microsoft Docs
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 752f4722906d580c7b1da208ac9bd641d0bae1c5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="score-new-data"></a>Auswertung neuer Daten

Nachdem Sie ein Modell für Vorhersagen erstellt haben, müssen Sie es mit Daten aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank füttern, um Vorhersagen zu generieren.

Sie verwenden das logistische Regressionsmodell *logitObj*zum Erstellen von Auswertungen für einen weiteren Datensatz, das dieselben unabhängigen Variablen als Eingaben verwendet.

> [!NOTE]
> Sie benötigen DDL-Administratorberechtigungen für einige der folgenden Schritte.

## <a name="generate-and-save-scores"></a>Erstellen und Speichern der Ergebnisse
  
1. Aktualisieren Sie die Datenquelle *sqlScoreDS*, die Sie zuvor eingerichtet haben, um die erforderlichen Spalteninformationen hinzuzufügen.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Sie werden ein neues Datenquellenobjekt erstellen und damit eine neue Tabelle in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank auffüllen, um sicherzustellen, dass die Ergebnisse nicht verloren gehen.
  
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
  
    -  Die Funktion RxSqlServerTableExists fragt den ODBC-Treiber ab und gibt "true" zurück, wenn die Tabelle "false" vorhanden, andernfalls ist.
    -  Die RxSqlServerDropTable-Funktion führt die DDL-Anweisungen aus und gibt "true" zurück, wenn die Tabelle erfolgreich, "false" andernfalls gelöscht wird.
  
5. Nun können Sie mithilfe der Funktion **rxPredict** die Bewertungen erstellen und diese in der neuen Tabelle speichern, die in der Datenquelle *sqlScoreDS*definiert ist.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    Die RxPredict-Funktion ist eine andere Funktion, die auf remote rechenkontexte unterstützt. Sie können die RxPredict-Funktion verwenden, Bewertungen aus mit RxLinMod, RxLogit oder RxGlm erstellte Modelle erstellen.
  
    - Der Parameter *writeModelVars* wurde in diesem Beispiel auf **TRUE** festgelegt. Dies bedeutet, dass die Variablen, die für die Schätzung verwendet wurden, in die neue Tabelle aufgenommen werden.
  
    - Der Parameter *predVarNames* gibt die Variable an, in der Ergebnisse gespeichert werden. Im oben angeführten Beispiel wird eine neue Variable namens *ccFraudLogitScore*übergeben.
  
    - Die *Typ* -Parameter für RxPredict definiert, wie die Vorhersagen berechnet werden soll. Legen Sie das Schlüsselwort **response** fest, um Auswertungen basierend auf der Skala der response-Variable zu generieren. Verwenden Sie alternativ das Schlüsselwort **Link** , um Auswertungen basierend auf der zugrunde liegenden link-Funktion zu generieren. In diesem Fall werden die Vorhersagen auf Grundlage einer logistischen Skala generiert.

6. Nach einer Weile können Sie die Tabellenliste in Management Studio aktualisieren, um die neue Tabelle und deren Daten anzuzeigen.

7. Sie können zum Hinzufügen von zusätzlichen Variablen zu den Ausgabevorhersagen das Argument *extraVarsToWrite* verwenden.  Im folgenden Beispiel wird z.B. die Variable *custID* aus der Auswertungsdatentabelle zu der Ausgabetabelle der Vorhersagen hinzugefügt.
  
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

## <a name="display-scores-in-a-histogram"></a>Anzeigen der Auswertungen in einem Histogramm

Nachdem die neue Tabelle erstellt wurde, berechnen Sie ein Histogramm von 10.000 vorhergesagten Auswertungen, und zeigen Sie es an. Die Berechnung wird schneller, wenn Sie die hohen und niedrigen Werte angeben, sodass Sie diese aus der Datenbank abrufen und Ihren Arbeitsdaten hinzufügen können.

1. Erstellen Sie eine neue Datenquelle *sqlMinMax*, die die Datenbank nach den hohen und niedrigen Werten abfragt.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Aus diesem Beispiel können Sie sehen, wie einfach RxSqlServerData Datenquellenobjekte verwenden, um beliebige Datasets basierend auf SQL-Abfragen, Funktionen oder gespeicherte Prozeduren zu definieren und verwenden Sie diese in Ihrem R-Code. Die Variable nicht die tatsächlichen Werte, die nur die Datenquellendefinition gespeichert; die Abfrage wird ausgeführt, um die Werte zu generieren, nur, wenn Sie ihn in einer Funktion wie RxImport verwenden.
      
2. Rufen Sie die RxImport-Funktion zum Einfügen einer Compute kontextübergreifend die Werte in einem Datenrahmen, der gemeinsam genutzt werden kann.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **Ergebnisse**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. Die maximalen und minimalen Werte verfügbar sind, verwenden Sie die Werte die Bewertung Datenquelle zu erstellen.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Verwenden Sie schließlich das Auswertungsdatenquell-Objekt, um die Auswertungsdaten abzurufen und ein Histogramm zu berechnen und anzuzeigen. Fügen Sie bei Bedarf den Code hinzu, um den Computekontext festzulegen.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Ergebnisse**
  
    ![Komplexes von R erstelltes Histogramm](media/rsql-sue-complex-histogram.png "complex histogram created by R")
  
## <a name="next-step"></a>Nächster Schritt

[Transformieren von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Erstellen von Modellen](../../advanced-analytics/tutorials/deepdive-create-models.md)


