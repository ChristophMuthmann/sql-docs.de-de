---
title: 'Analysis Services Tutorial Lektion 5: Erstellen von berechneten Spalten | Microsoft Docs'
description: Beschreibt, wie berechnete Spalten in der Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: daed9d78d8b88bcf8088d8b19b4a34ba3a9f16c0
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="create-calculated-columns"></a>Erstellen von berechneten Spalten

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie Daten in Ihrem Modell durch Hinzufügen von berechneten Spalten. Sie können berechnete Spalten (als benutzerdefinierte Spalten) erstellen beim Abrufen von Daten verwenden, mit dem Abfrage-Editor oder später im Modell-Designer wie Sie machen. Weitere Informationen finden Sie unter [berechnete Spalten](../tabular-models/ssas-calculated-columns.md).
  
Sie erstellen fünf neue berechnete Spalten in drei verschiedenen Tabellen. Die Schritte unterscheiden sich geringfügig für jede Aufgabe, die anzeigt, dass verschiedene Methoden zum Erstellen von Spalten, benennen Sie diese und platzieren sie an verschiedenen Positionen in einer Tabelle vorhanden sind.  

Diese Lektion ist auch, wo Sie zuerst Data Analysis Expressions (DAX) verwenden. DAX ist eine spezielle Sprache zum Erstellen von äußerst anpassbarer Formel Ausdrücken für tabellarische Modelle. In diesem Lernprogramm verwenden Sie DAX zum Erstellen von berechneten Spalten, Measures und Rollenfilter an. Weitere Informationen finden Sie unter [DAX in tabellarischen Modellen](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md). 
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 4: Erstellen von Beziehungen](../tutorial-tabular-1400/as-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Erstellen von berechneten Spalten  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Erstellen Sie eine berechnete MonthCalendar-Spalte der DimDate-Tabelle  
  
1.  Klicken Sie auf die **Modell** Menü > **Modellansicht** > **Data Source View**.  
  
    Berechnete Spalten können nur mit dem Modell-Designer in der Datensicht erstellt werden.  
  
2.  Klicken Sie im Modell-Designer auf die **DimDate** Tabelle (Registerkarte).  
  
3.  Mit der rechten Maustaste die **"calendarquarter"** Spaltenüberschrift, und klicken Sie dann auf **Spalte einfügen**.  
  
    Eine neue Spalte mit dem Namen **Calculated Column 1** wird links von der Spalte **Calendar Quarter** eingefügt.  
  
4.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgenden DAX-Formel: AutoVervollständigen-Funktion können Sie den vollqualifizierten Namen von Spalten und Tabellen zu geben, und listet die Funktionen, die verfügbar sind.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Werte werden dann für alle Zeilen in der berechneten Spalte eingetragen. Wenn Sie über die Tabelle nach unten blättern, sehen Sie, dass Zeilen für diese Spalte basierend auf den Daten in jeder Zeile unterschiedliche Werte haben können.    
  
5.  Benennen Sie diese Spalte in **MonthCalendar**. 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
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
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
    
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
  
Die berechnete Spalte "productcategoryname" wird verwendet, um eine Hierarchie in der DimProduct-Tabelle zu erstellen, der Daten aus der EnglishProductCategoryName-Spalte in der Tabelle DimProductCategory enthalten. Hierarchien können maximal eine Tabelle umfassen.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Erstellen Sie eine berechnete Spalte mit Rand in die FactInternetSales-Tabelle  
  
1.  Wählen Sie im Modell-Designer die **FactInternetSales** Tabelle.  
  
2.  Erstellen Sie eine neue berechnete Spalte zwischen die **"SalesAmount"** Spalte und die **TaxAmt** Spalte.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Benennen Sie die Spalte in **Margin**um.  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    Die Rand berechnete Spalte wird verwendet, um Gewinnspannen für jeden Verkauf zu analysieren.  
  
## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 6: Erstellen von Measures](../tutorial-tabular-1400/as-lesson-6-create-measures.md).
  
  
  
