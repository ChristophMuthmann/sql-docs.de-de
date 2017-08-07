---
title: "Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
- "10121"
- sql13.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ab2138bdee0abc064ae1fabb06ef04ed3c490170
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix (Berichts-Generator und SSRS)
  Sie können interaktive Sortierschaltflächen hinzufügen, um es Benutzern zu ermöglichen, die Sortierreihenfolge von Zeilen und Spalten in Tabellen und Matrizen zu ändern. Diese Funktion wird nur in Renderingformaten unterstützt, die Benutzeraktionen unterstützen, z. B. HTML.  
  
 Wenn Sie eine interaktive Sortierschaltfläche erstellen, müssen Sie die zu sortierenden Elemente, die Sortierkriterien sowie den Bereich angeben, auf den die Sortierung angewendet werden soll. Zum Beispiel können Sie Detailzeilen nach Nachnamen von Kunden, Unterkategoriegruppenwerte in einer Kategoriegruppe nach Umsätzen oder auch kombinierte Kategorie- und Unterkategoriegruppenwerte nach Gesamtwerten sortieren.  
  
 Wenn Sie den Bericht anzeigen, werden für Spalten, die das interaktive Sortieren unterstützen, Pfeilsymbole angezeigt, mit denen die Sortierreihenfolge geändert werden kann. Beim ersten Mal, dass Sie auf eine interaktive Sortierschaltfläche klicken, werden Elemente in aufsteigender Reihenfolge sortiert. Mit jedem nachfolgenden Klicken wird zwischen aufsteigender und absteigender Reihenfolge gewechselt.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="BackToTop"></a> In diesem Artikel  
 [Sortieren von Detailzeilen für eine Tabelle ohne Gruppen](#SortingDetailRows)  
  
 [Sortieren einer übergeordneten Zeilengruppe der obersten Ebene für eine Tabelle oder eine Matrix](#SortingTopLevelParent)  
  
 [Sortieren von untergeordneten Gruppen oder Detailzeilen für eine Gruppe](#SortingChildGroups)  
  
 [Sortieren von Zeilen anhand eines komplexen Gruppierungsausdrucks](#SortingMultipleRowGroups)  
  
 [Synchronisieren der Sortierreihenfolge für mehrere Datenbereiche](#SynchronizingSortOrder)  
  
##  <a name="SortingDetailRows"></a> Sortieren von Detailzeilen für eine Tabelle ohne Gruppen  
 Fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um es Benutzern zu ermöglichen, auf den Spaltenheader zu klicken und die Detailzeilen in einer Tabelle nach den in der betreffenden Spalte angezeigten Werten zu sortieren.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>So fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um die Tabelle nach Werten zu sortieren  
  
1.  Klicken Sie in der Berichtsentwurfsansicht in einer Tabelle ohne Gruppen mit der rechten Maustaste auf das Textfeld im Spaltenheader, dem Sie eine interaktive Sortierschaltfläche hinzufügen möchten, und klicken Sie anschließend auf **Textfeldeigenschaften**.  
  
2.  Klicken Sie auf **Interaktive Sortierung**.  
  
3.  Wählen Sie **Interaktive Sortierung für dieses Textfeld aktivieren**aus.  
  
4.  Klicken Sie unter **Zu sortierende Elemente auswählen**auf **Detailzeilen**.  
  
5.  Geben Sie unter **Sortieren nach**einen Sortierungsausdruck an. Wählen Sie in der Dropdownliste das Feld aus, das der Spalte entspricht, für die Sie einen Sortierungsvorgang definieren möchten (für eine Spaltenüberschrift mit dem Namen „Title“ würden Sie beispielsweise `[Title]`auswählen). Die Angabe eines Sortierungsausdrucks ist erforderlich.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Wiederholen Sie die Schritte 1 bis 6 für jede Spalte, der Sie eine interaktive Sortierschaltfläche hinzufügen möchten.  
  
 Sie können den Sortierungsvorgang überprüfen, indem Sie mit **Ausführen** eine Vorschau des Berichts anzeigen und dann auf die interaktiven Sortierschaltflächen klicken.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="SortingTopLevelParent"></a> Sortieren einer übergeordneten Zeilengruppe der obersten Ebene für eine Tabelle oder eine Matrix  
 Fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um es Benutzern zu ermöglichen, auf den Spaltenheader zu klicken und die übergeordneten Gruppenzeilen in einer Tabelle oder Matrix nach den in der betreffenden Spalte angezeigten Werten zu sortieren. Die Reihenfolge der untergeordneten Gruppen bleibt unverändert.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>So fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um Gruppen zu sortieren  
  
1.  Klicken Sie in der Berichtsentwurfsansicht in einer Tabelle oder Matrix mit der rechten Maustaste auf das Textfeld im Spaltenheader für die Gruppe, der Sie eine interaktive Sortierschaltfläche hinzufügen möchten, und klicken Sie anschließend auf **Textfeldeigenschaften**.  
  
2.  Klicken Sie auf **Interaktive Sortierung**.  
  
3.  Wählen Sie **Interaktive Sortierung für dieses Textfeld aktivieren**aus.  
  
4.  Klicken Sie unter **Zu sortierende Elemente auswählen**auf **Gruppen**.  
  
5.  Wählen Sie in der Dropdownliste den Namen der zu sortierenden Gruppe aus. Bei auf einfachen Gruppenausdrücken basierenden Gruppen wird der Wert für **Sortieren nach** mit dem Gruppenausdruck aufgefüllt.  
  
    > [!NOTE]  
    >  Bei komplexen Gruppenausdrücken legen Sie den Ausdruck für **Sortieren nach** manuell auf denselben Wert fest, der auch für den Gruppenausdruck verwendet wird.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Sie können den Sortierungsvorgang überprüfen, indem Sie mit **Ausführen** eine Vorschau des Berichts anzeigen und dann auf die interaktiven Sortierschaltflächen klicken.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="SortingChildGroups"></a> Sortieren von untergeordneten Gruppen oder Detailzeilen für eine Gruppe  
 Fügen Sie einer Gruppenkopfzeile eine interaktive Sortierschaltfläche hinzu, um es Benutzern zu ermöglichen, die Werte einer untergeordneten Gruppe von einer übergeordneten Gruppe oder aber die Detailzeilen für die innerste untergeordnete Gruppe zu sortieren.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>So fügen Sie einem Textfeld in einem Gruppenzeilenheader eine interaktive Sortierschaltfläche hinzu, um untergeordnete Gruppen oder Detailzeilen zu sortieren  
  
1.  Klicken Sie in der Berichtsentwurfsansicht mit der rechten Maustaste auf das Textfeld in der Gruppenkopfzeile, der Sie eine interaktive Sortierschaltfläche hinzufügen möchten, und klicken Sie anschließend auf **Textfeldeigenschaften**.  
  
2.  Klicken Sie auf **Interaktive Sortierung**.  
  
3.  Wählen Sie **Interaktive Sortierung für dieses Textfeld aktivieren**aus.  
  
4.  Klicken Sie unter **Zu sortierende Elemente auswählen**auf eine der folgenden Optionen:  
  
    -   **Details** Klicken Sie auf **Details** , um die Detailzeilen zu sortieren. Wählen Sie in der Dropdownliste das Feld aus, nach dem die Sortierung erfolgen soll. Bei Verwendung dieser Option müssen Sie den Wert angeben, nach dem die Sortierung erfolgen soll.  
  
    -   **Gruppen** Klicken Sie auf **Gruppen** , um die Werte der untergeordneten Gruppen zu sortieren. Bei Verwendung dieser Option wird der Ausdruck für **Sortieren nach** automatisch aus dem Gruppierungsausdruck eingetragen.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Sie können den Sortierungsvorgang überprüfen, indem Sie mit **Ausführen** eine Vorschau des Berichts anzeigen und dann auf die interaktiven Sortierschaltflächen klicken.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="SortingMultipleRowGroups"></a> Sortieren von Zeilen anhand eines komplexen Gruppierungsausdrucks  
 Fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um es Benutzern zu ermöglichen, auf den Spaltenheader zu klicken und die kombinierten übergeordneten und untergeordneten Gruppen zu sortieren. Um diesen Effekt zu erzielen, müssen Sie den Gruppierungsausdruck in eine Zusammensetzung beider Gruppen ändern. Angenommen, in einer Matrix werden Gesamtwerte für die Lagerbestände eines Geschäfts angezeigt, wobei die Artikel nach Farbe und nach Größe gruppiert sind. Wenn Sie die Zeilen nach Kombination von Farbe und Größe sortieren möchten und keine getrennten Gruppen für Farbe und Größe verwendet werden sollen, können Sie eine Gruppe definieren, die auf der Kombination von Farbe und Größe beruht. Weitere Informationen zum Definieren von Gruppenausdrücken finden Sie unter [Beispiele für Gruppierungsausdrücke (Berichts-Generator und SSRS)](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 In der folgenden Prozedur bezeichnen die Begriffe Tablix-Datenbereiche. Weitere Informationen finden Sie unter [Zonen des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Wenn Sie Zeilen anhand mehrerer Gruppen sortieren, sollen in der Regel unabhängig von Spaltengruppen Gesamtwerte für die sortierten Zeilen angezeigt werden. In dieser Prozedur werden keine Spaltengruppen verwendet. Sie beginnen, indem Sie eine Matrix hinzufügen und die Standardspaltengruppe entfernen. Sie können auch beginnen, indem Sie eine Tabelle hinzufügen und die Detailgruppe entfernen.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>So fügen Sie einem Spaltenheader eine interaktive Sortierschaltfläche hinzu, um mehrere Gruppen zu sortieren  
  
1.  Fügen Sie in der Berichtsentwurfsansicht eine Matrix hinzu.  
  
2.  Ziehen Sie ein numerisches Feld in die Datenzelle, um das Dataset mit der Matrix zu verknüpfen.  
  
     Anschließend erstellen Sie eine Gruppe mit einem Gruppierungsausdruck, in dem mehrere Felder angegeben sind, sowie einen Gruppenkopf zum Anzeigen der Gruppenwerte.  
  
3.  Überprüfen Sie, ob die Matrix auf der Entwurfsoberfläche ausgewählt ist. Im Bereich Gruppierung werden eine Standardzeile und eine Spaltengruppe angezeigt.  
  
4.  Klicken Sie im Bereich Zeilengruppen mit der rechten Maustaste auf die Standardzeilengruppe, und klicken Sie anschließend auf **Gruppe bearbeiten**. Das Dialogfeld **Gruppeneigenschaften** wird angezeigt.  
  
5.  Ersetzen Sie unter **Name**den Standardnamen durch einen Namen, der mehrere Gruppen angibt, nach denen die Sortierung erfolgen soll.  
  
6.  Klicken Sie unter **Gruppierungsausdrücke**und **Gruppieren nach**auf die Schaltfläche „Ausdruck“ (**fx**), um das Dialogfeld **Ausdruck** zu öffnen.  
  
7.  Geben Sie den Ausdruck ein, der alle Felder angibt, nach denen die Gruppierung vorgenommen werden soll. Zum Beispiel kombiniert der folgende Gruppierungsausdruck das Feld "Color" und das Feld "Size": `=Fields!Color.Value & Fields!Size.Value`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Sie haben nun die Gruppe definiert. Ziehen Sie danach die Felder, die im Tablix-Textbereich der Matrix angezeigt werden sollen. Fügen Sie die Felder, die Sie in Schritt 7 als Sortierkriterium festgelegt haben, jeweils einer Spalte des Tablix-Textbereichs hinzu.  
  
     In diesem Szenario wird die erste Spalte im Tablix-Zeilengruppenbereich nicht benötigt. Zum Löschen der Spalte klicken Sie mit der rechten Maustaste auf den Spaltenheader und anschließend auf **Spalten löschen**. In einem Dialogfeld werden Sie gefragt, ob die zugeordneten Gruppen gelöscht werden sollen. Klicken Sie auf **Nein**. Der Zeilengruppenbereich wird gelöscht, und nur der Tablix-Textbereich verbleibt.  
  
     Als nächstes entfernen Sie die Standardspaltengruppe.  
  
9. Klicken Sie im Bereich Spaltengruppen mit der rechten Maustaste auf die Standardspaltengruppe, und klicken Sie anschließend auf **Gruppe löschen**. In einem Dialogfeld werden sie gefragt, ob die Gruppe und zugehörige Zeilen und Spalten gelöscht werden sollen oder aber nur die Gruppe gelöscht werden soll. Klicken Sie auf **Nur Gruppe löschen**. Die Spaltengruppe und der Spaltengruppenbereich werden gelöscht. Nur der Tablix-Textbereich verbleibt.  
  
     Danach fügen Sie dem Textfeld, das sich über die Matrix erstreckt, eine interaktive Sortierschaltfläche hinzu.  
  
10. Klicken Sie im Textfeld in die erste Zeile, und klicken Sie anschließend auf **Eigenschaften von Textfeld**.  
  
11. Klicken Sie auf **Interaktive Sortierung**.  
  
12. Wählen Sie **Interaktive Sortierung für dieses Textfeld aktivieren**aus.  
  
13. Klicken Sie unter **Zu sortierende Elemente auswählen**auf **Gruppen**.  
  
14. Wählen Sie in der Dropdownliste den Namen der in Schritt 5 erstellten Gruppe aus. Der Gruppierungsausdruck wird automatisch ins Textfeld **Sortieren nach** kopiert.  
  
15. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Sie haben die Sortierschaltfläche dem Textfeld hinzugefügt.  
  
16. (Optional) Sie können doppelte Werte in den Spalten mit Gruppenwerten unterdrücken. Klicken Sie auf der Berichtsentwurfsoberfläche auf das Textfeld, in dem der Wert angezeigt wird, für den Sie sich wiederholende Werte ausblenden möchten. Scrollen Sie im Bereich „Eigenschaften“ zu **HideDuplicates**, und wählen Sie in der Dropdownliste den Namen des mit dieser Matrix verknüpften Datasets aus.  
  
 Sie können den Sortierungsvorgang überprüfen, indem Sie mit **Ausführen** eine Vorschau des Berichts anzeigen und dann auf die interaktive Sortierschaltfläche klicken. Die Matrix wird nach den kombinierten Werten des Gruppierungsausdrucks sortiert, jedoch wird jeder einzelne Wert in einer eigenen Spalte angezeigt.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="SynchronizingSortOrder"></a> Synchronisieren der Sortierreihenfolge für mehrere Datenbereiche  
 Fügen Sie eine interaktive Sortierschaltfläche hinzu, die es Benutzern ermöglicht, auf eine Sortierschaltfläche zu klicken und mehrere Datenbereiche zu sortieren. Wenn Sie eine interaktive Sortierschaltfläche erstellen, können Sie angeben, ob die Sortierung für mehrere Datenbereiche anhand desselben Berichtsdatasets synchronisiert werden soll. Zum Beispiel kann ein Bericht eine Matrix und ein Diagramm enthalten, in denen die Daten grafisch dargestellt sind. Wenn ein Benutzer die Sortierreihenfolge der Zeilen in der Matrix ändert, wird das Diagramm automatisch mit derselben Sortierreihenfolge angezeigt.  
  
 Zum Synchronisieren der Sortierreihenfolge müssen Sie für die Datenbereiche oder zu sortierenden Gruppen identische Sortierungsausdrücke verwenden und den Bereich für die Sortierung als gemeinsamen Vorgänger beider Datenbereiche definieren. Der gemeinsame Vorgänger kann ein Dataset sein, mit dem beide Datenbereiche verknüpft sind, oder ein enthaltender Datenbereich, in dem beide Datenbereiche angezeigt werden. Angenommen, in einem Bericht sind eine Matrix und ein Diagramm angegeben, in denen Daten aus demselben Dataset angezeigt werden, und die in einer Liste enthalten sind. Zum Synchronisieren der Sortierungsaktion müssen Sie die interaktive Sortierung für eine Spalte in der Matrix angeben und den Bereich für die Liste festlegen. Wenn der Benutzer die Matrix sortiert, wird das Diagramm ebenfalls sortiert.  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>So synchronisieren Sie die Sortierreihenfolge mit einem Diagramm für eine interaktive Sortierschaltfläche in einem Matrixdatenbereich  
  
1.  Fügen Sie dem Bericht in der Berichtsentwurfsansicht eine Matrix hinzu.  
  
2.  Fügen Sie der Matrixdatenzelle ein numerisches Datasetfeld hinzu, z. B. ein Feld, das eine Menge oder Verkäufe darstellt.  
  
3.  Definieren Sie eine Zeilengruppe. Die Sortierreihenfolge für die Gruppe ist standardmäßig auf einen Ausdruck festgelegt, der mit dem Gruppierungsausdruck identisch ist.  
  
4.  Fügen Sie dem Bericht ein Diagramm hinzu, z. B. ein Kreisdiagramm.  
  
5.  Ziehen Sie das Feld, das Sie in Schritt 2 ausgewählt haben, im Bereich **Diagrammdaten** zum Abschnitt **Wert** .  
  
6.  Ziehen Sie das Feld, das Sie als Sortierkriterium ausgewählt haben, zum Bereich **Kategoriegruppen** .  
  
     Die Gruppenausdrücke für die Matrixzeilengruppe und die Kategoriegruppe des Diagramms müssen identisch sein.  
  
7.  Klicken Sie mit der rechten Maustaste auf die Kategoriegruppe, und klicken Sie anschließend auf **Eigenschaften von Kategoriegruppe**.  
  
8.  Klicken Sie auf **Sortierung**.  
  
9. Klicken Sie auf **Hinzufügen**. Dem Raster der Sortieroptionen wird eine neue Sortierungszeile hinzugefügt.  
  
10. Wählen Sie unter Sortieren nach in der Dropdownliste das Feld aus, das Sie in Schritt 6 als Sortierkriterium ausgewählt haben.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
12. Klicken Sie in der Matrix mit der rechten Maustaste auf das Textfeld in dem Spaltenheader, dem Sie eine interaktive Sortierschaltfläche hinzufügen möchten, und klicken Sie anschließend auf **Textfeldeigenschaften**.  
  
13. Klicken Sie auf **Interaktive Sortierung**.  
  
14. Wählen Sie **Interaktive Sortierung für dieses Textfeld aktivieren**aus.  
  
15. Klicken Sie unter **Zu sortierende Elemente auswählen**auf **Gruppen**.  
  
16. Wählen Sie in der Dropdownliste unter **Gruppen**den Namen der zu sortierenden Gruppe aus. Der Gruppierungsausdruck für diese Gruppe wird automatisch für den Wert für **Sortieren nach** festgelegt.  
  
17. Wählen Sie **Diese Sortierung auch anwenden auf andere Gruppen und Datenbereiche in**aus. Geben Sie im Textfeld den Namen des Datasets ein, z. B. "Sales Data".  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Sie können den Sortierungsvorgang überprüfen, indem Sie mit **Ausführen** eine Vorschau des Berichts anzeigen und dann auf die interaktive Sortierschaltfläche klicken. Die Matrix wird nach den kombinierten Werten des Gruppierungsausdrucks sortiert, jedoch wird jeder einzelne Wert in einer eigenen Spalte angezeigt.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [Zurück zum Anfang](#BackToTop)  
  
## <a name="see-also"></a>Siehe auch  
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Interaktive Sortierung (Berichts-Generator und SSRS)](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)   
 [Sortieren von Daten in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Untersuchen der Flexibilität eines Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
