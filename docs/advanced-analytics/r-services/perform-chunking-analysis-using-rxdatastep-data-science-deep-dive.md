---
title: "St&#252;ckweise Analysieren mithilfe von rxDataStep (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# St&#252;ckweise Analysieren mithilfe von rxDataStep (Tieferer Einblick in Data Science)
Mithilfe der Funktion *rxDataStep* können Daten in Blöcken verarbeitet werden, d.h. dass das gesamte Dataset nicht in den Speicher geladen werden und gleichzeitig verarbeitet werden muss, wie es in R traditionell der Fall ist.Dazu müssen Sie die Daten in Blöcken auslesen und R-Funktionen verwenden, um jeden Datenblock zu verarbeiten. Anschließend müssen die Ergebnisse der Zusammenfassung für jeden Block in eine allgemeine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle geschrieben werden.  
  
In dieser Lektion üben Sie dieses Vorgehen, indem Sie die *table*-Funktion in R dazu verwenden, eine Kontingenztafel zu berechnen.  
  
> [!TIP]  
> Dieses Beispiel dient ausschließlich der Veranschaulichung. Wenn Sie echte Datasets tabellarisieren möchten, empfehlen wir die Verwendung der Funktionen *rxCrossTabs* oder *rxCube*, die in **RevoScaleR** integriert und für diese Art von Vorgang optimiert sind.  
  
## Partitionieren von Daten nach Werten  
  
1.  Erstellen Sie zuerst eine benutzerdefinierte R-Funktion namens *ProcessChunk*, die die *table*-Funktion für jeden Datenblock aufruft.  
  
    ```R  
    ProcessChunk <- function( dataList) {      
    # Convert the input list to a data frame and compute contingency table      
    chunkTable <- table(as.data.frame(dataList))   
  
    # Convert table output to a data frame with a single row      
    varNames <- names(chunkTable)     
    varValues <- as.vector(chunkTable)        
    dim(varValues) <- c(1, length(varNames))      
    chunkDF <- as.data.frame(varValues)       
    names(chunkDF) <- varNames   
  
    # Return the data frame, which has a single row   
    return( chunkDF )   
    }    
    ```  
 
  
2.  Legen Sie den Computekontext auf den Server fest.  
  
    ```R  
    rxSetComputeContext( sqlCompute )   
    ```  
  
3.  Sie werden eine SQL Server-Datenquelle für die Daten definieren, die Sie verarbeiten. Beginnen Sie, indem Sie einer Variablen eine SQL-Abfrage zuweisen.   
  
    ```R  
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"   
    ```  

4.  Platzieren Sie diese Variable im *sqlQuery*-Argument einer neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle.  
  
    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,  
        connectionString = sqlConnString,    
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",   
            levels = as.character(1:7))))    
    ```  
     Wenn Sie *rxGetVarInfo* für diese Datenquelle ausgeführt haben, sehen Sie, dass die Datenquelle nur eine einzelne Spalte enthält: *Var 1: DayOfWeek, Type: factor, no factor levels available*.
     
5.  Erstellen Sie vor dem Anwenden dieser Faktorvariablen auf die Quelldaten eine separate Tabelle für die Zwischenergebnisse. In diesem Fall verwenden Sie nur die Funktion *RxSqlServerData*, um die Daten zu definieren, und löschen alle bestehenden gleichnamigen Tabellen.   
  
    ```R  
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)   
    # Check whether the table already exists.  
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }   
    ```  
  
7.  Nun rufen Sie die benutzerdefinierte Funktion *ProcessChunk* auf, um die Daten während des Auslesens zu transformieren, indem die Funktion als *transformFunc*-Argument auf die Funktion *rxDataStep* angewendet wird.  
  
    ```R  
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)   
    ```  
  
8.  Weisen Sie die Ergebnisse von *rxImport* einer Variable zu, und geben Sie die Ergebnisse anschließend in der Konsole aus, um die Zwischenergebnisse von *ProcessChunk* anzuzeigen.  
  
    ```R  
    iroResults <- rxImport(iroDataSource)   
  
    iroResults   
    ```  

**Teilergebnisse**

|      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |
  
9. Summieren Sie die Spalten, und zeigen Sie die Ergebnisse in der Konsole an, um die Endergebnisse aller Blöcke zu berechnen.  
  
    ```R  
    finalResults <- colSums(iroResults)   
  
    finalResults   
    ```  
 **Ergebnisse**
  1  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 
  
10. Rufen Sie *rxSqlServerDropTable* erneut auf, um die Tabelle mit den Zwischenergebnissen zu entfernen.  
  
    ```R  
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)    
    ```  
  
## Nächster Schritt  
[Lektion 4: Analyze Data in Local Compute Context &#40;Data Science Deep Dive&#41; (Analysieren von Daten in einem lokalen Computekontext (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Create New SQL Server Table using rxDataStep &#40;Data Science Deep Dive&#41; (Erstellen einer neuen SQL Server-Tabelle mit rxDataStep (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
