---
title: "Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6462484e8665b1b124275d51e0a85790f2c27446
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>Hinzufügen oder Löschen einer Gruppe in einem Datenbereich (Berichts-Generator und SSRS)
Fügen Sie in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht einem Datenbereich eine Gruppe hinzu, wenn Sie Daten nach einem spezifischen Wert oder einer Reihe von Ausdrücken zu Anzeige- und Berechnungszwecken organisieren möchten. Eine Gruppe verfügt über einen Namen und einen Ausdruck, der angibt, welche Daten aus einem Dataset zur Gruppe gehören. Weitere Informationen zu Gruppen finden Sie unter [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
 Klicken Sie in einem Tablix-Datenbereich in die Tabelle, Matrix oder Liste, um den Gruppierungsbereich anzuzeigen. Ziehen Sie Datasetfelder in den Bereich Zeilengruppe und Spaltengruppe, um übergeordnete oder untergeordnete Gruppen zu erstellen. Klicken Sie mit der rechten Maustaste auf eine vorhandene Gruppe, um eine angrenzende Gruppe hinzuzufügen. Definitionsgemäß ist die Detailgruppe die innerste Gruppe, die nur als untergeordnete Gruppe hinzugefügt werden kann. Klicken Sie mit der rechten Maustaste auf eine vorhandene Gruppe, um diese zu löschen. Zeilen und die Spalten, in denen Gruppenwerte angezeigt werden sollen, werden automatisch hinzugefügt. Weitere Informationen finden Sie unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
 Klicken Sie in einem Diagrammdatenbereich in das Diagramm, um die Ablagezonen anzuzeigen. Erstellen Sie Gruppen, indem Sie Datasetfelder in die Ablagezonen für Kategorien und Reihen ziehen. Wenn Sie geschachtelte Gruppen hinzufügen möchten, fügen Sie der Ablagezone mehrere Felder hinzu.  
  
 In einem Messgerät sind standardmäßig keine Gruppen definiert. Das Standardverhalten des Messgeräts besteht darin, dass alle Werte im angegebenen Feld zu einem Wert aggregiert werden, der auf dem Messgerät angezeigt wird. Weitere Informationen finden Sie unter [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>So fügen Sie einem Tablix-Datenbereich eine übergeordnete oder untergeordnete Zeilen- oder Spaltengruppe hinzu  
  
1.  Ziehen Sie ein Feld aus dem **Berichtsdatenbereich** in den Bereich **Zeilengruppen** oder **Spaltengruppen** .  
  
    > [!NOTE]  
    >  Wenn der Gruppierungsbereich nicht angezeigt wird, klicken Sie auf der Registerkarte „Ansicht“ auf **Gruppierung**.  
  
2.  Legen Sie das Feld mithilfe des Führungsbalkens über oder unter der Gruppenhierarchie ab, um die Gruppe einer vorhandenen Gruppe als übergeordnete oder untergeordnete Gruppe hinzuzufügen.  
  
     Die Gruppe wird mit einem Standardnamen, einem Gruppierungsausdruck und einem Sortierungsausdruck hinzugefügt, die auf dem Feldnamen basieren.  
  
## <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>So fügen Sie einem Tablix-Datenbereich eine angrenzende Zeilen- oder Spaltengruppe hinzu  
  
1.  Klicken Sie im Gruppierungsbereich mit der rechten Maustaste auf eine Gruppe, die einen Peer der hinzuzufügenden Gruppe darstellt. Klicken Sie auf **Gruppe hinzufügen**, und klicken Sie anschließend auf **Angrenzend vor** oder **Angrenzend nach** , um die Position anzugeben, an der die Gruppe hinzugefügt werden soll. Das Dialogfeld **Tablix-Gruppe** wird geöffnet.  
  
2.  Geben Sie in **Name**einen Namen für die Gruppe ein.  
  
3.  Geben Sie unter **Gruppierungsausdruck**einen Ausdruck ein, oder klicken Sie auf die Ausdrucksschaltfläche (**fx**), um einen Ausdruck zu erstellen.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Dem Gruppierungsbereich wird eine neue Gruppe hinzugefügt, und dem Tablix-Datenbereich auf der Entwurfsoberfläche wird eine Zeile oder Spalte hinzugefügt, in der Gruppenwerte angezeigt werden.  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>So fügen Sie einem Tablix-Datenbereich eine Detailgruppe hinzu  
  
1.  Klicken Sie im Gruppierungsbereich mit der rechten Maustaste auf eine Gruppe, die der innersten untergeordneten Gruppe entspricht, jedoch nicht auf die Gruppe **Details** . Klicken Sie auf **Gruppe hinzufügen**und dann auf **Untergeordnete Gruppe**. Das Dialogfeld **Tablix-Gruppe** wird geöffnet.  
  
2.  Geben Sie in **Gruppierungsausdruck**keinen Ausdruck ein. Eine Detailgruppe verfügt über keinen Ausdruck.  
  
3.  Wählen Sie **Detaildaten anzeigen**aus.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Im Bereich Gruppierung wird eine neue Detailgruppe als untergeordnete Gruppe hinzugefügt, und vom Zeilenhandle für die in Schritt 1 ausgewählte Gruppe wird das Symbol für die Detailgruppe angezeigt. Weitere Informationen zu Handles finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>So bearbeiten Sie eine Zeilen- oder Spaltengruppe in einem Tablix-Datenbereich  
  
1.  Klicken Sie auf der Berichtsentwurfsoberfläche auf eine beliebige Stelle im Tablix-Datenbereich, um diesen auszuwählen. Im Gruppierungsbereich werden die Zeilen- und Spaltengruppen angezeigt.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Gruppe, und klicken Sie anschließend auf **Gruppeneigenschaften**.  
  
3.  Geben Sie unter **Name**den Namen der Gruppe ein.  
  
4.  Geben Sie unter **Gruppierungsausdrücke**einen einfachen Ausdruck ein, bzw. wählen Sie diesen aus, oder klicken Sie auf die Ausdrucksschaltfläche (**fx**), um einen Gruppierungsausdruck zu erstellen.  
  
5.  Klicken Sie auf **Hinzufügen** , um zusätzliche Ausdrücke zu erstellen. Alle angegebenen Ausdrücke werden mit einem logischen AND kombiniert, um Daten für diese Gruppe anzugeben.  
  
6.  (Optional) Klicken Sie auf **Seitenumbrüche** , um Seitenumbruchoptionen festzulegen.  
  
7.  (Optional) Klicken Sie auf **Sortierung** , um Ausdrücke auszuwählen bzw. einzugeben, mit denen die Sortierreihenfolge für Werte in der Gruppe angegeben wird.  
  
8.  (Optional) Klicken Sie auf **Sichtbarkeit** , um die Sichtbarkeitsoptionen für das Element auszuwählen.  
  
9. (Optional) Klicken Sie auf **Filter** , um Filter für diese Gruppe festzulegen.  
  
10. (Optional) Klicken Sie auf **Variablen** , um Variablen zu definieren, deren Bereich auf diese Gruppe festgelegt ist und auf die aus untergeordneten Gruppen zugegriffen werden kann.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-group-from-a-tablix-data-region"></a>So löschen Sie eine Gruppe aus einem Tablix-Datenbereich  
  
1.  Klicken Sie im Bereich „Gruppierung“ mit der rechten Maustaste auf die Gruppe, und klicken Sie anschließend auf **Gruppe löschen**.  
  
2.  Wählen Sie im Dialogfeld **Gruppe löschen** eine der folgenden Optionen aus:  
  
    -   **Gruppe und verwandte Zeilen und Spalten löschen** Wählen Sie diese Option aus, um die Gruppendefinition und alle zugehörigen Zeilen zu löschen, in denen Gruppendaten angezeigt werden. Für die Detailgruppe werden nur die Detaildatenzeilen gelöscht, wenn dieselbe Zeile sowohl zu den Zeilen- als auch zu den Gruppendaten gehört.  
  
    -   **Nur Gruppe löschen** Wählen Sie diese Option aus, wenn die Struktur des Tablix-Datenbereichs unverändert beibehalten und nur die Gruppendefinition gelöscht werden soll.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>So löschen Sie eine Detailgruppe aus einem Tablix-Datenbereich  
  
1.  Klicken Sie im Bereich Gruppierung mit der rechten Maustaste auf die Detailgruppe, und klicken Sie anschließend auf **Gruppe löschen**.  
  
2.  Wählen Sie im Dialogfeld **Gruppe löschen** eine der folgenden Optionen aus:  
  
    -   **Gruppe und verwandte Zeilen und Spalten löschen** Wählen Sie diese Option aus, um die Gruppendefinition und alle zugehörigen Zeilen zu löschen, in denen Gruppendaten angezeigt werden. Für die Detailgruppe werden nur die Detaildatenzeilen gelöscht, wenn dieselbe Zeile sowohl zu den Zeilen- als auch zu den Gruppendaten gehört.  
  
    -   **Nur Gruppe löschen** Wählen Sie diese Option aus, wenn die Struktur des Tablix-Datenbereichs unverändert beibehalten und nur die Gruppendefinition gelöscht werden soll.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die Detailgruppe wird gelöscht.  
  
    > [!NOTE]  
    >  Vergewissern Sie sich nach dem Entfernen einer Detailzeile, dass mit dem Ausdruck in den jeweiligen Zellen ggf. ein Aggregatausdruck angegeben wird. Bearbeiten Sie ggf. den Ausdruck, sodass dieser die benötigten Aggregatfunktionen angibt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Beispiele für Gruppierungsausdrücke (Berichts-Generator und SSRS)](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
