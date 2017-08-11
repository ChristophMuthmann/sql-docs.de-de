---
title: Gruppierungsbereich | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10033"
- sql13.rtp.rptdesigner.group.f1
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 8b4bd0b3-ec97-48f8-8bfb-82a53a2f35a1
caps.latest.revision: 22
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ed88ddae33151e46c080a8bd747fd8a7f5055eba
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="grouping-pane"></a>Gruppierungsbereich
Wenn Sie [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichte entwerfen, werden im Gruppierungsbereich die Zeilengruppen und Spaltengruppen für den derzeit ausgewählten Tablix-Datenbereich angezeigt. Der Gruppierungsbereich ist für die Diagramm- und Messgerätdatenbereiche nicht verfügbar. Der Gruppierungsbereich besteht aus dem Bereich Zeilengruppen und dem Bereich Spaltengruppen. Der Gruppierungsbereich weist zwei Modi auf, den Standard- und den erweiterten Modus. Im Standardmodus wird eine hierarchische Sicht der dynamischen Elemente für Zeilen- und Spaltengruppen angezeigt. Im erweiterten Modus werden dynamische und statische Elemente für Zeilen- und Spaltengruppen angezeigt. Eine Gruppe ist ein benannter Satz von Daten aus einem Berichtsdataset, der in einem Datenbereich angezeigt wird. Gruppen werden in Hierarchien organisiert, die statische und dynamische Elemente einschließen. Weitere Informationen finden Sie unter [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Wenn der Gruppierungsbereich nicht angezeigt wird, klicken Sie im Menü **Bericht** auf **Gruppierung**.
  
 Zellen in den Zeilen- und Spaltengruppenbereiche können statische oder dynamische Elemente einer Gruppe sein. Statische Elemente wiederholen sich einmal pro Gruppe und enthalten meist Bezeichnungen oder Gesamtbeträge. Dynamische Elemente wiederholen sich einmal pro Gruppeninstanz und enthalten meist die eindeutigen Werte des Gruppierungsausdrucks. Wenn Sie Tablix-Zellen im Zeilengruppenbereich oder Spaltengruppenbereich auswählen, wird das entsprechende Gruppenelement im Bereich Zeilengruppen oder Spaltengruppen ausgewählt. Wenn Sie umgekehrt Gruppen im Gruppierungsbereich auswählen, wird die entsprechende, dem Gruppenelement zugeordnete Zelle auf der Entwurfsoberfläche ausgewählt. Weitere Informationen zu Tablix-Zeilen- und spaltengruppenbereichen finden Sie unter [Tablix-Datenbereiche &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Der Gruppierungsbereich unterstützt die folgenden Modi:  
  
-   **Standard.** Verwenden Sie den Standardmodus, um Gruppen hinzuzufügen, zu bearbeiten oder zu löschen. Sie können übergeordnete, untergeordnete und Detailgruppen hinzufügen, indem Sie Felder aus dem Berichtsdatenbereich ziehen und diese in der Gruppenhierarchie einfügen. Um eine angrenzende Gruppe hinzuzufügen, müssen Sie die Verknüpfung **Gruppe hinzufügen** verwenden. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Erweitert**. Verwenden Sie den **erweiterten Modus** , um alle Elemente der Zeilen- und Spaltengruppen anzuzeigen und die Eigenschaften auf statische Elemente festzulegen. Wenn Sie Gruppen erstellen oder Gesamtwerte hinzufügen, werden die Eigenschaften automatisch festgelegt, mit denen gesteuert wird, wie der Tablix-Datenbereich Zeilen und Spalten für die einzelnen Berichtsseiten rendert. Um diese Eigenschaften manuell anzupassen, müssen Sie diese für das Tablix-Element festlegen. Weitere Informationen finden Sie unter [Steuern der Tablix-Datenbereichsanzeige auf einer Berichtsseite &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Standardmodus  
 Im Standardmodus wird im Bereich Zeilengruppen und im Bereich Spaltengruppen eine hierarchische Sicht für alle übergeordneten Gruppen, untergeordneten Gruppen und angrenzenden Gruppen angezeigt. Untergeordnete Gruppen werden eingezogen unter der jeweils übergeordneten Gruppe angezeigt. Angrenzende Gruppen werden auf der gleichen Einzugsebene wie gleichgeordnete Gruppen angezeigt. Die folgende Abbildung zeigt einen Tablix-Datenbereich mit geschachtelten Zeilengruppen und geschachtelten und angrenzenden Spaltengruppen.  
  
 ![Tablix, geschachtelte und angrenzende Zeilen- und Spaltengruppen](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpane.gif "Tablix, geschachtelte und angrenzende Zeilen- und Spaltengruppen")  
  
 Der Bereich Gruppierung zeigt die entsprechenden Zeilen- und Spaltengruppen an. In der folgenden Abbildung wurde die auf der Unterkategorie basierende Gruppe im Bereich Zeilengruppen ausgewählt, und die Gruppierungszelle [Subcat] ist im Tablix-Datenbereich ausgewählt:  
  
 ![Gruppierungsbereich für geschachtelte Zeilen- und Spaltengruppen](../../reporting-services/report-design/media/rs-basictablixdesigngroupingpanedefaultview.gif "Gruppierungsbereich für geschachtelte Zeilen- und Spaltengruppen")  
  
 Im Bereich Zeilengruppen ist die auf der Unterkategorie basierende Gruppe ein untergeordnetes Element der auf der Kategorie basierenden Gruppe. Im Bereich Spaltengruppen ist die Gruppe für Land und Region ein untergeordnetes Element der Gruppe für Geographie. Die Gruppe für das Jahr und die Gruppen für Land und Region sind angrenzende Gruppen.  
  
 Weitere Informationen finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>erweiterten Modus  
Im erweiterten Modus können Sie alle statischen und dynamischen Elemente einer Gruppe anzeigen. Wenn Sie ein Element auswählen, zeigt das Eigenschaftenfenster Eigenschaften für das derzeit ausgewählte **Tablix-Element**an.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Wenn Sie den **erweiterten Modus**umschalten möchten, klicken Sie am Rand des Bereichs „Spaltengruppen“ mit der rechten Maustaste auf den Pfeil nach unten, und klicken Sie dann auf **Erweiterter Modus**.  
  
In den meisten Fällen werden Eigenschaften, die die Anzeige statischer und dynamischer Gruppenzeilen und Gruppenspalten steuern, automatisch beim Erstellen einer Gruppe oder Hinzufügen von Gesamtwerten festgelegt. 

Zum Bearbeiten der Standardwerte müssen Sie das Gruppenelement im Bereich Zeilengruppen oder Spaltengruppen auswählen und die Eigenschaftenwerte im Eigenschaftenfenster ändern. Wenn der Bereich **Eigenschaften** nicht angezeigt wird, klicken Sie im Menü **Ansicht** auf **Eigenschaften**, oder drücken Sie F4.  Die folgenden Eigenschaften sind verfügbar:  
  
-   **FixedData**. Boolesch. Für äußere und Zeilen- und Spaltenheader. Frieren Sie den Zeilengruppenbereich für vertikale Bildläufe oder den Spaltengruppenbereich für horizontale Bildläufe in einem Renderer ein, z. B. HTML.  
  
-   **HideIfNoRows**. Boolesch. Nur für statische Elemente. Bei erfolgter Festlegung werden Hidden und ToggleItem ignoriert. Blenden Sie dieses Element aus, wenn der Tablix-Datenbereich keine Datenzeilen enthält.  
  
-   **KeepTogether**.  
  
-   **KeepWithGroup**. Boolesch. Nur für statische Zeilenelemente. Trennen Sie diese Zeile nach Möglichkeit nicht vom vorherigen oder folgenden gleichgeordneten dynamischen Element, sofern dieses nicht ausgeblendet ist.  
  
-   **RepeatOnNewPage**. Boolesch. Nur für statische Zeilenelemente und wenn KeepWithGroup nicht „None“ ist. Wiederholen Sie diese statische Zeile nach Möglichkeit auf jeder Seite, die mindestens eine Instanz des von KeepWithGroup angegebenen dynamischen Elements aufweist.  
  
-   **Hidden**. Boolesch. Gibt an, ob die Zeile oder die Spalte anfänglich ausgeblendet sein soll.  
  
-   **ToggleItem.** Zeichenfolge. Der Name des Textfelds, dem das Umschaltbild hinzugefügt werden soll. Das Textfeld muss demselben Gruppenbereich oder einem enthaltenden Bereich angehören.  
  
 Weitere Informationen dazu, wie dieses Verhalten in einem Tablix-Datenbereich gesteuert werden kann, finden Sie unter [Steuern der Tablix-Datenbereichsanzeige auf einer Berichtsseite &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
 Nicht jedes statische Element verfügt über einen Header, der einer Zelle auf der Entwurfsoberfläche entspricht. Im Gruppierungsbereich wird mit der folgenden Konvention angegeben, ob ein statisches Element keinen Header besitzt:  
  
-   **Statisch** Gibt ein statisches Element mit einer Headerzelle an.  
  
-   **(Statisch)** Gibt ein statisches Element ohne Headerzelle an, wird als ausgeblendet statisch bezeichnet.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filter, Gruppen, und Sortieren von Daten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
