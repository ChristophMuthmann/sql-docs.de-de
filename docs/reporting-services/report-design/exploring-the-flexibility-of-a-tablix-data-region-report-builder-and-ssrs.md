---
title: "Untersuchen der Flexibilität eines Tablix-Datenbereichs (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b795c6ab6d2106c781dbcd75cbf913dda85298d5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>Untersuchen der Flexibilität eines Tablix-Datenbereichs (Berichts-Generator und SSRS)
Wenn Sie in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht einen Tabellen-, Matrix- oder Listendatenbereich über die Registerkarte „Einfügen“ des Menübands hinzufügen, starten Sie mit einer Ausgangsvorlage für einen Tablix-Datenbereich. Diese Vorlage stellt jedoch keine Beschränkung für Sie dar. Sie können die Datenanzeige weiterentwickeln, indem Sie Tablix-Datenbereichsfunktionen wie Gruppen, Zeilen und Spalten hinzufügen oder entfernen.  
  
 Wenn Sie eine Zeilen- oder Spaltengruppe löschen, können Sie auch die Zeilen und Spalten löschen, die für die Anzeige von Gruppenwerten verwendet werden. Außerdem können Sie manuell Zeilen und Spalten hinzufügen oder entfernen. Weitere Informationen zum Anzeigen von Detail- und Gruppendaten in Zeilen und Spalten finden Sie unter [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md).  
  
 Nachdem Sie die Struktur des Tablix-Datenbereichs geändert haben, können Sie Eigenschaften festlegen, mit denen Sie steuern können, wie der Datenbereich im Bericht gerendert wird. Sie können z. B. Spaltenheader am Anfang jeder Seite wiederholen oder einen Gruppenkopf für die Gruppe beibehalten. Weitere Informationen finden Sie unter [Steuern der Tablix-Datenbereichsanzeige auf einer Berichtsseite &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>Ändern einer Tabelle in eine Matrix  
 Standardmäßig enthält eine Tabelle Detailzeilen, in denen die Werte aus dem Berichtsdataset angezeigt werden. Typischerweise enthält eine Tabelle Zeilengruppen, in denen die Detaildaten nach Gruppen organisiert sind, und die aggregierten Werte werden auf der Grundlage der einzelnen Gruppen eingebunden. Wenn Sie die Tabelle in eine Matrix ändern möchten, fügen Sie Spaltengruppen hinzu. Normalerweise entfernen Sie die Detailgruppe, wenn der Datenbereich sowohl Zeilengruppen als auch Spaltengruppen enthält, sodass Sie nur die Zusammenfassungswerte für die Gruppen anzeigen können. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Definitionsgemäß fügen Sie beim Erstellen einer Matrix eine Tablix-Eckzelle hinzu. Sie können Zellen in diesem Bereich zusammenführen und eine Bezeichnung hinzufügen. Weitere Informationen finden Sie unter [Zusammenführen von Zellen in einem Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="changing-a-matrix-to-a-table"></a>Ändern einer Matrix in eine Tabelle  
 Standardmäßig enthält eine Matrix Zeilengruppen und Spaltengruppen, jedoch keine Detailgruppe. Wenn Sie eine Matrix in eine Tabelle umwandeln möchten, entfernen Sie Spaltengruppen und fügen Sie eine Detailgruppe für die Anzeige in der Detailzeile hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) und [Hinzufügen einer Detailgruppe (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>Ändern einer Standardliste in eine gruppierte Liste  
 Standardmäßig enthält eine Liste Detailzeilen und keine Gruppen. Wenn Sie die Liste so ändern möchten, dass sie eine Gruppenzeile enthält, benennen Sie die Detailgruppe um, und geben Sie einen Gruppierungsausdruck an. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="creating-stepped-displays"></a>Erstellen von abgestuften Anzeigen  
 Standardmäßig werden beim Hinzufügen von Gruppen zu einem Tablix-Datenbereich in Zellen im Zeilengruppen-Kopfzeilenbereich Gruppenwerte in Spalten angezeigt. Wenn Sie über geschachtelte Gruppen verfügen, wird jede Gruppe in einer separaten Spalte angezeigt. Wenn Sie eine abgestufte Anzeige erstellen möchten, entfernen Sie alle Gruppenspalten mit Ausnahme einer Gruppenspalte, und formatieren Sie die verbleibende Spalte so, dass die Gruppenhierarchie als eingerückte Textanzeige angezeigt wird. Weitere Informationen finden Sie unter [Erstellen von abgestuften Berichten (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-a-stepped-report-report-builder-and-ssrs.md).  
  
## <a name="adding-an-adjacent-details-group"></a>Hinzufügen einer angrenzenden Detailgruppe  
 Standardmäßig ist die Detailgruppe die innerste untergeordnete Gruppe in einer Gruppenhierarchie. Unter der Detailgruppe können keine Gruppen geschachtelt werden. Sie können weitere, angrenzende Detailgruppen erstellen, um beispielsweise die besten 5 Produkte und die schlechtesten 5 Produkte in Bezug auf den Umsatz anzuzeigen. Da Sie den einzelnen Gruppen Filter- und Sortierungsausdrücke hinzufügen können, können Sie in einem Tablix-Datenbereich zwei Ansichten von Detaildaten eines Datasets anzeigen. Weitere Informationen finden Sie unter [Grundlegendes zu Gruppen (Berichts-Generator und SSRS)](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md), [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) und [Hinzufügen eines Filters zu einem Dataset (Berichts-Generator und SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tabellen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
  
  
