---
title: Visualisieren von SQL Server-Daten mithilfe von R (Tieferer Einblick in Data Science) | Microsoft-Dokumenation
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
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 023958a137515c519fe8d73e1ce1181dc7579356
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="visualize-sql-server-data-using-r"></a>Visualisieren von SQL Server Data mit R

Die erweiterten Pakete in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten mehrere Funktionen, die für die Skalierbarkeit und die parallele Verarbeitung optimiert wurden. Diese Funktionen besitzen in der Regel das Präfix *rx* oder *Rx*.

In dieser exemplarischen Vorgehensweise verwenden Sie die **rxHistogram** -Funktion zum Anzeigen der Verteilung von Werten in der _creditLine_ -Spalte nach Geschlecht.

## <a name="visualize-data-using-rxhistogram"></a>Visualisieren von Daten mit rxHistogram

1. Verwenden Sie die folgenden R-Code zum Aufrufen der Funktion RxHistogram und übergeben eine Formel und Datenquelle. Sie können dies zunächst lokal ausführen, um die erwarteten Ergebnisse anzuzeigen und zu sehen, wie lange es dauert.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Intern ruft RxHistogram die RxCube-Funktion, das Bestandteil der **"revoscaler"** Paket. Die RxCube-Funktion gibt eine einzelne Liste (oder Datenrahmen), eine Spalte für jede Variable, die in der Formel angegeben, enthält, sowie eine Spalte Zahlen.
    
2. Nun festlegen Sie des computekontexts mit dem SQL Server-Remotecomputer, und führen Sie RxHistogram erneut aus.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Die Ergebnisse sind identisch, da Sie die gleiche Datenquelle verwenden. Die Berechnungen werden jedoch auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer ausgeführt.  Die Ergebnisse werden anschließend an Ihre lokale Arbeitsstation zum Zeichnen zurückgegeben.
   
![Historgrammergebnisse](media/rsql-sue-histogramresults.jpg "histogram results")

4. Sie können auch die RxCube-Funktion aufrufen und die Ergebnisse an eine Zeichnungslinien R-Funktion übergeben.  Im folgenden Beispiel wird z. B. RxCube zum Berechnen des Mittelwerts der *FraudRisk* für jede Kombination von *NumTrans* und *NumIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Verwenden Sie zum Angeben der Gruppen, die zum Berechnen der Mittel der Gruppe verwendet werden, die Notation `F()` . In diesem Beispiel gibt `F(numTrans):F(numIntlTrans)` an, dass die ganzen Zahlen in den Variablen _numTrans_ und _numIntlTrans_ als Kategorievariablen mit einer Ebene für jeden Integer-Wert behandelt werden müssen.
  
    Da die niedrigen und hohen Ebenen schon zur Datenquelle *sqlFraudDS* hinzugefügt wurden (mithilfe des Parameters *colInfo* ), werden die Ebenen automatisch im Histogramm verwendet.
  
5. Der Rückgabewert der RxCube ist standardmäßig eine *RxCube Objekt*, die eine Kreuztabelle darstellt. Sie können jedoch die Funktion **rxResultsDF** verwenden, um die Ergebnisse in einen Datenrahmen zu konvertieren, der leicht in einem der Standardzeichenfunktionen von R verwendet werden kann.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > Beachten Sie, dass die Funktion RxCube ein optionales Argument enthält *ReturnDataFrame* = "true", Sie verwenden können, um die Ergebnisse direkt in einem Datenrahmen zu konvertieren. Beispiel:
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > Allerdings wird die Ausgabe des RxResultsDF ist wesentlich übersichtlicher und behält die Namen der Quellspalten.
  
6. Führen Sie schließlich den folgenden Code zum Erstellen eines Heat Map mithilfe der `levelplot` -Funktion von der **Vektorgitters** Paket, d. h. alle R-Verteilungen enthalten.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Ergebnisse**
  
    ![Punktdiagrammergebnisse](media/rsql-sue-scatterplotresults.jpg "scatterplot results")
  
Auch aus dieser schnellen Analyse können Sie herauslesen, dass das Betrugsrisiko jeweils mit der Anzahl der Transaktionen und der Anzahl der internationalen Transaktionen ansteigt.

Weitere Informationen über die RxCube-Funktion und Kreuztabellen im Allgemeinen finden Sie unter [Zusammenfassungen von Daten](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries).

## <a name="next-step"></a>Nächster Schritt

[Erstellen von Modellen](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Lektion 2: Erstellen und Ausführen von R-Skripts](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)



