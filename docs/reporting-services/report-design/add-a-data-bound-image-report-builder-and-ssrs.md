---
title: "Hinzufügen eines datengebundenen Bilds (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 253d3abfffae056d6300e2203623e7af023a2476
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>Hinzufügen eines datengebundenen Bilds (Berichts-Generator und SSRS)
  Ein Bericht kann einen Verweis auf ein Bild enthalten, das in einer Datenbank gespeichert ist. Ein solches Bild wird als *datengebundenes Bild*bezeichnet. Bilder, die neben Produktnamen in einer Produktliste angezeigt werden, sind Beispiele für datengebundene Bilder.  
  
 Für das Hinzufügen eines datengebundenes Bilds zu einem Seitenkopf oder -fuß sind zusätzliche Schritte erforderlich. Weitere Informationen finden Sie unter [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>So fügen Sie ein datengebundenes Bild hinzu  
  
1.  Erstellen Sie in der Berichtsentwurfsansicht eine Tabelle mit einer Datenquellenverbindung und einem Dataset mit einem Feld, das binäre Bilddaten enthält. Weitere Informationen finden Sie unter [Tabellen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
2.  Fügen Sie eine Spalte in die Tabelle ein. Weitere Informationen finden Sie unter [Einfügen oder Löschen einer Spalte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Klicken Sie im Menü **Einfügen** auf **Bild**und dann in die Datenzeile der neuen Spalte.  
  
4.  Geben Sie im Dialogfeld **Bildeigenschaften** auf der Seite **Allgemein** einen Namen im Textfeld Name ein, oder übernehmen Sie den Standardnamen.  
  
5.  (Optional) Geben Sie im Textfeld **QuickInfo** Text ein, der angezeigt wird, wenn der Benutzer in dem in HTML gerenderten Bericht auf das Bild zeigt.  
  
6.  Wählen Sie unter **Bildquelle auswählen**die Option **Datenbank**aus.  
  
7.  Wählen Sie unter **Dieses Feld verwenden**das Feld aus, das Bilder im Bericht enthält.  
  
8.  Wählen Sie unter **Diesen MIME-Typ verwenden**den MIME-Typ oder das Dateiformat des Bilds aus – beispielsweise BMP.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ein Bildplatzhalter wird auf der Berichtsentwurfsoberfläche angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Einbetten eines Bilds in einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Hinzufügen eines externen Bilds &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Bildeigenschaften &#40;Dialogfeld, Allgemein, Berichts-Generator und SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
