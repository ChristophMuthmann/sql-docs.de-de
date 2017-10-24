---
title: "Segmentierung Analysen mit RxDataStep ausführen | Microsoft Docs"
ms.custom: 
ms.date: 05/03/2017
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
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af375ddf99794b748699355203becd137227fbcd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="perform-chunking-analysis-using-rxdatastep"></a>Stückweise Analysieren mithilfe von rxDataStep

Mithilfe der Funktion **rxDataStep** können Daten in Blöcken verarbeitet werden, d.h. dass das gesamte Dataset nicht in den Speicher geladen werden und gleichzeitig verarbeitet werden muss, wie es in R traditionell der Fall ist.Dazu müssen Sie die Daten in Blöcken auslesen und R-Funktionen verwenden, um jeden Datenblock zu verarbeiten. Anschließend müssen die Ergebnisse der Zusammenfassung für jeden Block in eine allgemeine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle geschrieben werden.

In dieser Lektion werden Sie diese Technik üben, mithilfe der `table` -Funktion in R, um eine behelfslösung-Tabelle zu berechnen.

> [!TIP]
> Dieses Beispiel dient ausschließlich der Veranschaulichung. Wenn Sie reale Datasets zu Tabellarisieren müssen, wir empfehlen die Verwendung der **RxCrossTabs** oder **RxCube** Funktionen in **"revoscaler"**, die sind optimiert für diese Art von der Vorgang.

## <a name="partition-data-by-values"></a>Partitionieren von Daten nach Werten

1. Erstellen Sie zuerst eine benutzerdefinierte R-Funktion, die Aufrufe der *Tabelle* -Funktion auf jedes Segment von Daten, und nennen Sie sie `ProcessChunk`.
  
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

2. Legen Sie den Computekontext auf den Server fest.
  
    ```R
    rxSetComputeContext( sqlCompute )
    ```
  
3. Sie werden eine SQL Server-Datenquelle für die Daten definieren, die Sie verarbeiten. Beginnen Sie, indem Sie einer Variablen eine SQL-Abfrage zuweisen.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    ```

4. Platzieren Sie diese Variable im *sqlQuery* -Argument einer neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle.
  
    ```R
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
     Wenn Sie *rxGetVarInfo* für diese Datenquelle ausgeführt haben, sehen Sie, dass die Datenquelle nur eine einzelne Spalte enthält: *Var 1: DayOfWeek, Type: factor, no factor levels available*.
     
5. Erstellen Sie vor dem Anwenden dieser Faktorvariablen auf die Quelldaten eine separate Tabelle für die Zwischenergebnisse. Erneut Sie gerade verwenden die RxSqlServerData-Funktion, um die Daten zu definieren, und löschen vorhandenen Tabellen mit demselben Namen.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Nachdem Sie die benutzerdefinierte Funktion aufrufen müssen `ProcessChunk` zum Transformieren der Daten, sobald sie gelesen wird, indem Sie diesen als die *"transformfunc"* Argument für die RxDataStep-Funktion.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Zwischenergebnisse von anzuzeigenden `ProcessChunk`, weisen die Ergebnisse der RxImport einer Variablen, und klicken Sie dann die Ergebnisse werden an die Konsole ausgegeben.
  
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

10. Um die Zwischenergebnisse-Tabelle zu entfernen, stellen Sie einen weiteren Aufruf von RxSqlServerDropTable.
  
    ```R
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)
    ```

## <a name="next-step"></a>Nächster Schritt

[Analysieren von Daten im lokalen Computekontext;](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Erstellen Sie neue SQL Server-Tabelle mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)



