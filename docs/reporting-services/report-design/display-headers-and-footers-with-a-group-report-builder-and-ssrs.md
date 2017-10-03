---
title: "Anzeigen von Kopf- und Fußzeilen einer Gruppe (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 36fd7c4ac62280fb980bb24c89306a006605b665
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>Anzeigen von Kopf- und Fußzeilen einer Gruppe (Berichts-Generator und SSRS)
  Sie können bestimmen, ob eine statische Zeile wie eine Gruppenkopfzeile oder -fußzeile mit dynamischen Zeilen gerendert werden soll, die mit einer Gruppe in einem Tablix-Datenbereich verknüpft sind.  
  
 Wenn Sie alle Spalten- oder Zeilenüberschriften auf mehreren Seiten wiederholen möchten, können Sie Eigenschaften für den Tablix-Datenbereich festlegen. Weitere Informationen finden Sie unter [Anzeigen von Zeilen- und Spaltenüberschriften auf mehreren Seiten (Berichts-Generator und SSRS)](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Sie müssen Eigenschaften für das Tablix-Element festlegen, um das Renderingverhalten für dynamische, mit geschachtelten Gruppen verknüpfte Zeilen und Spalten oder für statische, mit Beschriftungen oder Zwischensummen verknüpfte Zeilen und Spalten zu bestimmen. Ein Tablix-Element stellt eine statische oder dynamische Zeile oder Spalte dar. Ein statisches Element wird einmal wiederholt. Beispiel: Eine Zeile mit einer Gesamtsumme ist eine statische Zeile. Ein dynamisches Element wird für jede Gruppeninstanz einmal wiederholt. Eine Zeile, die mit einer Gruppe mit dem Gruppierungsausdruck [Region] verknüpft ist, wird einmal für jeden eindeutigen Wert für eine Region wiederholt. Weitere Informationen zu Tablix-Elemente, finden Sie unter [Tablix-Datenbereichszelle, Zeilen und Spalten &#40; Berichts-Generator &#41; und SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Sie können ein Tablix-Element im Gruppierungsbereich auswählen und die Eigenschaften **KeepWithGroup**, **KeepTogether**und **RepeatOnNewPage** im Eigenschaftenbereich festlegen. Verwenden Sie **KeepWithGroup** , um Gruppenköpfe und Fußzeilen auf der gleichen Seite wie die Gruppe anzuzeigen. Verwenden Sie **KeepTogether** , um statische Elemente mit den Zeilen oder Spalten einer Gruppe anzuzeigen. Verwenden Sie **RepeatOnNewPage** , um den Gruppenkopf oder die Fußzeile auf jeder Seite zu wiederholen, auf der mindestens eine vollständige Instanz des mit dem **KeepWithGroup** -Wert festgelegten Zeilengruppenelements angezeigt wird. **RepeatOnNewPage** wird für Spaltengruppenelemente nicht unterstützt.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether**, und **RepeatOnNewPage** sind Eigenschaften, die Sie festlegen können, indem Sie mit der **Erweiterter Modus** der Gruppierung im Bereich. Weitere Informationen finden Sie unter [Bereichs "Gruppierung" &#40; Berichts-Generator &#41; ](../../reporting-services/report-design/grouping-pane-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>So behalten Sie eine statische Zeile mit einer Gruppe von dynamischen Zeilen bei, die mit einer Zeilengruppe verknüpft sind  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf eine beliebige Stelle im Tablix-Datenbereich, um diesen auszuwählen. Im Gruppierungsbereich werden die Zeilen- und Spaltengruppen für den Datenbereich angezeigt.  
  
2.  Klicken Sie auf der rechten Seite des Gruppierungsbereichs auf den Pfeil nach unten und anschließend auf **Erweiterter Modus**. Im Bereich Zeilengruppen werden die hierarchischen statischen und dynamischen Elemente für die Zeilengruppenhierarchie angezeigt.  
  
3.  Klicken Sie auf das statische Element, das der Zeilenkopf- oder -fußzeile entspricht, die Sie für die Gruppenzeilen beibehalten wollen. Im Eigenschaftenbereich werden die Eigenschaften für das **Tablix-Element** angezeigt.  
  
4.  Klicken Sie im Eigenschaftenbereich auf **KeepWithGroup**, und wählen Sie in der Dropdownliste einen der folgenden Werte aus:  
  
    -   **Keine** Wählen Sie diese Option aus, wenn Sie keine Einstellung bezüglich der Beibehaltung dieses Elements für die Elemente der ausgewählten Zeilengruppe festlegen möchten.  
  
    -   **Vor** Wählen Sie diese Option aus, um das Element für die Elemente der vorherigen Gruppe beizubehalten. Sie könnten diese Option für Gruppenfußzeilen verwenden.  
  
    -   **Nach** Wählen Sie diese Option aus, um das Element für die Elemente der folgenden Gruppe beizubehalten. Sie können diese Option für Gruppenkopfzeilen verwenden.  
  
5.  (Optional) Zeigen Sie eine Vorschau des Berichts an. Wenn möglich, wird dieses Element vom Berichtsrenderer mit den angegebenen Zeilengruppenelementen beibehalten.  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>So behalten Sie eine statische Spalte mit einer Gruppe von dynamischen Spalten bei, die mit einer Spaltengruppe verknüpft sind  
  
1.  Klicken Sie auf der Entwurfsoberfläche auf eine beliebige Stelle im Tablix-Datenbereich, um diesen auszuwählen. Im Gruppierungsbereich werden die Zeilen- und Spaltengruppen für den Datenbereich angezeigt.  
  
2.  Klicken Sie auf der rechten Seite des Gruppierungsbereichs auf den Pfeil nach unten und anschließend auf **Erweiterter Modus**. Im Bereich Spaltengruppen werden die hierarchischen statischen und dynamischen Elemente für die Spaltengruppenhierarchie angezeigt.  
  
3.  Klicken Sie auf das statische Element, das der Spaltenkopf- oder -fußzeile entspricht, die Sie für die Gruppenspalten beibehalten wollen. Im Eigenschaftenbereich werden die Eigenschaften für das **Tablix-Element** angezeigt.  
  
4.  Klicken Sie im Eigenschaftenbereich auf **KeepWithGroup**, und wählen Sie in der Dropdownliste einen der folgenden Werte aus:  
  
    -   **Keine** Wählen Sie diese Option aus, wenn Sie keine Einstellung bezüglich der Beibehaltung dieses Elements für die Elemente der ausgewählten Spaltengruppe festlegen möchten.  
  
    -   **Vor** Wählen Sie diese Option aus, um das Element für die Elemente der vorherigen Gruppe beizubehalten. Sie können diese Option für Spaltenbezeichnungen verwenden, die vor den angegebenen Spaltengruppenelementen angezeigt werden.  
  
    -   **Nach** Wählen Sie diese Option aus, um das Element für die Elemente der folgenden Gruppe beizubehalten. Sie können diese Option für Spaltengesamtwerte verwenden, die nach den angegebenen Spaltengruppenelementen angezeigt werden.  
  
5.  (Optional) Zeigen Sie eine Vorschau des Berichts an. Wo es möglich ist, wird dieses Element vom Berichtsrenderer mit den angegebenen Spaltengruppenelementen beibehalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Tablix-Datenbereichszelle, Zeilen und Spalten (Berichts-Generator) und SSRS](tablix-data-region-report-builder-and-ssrs.md)   
 
  
  
