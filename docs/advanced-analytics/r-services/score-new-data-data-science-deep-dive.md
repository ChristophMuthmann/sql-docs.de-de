---
title: "Auswertung neuer Daten (Tieferer Einblick in Data Science) | Microsoft Docs"
ms.custom: ""
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
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Auswertung neuer Daten (Tieferer Einblick in Data Science)
Nachdem Sie ein Modell für Vorhersagen erstellt haben, müssen Sie es mit Daten aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank füttern, um Vorhersagen zu generieren.  
  
## Auswertung neuer Daten  
Sie verwenden das logistische Regressionsmodell *logitObj* zum Erstellen von Auswertungen für einen weiteren Datensatz, das dieselben unabhängigen Variablen als Eingaben verwendet.  
  
> [!NOTE]  
> Sie benötigen DDL-Administratorberechtigungen für einige der folgenden Schritte.  
  
1.  Aktualisieren Sie die Datenquelle *sqlScoreDS*, die Sie zuvor eingerichtet haben, um die erforderlichen Spalteninformationen hinzuzufügen.  
  
    ```R  
    sqlScoreDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlScoreTable,   
        colInfo = ccColInfo,   
        rowsPerRead = sqlRowsPerRead)    
    ```  
  
2.  Sie werden ein neues Datenquellenobjekt erstellen und damit eine neue Tabelle in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank auffüllen, um sicherzustellen, dass die Ergebnisse nicht verloren gehen.  
  
    ```R    
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",   
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead )    
    ```  
     Zu diesem Zeitpunkt ist die Tabelle noch nicht erstellt worden. Diese Anweisung definiert lediglich einen Datencontainer.
     
3.  Überprüfen Sie den aktuellen Computekontext, und legen Sie ihn bei Bedarf auf den Server fest.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
4.  Vor der Ausführung der Vorhersagefunktion, die die Ergebnisse generiert, müssen Sie prüfen, ob eine Ausgabetabelle vorhanden ist. Andernfalls wird beim Schreiben der neuen Tabelle ein Fehler ausgegeben.  
  
    Rufen Sie dazu die Funktionen *rxSqlServerTableExists* und *rxSqlServerDropTable* auf, und übergeben Sie den Tabellennamen als Eingabe.  
  
    ```R  
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")   
    ```  
  
    -   Die Funktion *rxSqlServerTableExists* fragt den ODBC-Treiber ab und gibt TRUE zurück, wenn die Tabelle existiert, und FALSE, wenn dem nicht so ist.    
    -   Die Funktion *rxSqlServerDropTable* führt die DDL-Anweisungen aus und gibt TRUE zurück, wenn die Tabelle erfolgreich gelöscht wurde, und FALSE, wenn dem nicht so ist.   
  
5.  Nun können Sie mithilfe der Funktion *rxPredict* die Bewertungen erstellen und diese in der neuen Tabelle speichern, die in der Datenquelle *sqlScoreDS* definiert ist.  
  
    ```R  
    rxPredict(modelObject = logitObj,   
        data = sqlScoreDS,        
        outData = sqlServerOutDS,     
        predVarNames = "ccFraudLogitScore",   
          type = "link",      
        writeModelVars = TRUE,        
        overwrite = TRUE)    
    ```  
  
    Die Funktion *rxPredict* ist eine weitere Funktion, die die Ausführung in Remotecomputekontexten unterstützt. Sie können die Funktion *rxPredict* zum Erstellen von Bewertungen aus Modellen verwenden, die mithilfe von *rxLinMod*, *rxLogit* oder *rxGlm* erstellt wurden.  
  
    -   Der Parameter *writeModelVars* wurde in diesem Beispiel auf **TRUE** festgelegt. Dies bedeutet, dass die Variablen, die für die Schätzung verwendet wurden, in die neue Tabelle aufgenommen werden.  
  
    -   Der Parameter *predVarNames* gibt die Variable an, in der Ergebnisse gespeichert werden. Im oben angeführten Beispiel wird eine neue Variable namens *ccFraudLogitScore* übergeben.  
  
    -   Der *type*-Parameter für *rxPredict* definiert, wie die Vorhersagen berechnet werden sollen. Legen Sie das Schlüsselwort **response** fest, um Auswertungen basierend auf der Skala der response-Variable zu generieren. Verwenden Sie alternativ das Schlüsselwort **Link**, um Auswertungen basierend auf der zugrunde liegenden link-Funktion zu generieren. In diesem Fall werden die Vorhersagen auf Grundlage einer logistischen Skala generiert.  

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
  
## Anzeigen der Auswertungen in einem Histogramm  
Nachdem die neue Tabelle erstellt wurde, berechnen Sie ein Histogramm von 10.000 vorhergesagten Auswertungen, und zeigen Sie es an. Die Berechnung wird schneller, wenn Sie die hohen und niedrigen Werte angeben, sodass Sie diese aus der Datenbank abrufen und Ihren Arbeitsdaten hinzufügen können.  
  
1.  Erstellen Sie eine neue Datenquelle *sqlMinMax*, die die Datenbank nach den hohen und niedrigen Werten abfragt.  
  
    ```R  
    sqlMinMax <- RxSqlServerData(  
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",   
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),   
        connectionString = sqlConnString)    
    ```  
     In diesem Beispiel wird veranschaulicht, wie einfach die Verwendung von *RxSqlServerData*-Datenquellobjekten ist, um beliebige Datasets auf Grundlage von SQL-Abfragen, Funktionen oder gespeicherten Prozeduren zu definieren und diese anschließend in Ihrem R-Code zu verwenden. Die Variable speichert nicht die eigentlichen Werte, sondern lediglich die Datenquellendefinition. Die Abfrage wird ausgeführt, um die Werte nur dann zu generieren, wenn sie in einer Funktion wie *rxImport* verwendet wird.  
      
2.  Rufen Sie die Funktion *rxImport* auf, um die Werte in einem Datenrahmen zu platzieren, der für verschiedene Computekontexte freigegeben werden kann.  
  
    ```R  
    minMaxVals <- rxImport(sqlMinMax)   
    minMaxVals <- as.vector(unlist(minMaxVals))  
  
    ```  
     **Ergebnisse**
 
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3.  Da die minimalen und maximalen Werte nun verfügbar sind, können Sie sie verwenden, um die Auswertungsdatenquelle zu erstellen.  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",    
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead,   
            colInfo = list(ccFraudLogitScore = list(   
                low = floor(minMaxVals[1]),    
                        high = ceiling(minMaxVals[2]) ) ) )  
  
    ```  

  
4.  Verwenden Sie schließlich das Auswertungsdatenquell-Objekt, um die Auswertungsdaten abzurufen und ein Histogramm zu berechnen und anzuzeigen. Fügen Sie bei Bedarf den Code hinzu, um den Computekontext festzulegen.  
  
    ```R  
    # rxSetComputeContext(sqlCompute)   
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)  
  
    ```  
  
    **Ergebnisse**  
  
    ![complex histogram created by R](../../advanced-analytics/r-services/media/rsql-sue-complex-histogram.png "complex histogram created by R")  
  
## Nächster Schritt  
[Lektion 3: Transform Data Using R &#40;Data Science Deep Dive&#41; (Umwandeln von Daten mithilfe von R (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Create Models &#40;Data Science Deep Dive&#41; (Erstellen von Modellen (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## Siehe auch  
[Data Science Deep Dive: Overview &#40;SQL Server R Services&#41; (Tieferer Einblick in Data Science – Übersicht (SQL Server R Services))](http://msdn.microsoft.com/library/mt637368(SQL.130).aspx)  
  
  
  
