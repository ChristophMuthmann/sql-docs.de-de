---
title: "Lektion 7: Erstellen von Measures | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 7: Erstellen von Measures
In dieser Lektion erstellen Sie in das Modell einzufügende Measures. Ähnlich wie die berechneten Spalten, die Sie in der vorherigen Lektion erstellt haben, ist ein Measure im Wesentlichen eine mit einer DAX-Formel erstellte Berechnung. Im Gegensatz zu berechneten Spalten werden Measures jedoch auf Basis eines vom Benutzer ausgewählten *Filters* ausgewertet; z.B. eine bestimmte Spalte oder ein Slicer, die bzw. der dem Feld für Zeilenbezeichnungen in einer PivotTable hinzugefügt wurde.   Ein Wert für jede Zelle im Filter wird dann vom übernommenen Measure berechnet. Measures sind leistungsstarke, flexible Berechnungen, die Sie in fast alle Tabellenmodelle einbinden können, um dynamische Berechnungen für numerische Daten auszuführen. Weitere Informationen finden Sie unter [Measures &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Um Measures zu erstellen, verwenden Sie das Measureraster. Standardmäßig hat jede Tabelle ein leeres Measureraster. Sie erstellen jedoch in der Regel keine Measures für jede Tabelle. Das Measureraster wird in der Datensicht unter einer Tabelle im Modell-Designer angezeigt. Um das Measureraster für eine Tabelle auszublenden oder anzuzeigen, klicken Sie auf das Menü **Tabelle** und anschließend auf **Measureraster anzeigen**.  
  
Sie können ein Measure erstellen, indem Sie auf eine leere Zelle im Measureraster klicken und dann eine DAX-Formel in die Bearbeitungsleiste eingeben. Nach dem Abschließen der Formelerstellung mit der EINGABETASTE wird das Measure in der Zelle angezeigt. Sie können auch Measures mit einer Standardaggregationsfunktion erstellen, indem Sie auf eine Spalte und anschließend auf die Schaltfläche AutoSumme (**∑**) in der Symbolleiste klicken. Measures, die mithilfe der AutoSumme-Funktion erstellt wurden, werden im Measureraster direkt unterhalb der Spalte angezeigt, können bei Bedarf jedoch verschoben werden.  
  
In dieser Lektion erstellen Sie Measures sowohl durch Eingabe einer DAX-Formel in der Bearbeitungsleiste als auch mithilfe der AutoSumme-Funktion.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **30 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 6: Erstellen von berechneten Spalten](../analysis-services/lesson-6-create-calculated-columns.md).  
  
## Erstellen von Measures  
  
#### So erstellen Sie ein Measure vom Typ "Days Current Quarter to Date" in der Date-Tabelle.  
  
1.  Klicken Sie im Modell-Designer auf die **Datumstabelle**.  
  
2.  Wenn nicht bereits ein leeres Measureraster nicht unter der Tabelle angezeigt wird, klicken Sie auf das Menü **Tabelle** und anschließend auf **Measureraster anzeigen**.  
  
3.  Klicken Sie im Measureraster auf die linke obere leere Zelle.  
  
4.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein:  
  
    **=COUNTROWS( DATESQTD( 'Date'[Date]))**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
    Beachten Sie, dass die linke obere Zelle jetzt einen Measurenamen enthält, **Measure 1**, gefolgt von dem Ergebnis **92**. Der Measurename geht auch der Formel in der Bearbeitungsleiste voraus.  
  
5.  Um das Measure umzubenennen, markieren Sie den Namen **Measure 1** in der Bearbeitungsleiste, und geben Sie **Days Current Quarter to Date** ein. Drücken Sie anschließend die EINGABETASTE.  
  
    > [!TIP]  
    > Wenn Sie in der Bearbeitungsleiste eine Formel eingeben, können Sie auch zuerst den Measurenamen eingeben, dem ein Doppelpunkt (:) und die Formel folgt. Bei dieser Methode müssen Sie das Measure nicht umbenennen.  
  
