---
title: 'Lektion 6: Erstellen von berechneten Spalten | Microsoft Docs'
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c59e137942d45cbe6c20a71b9fa785988b9876fa
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-5-create-calculated-columns"></a>Lektion 5: Erstellen von berechneten Spalten
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie neue Daten in Ihrem Modell durch Hinzufügen von berechneten Spalten. Eine berechnete Spalte basiert auf Daten, die bereits im Modell vorhanden sind. Weitere Informationen finden Sie unter [Calculated Columns](../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
Sie erstellen fünf neue berechnete Spalten in drei verschiedenen Tabellen. Die Schritte sind für jede Aufgabe etwas anders. Damit sollen Ihnen verschiedene Methoden zum Erstellen neuer Spalten, zum Umbenennen der Spalten und zum Platzieren der Spalten an verschiedenen Positionen in einer Tabelle aufgezeigt werden.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 4: Erstellen von Beziehungen](../analysis-services/lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Erstellen von berechneten Spalten  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Erstellen Sie eine berechnete MonthCalendar-Spalte der DimDate-Tabelle  
  
1.  Klicken Sie auf die **Modell** Menü > **Modellansicht** > **Data Source View**.  
  
    Berechnete Spalten können nur mit dem Modell-Designer in der Datensicht erstellt werden.  
  
2.  Klicken Sie im Modell-Designer auf die **DimDate** Tabelle (Registerkarte).  
  
3.  Mit der rechten Maustaste die **"calendarquarter"** Spaltenüberschrift, und klicken Sie dann auf **Spalte einfügen**.  
  
    Eine neue Spalte mit dem Namen **Calculated Column 1** wird links von der Spalte **Calendar Quarter** eingefügt.  
  
4.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein. Mit der AutoVervollständigen-Funktion können Sie die vollqualifizierten Namen von Spalten und Tabellen auf einfache Weise eingeben und die verfügbaren Funktionen auflisten.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Werte werden dann für alle Zeilen in der berechneten Spalte eingetragen. Wenn Sie in der Tabelle einen Bildlauf nach unten durchführen, sehen Sie, dass Zeilen für diese Spalte je nach den Daten in jeder Zeile unterschiedliche Werte haben können.    
  
5.  Benennen Sie diese Spalte in **MonthCalendar**. 

    ![als-tabellarische-lesson5-newcolumn](../analysis-services/media/as-tabular-lesson5-newcolumn.png) 
  
Die MonthCalendar berechnete Spalte einen sortierbaren Namen für den Monat enthält.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Erstellen Sie eine berechnete DayOfWeek-Spalte der DimDate-Tabelle  
  
1.  Mit der **DimDate** Tabelle weiterhin aktiv ist, klicken Sie auf die **Spalte** Menü, und klicken Sie dann auf **Add Column**.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Wenn Sie mit dem Erstellen der Formel abgeschlossen haben, drücken Sie die EINGABETASTE. Die neue Spalte wird ganz rechts von der Tabelle hinzugefügt.  
  
3.  Benennen Sie die Spalte in **DayOfWeek**.  
  
4.  Klicken Sie auf die Spaltenüberschrift, und ziehen Sie dann die Spalte zwischen die **EnglishDayNameOfWeek** Spalte und die **"daynumberofmonth"** Spalte.  
  
    > [!TIP]  
    > Durch das Verschieben von Spalten in der Tabelle wird die Navigation vereinfacht.  
  
Die DayOfWeek berechnete Spalte einen sortierbaren Namen für den Tag der Woche enthält.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Erstellen Sie eine berechnete Spalte von ProductSubcategoryName in der DimProduct-Tabelle  
  
  
1.  In der **DimProduct** Tabelle einen Bildlauf ganz rechts in der Tabelle. Beachten Sie, dass die ganz rechts stehende Spalte **Spalte hinzufügen** heißt (in Kursivschrift). Klicken Sie auf die Spaltenüberschrift.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Benennen Sie die Spalte in **ProductSubcategoryName**.  
  
Die ProductSubcategoryName berechnete Spalte wird verwendet, um eine Hierarchie in der DimProduct-Tabelle zu erstellen, der Daten aus der EnglishProductSubcategoryName-Spalte in der Tabelle DimProductSubcategory enthalten. Hierarchien können maximal eine Tabelle umfassen. Sie erstellen Hierarchien später in Lektion 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Erstellen Sie eine berechnete Spalte für "productcategoryname" in der DimProduct-Tabelle  
  
1.  Mit der **DimProduct** Tabelle weiterhin aktiv ist, klicken Sie auf die **Spalte** Menü, und klicken Sie dann auf **Add Column**.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Benennen Sie die Spalte in **"productcategoryname"**.  
  
Die berechnete Spalte "productcategoryname" wird verwendet, um eine Hierarchie in der DimProduct-Tabelle erstellen, das Daten aus der EnglishProductCategoryName-Spalte in der Tabelle DimProductCategory enthält. Hierarchien können maximal eine Tabelle umfassen.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Erstellen Sie eine berechnete Spalte mit Rand in die FactInternetSales-Tabelle  
  
1.  Wählen Sie im Modell-Designer die **FactInternetSales** Tabelle.  
  
2.  Fügen Sie eine neue Spalte hinzu.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Benennen Sie die Spalte in **Margin**um.  
  
5.  Ziehen Sie die Spalte zwischen die **"SalesAmount"** Spalte und die **TaxAmt** Spalte. 
 
      ![als-tabellarische-lesson5-newmargin](../analysis-services/media/as-tabular-lesson5-newmargin.png)
      
    Die Rand berechnete Spalte wird verwendet, um Gewinnspannen für jeden Verkauf zu analysieren.  
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 6: Erstellen von Measures](../analysis-services/lesson-6-create-measures.md).
  
  
  

