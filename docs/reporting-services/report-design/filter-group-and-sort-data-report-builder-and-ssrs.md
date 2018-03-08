---
title: Filtern, Gruppieren und Sortieren von Daten (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: ec9e18aeee47b023b6afcf8dbac2e733fd2c6223
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>Filtern, Gruppieren und Sortieren von Daten (Berichts-Generator und SSRS)
  In einem Bericht werden Ausdrücke zum Steuern, Organisieren und Sortieren von Berichtsdaten verwendet. Beim Erstellen von Datasets und Entwerfen des Berichtslayouts werden die Eigenschaften von Berichtselementen standardmäßig automatisch auf Ausdrücke festgelegt. Diese Einstellungen basieren auf den Datasetfeldern, Parametern und anderen Elementen, die im Berichtsdatenbereich angezeigt werden. Sie können einer Tabellen- oder Matrixzelle auch eine interaktive Sortierschaltfläche hinzufügen, um dem Benutzer das interaktive Ändern der Zeilensortierreihenfolge für Gruppen oder Zeilen innerhalb von Gruppen zu ermöglichen.  
  
-   **Filterausdrücke:** Ein Filterausdruck testet Daten auf Grundlage eines von Ihnen angegebenen Vergleichs und bestimmt so, ob sie ein- oder ausgeschlossen werden. Filter werden auf Daten in einem Bericht angewendet, nachdem die Daten über eine Datenverbindung abgerufen wurden. Den folgenden Elementen kann eine beliebige Kombination von Filtern hinzugefügt werden: einer Definition eines freigegebenen Datasets auf dem Berichtsserver, einer freigegebenen Datasetinstanz oder einem eingebetteten Dataset in einen Bericht, einem Datenbereich (z. B. eine Tabelle oder ein Diagramm) oder einer Datenbereichsgruppe (z. B. eine Zeilengruppe in einer Tabelle oder eine Kategoriegruppe in einem Diagramm).  
  
-   **Gruppierungsausdrücke:** Ein Gruppierungsausdruck organisiert Daten basierend auf einem Datasetfeld oder einem anderen Wert. Gruppierungsausdrücke werden automatisch erstellt, wenn Sie das Berichtslayout erstellen. Der Berichtsprozessor wertet Gruppierungsausdrücke nach dem Anwenden der Filter aus, wenn Berichtsdaten und Datenbereiche kombiniert werden. Sie können einen Gruppierungsausdruck nach seiner Erstellung weiter anpassen.  
  
-   **Sortierungsausdrücke:** Ein Sortierungsausdruck steuert die Reihenfolge, in der Daten in einem Datenbereich angezeigt werden. Sortierungsausdrücke werden automatisch erstellt, wenn Sie das Berichtslayout erstellen. Ein Sortierungsausdruck für eine Gruppe wird standardmäßig auf die gleichen Werte festgelegt wie der Gruppierungsausdruck. Sie können einen Sortierungsausdruck nach seiner Erstellung weiter anpassen.  
  
-   **Interaktive Sortierung:** Wenn Sie es dem Benutzer ermöglichen möchten, die Sortierreihenfolge einer Spalte zu festzulegen oder umzukehren, können Sie einem Spaltenheader oder einer Gruppenkopfzelle in einer Tabelle oder Matrix eine interaktive Sortierschaltfläche hinzufügen.  
  
 Sie können einen Ausdruck ändern, indem Sie einen Verweis auf einen Berichtsparameter hinzufügen, um den Benutzern das Anpassen von Filter-, Gruppierungs- oder Sortierungsausdrücke zu erleichtern. Weitere Informationen finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)" basiert.  
  
 Weitere Informationen und Beispiele finden Sie in den folgenden Themen:  
  
-   [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Lernprogramme für den Berichts-Generator](../../reporting-services/report-builder-tutorials.md)  
  
