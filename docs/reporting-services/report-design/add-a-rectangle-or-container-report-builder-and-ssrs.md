---
title: "Hinzufügen eines Rechtecks oder Containers (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c472b3486dc568f79540f1a6bb8c74209828e772
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Hinzufügen eines Rechtecks oder Containers (Berichts-Generator und SSRS)
  Fügen Sie einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht ein Rechteck hinzu, wenn Sie durch ein grafisches Element Bereiche des Berichts trennen oder hervorheben oder einen Hintergrund für ein oder mehrere Berichtselemente bereitstellen möchten. Rechtecke werden auch als Container verwendet, mit denen das Rendering von Datenbereichen in einem Bericht gesteuert werden kann. Sie können die Darstellung eines Rechtecks anpassen, indem Sie die Rechteckeigenschaften bearbeiten, z. B. den Hintergrund und die Rahmenfarben. Weitere Informationen zum Verwenden eines Rechtecks als Container finden Sie unter [Rechtecke und Linien (Berichts-Generator und SSRS)](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) und [Anzeigen derselben Daten in einer Matrix und einem Diagramm (Berichts-Generator)](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).    
   
## <a name="to-add-a-rectangle"></a>So fügen Sie ein Rechteck hinzu    
    
1.  Klicken Sie auf der Registerkarte **Einfügen** in der Gruppe **Berichtselemente** auf **Rechteck**.    
    
2.  Klicken Sie auf der Entwurfsoberfläche auf die Stelle, an der die obere linke Ecke des Rechtecks positioniert werden soll, und ziehen Sie den Mauszeiger an die Stelle, an der die untere rechte Ecke des Rechtecks positioniert werden soll.    
    
     Während Sie den Cursor bewegen, werden "Ausrichtungslinien" angezeigt, wenn der Cursor mit anderen Objekten auf der Entwurfsoberfläche ausgerichtet ist. Mit diesen Ausrichtungslinien können Sie die Objekte besser ausrichten.    
    
## <a name="to-create-a-container"></a>So erstellen Sie einen Container    
    
1.  Fügen Sie dem Bericht ein Rechteckberichtsobjekt hinzu.    
    
2.  Ziehen Sie andere Berichtselemente in das Rechteck.    
    
    > [!NOTE]    
    >  Ein Rechteck ist lediglich ein Container für Elemente, die Sie im Rechteck erstellen oder in das Rechteck ziehen. Wenn Sie ein Rechteck um ein Element zeichnen, das bereits auf der Entwurfsoberfläche vorhanden ist, fungiert das Rechteck nicht als Container.    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>So ändern Sie Rechteckeigenschaften, z. B. Farbe, Format oder Gewichtung    
    
1.  Wählen Sie das Rechteck aus, und klicken Sie auf die Optionen für Linienfarbe, Format oder Gewichtung im Abschnitt **Rahmen** der Registerkarte Home.    
    
2.  Klicken Sie auf den Pfeil neben der Schaltfläche **Rahmen** , um zu bestimmen, welche Seiten des Rechtecks geändert werden sollen.    
    
    > [!NOTE]    
    >  Wenn Sie die Linienart auf **Doppelt** festlegen und die Linienstärke 1 1/2 pt oder geringer ist, wird die Linie möglicherweise nicht doppelt angezeigt, wenn Sie den Bericht im Berichts-Generator, Berichts-Designer oder im [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Webportal ausführen. Sie wird doppelt angezeigt, wenn Sie den Bericht in andere Formate wie Microsoft Word oder Acrobat PDF exportieren.    
    
## <a name="see-also"></a>Siehe auch    
 [Rechtecke und Linien &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [Renderingverhalten (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
