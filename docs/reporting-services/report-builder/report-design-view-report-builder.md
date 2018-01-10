---
title: "Entwurfsansicht für Berichte (Berichts-Generator) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
caps.latest.revision: "23"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c5b5bc4bfaac7322b902cc4ea941c64c6b58f4f8
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-design-view-report-builder"></a>Berichtsentwurfsansicht (Berichts-Generator)
  Das Fenster des Berichts-Generators ist so aufgebaut, dass Sie Berichtsressourcen einfach anordnen und schnell die gewünschten paginierten Berichte erstellen können. Die Entwurfsoberfläche befindet sich in der Mitte des Fensters. Das Menüband und die Bereiche befinden sind um die Entwurfsoberfläche angeordnet. Auf der Entwurfsoberfläche können Sie die Berichtselemente hinzufügen und anordnen. Dieser Artikel erklärt die Bereiche, die Sie zum Hinzufügen, Auswählen und Organisieren Ihrer Berichtsressoucen und zum Verändern der Berichtselementeigenschaften verwenden.  
  
 ![Report Builder Design View](../../reporting-services/report-builder/media/ssrb-designview.png "Report Builder Design View")  
  
1.  Menüband  
  
2.  [Parameterbereich](#Ribbon)  
  
3.  [Berichtsteilkatalog](#ReptPartGallery)  
  
4.  [Eigenschaftenbereich](#PropertiesPane)  
  
5.  [Berichtsentwurfsoberfläche](#RptDesignSurface)  
  
6.  [Berichtsdatenbereich](#ReptDataPane)  
  
7.  [Gruppierung (Bereich)](#GroupPane)  
  
8.  Aktueller Berichtsstatusbalken  
  
##  <a name="Ribbon"></a> Parameterbereich  
 Mithilfe von Berichtsparametern können Sie Berichtsdaten steuern, eine Verbindung zwischen verwandten Berichten herstellen und die Berichtspräsentation anpassen. Der Parameter-Bereich bietet ein flexibles Layout für die Berichtsparameter.  
  
 Erfahren Sie mehr über [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="RptDesignSurface"></a> Berichtsentwurfsoberfläche  
 Die Berichtsentwurfsoberfläche des Berichts-Generators ist der Hauptarbeitsbereich zum Entwerfen der Berichte. Fügen Sie der Entwurfsoberfläche Berichtselemente wie Datenbereiche, Unterberichte, Textfelder, Bilder, Rechtecke und Linien aus dem Menüband oder dem Berichtsteilkatalog hinzu, um sie in den Bericht einzufügen. Dort können Sie den Berichtselementen Gruppen, Ausdrücke, Parameter, Filter, Aktionen, Sichtbarkeit und Formatierung hinzufügen.  
  
 Sie können auch folgende Eigenschaften ändern:  
  
-   Ändern Sie die Eigenschaften des Berichtshauptteils (z.B. Rahmen- und Füllfarbe), indem Sie außerhalb von Berichtselementen mit der rechten Maustaste auf die weiße Fläche der Entwurfsoberfläche klicken und anschließend auf **Eigenschaften des Berichtshauptteils**klicken.  
  
-   Ändern Sie die Kopf- und Fußzeileneigenschaften (z.B. Rahmen- und Füllfarbe), indem Sie außerhalb von Berichtselementen mit der rechten Maustaste auf die weiße Fläche der Entwurfsoberfläche klicken und anschließend auf **Seitenkopfeigenschaften** oder **Fußzeileneigenschaften**klicken.  
  
-   Ändern Sie die Eigenschaften des Berichts (z.B. Seiteneinrichtung), indem Sie mit der rechten Maustaste auf die graue Fläche um die Entwurfsoberfläche klicken und anschließend auf **Berichtseigenschaften**klicken.  
  
-   Ändern Sie die Eigenschaften von Berichtselementen, indem Sie mit der rechten Maustaste auf die Elemente klicken und anschließend auf **Eigenschaften**klicken.  
  
 Informationen zum Bearbeiten von Elementen auf der Entwurfsoberfläche über die Tastatur finden Sie unter [Tastenkombinationen (Berichts-Generator)](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md).  
  
### <a name="design-surface-size-and-print-area"></a>Entwurfsoberflächengröße und Druckbereich  
 Die Größe der Entwurfsoberfläche kann sich von der Größe des Druckbereichs unterscheiden, den Sie für das Drucken des Berichts angeben. Wenn Sie die Größe der Entwurfsoberfläche ändern, ändert sich der Druckbereich des Berichts dadurch nicht. Unabhängig von der Größe, die Sie für den Druckbereich des Berichts festlegen, ändert sich die Größe des vollständigen Entwurfsbereichs nicht. Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!TIP]  
>  Aktivieren Sie auf der Registerkarte **Ansicht** das Kontrollkästchen **Lineal**, um das Lineal anzuzeigen.  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 Im Berichtsdatenbereich des Berichts-Generators definieren Sie die für einen Bericht benötigten Berichtsdaten und -ressourcen, bevor Sie mit dem Entwurf des Berichtslayouts beginnen. Sie können dem Berichtsdatenbereich z. B. Datenquellen, Datasets, berechnete Felder, Berichtsparameter und Bilder hinzufügen.  
  
 Nachdem Sie dem Berichtsdatenbereich Elemente hinzugefügt haben, können Sie Felder in Berichtselemente auf der Entwurfsoberfläche ziehen und so bestimmen, wo die Daten auf der Berichtsseite angezeigt werden.  
  
> [!TIP]  
>  Wenn Sie ein Feld vom Berichtsdatenbereich direkt in die Berichtsentwurfsoberfläche ziehen, anstatt es in einem Datenbereich wie einer Tabelle oder einem Diagramm einzufügen, wird beim Ausführen des Berichts nur der erste Wert von den Daten in diesem Feld angezeigt.  
  
 Sie können auch integrierte Felder vom Berichtsdatenbereich in die Berichtsentwurfsoberfläche ziehen. Beim Rendern enthalten diese Felder Informationen zum Bericht, z. B. Berichtsname, Gesamtanzahl von Seiten im Bericht und aktuelle Seitennummer.  
  
 Einige Elemente werden dem Berichtsdatenbereich automatisch hinzugefügt, wenn Sie der Berichtsentwurfsoberfläche etwas hinzufügen. Wenn Sie z. B. ein Berichtsteil aus dem Berichtsteilkatalog hinzufügen und der Berichtsteil ein Datenbereich ist, wird das Dataset dem Berichtsdatenbereich automatisch hinzugefügt. Weitere Informationen finden Sie unter [Berichtsteile und Datasets](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md). Wenn Sie ein Bild in den Bericht einbetten, wird es dem Ordner "Bilder" im Berichtsdatenbereich hinzugefügt.  
  
> [!NOTE]  
>  Mit der Schaltfläche **Neu** können Sie dem Berichtsdatenbereich ein neues Element hinzufügen. Sie können dem Bericht mehrere Datasets aus derselben Datenquelle oder anderen Datenquellen hinzufügen. Außerdem können Sie dem Berichtsserver freigegebene Datasets hinzufügen. Klicken Sie mit der rechten Maustaste auf eine Datenquelle, und klicken Sie anschließend auf **Dataset hinzufügen**, um ein neues Dataset aus derselben Datenquelle hinzuzufügen.  
  
 Weitere Informationen zu den Elementen im Berichtsdatenbereich finden Sie in den folgenden Themen:  
  
-   [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)  
  
-   [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
-   [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [Datasetfelder-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> Berichtsteilkatalog  
 Die einfachste Methode zum Erstellen eines Berichts besteht darin, auf dem Berichtsserver oder einem in eine SharePoint-Website integrierten Berichtsserver nach einem vorhandenen Berichtsteil zu suchen (z. B. eine Tabelle oder ein Diagramm).  
  
 Wenn Sie auf der Registerkarte Einfügen auf **Berichtsteile** klicken, wird der Berichtsteilkatalog geöffnet. Dort können Sie Berichtsteile suchen, die Sie Ihrem Bericht hinzufügen. Sie können die Berichtsteile nach dem Namen des Berichtsteils (vollständig oder teilweise), nach der Person, von der der Berichtsteil erstellt oder zuletzt geändert wurde, nach dem letzten Änderungsdatum, dem Speicherort oder dem Typ des Berichtsteils filtern. Sie konnten z. B. nach allen Diagrammen suchen, die in der vorhergehenden Woche von einem oder mehreren Ihrer Kollegen erstellt wurden.  
  
> [!NOTE]  
>  Sie müssen mit einem Server verbunden sein, um den Berichtsteilkatalog anzuzeigen.  
  
 Sie können die Suchergebnisse als Miniaturansichten oder in Listenform anzeigen und nach Name, Erstellungs- und Änderungsdatum und dem Ersteller sortieren. Weitere Informationen finden Sie unter [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
  
##  <a name="PropertiesPane"></a> Eigenschaften (Bereich in Berichts-Generator)  
 Mit jedem Element in einem Bericht, Datenbereichen, Bildern und Textfeldern und im Berichtshauptteil selbst, sind Eigenschaften verknüpft. Beispiel: Die Eigenschaft BorderColor für ein Textfeld gibt den Farbwert für den Rahmen des Textfelds an, während die Eigenschaft PageSize für den Bericht die Seitengröße des Berichts angibt.  
  
 Diese Eigenschaften werden im Bereich "Eigenschaften" angezeigt. Die Eigenschaften im Bereich ändern sich je nach ausgewähltem Berichtselement.  
  
 Klicken Sie auf der Registerkarte "Ansicht" in der Gruppe "Ein-/Ausblenden" auf "Eigenschaften", um den Bereich "Eigenschaften" anzuzeigen.  
  
### <a name="changing-property-values"></a>Ändern von Eigenschaftswerten  
 In Berichts-Generator gibt es verschiedene Möglichkeiten, die Eigenschaften für Berichtselemente zu ändern:  
  
-   Durch Klicken auf Schaltflächen und Listen auf dem Menüband.  
  
-   Durch Ändern von Einstellungen in Dialogfeldern.  
  
-   Durch Ändern von Eigenschaftswerten im Eigenschaftenbereich.  
  
 Die gebräuchlichsten Eigenschaften sind in den Dialogfeldern und auf dem Menüband verfügbar.  
  
 Je nach Eigenschaft können Sie einen Eigenschaftswert aus einer Dropdownliste festlegen, den Wert eingeben oder auf `<Expression>` klicken, um einen Ausdruck zu erstellen.  
  
### <a name="changing-the-properties-pane-view"></a>Ändern der Eigenschaftenbereichsansicht  
 Standardmäßig sind die Eigenschaften, die im Eigenschaftenbereich angezeigt werden, in größere Kategorien unterteilt, wie Aktion, Rahmen, Ausfüllen, Schriftart und Allgemein. Mit jeder Kategorie ist eine Gruppe von Eigenschaften verknüpft. Beispiel: Die folgenden Eigenschaften werden in der Kategorie Schriftart aufgeführt: Color, FontFamily, FontSize, FontStyle, FontWeight, LineHeight und TextDecoration. Sie können alle Eigenschaften, die im Bereich aufgeführt werden, auch alphabetisieren. In diesem Fall werden die Kategorien entfernt. Alle Eigenschaften werden ungeachtet der Kategorie in alphabetischer Reihenfolge aufgeführt.  
  
 Der Eigenschaftenbereich enthält drei Schaltflächen am oberen Rand: Kategorie, Alphabetisieren und Eigenschaftenseiten. Klicken Sie auf die Schaltfläche Kategorie und Alphabetisieren, um zwischen den Ansichten des Eigenschaftenbereichs zu wechseln. Klicken Sie auf die Schaltfläche **Eigenschaftenseiten** , um das Eigenschaftendialogfeld für ein ausgewähltes Berichtselement zu öffnen.  
  
  
##  <a name="GroupPane"></a> Gruppierung (Bereich in Berichts-Generator)  
 Gruppen werden verwendet, um die Berichtsdaten in einer visuellen Hierarchie zu organisieren und Ergebnisse zu berechnen. Sie können die Zeilen- und Spaltengruppen innerhalb eines Datenbereichs auf der Entwurfsoberflache und im Gruppierungsbereich anzeigen. Der Gruppierungsbereich enthält zwei Bereiche: Zeilengruppen und Spaltengruppen. Wenn Sie einen Datenbereich wählen, werden im Gruppierungsbereich alle Gruppen innerhalb dieses Datenbereichs in Form einer hierarchischen Liste angezeigt: Untergeordnete Gruppen werden eingerückt unter den übergeordneten Gruppen angezeigt.  
  
 ![Berichts-Generator-Zeilengruppen](../../reporting-services/report-builder/media/ssrb-rowgroups.png "Report Builder Row Groups")  
  
 Sie können Gruppen erstellen, indem Sie Felder mit Drag and Drop aus dem Berichtsdatenbereich ziehen und auf der Entwurfsoberfläche oder im Gruppierungsbereich einfügen. Sie können übergeordnete, angrenzende und untergeordnete Gruppen im Gruppierungsbereich hinzufügen, Gruppeneigenschaften ändern und Gruppen löschen.  
  
 Der Gruppierungsbereich wird standardmäßig angezeigt. Sie können ihn jedoch schließen, indem Sie die Auswahl des Kontrollkästchens Gruppierungsbereich auf der Registerkarte Sicht aufheben. Der Gruppierungsbereich ist für die Diagramm- und Messgerätdatenbereiche nicht verfügbar.  
  
 Weitere Informationen finden Sie unter [Gruppierungsbereich &#40;Berichts-Generator&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md) und [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  
##  <a name="RunMode"></a> Anzeigen einer Berichtsvorschau im Ausführungsmodus  
 In der Berichtsentwurfsansicht arbeiten Sie nicht mit tatsächlichen Daten, sondern mit einer durch den Feldnamen oder Ausdruck angegebenen Darstellung der Daten. Wenn die tatsächlichen Daten im Kontext des entworfenen Berichts angezeigt werden sollen, können Sie den Bericht ausführen, um eine Vorschau der Daten aus der zugrunde liegenden Datenbank im Berichtslayout anzuzeigen. Durch Wechseln zwischen dem Entwurf und der Ausführung des Berichts können Sie den Entwurf des Berichts anpassen und die Ergebnisse sofort anzeigen. Um die Vorschau des Berichts anzuzeigen, klicken Sie auf **Ausführen** in der **Ansichten** group on the ribbon.  
  
 Wenn Sie auf **Ausführen**klicken, stellt der Berichts-Generator eine Verbindung mit den Berichtsdatenquellen her. Die Daten werden auf dem Computer zwischengespeichert und mit dem Layout kombiniert, und anschließend wird der Bericht im HTML-Viewer gerendert. Sie können den Bericht beliebig oft ausführen, während Sie weiterhin am Entwurf des Berichts arbeiten. Wenn Sie mit dem Entwurf des Berichts zufrieden sind, können Sie ihn auf dem Berichtsserver speichern. Dort kann er von Benutzern mit den entsprechenden Berechtigungen angezeigt werden.  
   
 Erfahren Sie mehr zu [Anzeigen einer Berichtsvorschau in Berichts-Generator](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
### <a name="running-a-report-with-parameters"></a>Ausführen eines Berichts mit Parametern  
 Wenn Sie den Bericht ausführen, wird er automatisch verarbeitet. Wenn der Bericht Parameter enthält, müssen alle Parameter Standardwerte haben, bevor der Bericht automatisch ausgeführt werden kann. Wenn ein Parameter keinen Standardwert hat, müssen Sie bei der Ausführung des Berichts einen Wert für den Parameter wählen und dann auf **Bericht anzeigen** auf der Registerkarte Ausführen klicken. Weitere Informationen finden Sie unter [Report Parameters &#40;Report Builder and Report Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="print-preview"></a>Seitenansicht  
 Wenn Sie im Ausführungsmodus einen Bericht in der Vorschau anzeigen, entspricht er einem in HTML erstellten Bericht. Die Vorschau ist kein HTML-Code, das Layout und die Paginierung des Berichts gleichen jedoch der HTML-Ausgabe. Sie können die Ansicht ändern und einen gedruckten Bericht darstellen, indem Sie zur Seitenansicht wechseln. Klicken Sie auf der Registerkarte **Ausführen** auf die Schaltfläche **Seitenansicht** . Der Bericht wird so angezeigt, wie er auf einer physischen Seite dargestellt werde würde. Diese Ansicht gleicht der Ausgabe durch die Bild- und PDF-Renderingerweiterung. Die Seitenansicht ist keine Bild- oder PDF-Datei, das Layout und die Paginierung des Berichts ähneln jedoch der Ausgabe in diesen Formaten.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Berichts-Generator in SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  
  
