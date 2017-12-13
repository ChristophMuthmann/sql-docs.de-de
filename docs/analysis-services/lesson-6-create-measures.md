---
title: 'Lektion 7: Erstellen von Measures | Microsoft Docs'
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 28d9d9b4cda3c97a555cce45db525cfb4a6c26f5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-6-create-measures"></a>Lektion 6: Erstellen von Measures
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie in das Modell einzufügende Measures. Ähnlich wie die berechneten Spalten, die Sie in der vorherigen Lektion erstellt haben, ist ein Measure eine Berechnung, die mithilfe einer DAX-Formel erstellt. Im Gegensatz zu berechneten Spalten werden Measures jedoch auf Basis eines vom Benutzer ausgewählten *Filters*ausgewertet; z.B. eine bestimmte Spalte oder ein Slicer, die bzw. der dem Feld für Zeilenbezeichnungen in einer PivotTable hinzugefügt wurde. Ein Wert für jede Zelle im Filter wird dann vom übernommenen Measure berechnet. Measures sind leistungsstarke, flexible Berechnungen, die Sie in fast alle Tabellenmodelle für dynamische Berechnungen für numerische Daten einschließen möchten. Weitere Informationen finden Sie unter [Measures](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Um Measures zu erstellen, verwenden Sie die *Measureraster*. Standardmäßig hat jede Tabelle ein leeres Measureraster. Sie erstellen jedoch in der Regel keine Measures für jede Tabelle. Das Measureraster wird in der Datensicht unter einer Tabelle im Modell-Designer angezeigt. Um das Measureraster für eine Tabelle auszublenden oder anzuzeigen, klicken Sie auf das Menü **Tabelle** und anschließend auf **Measureraster anzeigen**.  
  
Sie können ein Measure erstellen, indem Sie auf eine leere Zelle im Measureraster klicken und dann eine DAX-Formel in die Bearbeitungsleiste eingeben. Nach dem Abschließen der Formelerstellung mit der EINGABETASTE wird das Measure in der Zelle angezeigt. Sie können auch Measures mit einer Standardaggregationsfunktion erstellen, indem Sie auf eine Spalte und anschließend auf die Schaltfläche AutoSumme (**∑**) in der Symbolleiste klicken. Measures, die mithilfe der AutoSumme-Funktion erstellt erscheint im measureraster direkt unterhalb der Spalte, aber Sie können verschoben werden.  
  
In dieser Lektion erstellen Sie Measures sowohl durch Eingabe einer DAX-Formel in der Bearbeitungsleiste als auch mithilfe der AutoSumme-Funktion.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 5: Erstellen von berechneten Spalten](../analysis-services/lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Erstellen von Measures  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>So erstellen Sie ein Measure DaysCurrentQuarterToDate in der DimDate-Tabelle  
  
1.  Klicken Sie im Modell-Designer auf die **DimDate** Tabelle.  
  
2.  Klicken Sie im Measureraster auf die linke obere leere Zelle.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Beachten Sie, dass die linke obere Zelle jetzt einen Measurenamen enthält **DaysCurrentQuarterToDate**, gefolgt von dem Ergebnis **92**.
    
      ![als-tabellarische-lesson6-newmeasure](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    Im Gegensatz zu berechneten Spalten können Sie mit measureformeln der Measurename gefolgt von einem Komma, gefolgt von der Formel Ausdruck eingeben.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>So erstellen Sie ein Measure DaysInCurrentQuarter in der DimDate-Tabelle  
  
1.  Mit der **DimDate** Tabelle im Modell-Designer im measureraster immer noch aktiv, klicken Sie auf die leere Zelle unterhalb des Measures, die Sie gerade erstellt haben.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Bei der Erstellung eines Vergleichsverhältnisses zwischen einem unvollständigen Zeitraum und dem vorherigen Zeitraum muss in der Formel der Anteil des verstrichenen Zeitraums berücksichtigt und mit dem gleichen Anteil des vorherigen Zeitraums verglichen werden. In diesem Fall [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] Gibt den Anteil des aktuellen Zeitraums vergangen.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>So erstellen Sie eine Measure InternetDistinctCountSalesOrder in die FactInternetSales-Tabelle  
  
1.  Klicken Sie auf die **FactInternetSales** Tabelle.   
  
2.  Klicken Sie auf die **SalesOrderNumber** Spaltenüberschrift.  
  
3.  Klicken Sie in der Symbolleiste neben der AutoSumme-Schaltfläche (**∑**) auf den Pfeil nach unten, und wählen Sie **DistinctCount**aus.  
  
    Die AutoSumme-Funktion erstellt mit der DistinctCount-Standardaggregationsformel automatisch ein Measure für die ausgewählte Spalte.  
    
       ![als-tabellarische-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  Klicken Sie im measureraster auf das neue Measure, und klicken Sie dann in der **Eigenschaften** Fenster im **Measurename**, benennen Sie das Measure in **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>So erstellen Sie zusätzliche Measures in der FactInternetSales-Tabelle  
  
1.  Erstellen Sie unter Verwendung der AutoSumme-Funktion die folgenden Measures, und benennen Sie diese um:  
  
    |Measurename|Column|AutoSumme (∑)|Formel|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margin|Sum|=SUM([Margin])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Freight])|  
  
2.  Erstellen Sie durch Klicken auf eine leere Zelle im measureraster, und mithilfe der Bearbeitungsleiste und benennen Sie die folgenden Measures in der Reihenfolge:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Für die FactInternetSales-Tabelle erstellten Measures können verwendet werden, analysieren Sie wichtige Finanzdaten wie Verkäufe, Kosten und Gewinnspanne für Elemente, die durch vom Benutzer gewählte Filter definiert.  
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 7: Erstellen von Key Performance Indicators](../analysis-services/lesson-7-create-key-performance-indicators.md).  

  
