---
title: Verschieben von Daten zwischen SQL Server und XDF-Datei (SQL und R deep Dive) | Microsoft Docs
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
dev_langs:
- R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 19502fbed507fff36c038145d0e4dbd683d7acdc
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>Verschieben von Daten zwischen SQL Server und XDF-Datei (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In diesem Schritt erfahren Sie, um eine XDF-Datei zu verwenden, um die Datenübertragung zwischen remote und lokalen rechenkontexten. Das Speichern der Daten in einer XDF-Datei können Sie Transformationen für die Daten ausführen.

Wenn Sie fertig sind, Sie verwenden die Daten in der Datei zum Erstellen eines neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. Die Funktion [RxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) Transformationen auf die Daten anwenden und führt die Konvertierung zwischen Datenrahmen und xdf-Dateien.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Erstellen Sie eine SQL Server-Tabelle aus einer XDF-Datei

In dieser Übung verwenden Sie die Kreditkarte Betrug Daten erneut. In diesem Szenario wurden Sie gebeten, zusätzliche Analysen für Benutzer in den US-Bundesstaaten Kalifornien, Oregon und Washington durchzuführen. Um weitere werden haben effiziente, Sie sich entschieden, Speichern von Daten für die nur diese Zustände auf dem lokalen Computer, und Arbeiten mit Variablen Geschlecht, Karteninhabern, Status und Lastenausgleich.

1. Verwenden Sie erneut die `stateAbb` Variable, die Sie zuvor identifiziert die Ebenen enthalten, und Schreiben in eine neue Variable erstellt `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Ergebnisse**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. Definieren Sie die Daten, die Sie von SQL Server, bringen möchten mithilfe einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage.  Später verwenden Sie diese Variable als die *InData* Argument für **RxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Stellen Sie sicher, dass keine ausgeblendeten Zeichen, wie z. B. Zeilenvorschübe oder Registerkarten, in der Abfrage vorhanden sind.
  
3. Als Nächstes definieren Sie die Spalten aus, die beim Arbeiten mit Daten in r verwenden Z. B. fallen in kleineren Dataset nur drei Ebenen von Faktor, da die Abfrage gibt Daten für nur drei Status zurück.  Anwenden der `statesToKeep` Variable zur Identifizierung der richtigen Ebenen enthalten.
  
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
    
    Die [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) Funktion kann Daten aus beliebigen unterstützten Datenquellen in einer lokalen XDF-Datei importieren. Verwenden eine lokale Kopie der Daten eignet sich, wenn Sie viele verschiedene Analysen der Daten zu tun möchten, aber vermeiden Sie dieselbe Abfrage immer wieder ausführen möchten.

5. Erstellen Sie das Datenquellenobjekt durch Übergeben der Variablen als Argumente für zuvor definierten **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Rufen Sie **RxImport** , schreiben die Daten in eine Datei namens `ccFraudSub.xdf`, in das aktuelle Arbeitsverzeichnis.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    Die `localDs` zurückgegebenes Objekt die **RxImport** Funktion ist ein Lightweight- **RxXdfData** Datenquellenobjekt, das darstellt der `ccFraud.xdf` Datendatei, die lokal auf dem Datenträger gespeichert.
  
7. Rufen Sie [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) für die XDF-Datei auf, um zu überprüfen, ob das Schema identisch ist.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Ergebnisse**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. Sie können nun beliebige R-Funktionen aufrufen, um das `localDs`-Objekt genau so wie die Quelldaten auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu analysieren. Sie können z. B. nach Geschlecht zusammenfassen:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Da Sie nun wissen, wie Computekontexte verwendet werden und die Arbeit mit verschiedenen Datenquellen kennen, ist es an der Zeit, etwas lustiges auszuprobieren. In der nächsten und letzten Lektion erstellen Sie eine einfache Simulation, die eine benutzerdefinierte R-Funktion auf dem Remoteserver ausgeführt wird.

## <a name="next-step"></a>Nächster Schritt

[Erstellen einer einfachen Simulation](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Analysieren von Daten in einem lokalen Rechenkontext](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



