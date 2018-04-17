---
title: Visualisieren von SQL Server-Daten mithilfe von R (SQL und R deep Dive) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 923b8201b6948a93f0994306269c0d3338f54c2d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>Visualisieren von SQL Server-Daten mithilfe von R (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Die erweiterten Pakete in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten mehrere Funktionen, die für die Skalierbarkeit und die parallele Verarbeitung optimiert wurden. Diese Funktionen besitzen in der Regel das Präfix **rx** oder **Rx**.

In dieser exemplarischen Vorgehensweise verwenden Sie die **RxHistogram** Funktion zum Anzeigen der Verteilung der Werte in der _CreditLine_ Spalte nach Geschlecht.

## <a name="visualize-data-using-rxhistogram"></a>Visualisieren von Daten mit rxHistogram

1. Verwenden Sie den folgenden R-Code zum Aufrufen der [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) -Funktion, und übergeben Sie eine Formel sowie eine Datenquelle. Sie können dies zunächst lokal ausführen, um die erwarteten Ergebnisse anzuzeigen und zu sehen, wie lange es dauert.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Intern ruft **rxHistogram** die [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) -Funktion ab, die im **RevoScaleR** -Paket enthalten ist. **RxCube** gibt eine einzelne Liste (oder Datenrahmen), eine Spalte für jede Variable, die in der Formel angegeben, enthält außerdem eine Spalte Zahlen.
    
2. Nun, Festlegen des computekontexts mit dem SQL Server-Remotecomputer, und führen **RxHistogram** erneut aus.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Die Ergebnisse sind identisch, da Sie die gleiche Datenquelle verwenden. Die Berechnungen werden jedoch auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer ausgeführt.  Die Ergebnisse werden anschließend an Ihre lokale Arbeitsstation zum Zeichnen zurückgegeben.
   
![Historgrammergebnisse](media/rsql-sue-histogramresults.jpg "histogram results")

4. Sie können auch aufrufen, die **RxCube** Funktion, und übergeben Sie die Ergebnisse an einer Funktion zeichnen R.  Das folgende Beispiel verwendet z.B. **rxCube** zur Berechnung des Mittelwerts von *fraudRisk* für jede Kombination von *numTrans* und *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Verwenden Sie zum Angeben der Gruppen, die zum Berechnen der Mittel der Gruppe verwendet werden, die Notation `F()` . In diesem Beispiel `F(numTrans):F(numIntlTrans)` gibt an, dass der ganzen Zahlen in den Variablen `_numTrans` und `numIntlTrans` als kategorievariablen mit einer Ebene für jeden ganzzahligen Wert behandelt werden soll.
  
    Da die unteren und oberen Ebenen bereits, mit der Datenquelle hinzugefügt wurden `sqlFraudDS` (mithilfe der `colInfo` Parameter), die Ebenen werden automatisch im Histogramm verwendet.
  
5. Wert ist der Rückgabetyp **RxCube** ist ein *RxCube Objekt*, die eine Kreuztabelle darstellt. Sie können jedoch die Funktion [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) verwenden, um die Ergebnisse in einen Datenrahmen zu konvertieren, der leicht in einem der Standardzeichenfunktionen von R verwendet werden kann.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    Die **RxCube** Funktion schließt ein optionales Argument *ReturnDataFrame* = **"true"**, die Sie verwenden können, um die Ergebnisse direkt in einem Datenrahmen zu konvertieren. Beispiel:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    Die Ausgabe von **rxResultsDF** ist jedoch viel genauer und behält die Namen der Quellspalten bei.
  
6. Führen Sie schließlich den folgenden Code zum Erstellen eines Heat Map mithilfe der `levelplot` -Funktion von der **Vektorgitters** Paket, d. h. alle R-Verteilungen enthalten.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Ergebnisse**
  
    ![Punktdiagrammergebnisse](media/rsql-sue-scatterplotresults.jpg "scatterplot results")
  
Auch aus dieser schnellen Analyse können Sie herauslesen, dass das Betrugsrisiko jeweils mit der Anzahl der Transaktionen und der Anzahl der internationalen Transaktionen ansteigt.

Weitere Informationen zu den **RxCube** -Funktion und Kreuztabellen im Allgemeinen finden Sie unter [Zusammenfassungen von Daten mithilfe von RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-step"></a>Nächster Schritt

[Erstellen Sie R-Modelle mithilfe von SQL Server-Daten](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