-   [Reporting Services-Tutorials &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [Berichtsbeispiele (Berichts-Generator und SSRS)](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> Filtern von Daten im Bericht  
 Filter sind Teile eines Berichts, mit denen Berichtsdaten gesteuert werden können, nachdem sie über die Datenverbindung abgerufen wurden. Verwenden Sie Filter, wenn Sie eine Datasetabfrage nicht ändern können, um Daten vor dem Abrufen aus einer externen Datenquelle zu filtern.  
  
 Erstellen Sie möglichst Datasetabfragen, die nur die Daten zurückgeben, die Sie im Bericht anzeigen möchten. Wenn Sie die Menge abzurufender und zu verarbeitender Daten reduzieren, verbessern Sie die Berichtsleistung. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Nachdem die Daten aus der externen Datenquelle abgerufen wurden, können Sie Datasets, Datenbereichen und Datenbereichsgruppen (auch Detailgruppen) Filter hinzufügen. Filter werden zuerst auf das Dataset, dann auf den Datenbereich und anschließend auf die Gruppe angewendet (von oben nach unten bei Gruppenhierarchien). In einer Tabelle, Matrix oder Liste werden Filter für Zeilen- und Spaltengruppen sowie für angrenzende Gruppen unabhängig voneinander angewendet. In Diagrammen werden Filter für Kategorie- und Reihengruppen unabhängig voneinander angewendet. Weitere Informationen finden Sie unter [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Für jeden Filter geben Sie eine *Filtergleichung*an. Eine Filtergleichung enthält ein Datasetfeld oder einen Ausdruck, das bzw. der die zu filternden Daten, einen Operator und einen Vergleichswert definiert. Nur die mit der Filterbedingung übereinstimmenden Datenwerte werden bei der Verarbeitung des Elements berücksichtigt.  
  
 Sie können Parameter in Filterausdrücke einschließen, um Benutzern das Steuern der Daten in einem Bericht zu ermöglichen. Weitere Informationen finden Sie unter [Verweise auf Parametersammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).  
  
 Sie können einen Verweis auf das integrierte "UserID"-Feld in einen Filter einschließen, um eine Sicht für jeden Benutzer anzupassen. Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
  
##  <a name="Grouping"></a> Gruppieren von Daten im Bericht  
 Durch Gruppen werden Daten in einem Bericht für die Anzeige oder zum Berechnen von Aggregatwerten organisiert. Kenntnisse im Definieren von Gruppen und Verwenden von Gruppenfunktionen sind für das Entwerfen präziserer Berichte hilfreich.  
  
 Gruppierungsausdrücke werden bei den folgenden Aktionen automatisch erstellt:  
  
-   Anordnen von Datasetfeldern in einem Tabellen-, Matrix- oder Diagramm-Assistenten oder Zuordnen von Feldern im Karten-Assistenten  
  
-   Hinzufügen eines Felds zum Zeilengruppen- oder Spaltengruppenbereich im Bereich "Gruppierung" in einer Tabelle, Matrix oder Liste  
  
-   Hinzufügen eines Felds zum Kategoriegruppen- oder Reihengruppenbereich im Bereich "Diagrammdaten"  
  
-   Festlegen eines Felds in einer Karte, um Kartenelemente mit analytischen Daten im Kontextmenüelement "Ebenendaten" zu vergleichen  
  
 Eine Gruppe ist ein Teil der Berichtsdefinition. Jede Gruppe hat einen Namen. Standardmäßig entspricht der Gruppenname dem Datasetfeld, auf dem die Gruppe basiert.  
  
 In einem Tabellen- oder Matrixdatenbereich können mehrere Zeilengruppen und Spaltengruppen erstellt werden. Sie können die Daten in einer visuellen Hierarchie anzeigen, indem Sie geschachtelte Gruppen, angrenzende Gruppen und rekursive Hierarchiegruppen organisieren (z. B. ein Organigramm).  
  
 Der Gruppenname gibt einen Ausdrucksbereich an. Sie können den Namen einer Gruppe als Bereich angeben, in dem Aggregate berechnet werden sollen, um Daten hierarchisch zu organisieren und die Anzeige von untergeordneten Knoten in übergeordneten Knoten in einem Drilldownbericht umzuschalten, andere Sichten derselben Daten für mehrere Datenbereiche anzuzeigen und Zusammenfassungsdaten in einer Tabelle, einer Matrix, einem Diagramm, einem Messgerät oder einer Karte visuell darzustellen. Weitere Informationen finden Sie unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)-Ausdruck dar.  
  
 Fügen Sie dem Satz von Gruppierungsausdrücken die einzelnen Felder hinzu, um eine Gruppierung für mehrere Datasetfelder vorzunehmen. Sie können auch eigene Gruppierungsausdrücke in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]erstellen. Sie können z. B. eine Gruppierung anhand eines Bereichs von Werten oder mit einem Berichtsparameter durchführen, um Benutzern verschiedene Möglichkeiten zur Gruppierung von Daten in einem Datenbereich zu bieten. Weitere Informationen finden Sie unter [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 Für jede Berichtsdarstellung können Sie beim Erstellen von Gruppen vor und nach jeder Gruppe oder jeder Instanz einer Gruppe Seitenumbrüche hinzufügen. So kann die Datenmenge auf jeder Seite reduziert und die Leistung beim Rendern der Berichte besser verwaltet werden. Weitere Informationen finden Sie unter [Hinzufügen eines Seitenumbruchs (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md).  
  
 Das Erstellen von Datenbereichsgruppen ist eine Möglichkeit, Daten in einem Bericht zu organisieren. Zum Organisieren von Daten stehen mehrere weitere Methoden zur Verfügung, die alle bestimmte Vorteile bieten. Weitere Informationen finden Sie unter [Drillthrough, Drilldown, Unterberichte und geschachtelte Datenbereiche &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
### <a name="defining-group-variables"></a>Definieren von Gruppenvariablen  
 Beim Definieren einer Gruppe können Sie eine Gruppenvariable zur Verwendung in Ausdrücken erstellen, die auf den Bereich der Gruppe ausgelegt und über geschachtelte Gruppen zugänglich sind. Eine Gruppenvariable wird einmal pro Gruppeninstanz berechnet, und der Zugriff auf die Variable erfolgt über Ausdrücke in untergeordneten Gruppen. Für nach Bereich und Teilbereich gruppierte Daten können Sie z. B. eine Steuer für jeden Bereich berechnen und diese Steuer in Berechnungen der Teilbereichsgruppe verwenden.  
  
 Weitere Informationen finden Sie unter [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
### <a name="groups-and-scope-in-data-regions"></a>Gruppen und Bereiche in Datenbereichen  
 Geben Sie für jeden Datenbereich die gleichen Gruppierungsausdrücke an, um mehrere Sichten der Daten aus einem Dataset bereitzustellen. Sie können kategorisierte Daten z. B. zur Anzeige aller Detaildaten in einer Tabelle und zur Anzeige von Aggregaten in einem Kreisdiagramm anzeigen, um jede Kategorie in Bezug zum gesamten Dataset zu visualisieren. Weitere Informationen finden Sie unter [Verknüpfen mehrerer Datenbereiche mit einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
 Wenn Sie einen Datenbereich in einer Zelle in einer Tabelle, Matrix oder Liste schachteln, legen Sie die Daten automatisch auf die innersten Gruppenmitgliedschaften der Zelle aus. Angenommen, Sie fügen einer Zelle, die sich in einer Zeilengruppe und in einer Spaltengruppe befindet, ein Diagramm hinzu. Die für dieses Diagramm verfügbaren Daten werden zur Laufzeit dem Bereich der innersten Zeilengruppeninstanz und innersten Spaltengruppeninstanz zugeordnet. Weitere Informationen finden Sie unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
  
##  <a name="Sorting"></a> Sortieren von Daten im Bericht  
 Wenn Sie die Sortierreihenfolge für Daten in einem Bericht steuern möchten, können Sie Daten in einer Datasetabfrage sortieren oder einen Sortierungsausdruck für einen Datenbereich oder eine Datengruppe definieren. Außerdem können Sie Tabellen und Matrizen interaktive Sortierschaltflächen hinzufügen, um es Benutzern zu ermöglichen, die Sortierreihenfolge für Zeilen zu ändern.  
  
 Alle drei Typen von Sortierungen können im gleichen Bericht kombiniert werden. Standardmäßig wird die Sortierreihenfolge durch die Reihenfolge bestimmt, in der Daten von der Datasetabfrage zurückgegeben werden. Sortierungsausdrücke werden im Datenbereich und in der Datenbereichsgruppe angewendet. Interaktive Sortierungen werden nach Sortierungsausdrücken angewendet.  
  
 Bei Ausdrücken, die Aggregatfunktionen enthalten, sind die meisten Ergebnisse nicht von der Sortierreihenfolge betroffen. Rückgabewerte für die folgenden Aggregatfunktionen sind von der Sortierreihenfolge betroffen: „First“, „Last“ und „Previous“. Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
### <a name="sorting-data-in-a-dataset-query"></a>Sortieren von Daten in einer Datasetabfrage  
 Schließen Sie Sortierreihenfolge in der Datasetabfrage ein, um diese vorzusortieren, bevor sie für einen Bericht abgerufen werden. Beim Sortieren von Daten in der Abfrage wird die Sortierung selbst von der Datenquelle und nicht vom Berichtsprozessor ausgeführt.  
  
 Beim Datenquellentyp [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie der Datenbankabfrage eine ORDER BY-Klausel hinzufügen. Beispielsweise sortiert die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage die Spalten Sales und Region by Sales in absteigender Reihenfolge von der Tabelle SalesOrders: `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`. Weitere Informationen finden Sie in "Sortieren von Zeilen mit ORDER BY" in der [SQL Server-Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=98335).  
  
> [!NOTE]  
>  Nicht alle Datenquellen unterstützen die Möglichkeit, in der Abfrage die Sortierreihenfolge anzugeben.  
  
### <a name="sorting-data-with-sort-expressions"></a>Sortieren von Daten mit Sortierungsausdrücken  
 Wenn Sie Daten im Bericht sortieren möchten, nachdem diese aus der Datenquelle abgerufen wurden, können Sie Sortierungsausdrücke für einen Tablix-Datenbereich oder eine entsprechende Gruppe festlegen, einschließlich der Detailgruppe. Die folgende Liste beschreibt die Auswirkungen durch das Festlegen von Sortierungsausdrücken für verschiedene Elemente:  
  
-   **Tablix-Datenbereich.** Legen Sie Sortierungsausdrücke für eine Tabelle, eine Matrix oder einen Listendatenbereich fest, um die Sortierreihenfolge der Daten im Datenbereich zu steuern, nachdem Datasetfilter und Datenbereichsfilter zur Laufzeit angewendet wurden.  
  
-   **Tablix-Datenbereichsgruppe.** Legen Sie Sortierungsausdrücke für jede Gruppe, einschließlich der Detailgruppe, fest, um die Sortierreihenfolge von Gruppeninstanzen zu steuern. Zum Beispiel können Sie bei der Detailgruppe die Reihenfolge der Detailzeilen steuern. Bei einer untergeordneten Gruppe können Sie die Reihenfolge der Gruppeninstanzen für die untergeordnete Gruppe innerhalb der übergeordneten Gruppe steuern. Wenn Sie eine Gruppe erstellen, wird der Sortierungsausdruck standardmäßig auf den Gruppierungsausdruck und auf aufsteigende Reihenfolge festgelegt.  
  
     Bei nur einer Detailgruppe können Sie mit gleichem Ergebnis einen Sortierungsausdruck in der Abfrage, für den Datenbereich oder aber für die Detailgruppe definieren.  
  
-   **Diagrammdatenbereich.** Legen Sie einen Sortierungsausdruck für die Kategorie- und Reihengruppen fest, um die Sortierreihenfolge für Datenpunkte zu steuern. Standardmäßig ist die Reihenfolge der Datenpunkte mit der Reihenfolge der Farben in der Diagrammlegende identisch. Weitere Informationen finden Sie unter [Formatieren von Reihenfarben in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   **Kartenberichtselement.** Normalerweise müssen die Daten für einen Kartendatenbereich nicht sortiert werden, da die Karte für Kartenelemente anzuzeigende Daten gruppiert.  
  
-   **Messgerätdatenbereich.** Normalerweise müssen die Daten für einen Messgerätdatenbereich nicht sortiert werden, da auf dem Messgerät ein einzelner Wert in Bezug auf einen Bereich angezeigt wird. Wenn Sie die Daten eines Messgeräts dennoch sortieren müssen, definieren Sie zunächst eine Gruppe, und legen Sie dann einen Sortierungsausdruck für die Gruppe fest.  
  
#### <a name="sorting-by-a-different-value"></a>Sortieren nach einem anderen Wert  
 Möglicherweise möchten Sie die Zeilen in einem Datenbereich nach einem Wert als dem Feldwert sortieren. Angenommen, das Feld "Size" enthält Textwerte, die "Small", "Medium", "Large" und "Extra Large" entsprechen. Standardmäßig ist der Sortierungsausdruck für eine auf "Size" basierende Zeilengruppe ebenfalls [Size]. Sie können der Datasetabfrage ein Feld hinzufügen, das die gewünschte Sortierreihenfolge definiert, um die Sortierung der Daten besser steuern zu können.  
  
 Alternativ können Sie ein Dataset definieren, das nur die Größen und einen Wert zur Angabe der gewünschten Reihenfolge enthält. Sie können den Sortierungsausdruck ändern, um die Suchfunktion für den Sortierreihenfolgenwert zu verwenden.  
  
 Angenommen, die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage definiert ein Dataset mit dem Namen "Sizes". Die Abfrage definiert mithilfe einer CASE-Anweisung einen Sortierreihenfolgenwert "SizeSortOrder" für jeden Wert von "Size":  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 In einer Tabelle mit einer Zeilengruppe, die auf `[Size]`basiert, kann der Gruppensortierungsausdruck für die Verwendung einer Suchfunktion angepasst werden, um das numerische Feld zu suchen, das dem Größenwert entspricht. Der Ausdruck sieht in diesem Fall in etwa wie folgt aus:  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 Weitere Informationen finden Sie unter [Sortieren von Daten in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md) und [Lookup-Funktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md).  
  
###  <a name="Interactive"></a> Hinzufügen einer interaktiven Sortierung für den Benutzer  
 Wenn Sie es dem Benutzer ermöglichen möchten, die Sortierreihenfolge der Berichtsdaten in einer Tabelle oder Matrix zu ändern, können Sie Spaltenheadern oder Gruppenköpfen interaktive Sortierschaltflächen hinzufügen. Benutzer können auf die Schaltfläche klicken, um die Sortierreihenfolge umzuschalten. Die interaktive Sortierung wird in Renderingformaten unterstützt, die Benutzeraktionen zulassen, z. B. HTML.  
  
 Sie fügen einem Textfeld in einer Tablix-Datenbereichszelle interaktive Sortierschaltflächen hinzu. Standardmäßig enthält jede Zelle ein Textfeld. In den Eigenschaften des Textfelds geben Sie den zu sortierenden Teil eines Tabellen- oder Matrixdatenbereichs an (die Werte der übergeordneten Gruppe, die Werte der untergeordneten Gruppe oder die Detailzeilen), außerdem das Element, nach dem die Sortierung erfolgen soll, und ob der Sortierungsausdruck auf weitere Berichtselemente angewendet werden soll, mit denen eine Peerbeziehung besteht. Wenn beispielsweise eine Tabelle und ein Diagramm, die Sichten desselben Datasets bereitstellen, in einem Rechteck eingeschlossen sind, handelt es sich bei diesen um Peerdatenbereiche. Wenn ein Benutzer die Sortierreihenfolge der Tabelle umschaltet, wird die Sortierreihenfolge des Diagramms ebenfalls umgeschaltet. Weitere Informationen finden Sie unter [Interaktive Sortierung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 [Sichtbarhalten von Kopfzeilen beim Durchführen eines Bildlaufs durch einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [Anzeigen von Kopf- und Fußzeilen einer Gruppe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [Festlegen einer Meldung über fehlende Daten für einen Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Erstellen einer rekursiven Hierarchiegruppe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [Anzeigen von Kopf- und Fußzeilen einer Gruppe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Hinzufügen oder Löschen einer Gruppe in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [Hinzufügen eines Gesamtergebnisses zu einer Gruppe oder einem Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> In diesem Abschnitt  
 [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> Verwandte Abschnitte  
 [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [Erstellen von rekursiven Hierarchiegruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [Anzeigen einer Reihe mit mehreren Datenbereichen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [Verknüpfen mehrerer Datenbereiche mit einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Sparklines und Datenbalken (Berichts-Generator und SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
