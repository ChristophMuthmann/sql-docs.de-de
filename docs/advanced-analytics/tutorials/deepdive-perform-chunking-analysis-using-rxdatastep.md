---
title: Aufteilung RxDataStep (SQL und R deep Dive) mit Analysen ausführen | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7037ced2194a5076f12f81858e98cc7dc9b89aad
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>Ausführen von Aufteilung Analysen mit RxDataStep (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In dieser Lektion verwenden Sie die **RxDataStep** erfordern, dass das gesamte Dataset in den Arbeitsspeicher geladen und wie bei herkömmlichen r gleichzeitig verarbeitet werden, statt zum Verarbeiten von Daten in Segmenten-Funktion Die **RxDataStep** Funktionen liest die Daten im Segment, gilt R-Funktionen wiederum für jedes Segment von Daten und speichert dann die Zusammenfassung der Ergebnisse für jedes Segment in eine gemeinsame [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle. Wenn alle Daten gelesen wurden, werden die Ergebnisse kombiniert.

> [!TIP]
> In dieser Lektion berechnen Sie eine Notfall-Tabelle anhand der `table` -Funktion in R. In diesem Beispiel dient nur der Veranschaulichung. 
> 
> Wenn Sie reale Datasets zu Tabellarisieren müssen, wir empfehlen die Verwendung der **RxCrossTabs** oder **RxCube** Funktionen in **"revoscaler"**, die sind optimiert für diese Art von der Vorgang.

## <a name="partition-data-by-values"></a>Partitionieren von Daten nach Werten

1. Erstellen Sie eine benutzerdefinierte R-Funktion, die R aufruft `table` -Funktion auf jedes Segment von Daten, und nennen Sie die neue Funktion `ProcessChunk`.
  
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
  
3. Definieren Sie eine SQL Server-Datenquelle, um die Daten aufzunehmen, die Sie verarbeiten möchten. Beginnen Sie, indem Sie einer Variablen eine SQL-Abfrage zuweisen. Verwenden Sie dann diese Variable in der *SqlQuery* Argument eines neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle.
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. Sie können optional ausführen **von RxGetVarInfo** für diese Datenquelle. Zu diesem Zeitpunkt enthält es eine einzelne Spalte: *Var 1: Geben Sie einen Wochentag: verlagern, keine Faktor Ebenen verfügbar*
     
5. Erstellen Sie vor dem Anwenden dieser Faktorvariablen auf die Quelldaten eine separate Tabelle für die Zwischenergebnisse. Erneut, verwenden Sie einfach die RxSqlServerData-Funktion zum Definieren der Daten Makign sicher, dass alle vorhandenen Tabellen mit demselben Namen zu löschen.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Rufen Sie die benutzerdefinierte Funktion `ProcessChunk` zum Transformieren der Daten, sobald sie gelesen wird, indem Sie diesen als die *"transformfunc"* Argument an die **RxDataStep** Funktion.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Zwischenergebnisse von anzeigen `ProcessChunk`, weisen die Ergebnisse der **RxImport** einer Variablen zu, und klicken Sie dann die Ergebnisse werden an die Konsole ausgegeben.
  
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

10. Um die Zwischenergebnisse-Tabelle zu entfernen, stellen Sie einen Aufruf von **RxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>Nächster Schritt

[Analysieren von Daten in einem lokalen Rechenkontext](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Erstellen einer neuen SQL Server-Tabelle mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
