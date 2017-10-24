---
title: Transformieren von Daten mithilfe von R | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10670f1a5ac3e002d67eab076c41b822b2e757fd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="transform-data-using-r"></a>Transformieren von Daten mithilfe von R

Das **RevoScaleR** -Paket stellt mehrere Funktionen zum Transformieren von Daten in verschiedenen Phasen der Analyse bereit:

- **rxDataStep** kann zum Erstellen und Transformieren von Datenteilmengen verwendet werden.

- **rxImport** unterstützt das Transformieren von Daten, da Daten in eine XDF-Datei importiert oder aus dieser exportiert oder in einen Datenrahmen im Arbeitsspeicher importiert werden.

- Obwohl die Funktionen **rxSummary**, **rxCube**, **rxLinMod**und **rxLogit** nicht speziell für die Datenverschiebung vorgesehen sind, unterstützen sie jedoch alle dynamische Datentransformationen.

In diesem Abschnitt erfahren Sie, wie Sie diese Funktionen verwenden. Beginnen wir mit RxDataStep.

## <a name="use-rxdatastep-to-transform-variables"></a>Verwenden von rxDataStep zum Transformieren von Variablen

Die RxDataStep-Funktion verarbeitet einen Datenblock gleichzeitig aus einer Datenquelle lesen und Schreiben in eine andere. Sie können die Spalten angeben, die transformiert werden sollen, die zu ladenden Transformationen usw.

Um dieses Beispiel interessant zu gestalten, verwenden Sie eine Funktion aus einem anderen R-Paket zum Transformieren Ihrer Daten.  Das Paket **boot** stellt eines der „empfohlenen“ Pakete dar, was bedeutet, dass **Start** in jeder Verteilung von R enthalten ist, jedoch nicht automatisch beim Starten geladen wird. Aus diesem Grund sollte das Paket schon auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verfügbar sein, die Sie mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]verwenden.

Aus dem Paket **boot** verwenden Sie die Funktion `inv.logit`, die die Umkehrfunktion eines Logit berechnet. Das bedeutet, dass die Funktion `inv.logit` ein Logit zurück zu einer Wahrscheinlichkeit auf der Skala [0,1] konvertiert.

> [!TIP] 
> Eine weitere Möglichkeit zum Abrufen von Vorhersagen in diesem Maßstab wäre, legen Sie die *Typ* Parameter **Antwort** in den ursprünglichen Aufruf von RxPredict.

1. Erstellen Sie zunächst eine Datenquelle, die die Daten aufnimmt, die für die Tabelle *ccScoreOutput*bestimmt sind.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Fügen Sie eine weitere Datenquelle hinzu, um die Daten für die Tabelle ccScoreOutput2 aufzunehmen.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    In der neuen Tabelle erhalten Sie alle Variablen aus der vorherigen Tabelle *ccScoreOutput* sowie die neu erstellte Variable.
  
3. Legen Sie den Computekontext auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz fest.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Verwenden Sie die Funktion RxSqlServerTableExists, um zu überprüfen, ob die Ausgabetabelle *ccScoreOutput2* bereits vorhanden ist und wenn dies der Fall ist, verwenden Sie die Funktion RxSqlServerDropTable auf die Tabelle zu löschen.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Rufen Sie die RxDataStep-Funktion, und geben Sie die gewünschten Transformationen in einer Liste.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Wenn Sie die Transformationen definieren, die für die einzelnen Spalten angewendet werden, können Sie auch alle zusätzlichen R-Pakete angeben, die für die Durchführung der Transformationen notwendig sind.  Weitere Informationen zu den Arten von Transformationen, die Sie ausführen können, finden Sie unter  [Transforming and Subsetting Data (Transformieren von Daten und Erstellen von Teilmengen)](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform).
  
6. Aufrufen von RxGetVarInfo, um eine Zusammenfassung der Variablen in das neue Dataset anzuzeigen.
  
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

Beachten Sie, dass die Faktorvariablen als Zeichendaten in die Tabelle *ccScoreOutput2* geschrieben wurden.  Um diese als Faktoren in nachfolgenden Analysen zu verwenden, geben Sie die Ebenen mit dem Parameter *colInfo* an.

## <a name="next-step"></a>Nächster Schritt

[Laden von Daten in den Arbeitsspeicher mit rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

