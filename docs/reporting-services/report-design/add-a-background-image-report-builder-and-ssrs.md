---
title: "Hinzufügen eines Hintergrundbilds (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e8384182f7eb57df836a9530af6baf3f0b008154
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>Hinzufügen eines Hintergrundbilds (Berichts-Generator und SSRS)
  Sie können einem Berichtselement, z. B. einem Rechteck, Textfeld, einer Liste, Matrix, Tabelle und einigen Teilen eines Diagramms, oder einem Berichtsabschnitt, z. B. dem Seitenkopf, Seitenfuß oder Berichtshauptteil, ein Hintergrundbild hinzufügen. Sie können ein Hintergrundbild für jedes ausgewählte Element in der Berichtsentwurfsoberfläche definieren, für das **BackgroundImage** im Bereich Eigenschaften angezeigt wird. Bei dem Hintergrundbild kann es sich wie bei anderen Bildern um eine URL zu einem Bild auf dem Berichtsserver handeln, ein Bild aus einem Datasetfeld oder ein in die Berichtsdefinition eingebettetes Bild. Wenn Sie ein in den Bericht eingebettetes Bild verwenden möchten, müssen Sie es der Berichtsdefinition hinzufügen, bevor Sie es der Entwurfsoberfläche hinzufügen können.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>So betten Sie ein Bild in die Berichtsdefinition ein  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf den Knoten **Bilder** , und klicken Sie dann auf **Bild hinzufügen**.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Berichtsdatenbereichs klicken Sie auf der Registerkarte **Ansicht** auf **Berichtsdaten**.  
  
2.  Navigieren Sie zu dem Bild, das Sie in die Berichtsdefinition einbetten möchten, und klicken Sie dann auf **OK**.  
  
### <a name="to-add-a-background-image"></a>So fügen Sie ein Hintergrundbild hinzu  
  
1.  Wählen Sie in der Berichtsentwurfsansicht das Berichtselement aus, dem Sie ein Hintergrundbild hinzufügen möchten.  
  
2.  Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**, falls der Bereich "Eigenschaften" nicht angezeigt wird.  
  
3.  Erweitern Sie im Bereich "Eigenschaften" die **BackgroundImage**-Eigenschaft, und führen Sie dann die folgenden Schritte aus:  
  
    -   Eingebettetes Bild:  
  
         Legen Sie **Source** auf **Embedded**fest.  
  
         Legen Sie für **Value** den Namen eines Bilds fest, das in den Bericht eingebettet ist.  
  
    -   Externes Bild:  
  
         Legen Sie **Source** auf **External**fest.  
  
         Legen Sie für **Value** einen gültigen Pfad zu einem Bild fest. Dieses kann sich auf einem Berichtsserver im einheitlichen Modus oder im integrierten SharePoint-Modus bzw. auf einer beliebigen anderen Website befinden. Weitere Informationen finden Sie unter [Hinzufügen eines externen Bilds (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md).  
  
    -   Bild, das in einem Feld in der Datenbank enthalten ist, mit der das Berichtselement verbunden ist:  
  
         Legen Sie **Source** auf **Database**fest.  
  
         Legen Sie für **Value** den Namen eines Felds im Berichtsdataset fest. Weitere Informationen finden Sie unter [Hinzufügen eines datengebundenen Bilds (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md).  
  
         Wählen Sie für **MIMEType**oder als Dateiformat den entsprechenden MIME-Typ für das Bild aus – beispielsweise BMP.  
  
        > [!NOTE]  
        >  Die MIMEType-Eigenschaft trifft nur dann zu, wenn die **Source** -Eigenschaft auf **Database**festgelegt ist. Wenn die **Source** -Eigenschaft auf **External** oder **Embedded**festgelegt ist, wird der Wert von **MIMEType** ignoriert.  
  
    -   Wählen Sie für **BackgroundRepeat**einen Ausdruck, **Default**, **Repeat**, **RepeatX**, **RepeatY**oder **Clip**aus.  
  
         Für Hintergrundbilder in einem Diagramm kann **BackgroundRepeat** auf **Default**, **Repeat**, **Fit**und **Clip**festgelegt werden, jedoch nicht auf **RepeatX** oder **RepeatY**.  
  
## <a name="see-also"></a>Siehe auch  
 [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Bildeigenschaften (Dialogfeld), Allgemein (Berichts-Generator und SSRS)](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