#### So erstellen Sie ein Measure vom Typ "Days in Current Quarter" in der Date-Tabelle.  
  
1.  Klicken Sie mit der im Modell-Designer nach wie vor aktiven Tabelle **Date** auf die leere Zelle unterhalb des Measures, das Sie gerade erstellt haben.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    **Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))**  
  
    Hinweis: In dieser zuerst einbezogenen Formel folgt ein Doppelpunkt (:) auf den Rasternamen.  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
Bei der Erstellung eines Vergleichsverhältnisses zwischen einem unvollständigen Zeitraum und dem vorherigen Zeitraum muss in der Formel der Anteil des verstrichenen Zeitraums berücksichtigt und mit dem gleichen Anteil des vorherigen Zeitraums verglichen werden. In diesem Fall gibt [Days Current Quarter to Date]/[Days in Current Quarter] den verstrichenen Anteil des aktuellen Zeitraums zurück.  
  
#### So erstellen Sie eine Measure vom Typ "Internet Distinct Count Sales Order" in der Internet Sales-Tabelle  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle (Registerkarte) **Internet Sales**.  
  
    Wenn das Measureraster nicht bereits angezeigt wird, klicken Sie mit der rechten Maustaste auf die Tabelle (Registerkarte) **Internet Sales** und anschließend auf **Measureraster anzeigen**.  
  
2.  Klicken Sie auf die Spaltenüberschrift **Sales Order Number**.  
  
3.  Klicken Sie in der Symbolleiste neben der AutoSumme-Schaltfläche (**∑**) auf den Pfeil nach unten, und wählen Sie **DistinctCount** aus.  
  
    Die AutoSumme-Funktion erstellt mit der DistinctCount-Standardaggregationsformel automatisch ein Measure für die ausgewählte Spalte.  
  
    Beachten Sie die oberste Zelle unter der Spalte im Measureraster. Sie enthält jetzt einen Measurenamen, **Distinct Count Sales Order Number**. Mit der AutoSumme-Funktion erstellte Measures werden automatisch unter der zugeordneten Spalte in der obersten Zelle im Measureraster eingefügt.  
  
4.  Klicken Sie im Measureraster auf das neue Measure, und benennen Sie anschließend im Fenster **Eigenschaften** im Feld **Measurename** das Measure in **Internet Distinct Count Sales Order** um.  
  
#### So erstellen Sie zusätzliche Measures in der Internet Sales-Tabelle  
  
1.  Erstellen Sie unter Verwendung der AutoSumme-Funktion die folgenden Measures, und benennen Sie diese um:  
  
    |Measurename|Column|AutoSumme (∑)|Formel|  
    |----------------|----------|-----------------|-----------|  
    |Internet Order Lines Count|Sales Order Line Number|Count|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|Sum|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|Discount Amount|Sum|=SUM([Discount Amount])|  
    |Internet Total Product Cost|Total Product Cost|Sum|=SUM([Total Product Cost])|  
    |Internet Total Sales|Sales Amount|Sum|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|Sum|=SUM([Margin])|  
    |Internet Total Tax Amt|Tax Amt|Sum|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|Sum|=SUM([Freight])|  
  
2.  Erstellen Sie durch Klicken auf eine leere Zelle im Measureraster und durch Verwenden der Bearbeitungsleiste die folgenden Measures, und benennen Sie diese um:  
  
    > [!IMPORTANT]  
    > Sie müssen die folgenden Measures in entsprechender Reihenfolge erstellen. Formeln in späteren Measures verweisen auf vorherige Measures.  
  
    |Measurename|Formel|  
    |----------------|-----------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
Mit den für die Internet Sales-Tabelle erstellten Measures lassen sich wichtige Finanzdaten wie Verkäufe, Kosten und Gewinnspanne für Elemente analysieren, die durch vom Benutzer gewählte Filter definiert sind.  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 8: Erstellen von Leistungskennzahlen](../analysis-services/lesson-8-create-key-performance-indicators.md).  
  
  
  
