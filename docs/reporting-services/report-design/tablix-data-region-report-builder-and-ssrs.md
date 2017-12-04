---
title: Tablix-Datenbereich (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 49d872c920e735ffa2b1891f09c16e2738518b69
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Tablix-Datenbereich (Berichts-Generator und SSRS)
  Der Tablix-Datenbereich ist in [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]ein Berichtselement mit verallgemeinertem Layout, in dem paginierte Berichtsdaten in Zellen angezeigt werden, die in Zeilen und Spalten organisiert sind. Bei den Berichtsdaten kann es sich um aus der Datenquelle abgerufene Detaildaten oder in benutzerdefinierten Gruppen organisierte aggregierte Detaildaten handeln. Jede Tablix-Zelle kann ein beliebiges Berichtselement enthalten, z. B. ein Textfeld, ein Bild oder einen anderen Datenbereich (z. B. einen Tablix-Bereich, ein Diagramm oder ein Messgerät). Wenn Sie einer Zelle mehrere Berichtselemente hinzufügen möchten, erstellen Sie zuerst ein Rechteck, das als Container fungiert. Anschließend fügen Sie dem Rechteck Berichtselemente hinzu.  
  
 Die Tabellen-, Matrix- und Listendatenbereiche werden auf dem Menüband durch Vorlagen für den zugrunde liegenden Tablix-Datenbereich dargestellt. Wenn Sie einem Bericht eine dieser Vorlagen hinzufügen, fügen Sie tatsächlich einen Tablix-Datenbereich hinzu, der für ein spezifisches Datenlayout optimiert ist. Standardmäßig werden von einer Tabellenvorlage Detaildaten in einem Gitternetzlayout angezeigt, während eine Matrix Gruppendaten in einem Gitternetzlayout und eine Liste Detaildaten in einem Freiformlayout anzeigt.  
  
 Jede Tablix-Zelle in einer Tabelle oder Matrix enthält standardmäßig ein Textfeld. Die Zelle in einer Liste enthält ein Rechteck. Sie können ein Standardberichtselement durch ein anderes Berichtselement ersetzen, z. B. durch ein Bild.  
  
 Beim Definieren von Gruppen für eine Tabelle, Matrix oder Liste fügen Berichts-Generator und Berichts-Designer dem Tablix-Datenbereich Zeilen und Spalten hinzu, in denen die gruppierten Daten angezeigt werden.  
  
 Folgende Kenntnisse sind für das Verständnis des Tablix-Datenbereichs hilfreich:  
  
*   Der Unterschied zwischen Detaildaten und gruppierten Daten  
  
*   Gruppen, die als Zeilengruppen auf der horizontalen Achse und als Spaltengruppen auf der vertikalen Achse als Elemente von Gruppenhierarchien organisiert sind.  
  
*  Der Zweck von Tablix-Zellen in den vier Bereichen eines Tablix-Datenbereichs: Text, Kopfzeilen von Zeilengruppen, Kopfzeilen von Spaltengruppen und Ecke  
  
*  Statische und dynamische Zeilen und Spalten sowie deren Beziehung zu Gruppen  
  
 Dieser Artikel beschreibt diese Konzepte zur Erklärung der Struktur, die vom Berichts-Generator und vom Berichts-Designer hinzugefügt werden, wenn Sie Vorlagen hinzufügen und Gruppen erstellen, damit Sie die Struktur entsprechend Ihren Anforderungen ändern können. Berichts-Generator und Berichts-Designer stellen eine Reihe von visuellen Indikatoren bereit, die Ihnen das Verständnis der Tablix-Datenbereichsstruktur erleichtern. Weitere Informationen finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>Grundlegendes zu Detaildaten und gruppierten Daten  
 Detaildaten sind sämtliche Daten aus einem Berichtsdataset, die von der Datenquelle zurückgegeben werden. Detaildaten sind im Wesentlichen die Daten, die beim Ausführen einer Datasetabfrage im Ergebnisbereich des Abfrage-Designers angezeigt werden. Zu den tatsächlichen Detaildaten zählen die vom Benutzer erstellten berechneten Felder. Sie werden durch Filter beschränkt, die für das Dataset, den Datenbereich und die Detailgruppe festgelegt sind. Detaildaten werden in einer Detailzeile mithilfe eines einfachen Ausdrucks angezeigt, z. B. [Quantity]. Beim Ausführen des Berichts wird die Detailzeile zur Laufzeit in den Abfrageergebnissen einmal pro Zeile wiederholt.  
  
 Gruppierte Daten sind Detaildaten, die anhand eines Werts organisiert werden, den Sie in der Gruppendefinition angeben, z.B. [SalesOrder]. Gruppierte Daten werden in Gruppenzeilen und -spalten mithilfe einfacher Ausdrücke angezeigt, durch die die gruppierten Daten aggregiert werden, z. B. [Sum(Quantity)]. Weitere Informationen finden Sie unter [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-group-hierarchies"></a>Grundlegendes zu Gruppenhierarchien  
 Gruppen sind als Elemente von Gruppenhierarchien organisiert. Hierarchien von Zeilengruppen und Spaltengruppen sind identische Strukturen auf unterschiedlichen Achsen. Stellen Sie sich vor, dass Zeilengruppen auf der Seite nach unten und Spaltengruppen quer über die Seite erweitert werden.  
  
 Eine Baumstruktur stellt geschachtelte Zeilen- und Spaltengruppen mit einer Über-/Unterordnungsbeziehung dar, z. B. eine Kategorie mit Unterkategorien. Die übergeordnete Gruppe stellt den Stamm der Struktur dar, während die untergeordneten Gruppen ihre Verzweigungen bilden. Gruppen können auch eine unabhängige Beziehung angrenzender Elemente aufweisen, z. B. Umsatz nach Gebiet oder Umsatz nach Jahr. Mehrere nicht miteinander verknüpfte Strukturhierarchien werden als Gesamtstruktur bezeichnet. In einem Tablix-Datenbereich werden Zeilengruppen und Spaltengruppen jeweils als unabhängige Gesamtstruktur dargestellt. Weitere Informationen finden Sie unter [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-tablix-data-region-areas"></a>Grundlegendes zu Tablix-Datenbereichen  
 Ein Tablix-Datenbereich enthält vier mögliche Bereiche für Zellen: die Tablix-Ecke, die Tablix-Zeilengruppenhierarchie, die Tablix-Spaltengruppenhierarchie und den Tablix-Text. Der Tablix-Text ist immer vorhanden. Die anderen Bereiche sind optional.  
  
 In den Zellen im Tablix-Textbereich werden Detail- und Gruppendaten angezeigt.  
  
 Zellen im Zeilengruppenbereich werden beim Erstellen einer Zeilengruppe automatisch erstellt. Dabei handelt es sich um Zellen in Zeilengruppen-Kopfzeilen, in denen standardmäßig Werte von Zeilengruppeninstanzen angezeigt werden. Wenn Sie beispielsweise nach [SalesOrder] gruppieren, sind die Gruppeninstanzwerte die einzelnen Bestellungen, nach denen gruppiert wird.  
  
 Zellen im Spaltengruppenbereich werden beim Erstellen einer Spaltengruppe automatisch erstellt. Dabei handelt es sich um Zellen in Spaltengruppen-Kopfzeilen, in denen standardmäßig Werte von Spaltengruppeninstanzen angezeigt werden. Wenn Sie z. B. nach [Year] gruppieren, sind die Gruppeninstanzwerte die einzelnen Jahre, nach denen gruppiert wird.  
  
 Zellen im Tablix-Eckbereich werden automatisch erstellt, wenn sowohl Zeilengruppen als auch Spaltengruppen definiert wurden. In Zellen in diesem Bereich können Bezeichnungen angezeigt werden. Sie können die Zellen jedoch auch zusammenführen und einen Titel erstellen.  
  
 Weitere Informationen finden Sie unter [Zonen des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>Grundlegendes zu statischen und dynamischen Zeilen und Spalten  
 In einem Tablix-Datenbereich werden Zellen in Zeilen und Spalten organisiert, die Gruppen zugeordnet sind. Gruppenstrukturen für Zeilengruppen und Spalten sind identisch. In diesem Beispiel werden Zeilengruppen verwendet, die gleichen Konzepte gelten aber auch für Spaltengruppen.  
  
 Eine Zeile ist entweder statisch oder dynamisch. Eine statische Zeile ist keiner Gruppe zugeordnet. Beim Ausführen des Berichts wird eine statische Zeile einmal gerendert. Kopf- und Fußzeilen von Tabellen sind statische Zeilen. In statischen Zeilen werden Bezeichnungen und Gesamtwerte angezeigt. Zellen in einer statischen Zeile sind auf den Datenbereich beschränkt.  
  
 Eine dynamische Zeile ist einer oder mehreren Gruppen zugeordnet. Eine dynamische Zeile wird für jeden eindeutigen Gruppenwert für die innerste Gruppe einmal gerendert. Der Gültigkeitsbereich von Zellen in einer dynamischen Zeile ist auf die innerste Zeilengruppe und die innerste Spaltengruppe festgelegt, zu denen die Zelle gehört.  
  
 Dynamische Detailzeilen sind der Detailgruppe zugeordnet, die automatisch erstellt wird, wenn Sie der Entwurfsoberfläche eine Tabelle oder Liste hinzufügen. Definitionsgemäß ist die Detailgruppe für einen Tablix-Datenbereich die innerste Gruppe. In Zellen in Detailzeilen werden Detaildaten angezeigt.  
  
 Dynamische Gruppenzeilen werden erstellt, wenn Sie einem vorhandenen Tablix-Datenbereich eine Zeilengruppe oder Spaltengruppe hinzufügen. In Zellen in dynamischen Gruppenzeilen werden aggregierte Werte für den Standardbereich angezeigt.  
  
 Durch die Funktion Gesamtergebnis hinzufügen wird automatisch eine Zeile außerhalb der aktuellen Gruppe erstellt, in der Werte angezeigt werden, die im Bereich der Gruppe liegen. Sie können statische und dynamische Zeilen auch manuell hinzufügen. Anhand von visuellen Indikatoren können Sie statische Zeilen von dynamischen Zeilen unterscheiden. Weitere Informationen finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verknüpfen mehrerer Datenbereiche mit einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Steuern der Tablix-Datenbereichsanzeige auf einer Berichtsseite (Berichts-Generator und SSRS)](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [Untersuchen der Flexibilität eines Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
