---
title: Rechtecke und Linien (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bc6c8bc8ddf4e23afe15c533a49a30c96702294c
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Rechtecke und Linien (Berichts-Generator und SSRS)
  Mit Rechtecken und Linien können visuelle Effekte in einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht erzeugt werden. Sie können Anzeigeeigenschaften für diese Berichtselemente im Abschnitt „Rahmen“ auf der Registerkarte „Home“ festlegen. Im Bereich „Eigenschaften“ können weitere Eigenschaften festgelegt werden. Sie können einem Rechteck Funktionen wie eine Hintergrundfarbe oder ein Bild, eine QuickInfo oder ein Lesezeichen hinzufügen.  
  
##  <a name="RectanglesLinesReportParts"></a> Rechtecke und Linien als Berichtsteile  
 Sie können Rechtecke mit den darin enthaltenen Elementen getrennt von den Berichten als Berichtsteile veröffentlichen. Berichtsteile sind eigenständige Berichtselemente, die auf dem Berichtsserver gespeichert werden und in andere Berichte eingeschlossen werden können.  
  
 Die Berichtselemente innerhalb eines Rechtecks können nicht als Berichtsteile veröffentlicht werden. Wenn Benutzer das Rechteck einem Bericht hinzufügen, erhalten sie das Rechteck und die darin enthaltenen Elemente.  Erfahren Sie mehr über [Berichtsteile](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="RectangleAsContainer"></a> Verwenden eines Rechtecks als Container  
 Ein Rechteck kann als Container für andere Elemente verwendet werden. Wenn Sie das Rechteck verschieben, werden gleichzeitig die darin enthaltenen Elemente verschoben. Ein Element innerhalb des Rechtecks zeigt den Namen des Rechtecks in seiner **Parent** -Eigenschaft an. Weitere Informationen zum Verwenden eines Rechtecks als Container finden Sie unter [Hinzufügen eines Rechtecks oder Containers &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md) und [anzeigen derselben Daten in einer Matrix und einem Diagramm &#40; Berichts-Generator &#41; ](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Ein Rechteck ist lediglich ein Container für Elemente, die Sie im Rechteck erstellen oder in das Rechteck ziehen. Wenn Sie ein Rechteck um ein Element zeichnen, das bereits auf der Entwurfsoberfläche vorhanden ist, fungiert das Rechteck nicht als Container. Das Rechteck wird nicht in der Parent-Eigenschaft des Elements aufgelistet.  
  
 Wenn Rechtecke als Container für Berichtselemente verwendet werden, sollten Sie berücksichtigen, wie die Elemente als Ganzes beim Rendern des Berichts beeinflusst werden. Berichtselemente, die wiederholte Zeilen von Daten enthalten (z. B. Tabellen), werden erweitert, um die Daten aufzunehmen, die von einer Abfrage zurückgegeben werden, was die Positionierung anderer Elemente im Rechteck beeinflusst. Elemente werden von einer Tabelle nach unten verschoben, wenn sich diese Elemente unterhalb des Datenbereichs befinden. Um ein Element an einem bestimmten Platz zu verankern, können Sie das Berichtselement innerhalb eines Rechtecks platzieren, dessen oberer Rand oberhalb des unteren Randes der Tabelle liegt. Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
##  <a name="ReportBorder"></a> Hinzufügen von Berichtsrahmen  
 Sie können einem Bericht ohne Hinzufügen von Linien oder Rechtecken einen Rahmen hinzufügen, indem Sie Kopfzeilen, Fußzeilen und dem Berichtshauptteil selbst Rahmen hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Rahmens zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 [Hinzufügen eines Rahmens zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Hinzufügen eines Rechtecks oder Containers &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Hinzufügen und Ändern einer Linie &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen eines Rechtecks oder Containers &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
