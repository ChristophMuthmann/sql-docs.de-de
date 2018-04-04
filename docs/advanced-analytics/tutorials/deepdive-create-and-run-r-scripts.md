---
title: Erstellen und Ausführen von R-Skripts (SQL und R deep Dive) | Microsoft Docs
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
ms.openlocfilehash: 38e32f66f52c442090927296db6cd3d1bec62fd0
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>Erstellen und Ausführen von R-Skripts (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Da Sie nun Ihre Datenquellen eingerichtet und mindestens einen Computekontext festgelegt haben, können Sie leistungsstarke R-Skripts mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden.  In dieser Lektion verwenden Sie die Server-computekontext möchten Sie einige allgemeine den Machine learning-Aufgaben:

- Visualisieren von Daten und Generieren einiger Zusammenfassungsstatistiken
- Erstellen eines linearen Regressionsmodells
- Erstellen eines logistischen Regressionsmodells
- Bewerten von neuen Daten und Erstellen eines Histogramms der Bewertungen

## <a name="change-compute-context-to-the-server"></a>Ändern von computekontext mit dem server

Bevor Sie einen beliebigen R-Code ausführen können, müssen Sie den *aktuellen* oder *aktiven* Computekontext angeben.

1. Um einen Computekontext zu aktivieren, den Sie bereits mit R definiert haben, verwenden Sie die Funktion **rxSetComputeContext** so wie hier dargestellt:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    Sobald Sie diese Anweisung ausführen, alle nachfolgende Berechnungen erfolgen auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im angegebenen Computer die *SqlCompute* Parameter.
  
2. Wenn Sie sich dazu entscheiden, den R-Code lieber auf Ihrer Arbeitsstation auszuführen, können lokalen Computer wieder als Kontext verwenden, indem Sie das Schlüsselwort  **local** verwenden.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    Sie erhalten eine Liste der Schlüsselwörter, die von dieser Funktion unterstützt werden, indem Sie `help("rxSetComputeContext")` in der Befehlszeile von R eingeben.
  
3. Nachdem Sie einen Computekontext angegeben haben, bleibt er aktiv, bis Sie ihn ändern. Alle R-Skripts, die *nicht* in einem Remoteserverkontext ausgeführt werden können, werden lokal ausgeführt.

## <a name="compute-some-summary-statistics"></a>Einige Übersichtsstatistiken zu berechnen

Um die Funktionsweise des computekontexts, versuchen Sie es generiert einige zusammenfassende Statistiken mit der `sqlFraudDS` -Datenquelle.  Beachten Sie, dass das Datenquellenobjekt einfach die Daten definiert, die Sie verwenden; Es wird die computekontext nicht geändert.

+ Verwenden Sie zum Ausführen der Zusammenfassung lokal **RxSetComputeContext** , und geben Sie die _lokale_ Schlüsselwort.
+ Wechseln Sie zum Erstellen der gleichen Berechnungen auf dem SQL Server-Computer zum SQL-Computekontext, den Sie zuvor definiert haben.

1. Rufen Sie die [RxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) Funktion und übergeben der erforderlichen Argumente, z. B. die Formel und die Datenquelle aus, und weisen die Ergebnisse der Variablen `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    Die Sprache "R" stellt viele Funktionen, jedoch **RxSummary** unterstützt die Ausführung auf verschiedenen remote rechenkontexte, einschließlich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Informationen über ähnliche Funktionen finden Sie unter [Zusammenfassungen von Daten mithilfe von RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
2. Wenn die Verarbeitung abgeschlossen ist, können Sie den Inhalt Drucken der `sumOut` Variable an die Konsole.
  
    ```R
    sumOut
    ```
  
    > [!NOTE]
    > Versuchen Sie nicht, die Ergebnisse zu auszugeben, bevor sie vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer zurückgegeben wurden, sonst wird möglicherweise ein Fehler angezeigt.

**Ergebnisse**

*Summary Statistics Results for: ~gender + balance + numTrans +*

 *numIntlTrans + creditLine*

 *Data: sqlFraudDS (RxSqlServerData Data Source)*

 *Number of valid observations: 10000*

 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*

 *balance       4075.0318 3926.558714            0   25626 100000*

 *numTrans        29.1061   26.619923 0     100 10000    0           100000*

 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*

 *creditLine       9.1856    9.870364 1      75 10000    0          100000*

 *Anzahl der Kategorie für das Geschlecht*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male 6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>Maximale und minimale Werte hinzufügen

Auf Grundlage der berechneten Zusammenfassungsstatistiken haben Sie einige nützliche Informationen über die Daten gefunden, die Sie in die Datenquelle für weitere Berechnungen einfügen möchten. Beispielsweise können die minimalen und maximalen Werte verwendet werden, um Histogramme zu berechnen. Aus diesem Grund fügen Sie den hohen und niedrigen Werten auf der **RxSqlServerData** -Datenquelle.

Glücklicherweise [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] beinhaltet optimierte Funktionen, die effizient Ganzzahldaten "categorical" Faktor Daten konvertieren können.

1. Beginnen Sie, indem Sie einige temporäre Variablen einrichten.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Verwenden Sie die Variable `ccColInfo`, die Sie zuvor zum Definieren von Spalten in der Datenquelle erstellt haben.
  
    Fügen Sie einige neue berechnete Spalten zusätzlich hinzu (`numTrans`, `numIntlTrans`, und `creditLine`) auf die spaltenauflistung.
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. Die spaltenauflistung aktualisiert, dass die folgende Anweisung hinzu, erstellen Sie eine aktualisierte Version des gelten die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenquelle, die Sie zuvor definiert.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    Die `sqlFraudDS` Datenquelle enthält nun die neuen Spalten hinzugefügt, mit `ccColInfo`.
  

An diesem Punkt beeinflussen die Änderungen nur das Datenquellenobjekt in R; keine neuen Daten wurde noch der Datenbanktabelle geschrieben. Sie können jedoch die aufgezeichneten Daten der `sumOut` Variable zum Erstellen von Visualisierungen und Zusammenfassungen. Im nächsten Schritt erfahren Sie, wie beim Wechsel rechenkontexte dazu.

> [!TIP]
> Wenn Sie die computekontext Sie verwenden vergessen, führen Sie `rxGetComputeContext()`.  Ein Rückgabewert von "RxLocalSeq Compute Context" gibt an, dass Sie im lokalen rechenkontext ausgeführt werden.

## <a name="next-step"></a>Nächster Schritt

[Visualisieren von SQL Server-Daten mit R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Definieren und Verwenden von Rechenkontexten](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
