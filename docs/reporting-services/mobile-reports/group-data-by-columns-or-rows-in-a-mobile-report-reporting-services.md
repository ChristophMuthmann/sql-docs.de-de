---
title: Gruppieren Sie Daten nach Spalten oder Zeilen in einem mobilen Bericht | Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c1b584f5a88af5055ffac67932fd94a37734bfd
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="group-data-by-columns-or-rows-in-a-mobile-report--reporting-services"></a>Gruppieren von Daten nach Spalten oder Zeilen in einem mobilen Bericht | Reporting Services
Sie können in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]Daten in vielen Arten von Diagrammen nach Spalten oder Zeilen organisieren. Befolgen Sie dazu die Schritte in dieser detaillierten Anleitung.

In Zeit-, Summen-, Kreis- und Trichterdiagrammen können Sie die Daten nach Zeilen oder Spalten organisieren. 
* Das Organisieren nach Spalten ist nützlich, wenn eine Tabelle mehrere Spalten mit Daten enthält, die Sie vergleichen möchten. 
* Das Organisieren nach Zeilen funktioniert besser, wenn eine Spalte in der Tabelle die Namen der verschiedenen Kategorien enthält. 

In den folgenden Schritten wird eine vergleichende Tabelle mit Gesamtwerten mit den simulierten Daten in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] verwendet, um den Unterschied bei der Strukturierung der Daten nach Zeilen oder Spalten in einem Diagramm zu veranschaulichen.  

1. Ziehen Sie ein **vergleichendes Diagramm mit Gesamtwerten** von der Registerkarte **Layout** auf die Entwurfsoberfläche, und vergrößern Sie es.

2. Wählen Sie die Registerkarte **Daten** aus. Sie sehen, dass die Tabelle „SimulatedTable“ eine Reihe von Spalten enthält: **Metric1** bis **Metric5** und **Comparison1** bis **Comparison5**. 

   ![mobile-report-data-group-column](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. Im Bereich **Dateneigenschaften** ist **SimulatedTable** für **Hauptreihe**festgelegt. Klicken Sie auf den Pfeil im Feld neben **Hauptreihe**. Sie sehen, dass **Metric1** bis **Metric5** ausgewählt sind.

   ![mobile-report-properties-columns](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   Für **Vergleichsreihe** --  sind **Comparison1** bis **Comparison5** ausgewählt.
   
4. Wählen Sie **Vorschau** aus.

   ![mobile-report-chart-by-columns](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   Jeder Balken im Diagramm stellt eine Spalte in der Tabelle dar. Die dickeren Balken sind die Metrikspalten, die dünneren die Vergleichsspalten.

5. Klicken Sie links oben auf den Zurück-Pfeil, um den Vorschaumodus zu beenden.

6. Ändern Sie auf der Registerkarte **Layout** im Bereich **Visuelle Eigenschaften** die **Datenstruktur** von **Nach Spalten** in **Nach Zeilen**.  

7. Wählen Sie die Registerkarte **Daten** aus. Nun enthält die Tabelle „SimulatedTable“ die Spalte **Category** sowie die Spalten **Metric** und **Comparison** , mit „Category“ von A bis E. 

   ![mobile-report-data-group-rows](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  Im Bereich **Dateneigenschaften** befindet sich nun das Feld „Kategoriespalte“, das die Spalte „Category“ aus der Tabelle „SimulatedTable“ enthält. In der Hauptreihe können Sie auswählen, welche Spalte für die Werte verwendet werden soll. In der Standardeinstellung wählt [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] „Metric1“ bis „Metric5“ für die Hauptreihe und „Comparison1“ bis „Comparison5“ für die Vergleichsreihe aus. 

    ![mobile-report-properties-rows](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. Wählen Sie **Vorschau**aus.

   ![mobile-report-chart-by-rows](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   Nun stellt jeder Balken im Diagramm die Werte jeder Kategorie in der Spalte „Category“ dar.

### <a name="see-also"></a>Siehe auch
* [Visualisierungen in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
