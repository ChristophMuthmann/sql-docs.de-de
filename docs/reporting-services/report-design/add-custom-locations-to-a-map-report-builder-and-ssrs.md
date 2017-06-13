---
title: "Hinzufügen benutzerdefinierter Orte zu einer Karte (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c78f99c32d37e36986c4ea8bac20c12f87d4d568
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>Hinzufügen benutzerdefinierter Orte zu einer Karte (Berichts-Generator und SSRS)
  Nachdem Sie einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht eine Karte hinzugefügt haben, können Sie eigene Punktpositionen hinzufügen.  
  
 Die Anzeigeeigenschaften für alle Punkte in einer Ebene werden durch Festlegen von Optionen für die Punkteigenschaften für die Ebene gesteuert. Für einen ausgewählten eingebetteten Punkt können Sie die Anzeigeeigenschaften überschreiben.  
  
> [!NOTE]  
>  Wenn Sie die Ebenenanzeigeeigenschaften für den eingebetteten Punkt überschreiben, sind die Änderungen, die Sie vornehmen, nicht umkehrbar.  
  
 Weitere Informationen finden Sie unter [Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-point-layer"></a>So fügen Sie eine Punktebene hinzu  
  
1.  Klicken Sie auf der Berichtsentwurfsoberfläche auf die Karte, um sie auszuwählen und den Kartenbereich anzuzeigen.  
  
2.  Klicken Sie auf der Symbolleiste auf **Ebene hinzufügen**.  
  
3.  Klicken Sie in der Dropdownliste auf **Punktebene hinzufügen**. Der Karte wird eine Punktebene ohne Punkte hinzugefügt. Standardmäßig ist die Punktebene für eingebettete Punkte bereit.  
  
## <a name="to-add-a-custom-point"></a>So fügen Sie einen benutzerdefinierten Punkt hinzu  
  
1.  Klicken Sie auf der Berichtsentwurfsoberfläche auf die Karte, um sie auszuwählen und den Kartenbereich anzuzeigen.  
  
2.  Klicken Sie im Kartenbereich mit der rechten Maustaste auf eine Punktebene, die den Typ **Eingebettet**aufweist, und klicken Sie dann auf **Punkt hinzufügen**. Der Cursor verändert sich zu einem Fadenkreuz.  
  
3.  Um einen Punkt hinzuzufügen, klicken Sie auf einen Ort auf der Karte. Der ausgewählten Ebene wird an der Position, an der Sie klicken, ein eingebetteter Punkt hinzugefügt.  
  
## <a name="to-customize-the-display-for-an-embedded-point"></a>So passen Sie die Anzeige für einen eingebetteten Punkt an  
  
1.  Klicken Sie mit der rechten Maustaste auf den Punkt, und klicken Sie dann auf **Punkteigenschaften**. Das Dialogfeld **Eigenschaften für eingebettete Punkte der Karte** wird geöffnet.  
  
2.  Klicken Sie auf **Punktoptionen für diese Ebene überschreiben**. Mehrere Eigenschaftenseiten werden im linken Bereich angezeigt.  
  
3.  Klicken Sie auf die Seiten, und legen Sie die Anzeigeeigenschaften fest, die Sie auf diesen Punkt anwenden möchten.  
  
## <a name="see-also"></a>Siehe auch  
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
