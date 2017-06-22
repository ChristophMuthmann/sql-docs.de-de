---
title: "Hinzufügen einer Drillthroughaktion für einen Bericht (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f1e5c7c678cb3c38d9e0225ce47bc2dca91ab326
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>Hinzufügen einer Drillthroughaktion für einen Bericht (Berichts-Generator und SSRS)
  Der Bericht, der geöffnet wird, wenn Sie auf den Link im Hauptbericht klicken, wird als *Drillthroughbericht*bezeichnet. Der Drillthrough-Link ermöglicht einen Drillthrough-Vorgang.  
  
 Drillthroughberichte müssen auf demselben Berichtsserver wie der Hauptbericht veröffentlicht werden, können aber in anderen Ordnern abgelegt sein. Sie können jedem Element einen Drillthroughlink hinzufügen, das über eine Eigenschaft **Aktion** verfügt, z. B. ein Textfeld, ein Bild oder Datenpunkte in einem Diagramm.  
  
 Sie müssen zuerst den Drillthroughbericht erstellen, mit dem der Hauptbericht verknüpft wird, um einem Bericht einen Drillthroughlink hinzuzufügen. Ein Drillthroughbericht enthält im Allgemeinen Details zu einem im ursprünglichen Zusammenfassungsbericht enthaltenen Element und enthält oft Parameter, mit denen der Drillthroughbericht basierend auf Parametern, die vom Hauptbericht übergeben werden, gefiltert wird. Weitere Informationen zum Erstellen des Drillthroughberichts finden Sie unter [Drillthroughberichte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>So fügen Sie eine Drillthroughaktion hinzu  
  
1.  Klicken Sie in der Entwurfsansicht mit der rechten Maustaste auf das Textfeld, Bild oder Diagramm, dem Sie einen Link hinzufügen möchten, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Eigenschaften** des Elements auf **Aktion**.  
  
3.  Wählen Sie **Gehe zu Bericht**. Im Dialogfeld für diese Option werden zusätzliche Abschnitte angezeigt.  
  
4.  Klicken Sie unter **Bericht angeben**auf **Durchsuchen** , um nach dem Namen des gewünschten Berichts zu suchen, oder geben Sie den Namen ein. Alternativ können Sie auf die Ausdrucksschaltfläche (**fx**) klicken, um einen Ausdruck für den Berichtsnamen zu erstellen.  
  
     Das Format des Pfads zum Drillthroughbericht unterscheidet sich beim einheitlichen und integrierten SharePoint-Modus. Wenn Sie den Bericht über "Durchsuchen" auswählen, wird der Pfad im richtigen Format angegeben. Weitere Informationen finden Sie unter [Angeben von Pfaden zu externen Elementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
     Wenn Sie Parameter für den Drillthroughbericht angeben müssen, führen Sie den nächsten Schritt aus.  
  
5.  Klicken Sie in **Diese Parameter zum Ausführen des Berichts verwenden**auf **Hinzufügen**. Dem Parameterraster wird eine neue Zeile hinzugefügt.  
  
    -   Klicken Sie im Textfeld **Name** auf die Dropdownliste, oder geben Sie den Namen des Berichtsparameters im Drillthroughbericht ein.  
  
        > [!NOTE]  
        >  Die Namen in der Parameterliste müssen mit den erwarteten Parametern im Zielbericht genau übereinstimmen. Beispiel: Die Schreibweise von Parameternamen muss übereinstimmen. Falls die Namen nicht übereinstimmen oder ein erwarteter Parameter nicht aufgeführt ist, ergibt der Drillthroughbericht einen Fehler.  
  
    -   Geben Sie den Wert, der an den Parameter im Drillthroughbericht übergeben werden soll, in das Feld **Wert**ein bzw. wählen Sie ihn aus.  
  
        > [!NOTE]  
        >  Werte können einen Ausdruck enthalten, der zu einem an den Berichtsparameter zu übergebenden Wert ausgewertet werden kann. Die Ausdrücke in der Werteliste beinhalten die Feldliste für den aktuellen Bericht.  
  
     Informationen zum Ausblenden von Parametern in Berichten finden Sie unter [Hinzufügen, Ändern oder Löschen von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md).  
  
6.  (Optional) Bei Textfeldern ist es hilfreich, die Farbe und den Effekt des Texts zu ändern, um zu verdeutlichen, dass es sich um einen Link handelt. Verwenden Sie dazu die Registerkarte **Home** auf dem Menüband.  
  
7.  Führen Sie den Bericht aus, und klicken Sie auf das Berichtselement, für das Sie den Link festgelegt haben, um den Link zu testen.  
  
## <a name="see-also"></a>Siehe auch  
 [Aktionseigenschaften (Dialogfeld) &#40;Berichts-Generator und SSRS&#41;](http://msdn.microsoft.com/library/2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9)   
 [Formatieren von Datenpunkten in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Anzeigen von QuickInfos für eine Reihe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  
