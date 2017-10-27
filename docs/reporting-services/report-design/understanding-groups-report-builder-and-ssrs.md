---
title: Grundlegendes zu Gruppen (Berichts-Generator und SSRS) | Microsoft Docs
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
- "10056"
- "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 553bcb01f914c7b63afe3b20f93b790749cc30cf
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="understanding-groups-report-builder-and-ssrs"></a>Grundlegendes zu Gruppen (Berichts-Generator und SSRS)
  In einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht ist eine Gruppe ein benannter Satz von Daten aus dem Berichtsdataset, der an einen Datenbereich gebunden ist. Im Grunde wird mit einer Gruppe eine Sicht eines Berichtsdatasets organisiert. Alle Gruppen in einem Datenbereich geben unterschiedliche Sichten desselben Berichtsdatasets an.  
  
 Zur besseren Veranschaulichung einer Gruppe betrachten Sie die folgende Abbildung, in der der Tablix-Datenbereich in der Vorschau dargestellt ist. In dieser Abbildung kategorisieren die Zeilengruppen das Dataset nach Produkttyp, und die Spaltengruppen kategorisieren das Dataset nach geografischer Region und Jahr.  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 In den folgenden Abschnitten sind die verschiedenen Aspekte von Gruppen beschrieben.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="what-makes-a-group"></a>Wodurch ist eine Gruppe gekennzeichnet?  
 Eine Gruppe besitzt einen Namen und einen Satz von Gruppierungsausdrücken, den Sie festlegen. Der Satz von Gruppierungsausdrücken kann ein Verweis auf ein einzelnes Datasetfeld oder eine Kombination mehrerer Ausdrücke sein. Zur Laufzeit werden Gruppenausdrücke kombiniert, wenn die Gruppe mehrere Ausdrücke enthält, und für Daten in einer Gruppe angewendet. Angenommen, Sie verfügen über eine Gruppe, die die Daten im Datenbereich mithilfe eines Datumsfelds organisiert. Zur Laufzeit werden die Daten nach Datum angeordnet und dann mit dem Gesamtwerten anderer Datasetwerte für jedes Datum angezeigt.  
  
