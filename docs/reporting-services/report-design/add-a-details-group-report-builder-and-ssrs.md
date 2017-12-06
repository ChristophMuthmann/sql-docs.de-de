---
title: "Hinzufügen einer Detailgruppe (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: fdaf1a752a6235ac31d0043920f7ac264d838810
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>Hinzufügen einer Detailgruppe (Berichts-Generator und SSRS)
In einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht werden die Detaildaten aus einem Berichtsdataset als Gruppe ohne Gruppierungsausdruck angegeben. Fügen Sie einem Tablix-Datenbereich eine Detailgruppe hinzu, wenn die Detaildaten für eine Matrix angezeigt, wenn aus einer Tabelle bzw. Liste gelöschte Detaildaten wieder hinzugefügt oder wenn zusätzliche Detailgruppen hinzugefügt werden sollen. Weitere Informationen zu Gruppen finden Sie unter [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>So fügen Sie einem Tablix-Datenbereich eine Detailgruppe hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf eine beliebige Stelle im Tablix-Datenbereich, um diesen auszuwählen. Im Bereich Gruppierung werden die Zeilengruppen und Spaltengruppen für den derzeit ausgewählten Tablix-Datenbereich angezeigt.  
  
2.  Klicken Sie im Bereich „Gruppierung“ mit der rechten Maustaste auf eine Gruppe, die die innerste untergeordnete Gruppe darstellt. Klicken Sie auf **Gruppe hinzufügen**und dann auf **Untergeordnete Gruppe**. Das Dialogfeld **Tablix-Gruppe** wird geöffnet.  
  
3.  Geben Sie in **Gruppierungsausdruck**keinen Ausdruck ein. Eine Detailgruppe verfügt über keinen Ausdruck.  
  
4.  Wählen Sie **Detaildaten anzeigen**aus.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Im Bereich Gruppierung wird eine neue Detailgruppe als untergeordnete Gruppe hinzugefügt, und vom Zeilenhandle für die in Schritt 1 ausgewählte Gruppe wird das Symbol für die Detailgruppe angezeigt. Weitere Informationen zu Handles finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) [Matrizen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md) .  
 [Listen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
