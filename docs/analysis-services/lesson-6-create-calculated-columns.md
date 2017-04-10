---
title: "Lektion 6: Erstellen von berechneten Spalten | Microsoft Docs"
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
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 6: Erstellen von berechneten Spalten
In dieser Lektion erstellen Sie neue Daten in Ihrem Modell durch Hinzufügen von berechneten Spalten. Eine berechnete Spalte basiert auf Daten, die bereits im Modell vorhanden sind. Weitere Informationen finden Sie unter [Berechnete Spalten &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/calculated-columns-ssas-tabular.md).  
  
Sie erstellen fünf neue berechnete Spalten in drei verschiedenen Tabellen. Die Schritte sind für jede Aufgabe etwas anders. Damit sollen Ihnen verschiedene Methoden zum Erstellen neuer Spalten, zum Umbenennen der Spalten und zum Platzieren der Spalten an verschiedenen Positionen in einer Tabelle aufgezeigt werden.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 5: Erstellen von Beziehungen](../analysis-services/lesson-5-create-relationships.md).  
  
## Erstellen von berechneten Spalten  
  
#### Erstellen einer berechneten Spalte "Month Calendar" in der Date-Tabelle  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Modell**, zeigen Sie auf **Modellansicht**, und klicken Sie anschließend auf **Datensicht**.  
  
    Berechnete Spalten können nur mit dem Modell-Designer in der Datensicht erstellt werden.  
  
2.  Klicken Sie im Modell-Designer auf die Tabelle (Registerkarte) **Date**.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Spalte **Calendar Quarter** und anschließend auf **Spalte einfügen**.  
  
    Eine neue Spalte mit dem Namen **Calculated Column 1** wird links von der Spalte **Calendar Quarter** eingefügt.  
  
4.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein. Mit der AutoVervollständigen-Funktion können Sie die vollqualifizierten Namen von Spalten und Tabellen auf einfache Weise eingeben und die verfügbaren Funktionen auflisten.  
  
    **=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
    Werte werden dann für alle Zeilen in der berechneten Spalte eingetragen. Wenn Sie in der Tabelle einen Bildlauf nach unten durchführen, sehen Sie, dass Zeilen für diese Spalte je nach den Daten in jeder Zeile unterschiedliche Werte haben können.  
  
    > [!NOTE]  
    > Wenn Sie einen Fehler erhalten, überprüfen Sie, ob die Spaltennamen in der Formel mit den von Ihnen in [Lektion 3: Umbenennen von Spalten](../analysis-services/lesson-3-rename-columns.md) geänderten Spaltennamen übereinstimmen.  
  
5.  Benennen Sie diese Spalte in **Month Calendar** um.  
  
Die berechnete Spalte "Month Calendar" bietet einen sortierbaren Namen für den Monat.  
  
#### Erstellen einer berechneten Spalte "Day of Week" in der Date-Tabelle  
  
1.  Klicken Sie bei nach wie vor aktiver Tabelle **Date** auf das Menü **Spalte** und anschließend auf **Spalte hinzufügen**.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    **=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE. Die neue Spalte wird ganz rechts von der Tabelle hinzugefügt.  
  
3.  Benennen Sie die Spalte in **Day of Week** um.  
  
4.  Klicken Sie auf die Spaltenüberschrift und ziehen Sie die Spalte zwischen die Spalte **Day Name** und die Spalte **Day of Month**.  
  
    > [!TIP]  
    > Durch das Verschieben von Spalten in der Tabelle wird die Navigation vereinfacht.  
  
Die berechnete Spalte "Day of Week" bietet einen sortierbaren Namen für den Wochentag.  
  
#### Erstellen einer berechneten Spalte "Product Subcategory Name" in der Product-Tabelle  
  
1.  Wählen Sie im Modell-Designer die Tabelle **Product** aus.  
  
2.  Führen Sie in der Tabelle einen Bildlauf nach ganz rechts aus. Beachten Sie, dass die ganz rechts stehende Spalte **Spalte hinzufügen** heißt (in Kursivschrift). Klicken Sie auf die Spaltenüberschrift.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein.  
  
    **=RELATED('Product Subcategory'[Product Subcategory Name])**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
4.  Benennen Sie die Spalte in **Product Subcategory Name** um.  
  
Die berechnete Spalte "Product Subcategory Name" wird verwendet, um eine Hierarchie in der Product-Tabelle zu erstellen, in der Daten der Spalte "Product Subcategory Name" in der Tabelle " Product Subcategory" enthalten sind. Hierarchien können maximal eine Tabelle umfassen. Sie erstellen Hierarchien später in Lektion 7.  
  
#### Erstellen einer berechneten Spalte "Product Category Name" in der Product-Tabelle  
  
1.  Klicken Sie bei nach wie vor aktiver Tabelle **Product** auf das Menü **Spalte** und anschließend auf **Spalte hinzufügen**.  
  
2.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    **=RELATED('Product Category'[Product Category Name])**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
3.  Benennen Sie die Spalte in **Product Category Name** um.  
  
Die berechnete Spalte "Product Category Name" wird verwendet, um eine Hierarchie in der Product-Tabelle zu erstellen, in der Daten der Spalte "Product Category Name" in der Tabelle " Product Category" enthalten sind. Hierarchien können maximal eine Tabelle umfassen.  
  
#### Erstellen einer berechneten Spalte "Margin" in der Internet Sales-Tabelle  
  
1.  Wählen Sie im Modell-Designer die Tabelle **Internet Sales** aus.  
  
2.  Fügen Sie eine neue Spalte hinzu.  
  
3.  Geben Sie in der Bearbeitungsleiste folgende Formel ein:  
  
    **=[Sales Amount]-[Total Product Cost]**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
4.  Benennen Sie die Spalte in **Margin** um.  
  
5.  Ziehen Sie die Spalte zwischen die Spalte **Sales Amount** und die Spalte **Tax Amt**.  
  
Die berechnete Spalte "Margin" dient zur Analyse von Gewinnspannen für jede Zeile (Produktzeile).  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 7: Erstellen von Measures](../analysis-services/lesson-7-create-measures.md).  
  
  
  
