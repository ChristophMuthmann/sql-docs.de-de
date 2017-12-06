---
title: "Hinzufügen eines externen Bilds (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7b27b9c57ac19450d279735945bd3d9fe2ea40a7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>Hinzufügen eines externen Bilds (Berichts-Generator und SSRS)
  Externe Bilder können auf einem Berichtsserver im einheitlichen Modus bzw. im integrierten SharePoint-Modus oder auf einer beliebigen anderen Website gespeichert sein. Wenn Sie externe Bilder im Bericht verwenden, müssen Sie prüfen, ob das Bild vorhanden ist und ob der Leser des Berichts Zugriffsberechtigungen für das Bild hat. Weitere Informationen finden Sie unter [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>So fügen Sie ein externes Bild hinzu  
  
1.  Klicken Sie in der Berichtsentwurfsansicht auf der Registerkarte **Einfügen** auf **Bild**.  
  
2.  Klicken Sie auf die Entwurfsoberfläche, und ziehen Sie ein Feld auf die gewünschte Größe des Bilds.  
  
3.  Geben Sie im Dialogfeld **Bildeigenschaften** auf der Registerkarte **Allgemein** einen Namen im Textfeld **Name** ein, oder übernehmen Sie den Standardnamen.  
  
4.  (Optional) Geben Sie im Textfeld **QuickInfo** Text ein, der angezeigt wird, wenn der Benutzer in einem in HTML gerenderten Bericht auf das Bild zeigt.  
  
5.  Wählen Sie unter **Bildquelle auswählen**die Option **Extern**aus.  
  
     Wenn ein Bild auf einem Berichtsserver im einheitlichen Modus gespeichert ist, geben Sie im Feld **Dieses Bild verwenden** einen relativen Pfad zu dem Bild ein – beispielsweise „../images/image1.jpg“.  
  
     Um ein Bild auf einem Berichtsserver im integrierten SharePoint-Modus oder in einer beliebigen anderen Website zu verwenden, geben Sie im Feld **Dieses Bild verwenden** eine vollständige URL zum Bild ein – beispielsweise „http://\<SharePointservername>/\<site>/Documents/images/image1.jpg“.  
  
     Weitere Informationen finden Sie unter [Angeben von Pfaden zu externen Elementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Optional) Klicken Sie auf **Größe**, **Sichtbarkeit**, **Aktion**oder **Rahmen** , um weitere Eigenschaften für das Bildberichtselement festzulegen.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Einbetten eines Bilds in einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Hinzufügen eines Hintergrundbilds (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [Bildeigenschaften (Dialogfeld), Allgemein (Berichts-Generator und SSRS)](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
