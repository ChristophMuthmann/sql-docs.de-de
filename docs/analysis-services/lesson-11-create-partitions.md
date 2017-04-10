---
title: "Lektion 11: Erstellen von Partitionen | Microsoft Docs"
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
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 11: Erstellen von Partitionen
In dieser Lektion erstellen Sie Partitionen, um die Internet Sales-Tabelle in kleinere logische Teile aufzuteilen, die unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden können. Standardmäßig verfügt jede Tabelle, die Sie ins Modell einbinden, über eine Partition. Diese beinhaltet alle Spalten und Zeilen der Tabelle. Für die Internet Sales-Tabelle sollen die Daten nach Jahr aufgeteilt werden, wobei jede Partition jeweils ein Jahr von den fünf Jahren der Tabelle umfasst.  Jede Partition kann dann unabhängig verarbeitet werden. Weitere Informationen finden Sie unter [Partitionen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 10: Erstellen von Hierarchien](../analysis-services/lesson-10-create-hierarchies.md).  
  
## Erstellen von Partitionen  
  
#### So erstellen Sie Partitionen in der Internet Sales-Tabelle  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle **Internet Sales** und dann auf das Menü **Tabelle**. Klicken Sie anschließend auf **Partitionen**.  
  
    Das Dialogfeld **Partitions-Manager** wird geöffnet.  
  
2.  Klicken Sie im Dialogfeld **Partitions-Manager** unter „Partitionen“ auf die Partition **Internet Sales**.  
  
3.  Ändern Sie unter **Partitionsname** den Namen in **Internet Sales 2010**.  
  
    > [!TIP]  
    > Vor dem Fortfahren mit dem nächsten Schritt ist zu beachten, dass die Spaltennamen für diese in der Modelltabelle enthaltenen (aktivierten) Spalten im Tabellenvorschaufenster den Spaltennamen der Quelle entsprechen. Das liegt daran, dass das Tabellenvorschaufenster Spalten von der Quelltabelle und nicht von der Modelltabelle anzeigt.  
  
4.  Klicken Sie direkt rechts oberhalb des Vorschaufensters auf die Schaltfläche **Abfrage-Editor**.  
  
    Da die Partition nur die Zeilen eines bestimmten Zeitraums beinhalten soll, ist die WHERE-Klausel einzufügen. Sie können nur anhand einer SQL-Anweisung eine WHERE-Klausel erstellen.  
  
5.  Ersetzen Sie im Feld **SQL-Anweisung** die vorhandene Anweisung durch die folgende Anweisung:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Diese Anweisung gibt an, dass die Partition alle Daten der Zeilen beinhalten soll, bei denen OrderDate für das Kalenderjahr 2010 gilt (wie in der WHERE-Klausel angegeben).  
  
6.  Klicken Sie auf **Überprüfen**.  
  
  
#### So erstellen Sie eine Partition für das Jahr 2011  
  
1.  Klicken Sie in der Liste der Partitionen auf die Partition **Internet Sales 2010**, die Sie gerade erstellt haben. Klicken Sie anschließend auf **Kopieren**.  
  
2.  Geben Sie in das Feld **Partitionsname** die Zeichenfolge **Internet Sales 2011** ein.  
  
3.  Ersetzen Sie in der SQL-Anweisung die WHERE-Klausel durch Folgendes, damit die Partition nur die Zeilen für das Jahr 2011 enthält:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### So erstellen Sie eine Partition für das Jahr 2012  
  
1.  Klicken Sie im Dialogfeld **Partitions-Manager** auf **Kopieren**.  
  
2.  Geben Sie in das Feld **Partitionsname** die Zeichenfolge **Internet Sales 2012** ein.  
  
3.  Ersetzen Sie in der SQL-Anweisung die WHERE-Klausel durch Folgendes, damit die Partition nur die Zeilen für das Jahr 2012 enthält:  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### So erstellen Sie eine Partition für das Jahr 2013  
  
1.  Klicken Sie im Dialogfeld **Partitions-Manager** auf **Neu**.  
  
2.  Geben Sie in das Feld **Partitionsname** die Zeichenfolge **Internet Sales 2013** ein.  
  
3.  Ersetzen Sie in der SQL-Anweisung die WHERE-Klausel durch Folgendes, damit die Partition nur die Zeilen für das Jahr 2013 enthält:  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### So erstellen Sie für das Jahr 2014 in der Internet Sales-Tabelle eine Partition  
  
1.  Klicken Sie im Dialogfeld **Partitions-Manager** auf **Neu**.  
  
2.  Geben Sie in das Feld **Partitionsname** die Zeichenfolge **Internet Sales 2014** ein.  
  
3.  Ersetzen Sie in der SQL-Anweisung die WHERE-Klausel durch Folgendes, damit die Partition nur die Zeilen für das Jahr 2014 enthält:  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## Partitionen verarbeiten  
Achten Sie im Dialogfeld **Partitions-Manager** auf das Sternchen (**\***) neben den Partitionsnamen für jede der gerade neu erstellten Partitionen. Dies gibt an, dass die Partition noch nicht verarbeitet (aktualisiert) wurde. Wenn Sie neue Partitionen erstellen, führen Sie einen Partitionsverarbeitungs- bzw. Tabellenverarbeitungsvorgang aus, um die Daten dieser Partitionen zu aktualisieren.  
  
#### So verarbeiten Sie die Internet Sales-Partitionen  
  
1.  Klicken Sie auf **OK**, um das Dialogfeld **Partitions-Manager** zu schließen.  
  
2.  Klicken Sie im Modell-Designer auf die Tabelle **Internet Sales**. Klicken Sie anschließend auf das Menü **Modell**, zeigen Sie auf **Verarbeiten** (Aktualisieren), und klicken Sie auf **Partitionen verarbeiten**.  
  
3.  Überprüfen Sie im Dialogfeld **Partitionen verarbeiten**, ob der Wert für **Modus** auf **Standard verarbeiten** festgelegt ist.  
  
4.  Aktivieren Sie das Kontrollkästchen in der Spalte **Verarbeiten** für jede der fünf von Ihnen erstellten Partitionen, und klicken Sie anschließend auf **OK**.  
  
    Wenn Identitätswechsel-Anmeldeinformationen verlangt werden, geben Sie die Kombination aus Windows-Benutzername und Kennwort ein, die Sie in Lektion 2 (Schritt 6) angegeben haben.  
  
    Das Dialogfeld **Datenverarbeitung** wird daraufhin angezeigt. Es zeigt die Verarbeitungsdetails für jede Partition an. Beachten Sie, dass eine unterschiedliche Anzahl an Zeilen für jede Partition übertragen wird. Das liegt daran, dass jede Partition nur die Zeilen für das in der WHERE-Klausel der SQL-Anweisung angegebene Jahr beinhaltet. Wenn die Verarbeitung abgeschlossen ist, fahren Sie fort und schließen Sie das Dialogfeld „Datenverarbeitung“.  
  
  
  
## Nächste Schritte  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 12: Erstellen von Rollen](../analysis-services/lesson-12-create-roles.md).  
  
  
  
