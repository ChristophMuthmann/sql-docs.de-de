---
title: "Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c1c0be54c8cfba5a8cde5e7b79deb6f8ef15f561
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich (Berichts-Generator und SSRS)
  Datasetfelder sind die integrierte Auflistung von Feldnamen, die die Daten darstellen, die zurückgegeben werden, wenn eine Datasetabfrage in einer externen Datenquelle ausgeführt wird.  
  
 Bei einem eingebetteten Dataset sind Datasetfelder die Felder, die erstellt werden, nachdem Sie die Erstellung einer Abfrage abgeschlossen und den Bereich Abfrage-Designer geschlossen haben, und von Ihnen erstellte Felder berechnet werden.  
  
 Bei einem freigegebenen Dataset entsprechen die Datasetfelder den Feldern aus der freigegebenen Datasetdefinition, die dem Bericht hinzugefügt wurden. Obwohl die Abfrage vom freigegebenen Dataset auf dem Berichtsserver bei jeder Ausführung des Berichts verwendet wird, ist die Liste der Datasetfelder im Bericht statisch.  
  
 Aktualisieren Sie mit der Option **Felder Aktualisieren** die Liste der Felder im Bericht, damit Sie mit der aktuellen Liste der Felder der freigegebenen Datasetabfrage übereinstimmen. Die Aktualisierung der Feldliste wirkt sich nicht auf die berechneten Felder aus, die Sie im Bericht definieren.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>So fügen Sie ein Abfragefeld hinzu  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Dataset, und klicken Sie anschließend auf **Abfragefeld hinzufügen**.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten**.  
  
2.  Klicken Sie auf der Seite **Felder** des Dialogfelds **Dataseteigenschaften** auf **Hinzufügen**und dann auf **Abfragefeld**. Unten im Raster wird eine neue Zeile hinzugefügt.  
  
3.  Geben Sie einen Namen für das neue Feld im Textfeld **Feldname** ein.  
  
    > [!NOTE]  
    >  Namen müssen innerhalb des Datasets eindeutig sein.  
  
4.  Geben Sie im Textfeld **Feldquelle** den Namen eines vorhandenen Felds in der Datenquelle ein.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>So fügen Sie ein berechnetes Feld hinzu  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Dataset, und klicken Sie anschließend auf **Berechnetes Feld hinzufügen**.  
  
2.  Klicken Sie auf der Seite **Felder** des Dialogfelds **Dataseteigenschaften** auf **Hinzufügen**und dann auf **Berechnetes Feld**. Unten im Raster wird eine neue Zeile hinzugefügt.  
  
3.  Geben Sie einen Namen für das neue Feld im Textfeld **Feldname** ein.  
  
    > [!NOTE]  
    >  Namen müssen innerhalb des Datasets eindeutig sein.  
  
4.  Geben Sie den Ausdruck für das neue Feld im Textfeld **Feldquelle** ein. Klicken Sie auf die Ausdrucksschaltfläche (**fx**), um einen Ausdruck zu erstellen.  
  
    > [!NOTE]  
    >  Der Ausdruck für ein berechnetes Feld darf keine Aggregate oder Verweise auf Berichtselemente enthalten.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>So bearbeiten Sie ein Abfragefeld oder ein Datasetfeld  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Feld, und klicken Sie anschließend auf **Feldeigenschaften**.  
  
2.  Klicken Sie auf der Seite **Felder** des Dialogfelds **Dataseteigenschaften** auf ein bereits vorhandenes Feld, um die Zeile auszuwählen.  
  
3.  Ändern Sie den Namen des Felds oder den Wert des Felds.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>So löschen Sie ein Abfragefeld oder ein berechnetes Feld  
  
1.  Erweitern Sie im Berichtsdatenbereich das Dataset, um die Feldauflistung anzuzeigen.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Feld, das Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>So aktualisieren Sie die Feldauflistung im Berichtsdatenbereich für ein freigegebenes Dataset  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Dataset, und klicken Sie anschließend auf **Abfrage**.  
  
2.  Klicken Sie auf **Felder aktualisieren**.  
  
     Die Abfrage des freigegebenen Datasets wird auf dem Berichtsserver ausgeführt und gibt die aktuelle Feldauflistung zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Datasetfelder-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Abfrage-Designer in Reporting Services](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)   
 [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
