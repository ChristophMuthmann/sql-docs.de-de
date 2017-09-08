---
title: Verschieben von Daten zwischen SQLServer und XDF-Datei | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
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
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1db44423f71f1808d99a9611062bdc8291640ece
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="move-data-between-sql-server-and-xdf-file"></a>Verschieben von Daten zwischen SQL Server und einer XDF-Datei

Wenn Sie in einen lokalen computekontext arbeiten, haben Sie Zugriff auf beide lokalen Datendateien und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank (definiert als RxSqlServerData-Datenquelle).

In diesem Abschnitt erfahren Sie, wie Daten abgerufen und in einer Datei auf dem lokalen Computer gespeichert werden, sodass Sie die Daten transformieren können. Wenn Sie fertig sind, müssen Sie die Daten in der Datei verwenden, zum Erstellen eines neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle, mithilfe von RxDataStep.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Erstellen einer SQL Server-Tabelle aus einer XDF-Datei

Die RxImport-Funktion können Sie die Daten aus beliebigen unterstützten Datenquellen in einer lokalen XDF-Datei importieren. Die Verwendung einer lokalen Datei eignet sich, wenn Sie verschiedene Analysen der in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank gespeicherten Daten ausführen oder verhindern möchten, dass dieselbe Abfrage immer wieder ausgeführt wird.

Verwenden Sie für diese Übung wieder die Daten über Kreditkartenbetrug. In diesem Szenario wurden Sie gebeten, zusätzliche Analysen für Benutzer in den US-Bundesstaaten Kalifornien, Oregon und Washington durchzuführen. Sie haben sich der Effizienz halber dazu entschieden, Daten nur für diese Bundesstaaten auf Ihrem lokalen Computer zu speichern und mit den Variablen „gender“ (Geschlecht), „cardholder“ (Karteninhaber/in), „state“ (Bundesstaat) und „balance“ (Kontostand) zu arbeiten.

1. Verwenden Sie erneut den Vektor *stateAbb* , den Sie vorher erstellt haben, um die einzuschließenden Ebenen zu identifizieren und die neue Variable *statesToKeep*anschließend in der Konsole auszugeben.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Ergebnisse**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. Nun definieren Sie die Daten, die mithilfe einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage von SQL Server übermittelt werden sollen.  Später verwenden Sie diese Variable als das *inData* -Argument für *rxImport*.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Stellen Sie sicher, dass keine ausgeblendeten Zeichen, wie z. B. Zeilenvorschübe oder Registerkarten, in der Abfrage vorhanden sind.
  
3. Als Nächstes müssen Sie die Spalten aus, die beim Arbeiten mit Daten in r verwenden definieren. Z. B. fallen in kleineren Dataset, nur drei Ebenen von Faktor, da die Abfrage für Daten nur drei Zustände zurückgegeben wird.  Sie können die *statesToKeep* -Variable erneut verwenden, um die richtigen Ebenen zu identifizieren, die eingeschlossen werden sollen.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Festlegen des computekontexts **lokale**, da alle Daten auf dem lokalen Computer verwendet werden soll.
  
    ```R
    rxSetComputeContext("local")
    ```
  
5. Erstellen Sie das Datenquellenobjekt, indem alle Variablen, die gerade als Argumente für RxSqlServerData definierte übergeben.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Rufen Sie dann **RxImport** , schreiben die Daten in eine Datei namens `ccFraudSub.xdf`, in das aktuelle Arbeitsverzeichnis.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    Die *LocalDs* von der Funktion RxImport zurückgegebene Objekt ist ein Lightweight-RxXdfData Datenquellenobjekt, das die ccFraud.xdf-Datendatei, die lokal auf einem Datenträger gespeicherten darstellt.
  
7. Aufrufen von RxGetVarInfo für die XDF-Datei überprüfen, ob das Datenschema identisch ist.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Ergebnisse**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. Sie können nun verschiedene R-Funktionen aufrufen, um das *localDs* -Objekt zu analysieren, so Sie wie die auch mit den Quelldaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfahren würden. Beispiel:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Da Sie nun wissen, wie Computekontexte verwendet werden und die Arbeit mit verschiedenen Datenquellen kennen, ist es an der Zeit, etwas lustiges auszuprobieren. In der nächsten, finalen Lektion, werden Sie eine einfache Simulation mit einer benutzerdefinierten R-Funktion erstellen und sie auf dem Remoteserver ausführen.

## <a name="next-step"></a>Nächster Schritt

[Erstellen Sie eine einfache Simulation](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Analysieren von Daten im lokalen Computekontext.](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)




