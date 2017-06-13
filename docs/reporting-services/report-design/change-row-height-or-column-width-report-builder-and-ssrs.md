---
title: "Ändern der Zeilenhöhe oder der Spaltenbreite (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aef6ef0fe1f32f015abe3b48177f6e4d3e45648d
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Ändern der Zeilenhöhe oder der Spaltenbreite (Berichts-Generator und SSRS)
  Wenn Sie eine Zeilenhöhe festlegen, legen Sie damit die maximale Höhe der Zeile im gerenderten Bericht fest. Textfelder in einer Zeile passen sich jedoch zur Laufzeit automatisch vertikal an die darin enthaltenen Daten an. Dies kann dazu führen, dass eine Zeile über die festgelegte Höhe hinausgeht. Wenn Sie eine feste Zeilenhöhe definieren möchten, müssen Sie die Textfeldeigenschaften so ändern, dass sich die Zeile nicht automatisch ausdehnt.  
  
 Wenn Sie eine Spaltenbreite festlegen, legen Sie damit die maximale Breite der Spalte im gerenderten Bericht fest. Spalten passen sich nicht automatisch horizontal an den darin enthaltenen Text an.  
  
 Falls eine Zelle in einer Zeile oder Spalte ein Rechteck oder einen Datenbereich enthält, werden die Mindesthöhe und -breite der Zelle durch die Höhe und Breite des darin enthaltenen Elements bestimmt. Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>So ändern Sie die Zeilenhöhe durch das Bewegen von Zeilenhandles  
  
1.  Klicken Sie in der Entwurfsansicht auf eine Stelle im Tablix-Datenbereich, um diesen auszuwählen. Graue Zeilenziehpunkte werden am Außenrand des Tablix-Datenbereichs angezeigt.  
  
2.  Zeigen Sie mit der Maus auf die Ziehpunktkante der Zeile, die Sie erweitern möchten. Es wird ein Pfeil mit zwei Spitzen angezeigt.  
  
3.  Klicken Sie mit der Maus, und ziehen Sie die Kante der Zeile nach oben oder unten, um die Zeilenhöhe zu ändern.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>So ändern Sie die Zeilenhöhe durch das Festlegen von Zelleneigenschaften  
  
1.  Klicken Sie in der Ansicht Entwurf auf eine Zelle in der Tabellenzeile.  
  
     ![Ausgewählte Zelle in einer Tabelle](../../reporting-services/report-design/media/table-selectcell.png "ausgewählte Zelle in einer Tabelle")  
  
2.  Ändern Sie im angezeigten Bereich **Eigenschaften** die Eigenschaft **Höhe** , und klicken Sie anschließend auf eine beliebige Stelle außerhalb des Bereichs **Eigenschaften** .  
  
     ![Bereich "Eigenschaften" für ausgewählte Tabellenzelle](../../reporting-services/report-design/media/cell-propertiespane.png "Bereich "Eigenschaften" für ausgewählte Tabellenzelle")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>So deaktivieren Sie die automatische Ausdehnung einer Zeile  
  
1.  Klicken Sie in der Entwurfsansicht auf eine Stelle im Tablix-Datenbereich, um diesen auszuwählen. Graue Zeilenziehpunkte werden am Außenrand des Tablix-Datenbereichs angezeigt.  
  
2.  Klicken Sie auf den Zeilenziehpunkt, um die Zeile auszuwählen.  
  
3.  Legen Sie im Eigenschaftenbereich CanGrow auf **FALSE**fest.  
  
    > [!NOTE]  
    >  Falls der Eigenschaftenbereich noch nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Eigenschaften**.  
  
### <a name="to-change-column-width"></a>So ändern Sie die Spaltenbreite  
  
1.  Klicken Sie in der Entwurfsansicht auf eine Stelle im Tablix-Datenbereich, um diesen auszuwählen. Graue Spaltenziehpunkte werden am Außenrand des Tablix-Datenbereichs angezeigt.  
  
2.  Zeigen Sie mit der Maus auf die Ziehpunktkante der Spalte, die Sie erweitern möchten. Es wird ein Pfeil mit zwei Spitzen angezeigt.  
  
3.  Klicken Sie mit der Maus, und ziehen Sie die Kante der Spalte nach links oder rechts, um die Spaltenbreite zu ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Tablix-Datenbereich (Berichts-Generator und SSRS)](https://msdn.microsoft.com/library/dd220587.aspx)   
 [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](https://msdn.microsoft.com/library/dd220511.aspx)   
 [Tabellen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen (Berichts-Generator und SSRS)](https://msdn.microsoft.com/library/dd207149.aspx)   
 [Listen (Berichts-Generator und SSRS)](https://msdn.microsoft.com/library/dd239330.aspx)   
 [Tabellen, Matrizen und Listen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
