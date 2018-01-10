---
title: "Anzeigen von Zeilen- und Spaltenüberschriften auf mehreren Seiten (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: f9c2cc9c26644cb4671f5a601ad4c755ff2a1019
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>Anzeigen von Zeilen- und Spaltenüberschriften auf mehreren Seiten (Berichts-Generator und SSRS)
  Sie können festlegen, ob bei einem Tablix-Datenbereich (Tabelle, Matrix oder Liste), der mehrere Seiten umfasst, Zeilen- und Spaltenüberschriften auf jeder Seite eines paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichts wiederholt werden sollen.
  
 Wie Zeilen und Spalten behandelt werden, hängt davon ab, ob der Tablix-Datenbereich Gruppenkopfzeilen enthält. Wenn Sie auf einen Tablix-Datenbereich klicken, der Gruppenkopfzeilen enthält, wird eine gepunktete Linie in den Tablix-Bereichen angezeigt, wie in der folgenden Abbildung dargestellt:  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 Zeilen- und Spaltengruppenkopfzeilen werden automatisch erstellt, wenn Sie Gruppen mit dem Tabellen- oder Matrix-Assistenten bzw. dem Diagramm-Assistenten hinzufügen, indem Felder zu dem Gruppierungsbereich hinzugefügt oder Kontextmenüs verwendet werden. Wenn der Tablix-Datenbereich nur einen Tablix-Textbereich und keine Gruppenkopfzeilen enthält, sind die Zeilen und Spalten Tablix-Elemente.  
  
 Bei statischen Elementen können Sie die obersten angrenzenden Zeilen oder die seitlichen angrenzenden Spalten auf mehreren Seiten anzeigen.  
  
## <a name="to-display-row-headers-on-multiple-pages"></a>So zeigen Sie Zeilenüberschriften auf mehreren Seiten an  
  
1.  Klicken Sie im Tablix-Datenbereich mit der rechten Maustaste auf den Zeilen-, Spalten- oder Eckziehpunkt, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
2.  Wählen Sie unter **Zeilenüberschriften**die Option **Kopfzeile auf jeder Seite wiederholen**aus.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-column-headers-on-multiple-pages"></a>So zeigen Sie Spaltenüberschriften auf mehreren Seiten an  
  
1.  Klicken Sie im Tablix-Datenbereich mit der rechten Maustaste auf den Zeilen-, Spalten- oder Eckziehpunkt, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
2.  Wählen Sie unter **Spaltenkopfzeilen**die Option **Spaltenüberschrift auf jeder Seite wiederholen**aus.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-display-a-static-row-or-column-on-multiple-pages"></a>So zeigen Sie eine statische Zeile oder Spalte auf mehreren Seiten an  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf den Zeilen- oder Spaltenziehpunkt des Tablix-Datenbereichs, um diesen auszuwählen. Im Gruppierungsbereich werden die Zeilen- und Spaltengruppen angezeigt.  
  
2.  Klicken Sie auf der rechten Seite des Gruppierungsbereichs auf den Pfeil nach unten und anschließend auf **Erweiterter Modus**. In den Bereichen Zeilengruppen und Spaltengruppen werden die hierarchischen und statischen Elemente für die Zeilengruppenhierarchie bzw. Spaltengruppenhierarchie angezeigt.  
  
3.  Klicken Sie auf das statische Element, das dem statischen Element (Zeile oder Spalte) entspricht, das beim Bildlauf sichtbar bleiben soll. Im Eigenschaftenbereich werden die Eigenschaften für das **Tablix-Element** angezeigt.  
  
     Wenn der Eigenschaftenbereich nicht angezeigt wird, klicken Sie am oberen Rand des Fensters Berichts-Generator auf die Registerkarte **Ansicht** und dann auf **Eigenschaften**.  
  
4.  Legen Sie im Eigenschaftenbereich **RepeatOnNewPage** auf True fest.  
  
5.  Legen Sie **KeepWithGroup** auf After fest.  
  
6.  Wiederholen Sie diesen Schritt für alle angrenzenden Elemente, die wiederholt werden sollen.  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
 Während Sie jede Seite des Berichts anzeigen, über die sich der Tablix-Datenbereich erstreckt, werden die statischen Tablix-Elemente auf jeder Seite wiederholt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Suchen, Anzeigen und Verwalten von Berichten (Berichts-Generator und SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Steuern von Seitenumbrüchen, Überschriften, Spalten und Zeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Anzeigen von Kopf- und Fußzeilen einer Gruppe (Berichts-Generator und SSRS)](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [Sichtbarhalten von Kopfzeilen beim Scrollen durch einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
