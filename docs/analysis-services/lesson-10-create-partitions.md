---
title: 'Lektion 11: Erstellen von Partitionen | Microsoft Docs'
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
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57ed4f364bcc7ca144c6e963c7b550a5dcc1831d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-10-create-partitions"></a>Lektion 10: Erstellen von Partitionen
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie Partitionen, um die FactInternetSales-Tabelle in kleinere logische Teile aufzuteilen, die verarbeitet werden können (aktualisiert) unabhängig von anderen Partitionen. Standardmäßig verfügt jede Tabelle, die Sie ins Modell einbinden, über eine Partition. Diese beinhaltet alle Spalten und Zeilen der Tabelle. Die FactInternetSales-Tabelle möchten die Daten nach Jahr unterteilen. eine Partition für jeden der fünf Jahren der Tabelle. Jede Partition kann dann unabhängig verarbeitet werden. Weitere Informationen finden Sie unter [Partitionen](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 9: Erstellen von Hierarchien](../analysis-services/lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Erstellen von Partitionen  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Zum Erstellen von Partitionen in der FactInternetSales-Tabelle  
  
1.  Erweitern Sie im tabellarischen Modell-Explorer **Tabellen**, mit der rechten Maustaste **FactInternetSales** > **Partitionen**.  
  
2.  Klicken Sie im Dialogfeld Partitions-Manager auf **Kopie**.  
  
3.  In **Partitionsname**, ändern Sie den Namen in **FactInternetSales2010**.  
  
    > [!TIP]  
    > Beachten Sie die Spaltennamen im Tabellenvorschaufenster die in der Modelltabelle (aktiviert), durch die Spaltennamen aus der Quelldatenbank enthaltenen Spalten anzuzeigen. Das liegt daran, dass das Tabellenvorschaufenster Spalten von der Quelltabelle und nicht von der Modelltabelle anzeigt.  
  
4.  Wählen Sie die **SQL** Schaltfläche direkt über der rechten Seite des Vorschaufensters auf die SQL-Anweisung-Editor zu öffnen.  
  
    Da die Partition nur die Zeilen eines bestimmten Zeitraums beinhalten soll, ist die WHERE-Klausel einzufügen. Sie können nur anhand einer SQL-Anweisung eine WHERE-Klausel erstellen.  
  
5.  In der **SQL-Anweisung** Feld, ersetzen Sie die vorhandene Anweisung durch Kopieren und Einfügen mit der folgenden Anweisung:  
  
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
  
    Diese Anweisung gibt an, dass die Partition alle Daten der Zeilen beinhalten soll, bei denen OrderDate für das Kalenderjahr 2010 gilt (wie in der WHERE-Klausel angegeben).  
  
6.  Klicken Sie auf **Überprüfen**.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>So erstellen Sie eine Partition für das Jahr 2011  
  
1.  Klicken Sie in der Liste auf die **FactInternetSales2010** Partitionieren Sie zuvor erstellt haben, und klicken Sie dann auf **Kopie**.  
  
2.  In **Partitionsname**, Typ **FactInternetSales2011**.  
  
3.  Ersetzen Sie in der SQL-Anweisung die WHERE-Klausel durch Folgendes, damit die Partition nur die Zeilen für das Jahr 2011 enthält:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>So erstellen Sie eine Partition für das Jahr 2012  
  
- Führen Sie die Schritte oben die folgende WHERE-Klausel verwenden. 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>So erstellen Sie eine Partition für das Jahr 2013  
  
- Führen Sie die Schritte oben die folgende WHERE-Klausel verwenden. 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>So erstellen eine Partition für das Jahr 2014  
  
- Führen Sie die Schritte oben die folgende WHERE-Klausel verwenden. 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>Löschen Sie die FactInternetSales-partition
Nun, da Sie Partitionen für jedes Jahr haben, können Sie die FactInternetSales-Partition löschen. Dies verhindert die Überlappung, bei der Auswahl von Prozess alle beim Verarbeiten von Partitionen.
#### <a name="to-delete-the-factinternetsales-partition"></a>So löschen Sie die FactInternetSales-partition
-  Klicken Sie auf die FactInternetSales-Partition, und klicken Sie dann auf **löschen**.



## <a name="process-partitions"></a>Partitionen verarbeiten  
Beachten Sie im Partitions-Manager die **letzten verarbeitet** Spalte für jede der neuen Partitionen Sie soeben erstellten zeigt diese Partitionen nie verarbeitet wurden. Wenn Sie neue Partitionen erstellen, führen Sie einen Partitionsverarbeitungs- bzw. Tabellenverarbeitungsvorgang aus, um die Daten dieser Partitionen zu aktualisieren.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>So verarbeiten Sie die FactInternetSales-Partitionen  
  
1.  Klicken Sie auf **OK** um das Dialogfeld Partitions-Manager zu schließen.  
  
2.  Klicken Sie auf die **FactInternetSales** Tabelle, und klicken Sie auf die **Modell** Menü > **Prozess** > **Partitionen verarbeiten**.  
  
3.  Überprüfen Sie im Dialogfeld Partitionen verarbeiten **Modus** festgelegt ist, um **Standard verarbeiten**.  
  
4.  Aktivieren Sie das Kontrollkästchen in der Spalte **Verarbeiten** für jede der fünf von Ihnen erstellten Partitionen, und klicken Sie anschließend auf **OK**.  

    ![als-tabellarische-lesson10-Prozess-Partitionen](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    Wenn Sie für Identitätswechsel-Anmeldeinformationen aufgefordert werden, geben Sie den Windows-Benutzernamen und Kennwort an, das Sie in Lektion 2 angegeben.  
  
    Das Dialogfeld **Datenverarbeitung** wird daraufhin angezeigt. Es zeigt die Verarbeitungsdetails für jede Partition an. Beachten Sie, dass eine unterschiedliche Anzahl an Zeilen für jede Partition übertragen wird. Das liegt daran, dass jede Partition nur die Zeilen für das in der WHERE-Klausel der SQL-Anweisung angegebene Jahr beinhaltet. Wenn die Verarbeitung abgeschlossen ist, fahren Sie fort und schließen Sie das Dialogfeld „Datenverarbeitung“.  
  
    ![als tabellarische-lesson10-Prozess-Vervollständigung](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 11: Erstellen von Rollen](../analysis-services/lesson-11-create-roles.md). 

