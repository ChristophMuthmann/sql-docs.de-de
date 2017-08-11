---
title: "Zusammenführen von Zellen in einem Datenbereich (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c643b94c86109a99e1448093b4b9744924fcd7f7
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Zusammenführen von Zellen in einem Datenbereich (Berichts-Generator und SSRS)
In einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht können Sie Zellen in einem Datenbereich zusammenführen, um Zellen zu kombinieren, die Darstellung des Datenbereichs zu verbessern oder umfassende Bezeichnungen für Spalten- und Zeilengruppen zur Verfügung zu stellen.  
  
Zellen können nur innerhalb der folgenden Bereiche eines Datenbereichs zusammengeführt werden: Ecke, Spaltenheader, Gruppendefinition (oder Zeilenheader) und Textkörper. Sie können keine Zellen zusammenführen, die über Bereichsgrenzen hinausgehen. Sie können beispielsweise eine Zelle im Eckbereich des Datenbereichs nicht mit einer Zelle im Zeilengruppenbereich zusammenführen. Erfahren Sie mehr unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-merge-cells-in-a-data-region"></a>So führen Sie Zellen in einem Datenbereich zusammen  
  
1.  Klicken Sie im Datenbereich auf der Berichtsentwurfsoberfläche auf die erste Zelle, die zusammengeführt werden soll. Drücken Sie die linke Maustaste, und ziehen Sie den Mauszeiger vertikal oder horizontal, um angrenzende Zellen auszuwählen. Die ausgewählten Zellen werden markiert.  
  
2.  Klicken Sie mit der rechten Maustaste auf die ausgewählten Zellen, und wählen Sie **Zellen zusammenführen**aus. Die ausgewählten Zellen werden zu einer einzigen Zelle kombiniert.  
  
3.  Wiederholen Sie die Schritte 1 und 2, um andere angrenzende Zellen in einem Datenbereich zusammenzuführen.  
  
## <a name="see-also"></a>Siehe auch  
[Tablix-Datenbereich](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 [Tabellen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Erstellen einer Matrix](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Create Invoices and Forms with Lists (Erstellen von Rechnungen und Formularen mit Listen)](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
[Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