## <a name="when-do-i-create-groups"></a>Wann sollten Gruppen erstellt werden?  
 In den meisten Fällen erstellen Berichts-Generator und Berichts-Designer eine Gruppe automatisch, wenn Sie einen Datenbereich entwerfen. Für eine Tabelle, Matrix oder Liste werden Gruppen erstellt, wenn Sie Felder im Gruppierungsbereich ablegen. Für ein Diagramm werden Gruppen erstellt, wenn Sie Felder in den Diagrammablagezonen ablegen. Für ein Messgerät müssen Sie das Dialogfeld für die Messgeräteigenschaften verwenden. Für eine Tabelle, Matrix oder Liste können Sie eine Gruppe auch manuell erstellen. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md). Ein Beispiel zum Hinzufügen von Gruppen beim Erstellen eines Berichts finden Sie im [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md) oder unter [Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
## <a name="how-can-i-modify-a-group"></a>Wie kann eine Gruppe geändert werden?  
 Wenn Sie eine Gruppe erstellt haben, können Sie die datenbereichsspezifischen Eigenschaften festlegen, z. B. Filter- und Sortierungsausdrücke, Seitenumbrüche und Gruppierungsvariablen für bereichsspezifische Daten. Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Um eine vorhandene Gruppe zu ändern, öffnen Sie das entsprechende Dialogfeld für Gruppeneigenschaften. Sie können den Namen der Gruppe ändern. Außerdem können Sie anhand eines einzelnen Felds, mehrerer Felder oder anhand eines Berichtsparameters, der zur Laufzeit einen Wert angibt, Gruppierungsausdrücke angeben. Zudem kann eine Gruppe auf einem Satz von Ausdrücken beruhen, z. B. dem Satz von Ausdrücken, mit denen Altersgruppen für demografische Daten angegeben werden. Weitere Informationen finden Sie unter [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Wenn Sie den Namen einer Gruppe ändern, müssen Sie manuell sämtliche Gruppierungsausdrücke aktualisieren, die auf den früheren Namen der Gruppe verweisen.  
  
## <a name="how-are-groups-organized"></a>Wie werden Gruppen organisiert?  
 Kenntnisse zur Organisation von Gruppen sind nützlich, wenn Sie durch Angabe identischer Gruppierungsausdrücke Datenbereiche entwerfen, in denen unterschiedliche Sichten derselben Daten angezeigt werden.  
  
 Gruppen sind intern als Elemente einer oder mehrerer Hierarchien für jeden Datenbereich organisiert. Eine Gruppenhierarchie enthält übergeordnete/untergeordnete Gruppen, die geschachtelt sind und angrenzende Gruppen aufweisen können.  
  
 Wenn Sie sich übergeordnete/untergeordnete Gruppen als Baumstruktur vorstellen, entspricht jede Gruppenhierarchie einer Gesamtstruktur von Baumstrukturen. Tablix-Datenbereiche enthalten eine Hierarchie von Zeilengruppen und eine Hierarchie von Spaltengruppen. Zeilengruppenelementen zugeordnete Daten werden horizontal über die Seite erweitert, und Spaltengruppenelementen zugeordnete Daten werden vertikal die Seite hinunter erweitert. Im Gruppierungsbereich werden Zeilengruppen- und Spaltengruppenelemente für den derzeit ausgewählten Tablix-Datenbereich auf der Entwurfsoberfläche angezeigt. Weitere Informationen finden Sie unter [Gruppierungsbereich &#40;Berichts-Generator&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md).  
  
 Diagrammdatenbereiche enthalten eine Hierarchie von Kategoriegruppen und eine Hierarchie von Reihengruppen. Kategoriegruppenelemente werden auf der Kategorieachse und Reihengruppenelemente auf der Reihenachse angezeigt.  
  
 Zwar sind Gruppen für Messgerätdatenbereiche meist nicht erforderlich, doch können Sie mit deren Hilfe angeben, wie Daten gruppiert werden sollen, die für das Messgerät aggregiert werden.  
  
## <a name="what-types-of-groups-are-available-per-data-region"></a>Welche Typen von Gruppen sind pro Datenbereich verfügbar?  
 Datenbereiche, die als Raster erweitert werden, unterstützen andere Gruppen als Datenbereiche, in denen visuell Zusammenfassungsdaten angezeigt werden. Tablix-Datenbereiche sowie die auf Tablix-Datenbereichen basierenden Tabellen, Listen und Matrizen unterstützen andere Gruppen als Diagramme oder Messgeräte. In den folgenden Abschnitten werden Typ und Zweck der Gruppierung in den einzelnen Typen von Datenbereichen erläutert.  
  
> [!NOTE]  
>  Zwar besitzen Gruppen in unterschiedlichen Datenbereichen unterschiedliche Namen, doch sind die Prinzipien der Erstellung und Verwendung von Gruppen gleich. Wenn Sie eine Gruppe für einen Datenbereich erstellen, geben Sie eine Möglichkeit an, die Detaildaten aus dem mit dem Datenbereich verknüpften Dataset zu organisieren. Jeder Datenbereich unterstützt eine Gruppenstruktur, in der gruppierte Daten angezeigt werden können.  
  
### <a name="groups-in-a-tablix-data-region-details-row-and-column-groups"></a>Gruppen in einem Tablix-Datenbereich: Detail-, Zeilen- und Spaltengruppen  
 Wie in diesem Thema bereits dargestellt, ermöglichen es Tablix-Datenbereiche, Daten nach Zeilen oder Spalten in Gruppen zu organisieren. Zeilen- und Spaltengruppen sind jedoch nicht die einzigen in einem Tablix-Datenbereich verfügbaren Gruppen. Dieser Datenbereich kann die folgenden Typen von Gruppen aufweisen:  
  
-   **Gruppe "Details"** Die Detailgruppe besteht aus sämtlichen Daten, die in einem Berichtsdataset enthalten sind, nachdem Dataset- und Datenbereichsfilter von Berichts-Generator oder Berichts-Designer angewendet wurden. Die Gruppe Details ist daher die einzige Gruppe, die keinen Gruppierungsausdruck besitzt.  
  
     Im Grunde gibt die Detailgruppe die Daten an, die angezeigt werden, wenn Sie in einem Abfrage-Designer eine Datasetabfrage ausführen. Angenommen, Sie verfügen über eine Abfrage, mit der alle Spalten in einer Tabelle mit Bestellungen abgerufen werden. Die Daten in dieser Detailgruppe enthalten dann sämtliche Werte für jede Zeile für alle Spalten in der Tabelle. Die Daten in dieser Detailgruppe enthalten außerdem die Werte für alle berechneten Datasetfelder, die Sie erstellt haben.  
  
    > [!NOTE]  
    >  Die Daten in einer Detailgruppe können auch Serveraggregate enthalten, d. h. Aggregate, die für die Datenquelle berechnet und in der Abfrage abgerufen werden. Standardmäßig behandeln Berichts-Generator und Berichts-Designer Serveraggregate als Detaildaten, sofern der Bericht keinen Ausdruck enthält, für den die „Aggregate“-Funktion verwendet wird. Weitere Informationen finden Sie unter [Aggregat](../../reporting-services/report-design/report-builder-functions-aggregate-function.md).  
  
     Wenn Sie einem Bericht eine Tabelle oder Liste hinzufügen, erstellen Berichts-Generator und Berichts-Designer automatisch die Gruppe Details und fügen eine Zeile hinzu, in der die Detaildaten angezeigt werden. Wenn Sie Zellen in dieser Zeile Datasetfelder hinzufügen, werden standardmäßig einfache Ausdrücke für die Felder angezeigt, z. B. [Sales]. Wenn Sie den Datenbereich anzeigen, wird die Detailzeile für jeden Wert im Resultset einmal wiederholt.  
  
-   **Zeilengruppen und Spaltengruppen** Sie können Daten nach Zeilen oder Spalten in Gruppen organisieren. Zeilengruppen werden vertikal auf einer Seite erweitert. Spaltengruppen werden horizontal auf einer Seite erweitert. Gruppen können geschachtelt werden, z. B., können Sie diese zuerst nach [Year], dann nach [Quarter] und dann nach [Month] gruppieren. Gruppen können auch aneinander grenzen, z. B. können Sie die Gruppierung nach [Territory] und unabhängig davon nach [ProductCategory] vornehmen.  
  
     Wenn Sie eine Gruppe für einen Datenbereich erstellen, fügen Berichts-Generator und Berichts-Designer dem Datenbereich automatisch Zeilen oder Spalten hinzu und verwenden diese Zeilen oder Spalten für die Anzeige von Gruppendaten.  
  
-   **Rekursive Hierarchiegruppen** In einer rekursiven Hierarchiegruppe sind Daten aus einem einzelnen Berichtsdataset organisiert, das mehrere Ebenen enthält. In einer rekursiven Hierarchiegruppe kann eine Organisationshierarchie angezeigt werden, z. B. [Employee], der an [Employee] berichtet. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt Gruppeneigenschaften und integrierte Funktionen bereit, mit denen Sie Gruppen für diese Art von Berichtsdaten erstellen können. Weitere Informationen finden Sie unter [Erstellen von rekursiven Hierarchiegruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
 Die folgende Liste fasst die Methoden für die Arbeit mit Gruppen für die einzelnen Datenbereiche zusammen:  
  
-   **Tabelle** Sie können geschachtelte Zeilengruppen, angrenzende Zeilengruppen und rekursive Hierarchiegruppen (z.B. für ein Organigramm) definieren. In einer Tabelle ist standardmäßig eine Detailgruppe enthalten. Fügen Sie Gruppen hinzu, indem Sie Datasetfelder in den Gruppierungsbereich für eine ausgewählte Tabelle ziehen.  
  
-   **Matrix** Sie können geschachtelte Zeilen- und Spaltengruppen sowie angrenzende Zeilen- und Spaltengruppen definieren. Fügen Sie Gruppen hinzu, indem Sie Datasetfelder in den Gruppierungsbereich für eine ausgewählte Matrix ziehen.  
  
-   **Liste** Unterstützt standardmäßig die Detailgruppe. Wird meist für die Unterstützung einer Gruppierungsebene verwendet. Fügen Sie Gruppen hinzu, indem Sie Datasetfelder in den Gruppierungsbereich für eine ausgewählte Liste ziehen.  
  
 Wenn Sie eine Gruppe hinzugefügt haben, werden die Zeilen- und Spaltenhandles des Datenbereichs so geändert, dass sie die Gruppenmitgliedschaft wiedergeben. Beim Löschen einer Gruppe können Sie entweder nur die Gruppendefinition oder die Gruppe und alle zugeordneten Zeilen und Spalten löschen. Weitere Informationen finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Zum Einschränken der Daten, die angezeigt oder in Berechnungen für Detail- oder Gruppendaten verwendet werden sollen, legen Sie für die Gruppe Filter fest. Weitere Informationen finden Sie unter [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Wenn Sie eine Gruppe erstellen, ist der Sortierungsausdruck für die Gruppe mit dem Gruppierungsausdruck identisch. Um die Sortierreihenfolge zu ändern, ändern Sie den Sortierungsausdruck. Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
#### <a name="understanding-group-membership-for-tablix-cells"></a>Grundlegendes zur Gruppenmitgliedschaft für Tablix-Zellen  
 Zellen in einer Zeile oder Spalte eines Tablix-Datenbereichs können zu mehreren Zeilen- und Spaltengruppen gehören. Wenn Sie einen Ausdruck im Textfeld einer Zelle definieren, für die eine Aggregatfunktion verwendet wird (z. B. `=Sum(Fields!FieldName.Value`), ist der Standardgruppenbereich für eine Zelle die innerste untergeordnete Gruppe, zu der dieser gehört. Wenn eine Zelle zu Zeilen- und zu Spaltengruppen gehört, besteht der Bereich aus beiden innersten Gruppen. Sie können auch Ausdrücke erstellen, mit denen Aggregatteilergebnisse berechnet werden, die relativ zu einer anderen Datenmenge zu einer Gruppe zusammengefasst werden. Beispielsweise können Sie den Prozentsatz einer Gruppe relativ zur Spaltengruppe oder zu allen Daten für den Datenbereich berechnen (z. B. `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`). Weitere Informationen finden Sie unter [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Hinzufügen eines Gesamtergebnisses zu einer Gruppe oder einem Tablix-Datenbereich &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [Sortieren von Daten in einem Datenbereich &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Drilldownaktion &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

