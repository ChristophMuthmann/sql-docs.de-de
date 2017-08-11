---
title: "Einfügen oder löschen eine Zeile (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3824222b71269de1bf500926b44ca55dd438a010
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Einfügen oder Löschen einer Zeile (Berichts-Generator und SSRS)
Sie können in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht Zeilen einem Tablix-Datenbereich hinzufügen bzw. daraus entfernen. Der Tablix-Datenbereich kann eine Tabelle, eine Matrix oder eine Liste sein. Die folgenden Vorgehensweisen gelten nicht für Diagramm- und Messgerätdatenbereiche.  
  
 In Tablix-Datenbereichen können Zeilen hinzugefügt werden, die mit einer Gruppe verknüpft sind (innerhalb einer Gruppe) oder die nicht mit einer Gruppe verknüpft sind (außerhalb einer Gruppe). Eine Zeile in einer Gruppe wiederholt sich einmal pro eindeutigem Gruppenwert. So wiederholt sich zum Beispiel eine Zeile in einer Gruppe, die auf dem Wert in einer Datenspalte mit Farbnamen basiert, einmal pro eindeutigem Farbnamen. Bei geschachtelten Gruppen kann sich die Zeile außerhalb der untergeordneten Gruppe, aber innerhalb der übergeordneten Gruppe befinden. In diesem Fall wiederholt sich die Zeile einmal für jeden eindeutigen Wert in der übergeordneten Gruppe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>So wählen Sie einen Datenbereich aus und zeigen die Zeilen- und Spaltenziehpunkte an  
  
-   Klicken Sie in der Entwurfsansicht auf die obere linke Ecke des Tablix-Datenbereichs, sodass die Spalten- und Zeilenziehpunkte über und neben dem Datenbereich angezeigt werden.  
  
     Weitere Informationen zu Datenbereichen finden Sie unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>So fügen Sie eine Zeile in einen ausgewählten Datenbereich ein  
  
-   Klicken Sie mit der rechten Maustaste an der Stelle, an der Sie eine Zeile einfügen möchten, auf einen Zeilenziehpunkt, klicken Sie auf **Zeile einfügen**und dann auf **Oberhalb** bzw. **Unterhalb**.  
  
     \- oder –  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zelle in dem Datenbereich, in dem Sie eine Zeile einfügen möchten, klicken Sie auf **Zeile einfügen**und dann auf **Oberhalb** bzw. **Unterhalb**.  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>So löschen Sie eine Zeile aus einem ausgewählten Datenbereich  
  
-   Wählen Sie die Zeile oder Zeilen aus, die Sie löschen möchten, klicken Sie mit der rechten Maustaste auf den Ziehpunkt einer der ausgewählten Zeilen, und klicken Sie dann auf **Zeilen löschen**.  
  
     \- oder –  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zelle in dem Datenbereich, in dem Sie eine Zeile löschen möchten, und klicken Sie dann auf **Zeilen löschen**.  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>So fügen Sie eine Zeile in eine Gruppe in einem ausgewählten Datenbereich ein  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zeilengruppenzelle im Zeilengruppenbereich eines Tablix-Datenbereichs, in dem Sie eine Zeile einfügen möchten, klicken Sie auf **Zeile einfügen**und dann auf **Oberhalb - Außerhalb von Gruppe**, **Oberhalb - Innerhalb von Gruppe**, **Unterhalb - Innerhalb von Gruppe**oder **Unterhalb - Außerhalb von Gruppe**.  
  
     Die Zeile wird entweder innerhalb oder außerhalb der Gruppe eingefügt, die durch die Zeilengruppenzelle, auf die Sie geklickt haben, repräsentiert wird.  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>So löschen Sie eine Zeile aus einer Gruppe in einem ausgewählten Datenbereich  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zeilengruppenzelle im Zeilengruppenbereich eines Tablix-Datenbereichs, aus dem Sie eine Zeile löschen möchten, und klicken Sie dann auf **Zeilen löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Grundlegendes zu Gruppen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tabellen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
