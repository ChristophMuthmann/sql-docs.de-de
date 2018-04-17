---
title: 'Analysis Services Tutorial Lektion 6: Erstellen von Measures | Microsoft Docs'
description: Beschreibt, wie Measures in der Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d37b1c5a307ea7f9c90fa29c83536a4b3d8ef0bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-measures"></a>Erstellen von Measures

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie Measures aus, die im Modell enthalten sein. Ähnlich wie die berechneten Spalten, die Sie erstellt haben, ist ein Measure eine Berechnung, die mithilfe einer DAX-Formel erstellt. Im Gegensatz zu berechneten Spalten, Measures werden jedoch ausgewertet. anhand eines vom Benutzer ausgewählten *Filter*. Z. B. eine bestimmte Spalte oder Slicer-Feld für Zeilenbezeichnungen in einer PivotTable hinzugefügt. Ein Wert für jede Zelle im Filter wird dann vom übernommenen Measure berechnet. Measures sind leistungsstarke, flexible Berechnungen, die in fast alle tabellarischen Modellen für dynamische Berechnungen für numerische Daten enthalten sein sollen. Weitere Informationen finden Sie unter [Measures](../tabular-models/measures-ssas-tabular.md).
  
Um Measures zu erstellen, verwenden Sie die *Measureraster*. Standardmäßig verfügt jede Tabelle ein leeres measureraster; Allerdings wird Measures für jede Tabelle in der Regel nicht erstellen. Das Measureraster wird in der Datensicht unter einer Tabelle im Modell-Designer angezeigt. Um das Measureraster für eine Tabelle auszublenden oder anzuzeigen, klicken Sie auf das Menü **Tabelle** und anschließend auf **Measureraster anzeigen**.  
  
Sie können ein Measure erstellen, indem Sie auf eine leere Zelle im measureraster, und klicken Sie dann eine DAX-Formel in der Bearbeitungsleiste eingeben. Wenn klicken Sie auf die EINGABETASTE, um das Abschließen der Formel, die das Measure dann in der Zelle angezeigt wird. Sie können auch Measures mit einer standardaggregationsfunktion, indem Sie auf eine Spalte, und klicken Sie dann auf die Schaltfläche "AutoSumme" erstellen (**∑**) auf der Symbolleiste. Mithilfe der AutoSumme-Funktion erstellte Measures im measureraster direkt unterhalb der Spalte angezeigt, jedoch verschoben werden können.  
  
In dieser Lektion erstellen Sie Measures sowohl durch Eingabe einer DAX-Formel in der Bearbeitungsleiste, und mithilfe der AutoSumme-Funktion.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 5: Erstellen von berechneten Spalten](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Erstellen von Measures  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>So erstellen Sie ein Measure DaysCurrentQuarterToDate in der DimDate-Tabelle  
  
1.  Klicken Sie im Modell-Designer auf die **DimDate** Tabelle.  
  
2.  Klicken Sie im Measureraster auf die linke obere leere Zelle.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Beachten Sie, dass die linke obere Zelle jetzt einen Measurenamen enthält **DaysCurrentQuarterToDate**, gefolgt von dem Ergebnis **92**. Das Ergebnis ist zu diesem Zeitpunkt nicht relevant, da kein Benutzerfilter angewendet wurde.
    
      ![als lesson6 newmeasure](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    Im Gegensatz zu berechneten Spalten können Sie mit measureformeln der Measurename gefolgt von einem Doppelpunkt, gefolgt von der Formel Ausdruck eingeben.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>So erstellen Sie ein Measure DaysInCurrentQuarter in der DimDate-Tabelle  
  
1.  Mit der **DimDate** Tabelle im Modell-Designer im measureraster immer noch aktiv, klicken Sie auf die leere Zelle unterhalb des Measures, die Sie erstellt haben.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Für die Erstellung eines vergleichsverhältnisses zwischen einem unvollständigen Zeitraum und dem vorherigen Zeitraum. Die Formel muss der Anteil des Zeitraums berechnen, die abgelaufen, und es mit dem gleichen Anteil des vorherigen Zeitraums verglichen. In diesem Fall [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] Gibt den Anteil des aktuellen Zeitraums vergangen.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>So erstellen Sie eine Measure InternetDistinctCountSalesOrder in die FactInternetSales-Tabelle  
  
1.  Klicken Sie auf die **FactInternetSales** Tabelle.   
  
2.  Klicken Sie auf die **SalesOrderNumber** Spaltenüberschrift.  
  
3.  Klicken Sie in der Symbolleiste neben der AutoSumme-Schaltfläche (**∑**) auf den Pfeil nach unten, und wählen Sie **DistinctCount**aus.  
  
    Die AutoSumme-Funktion erstellt mit der DistinctCount-Standardaggregationsformel automatisch ein Measure für die ausgewählte Spalte.  
    
       ![als lesson6 newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  Klicken Sie im measureraster auf das neue Measure, und klicken Sie dann in der **Eigenschaften** Fenster im **Measurename**, benennen Sie das Measure in **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>So erstellen Sie zusätzliche Measures in der FactInternetSales-Tabelle  
  
1.  Erstellen Sie unter Verwendung der AutoSumme-Funktion die folgenden Measures, und benennen Sie diese um:  

    |Column|Measurename|AutoSumme (∑)|Formel|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|SUM|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Freight])|  
  
2.  Durch Klicken auf eine leere Zelle im measureraster und mithilfe der Bearbeitungsleiste erstellt haben, die folgenden benutzerdefinierten Measures in der Reihenfolge:  
  
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

[Lektion 7: Erstellen von Key Performance Indicators](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  

  
