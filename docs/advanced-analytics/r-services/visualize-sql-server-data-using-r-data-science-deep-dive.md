---
title: "Visualisieren von SQL Server-Daten mithilfe von R (Tieferer Einblick in Data Science) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Visualisieren von SQL Server-Daten mithilfe von R (Tieferer Einblick in Data Science)
Die erweiterten Pakete in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten mehrere Funktionen, die für die Skalierbarkeit und die parallele Verarbeitung optimiert wurden. Diese Funktionen besitzen in der Regel das Präfix *rx* oder*Rx*.  
  
In dieser exemplarischen Vorgehensweise verwenden Sie die *rxHistogram*-Funktion zum Anzeigen der Verteilung von Werten in der _creditLine_-Spalte nach Geschlecht.  
  
## Visualisieren von Daten mit rxHistogram und rxCube  
  
1.  Verwenden Sie den folgenden R-Code zum Aufrufen der *rxHistogram*-Funktion, und übergeben Sie eine Formel sowie eine Datenquelle. Sie können dies zunächst lokal ausführen, um die erwarteten Ergebnisse anzuzeigen und zu sehen, wie lange es dauert.
  
    ```R  
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")   
    ```  
 
    Intern ruft *rxHistogram* die *rxCube*-Funktion ab, die im **RevoScaleR**-Paket enthalten ist. Die *rxCube*-Funktion gibt eine einzelne Liste (oder einen einzelnen Datenrahmen) aus, die (bzw. der) eine Spalte für jede in der Formel angegebene Variable enthält, sowie eine Spalte „counts“.
    
2. Nun legen Sie den Computekontext auf den SQL Server-Remotecomputer fest und führen *rxHistogram* erneut aus.
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
 
3.    Die Ergebnisse sind identisch, da Sie die gleiche Datenquelle verwenden. Die Berechnungen werden jedoch auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer ausgeführt.  Die Ergebnisse werden anschließend an Ihre lokale Arbeitsstation zum Zeichnen zurückgegeben.  
   
![histogram results](../../advanced-analytics/r-services/media/rsql-sue-histogramresults.jpg "histogram results")  

  
4.  Sie können auch die Funktion *rxCube* aufrufen und die Ergebnisse an Zeichenfunktionen von R übergeben.  Das folgende Beispiel verwendet z.B. *rxCube* zur Berechnung des Mittelwerts von *fraudRisk* für jede Kombination von *numTrans* und *numIntlTrans*:  
  
    ```R  
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)   
    ```  
  
    Verwenden Sie zum Angeben der Gruppen, die zum Berechnen der Mittel der Gruppe verwendet werden, die Notation `F()`. In diesem Beispiel gibt `F(numTrans):F(numIntlTrans)` an, dass die ganzen Zahlen in den Variablen _numTrans_ und _numIntlTrans_ als Kategorievariablen mit einer Ebene für jeden Integer-Wert behandelt werden müssen.  
  
    Da die niedrigen und hohen Ebenen schon zur Datenquelle *sqlFraudDS* hinzugefügt wurden (mithilfe des Parameters *colInfo*), werden die Ebenen automatisch im Histogramm verwendet.  
  
5.  Der Rückgabewert von *rxCube* ist standardmäßig ein *rxCube-Objekt*, das eine Kreuztabelle darstellt. Sie können jedoch die Funktion *rxResultsDF* verwenden, um die Ergebnisse in einen Datenrahmen zu konvertieren, der leicht in einem der Standardzeichenfunktionen von R verwendet werden kann.  
  
    ```R  
    cubePlot <- rxResultsDF(cube1)   
    ```  
  
    > [!TIP]  
    > Beachten Sie, dass die Funktion *rxCube* ein optionales Argument enthält, *returnDataFrame* = TRUE, das Sie zur direkten Konvertierung der Ergebnisse in einen Datenrahmen verwenden können. Beispiel:  
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`  
    >   
    > Die Ausgabe von *rxResultsDF* ist jedoch viel genauer und behält die Namen der Quellspalten bei.  
  
6.  Führen Sie zum Abschluss den folgenden Code aus, um eine Temperaturverteilungskarte mithilfe der *levelplot*-Funktion aus dem **lattice**-Paket zu erstellen, das in allen R-Verteilungen enthalten ist.  
  
    ```R  
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)   
    ```  
  
    **Ergebnisse**  
  
    ![scatterplot results](../../advanced-analytics/r-services/media/rsql-sue-scatterplotresults.jpg "scatterplot results")  
  
Auch aus dieser schnellen Analyse können Sie herauslesen, dass das Betrugsrisiko jeweils mit der Anzahl der Transaktionen und der Anzahl der internationalen Transaktionen ansteigt.

Weitere Informationen zur *rxCube*-Funktion und zu Kreuztabellen im Allgemeinen finden Sie unter [Data Summaries (Zusammenfassungen von Daten)](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries).  
  
## Nächster Schritt  
[Create Models &#40;Data Science Deep Dive&#41; (Erstellen von Modellen (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Lektion 2: Create and Run R Scripts &#40;Data Science Deep Dive&#41; (Erstellen und Ausführen von R-Skripts (Tieferer Einstieg in Data Science))](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
