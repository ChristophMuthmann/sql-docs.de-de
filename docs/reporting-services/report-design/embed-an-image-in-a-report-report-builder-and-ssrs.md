---
title: Einbetten eines Bilds in einem Bericht (Berichts-Generator und SSRS) | Microsoft Docs
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
f1_keywords:
- sql13.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1825a28cd9939228a73c1a4a6269c717b691ab2
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>Einbetten eines Bilds in einen Bericht (Berichts-Generator und SSRS)
  Ein Bericht kann ein eingebettetes Bild enthalten. Durch das Einbetten eines Bilds wird sichergestellt, dass das Bild immer für den Bericht verfügbar ist. Gleichzeitig nimmt allerdings die Größe der Berichtsdefinition zu; das ist die Datei, die den Bericht definiert. Die in einen Bericht eingebetteten Bilder werden im Berichtsdatenbereich aufgeführt.  
  
 Sie können ein Bild in die Berichtsdefinition einbetten, bevor Sie es der Entwurfsoberfläche hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Hintergrundbilds &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>So betten Sie ein Bild in einen Bericht ein  
  
1.  Klicken Sie in der Berichtsentwurfsansicht auf der Registerkarte **Einfügen** auf **Bild**.  
  
2.  Klicken Sie auf die Entwurfsoberfläche, und ziehen Sie ein Feld auf die gewünschte Größe des Bilds.  
  
3.  Geben Sie im Dialogfeld **Bildeigenschaften** auf der Seite **Allgemein** einen Namen im Textfeld **Name** ein, oder übernehmen Sie den Standardnamen.  
  
4.  Geben Sie (optional) im Textfeld **QuickInfo** Text ein, der angezeigt wird, wenn der Benutzer im gerenderten Bericht auf das Bild zeigt.  
  
5.  Wählen Sie unter **Bildquelle auswählen**die Option **Eingebettet**aus.  
  
6.  Klicken Sie neben dem Textfeld **Dieses Bild verwenden** auf die Schaltfläche **Importieren** .  
  
7.  Wählen Sie unter **Dateityp**den Bilddateityp aus, navigieren Sie zu der Datei, und klicken Sie dann auf **Öffnen**.  
  
8.  Klicken Sie im Dialogfeld **Bildeigenschaften** auf **OK**.  
  
     Das Bild wird in dem auf der Entwurfsoberfläche gezeichneten Feld und die Datei unterhalb des Bildordners im Berichtsdatenbereich angezeigt.  
  
    > [!NOTE]  
    >  Der MIME-Typ (z. B. BMP) wird beim Importieren des Bilds automatisch abgeleitet. Um den MIME-Typ zu ändern, befolgen Sie die nächste Vorgehensweise.  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>(Optional) So ändern Sie den MIME-Typ eines importierten Bilds  
  
1.  Öffnen Sie den Bericht in der Entwurfsansicht.  
  
2.  Wählen Sie das Bild in der Entwurfsoberfläche aus. Der Bereich **Eigenschaften** zeigt die Bildeigenschaften an.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Bereichs „Eigenschaften“ klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
3.  Klicken Sie auf das Textfeld neben der **MIMEType** -Eigenschaft, und wählen Sie in der Dropdownliste einen neuen MIME-Typ aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Hinzufügen eines datengebundenen Bilds &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Bildeigenschaften &#40;Dialogfeld, Allgemein, Berichts-Generator und SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
