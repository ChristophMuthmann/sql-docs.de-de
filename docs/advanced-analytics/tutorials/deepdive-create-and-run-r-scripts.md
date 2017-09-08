---
title: "R-Skripts erstellen und ausführen | Microsoft Docs"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 08549ecffb6877fd160db62bb54c70dbe9347ce3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-run-r-scripts"></a>Erstellen und Ausführen von R-Skripts

Da Sie nun Ihre Datenquellen eingerichtet und mindestens einen Computekontext festgelegt haben, können Sie leistungsstarke R-Skripts mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden.  In dieser Lektion verwenden Sie den Server-Computekontext, um einige gängige Machine Learning-Tasks auszuführen:

- Visualisieren von Daten und Generieren einiger Zusammenfassungsstatistiken
- Erstellen eines linearen Regressionsmodells
- Erstellen eines logistischen Regressionsmodells
- Bewerten von neuen Daten und Erstellen eines Histogramms der Bewertungen

## <a name="change-compute-context-to-the-server"></a>Ändern des Computekontexts am Server

Bevor Sie einen beliebigen R-Code ausführen können, müssen Sie den *aktuellen* oder *aktiven* Computekontext angeben.

1. Um einen Computekontext zu aktivieren, den Sie bereits mit R definiert haben, verwenden Sie die Funktion **rxSetComputeContext** so wie hier dargestellt:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    Sobald Sie diese Anweisung ausführen, erfolgen alle nachfolgenden Berechnungen auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer, der im *sqlCompute* -Parameter angegeben ist.
  
2. Wenn Sie sich dazu entscheiden, den R-Code lieber auf Ihrer Arbeitsstation auszuführen, können lokalen Computer wieder als Kontext verwenden, indem Sie das Schlüsselwort  **local** verwenden.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    Sie erhalten eine Liste der Schlüsselwörter, die von dieser Funktion unterstützt werden, indem Sie `help("rxSetComputeContext")` in der Befehlszeile von R eingeben.
  
3. Nachdem Sie einen Computekontext angegeben haben, bleibt er aktiv, bis Sie ihn ändern. Alle R-Skripts, die *nicht* in einem Remoteserverkontext ausgeführt werden können, werden lokal ausgeführt.

## <a name="compute-summary-statistics"></a>Berechnen von Zusammenfassungsstatistiken

Versuchen Sie, einige zusammenfassende Statistiken mithilfe der *sqlFraudDS* -Datenquelle zu generieren, um die Funktionsweise der Computekontexts anzuzeigen.  Beachten Sie, dass das Datenobjekt nur die Daten definiert, die Sie verwenden. Es verändert nicht den Computekontext.

+ Verwenden Sie zur lokalen Durchführung der Zusammenfassung **rxSetComputeContext** , und geben Sie das Schlüsselwort „local“ an.
+ Wechseln Sie zum Erstellen der gleichen Berechnungen auf dem SQL Server-Computer zum SQL-Computekontext, den Sie zuvor definiert haben.

1. Rufen Sie die Funktion **rxSummary** auf, und übergeben Sie alle erforderlichen Argumente, wie z.B. die Formel und die Datenquelle, und weisen Sie die Ergebnisse der Variablen *sumOut*zu.
  
    ```R
    sumOut \<- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    Die Sprache "R" stellt viele Funktionen, aber RxSummary unterstützt die Ausführung auf verschiedenen remote rechenkontexte, einschließlich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Weitere Informationen zu ähnlichen Funktionen finden Sie unter [Data Summaries (Datenzusammenfassungen)](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) in der [ScaleR-Referenz](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
2. Wenn die Verarbeitung abgeschlossen ist, können Sie die Inhalte der *sumOut* -Variable in der Konsole ausgeben.
  
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

 *CreditLine 9.1856 9.870364 1 75 10000 0 100000*

 *Anzahl der Kategorie für das Geschlecht*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male 6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>Hinzufügen von Maximum- und Minimumwerten

Auf Grundlage der berechneten Zusammenfassungsstatistiken haben Sie einige nützliche Informationen über die Daten gefunden, die Sie in die Datenquelle für weitere Berechnungen einfügen möchten. Beispielsweise können die minimalen und maximalen Werte verwendet werden, um Histogramme, zu berechnen, damit Sie die hohen und niedrigen Werten mit der Datenquelle RxSqlServerData hinzufügen möchten.

Glücklicherweise beinhaltet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] optimierte Funktionen, die Daten des Typs „Integer“ effizient in Daten des Typs „Faktor“ konvertieren können.

1. Beginnen Sie, indem Sie einige temporäre Variablen einrichten.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Verwenden Sie die Variable *ccColInfo* , die Sie zuvor zum Definieren von Spalten in der Datenquelle erstellt haben.
  
    Sie fügen auch einige neue berechnete Spalten (*numTrans*, *numIntlTrans*und *creditLine*) zur Spaltensammlung hinzu.
  
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
  
3. Nach dem Update der Spaltensammlung können Sie die folgende Anweisung anwenden, um eine aktualisierte Version der zuvor definierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle zu erstellen.
  
    ```R
    sqlFraudDS \<- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    Die Datenquelle *sqlFraudDS* enthält nun die neuen Spalten, die in *ccColInfo*hinzugefügt wurden.
  
  Diese Änderungen wirken sich nur auf das Datenquellenobjekt in R aus. Es wurden noch keine neuen Daten in die Datenbanktabelle geschrieben. Sie können jedoch die in der *sumOut* -Variablen aufgezeichneten Daten verwenden, um Visualisierungen und Zusammenfassungen zu erstellen. Im nächsten Schritt erfahren Sie, wie Sie dies bewerkstelligen und gleichzeitig zwischen Computekontexten wechseln.

> [!TIP]
> Wenn Sie die computekontext Sie verwenden vergessen, führen Sie `rxGetComputeContext()`.  Ein Rückgabewert von `RxLocalSeq Compute Context` gibt an, dass Sie im lokalen rechenkontext ausgeführt werden.

## <a name="next-step"></a>Nächster Schritt

[Visualisieren von SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Definieren Sie und verwenden Sie Rechenkontexte](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)


