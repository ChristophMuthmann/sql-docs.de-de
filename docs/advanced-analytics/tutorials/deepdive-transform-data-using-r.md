---
title: Transformieren von Daten mithilfe von R (SQL und R deep Dive) | Microsoft Docs
ms.date: 12/24/2017
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
ms.openlocfilehash: ad675c9e3cfbf7c48e8391131a8e32318cce65af
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>Transformieren von Daten mithilfe von R (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Das **RevoScaleR** -Paket stellt mehrere Funktionen zum Transformieren von Daten in verschiedenen Phasen der Analyse bereit:

- **rxDataStep** kann zum Erstellen und Transformieren von Datenteilmengen verwendet werden.

- **rxImport** unterstützt das Transformieren von Daten, da Daten in eine XDF-Datei importiert oder aus dieser exportiert oder in einen Datenrahmen im Arbeitsspeicher importiert werden.

- Obwohl die Funktionen **rxSummary**, **rxCube**, **rxLinMod**und **rxLogit** nicht speziell für die Datenverschiebung vorgesehen sind, unterstützen sie jedoch alle dynamische Datentransformationen.

In diesem Abschnitt erfahren Sie, wie Sie diese Funktionen verwenden. Beginnen wir mit [RxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).

## <a name="use-rxdatastep-to-transform-variables"></a>Verwenden Sie RxDataStep zum Transformieren von Variablen

Die Funktion **rxDataStep** verarbeitet Daten abschnittsweise und liest aus einer Datenquelle und schreibt in eine andere. Sie können die Spalten angeben, die transformiert werden sollen, die zu ladenden Transformationen usw.

Um dieses Beispiel interessant zu machen, ermöglicht die Verwendung einer Funktion aus einem anderen R-Paket zum Transformieren der Daten.  Das Paket **boot** stellt eines der „empfohlenen“ Pakete dar, was bedeutet, dass **Start** in jeder Verteilung von R enthalten ist, jedoch nicht automatisch beim Starten geladen wird. Aus diesem Grund sollte das Paket schon auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verfügbar sein, die Sie mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]verwenden.

Aus der **Boot** Verpacken, verwenden Sie die Funktion `inv.logit`, berechnet den Kehrwert der eine Logit. Das bedeutet, dass die Funktion `inv.logit` ein Logit zurück zu einer Wahrscheinlichkeit auf der Skala [0,1] konvertiert.

> [!TIP] 
> Eine weitere Möglichkeit zum Abrufen von Vorhersagen in diesem Maßstab wäre, legen Sie die *Typ* Parameter **Antwort** in den ursprünglichen Aufruf von RxPredict.

1. Starten Sie durch das Erstellen einer Datenquelle zum Speichern der Daten für die Tabelle bestimmt `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Hinzufügen einer anderen Datenquelle zum Speichern der Daten für die Tabelle `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    Speichern Sie in der neuen Tabelle alle Variablen aus dem vorherigen `ccScoreOutput` Tabelle sowie die neu erstellte Variable.
  
3. Legen Sie den Computekontext auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz fest.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Verwenden Sie die Funktion **RxSqlServerTableExists** zu überprüfen, ob die Ausgabetabelle `ccScoreOutput2` bereits vorhanden ist und wenn dies der Fall ist, verwenden Sie die Funktion **RxSqlServerDropTable** auf die Tabelle zu löschen.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Rufen Sie die Funktion **rxDataStep** auf, und geben Sie die gewünschten Transformationen in einer Liste an.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Wenn Sie die Transformationen definieren, die für die einzelnen Spalten angewendet werden, können Sie auch alle zusätzlichen R-Pakete angeben, die für die Durchführung der Transformationen notwendig sind.  Weitere Informationen zu den Arten von Transformationen, die Sie ausführen können, finden Sie unter [Transformation und Teilmenge von Daten mithilfe von RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Rufen Sie **rxGetVarInfo** auf, um eine Zusammenfassung der Variablen im neuen Dataset anzuzeigen.
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **Ergebnisse**
    
    *Var 1: ccFraudLogitScore, Type: numeric*
    
    *Var 2: state, Type: character*
    
    *Var 3: gender, Type: character*
    
    *Var 4: cardholder, Type: character*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Type: numeric*

Die ursprünglichen Logit-Ergebnisse werden beibehalten, jedoch wurde eine neue Spalte, *ccFraudProb*, hinzugefügt, in der die Logit-Ergebnisse als Werte zwischen 0 und 1 dargestellt sind.

Beachten Sie, die die Faktor Variablen in die Tabelle geschrieben wurden `ccScoreOutput2` als Zeichendaten. Um diese als Faktoren in nachfolgenden Analysen zu verwenden, geben Sie die Ebenen mit dem Parameter *colInfo* an.

## <a name="next-step"></a>Nächster Schritt

[Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
