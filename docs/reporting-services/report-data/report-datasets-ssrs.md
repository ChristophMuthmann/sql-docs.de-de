---
title: Berichts-Datasets (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b455aded926c073e3992165a35fb6b938b66e2de
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="report-datasets-ssrs"></a>Berichtsdatasets (SSRS)
  Um einem Bericht Daten hinzuzufügen, erstellen Sie Datasets. Jedes Dataset stellt das Resultset der Ausführung eines Abfragebefehls für eine Datenquelle dar. Die Spalten im Resultset sind die Feldauflistung. Die Zeilen im Resultset sind die Daten. Ein Dataset enthält nicht die tatsächlichen Daten. Es enthält die Informationen, die benötigt werden, um einen bestimmten Satz von Daten aus einer Datenquelle abzurufen.  
  
 Zwei Typen von Datasets werden unterschieden: eingebettet und freigegeben. Ein eingebettetes Dataset wird im Bericht definiert und nur von diesem Bericht verwendet. Ein freigegebenes Dataset wird auf dem Berichtsserver oder einer SharePoint-Website definiert und kann von mehreren Berichten verwendet werden. Im Berichts-Generator können Sie im Modus "Freigegebenes Dataset" freigegebene Datasets oder im Modus "Berichts-Designer" eingebettete Datasets erstellen. Im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können freigegebene Datasets als Teil eines Projekts oder eingebettete Datasets als Teil eines Berichts erstellt werden.  
  
-   **Eingebettete Datasets.** Anders als in Anwendungen wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel, in denen Sie direkt in einem Arbeitsblatt mit Daten arbeiten, arbeiten Sie im Berichts-Generator oder Berichts-Designer mit Metadaten, die die beim Verarbeiten des Berichts abgerufenen Daten darstellen. Um ein eingebettetes Dataset zu erstellen, wählen Sie die Quelle der Daten aus, und geben Sie eine Abfrage an. Nachdem Sie das Dataset erstellt haben, zeigen Sie im Berichtsdatenbereich die Feldauflistung an. Sie können Daten aus einem Dataset in einem Datenbereich wie einer Tabelle oder einem Diagramm anzeigen. In jedem Datenbereich können Sie die Daten gruppieren, filtern und sortieren, um sie zu organisieren. Nachdem Sie das Berichtslayout entworfen haben, führen Sie den Bericht aus, um die tatsächlichen Daten anzuzeigen.  
  
     In der folgenden Abbildung werden im Berichtsdatenbereich eine Datenquelle mit dem Namen [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)], ein Dataset namens "DataSet1" und fünf Felder in der Datasetfeldauflistung angezeigt. Im Layoutbereich wird eine Tabelle mit Spaltenüberschriften in der obersten Zeile und Tabellenzellen mit Text in der untersten Zeile angezeigt. Der Platzhaltertext [Name] stellt die Metadaten für das Namensfeld dar. Wenn der Bericht ausgeführt wird, wird der Platzhaltertext durch die tatsächlichen Datenwerte ersetzt. Die Tabelle wird entsprechend erweitert, um alle Daten anzuzeigen.  
  
     ![rs_DatendesignundVorschau](../../reporting-services/report-data/media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **Freigegebene Datasets.** Erstellen Sie ein freigegebenes Dataset, wenn Sie ein Dataset in mehreren Berichten verwenden möchten. In der Entwurfsansicht für freigegebene Datasets des Berichts-Generators können Sie ein freigegebenes Dataset erstellen und auf einem Berichtsserver oder auf einer SharePoint-Website speichern. Um ein freigegebenes Dataset als Teil eines Projekts zu erstellen, das auf einem Server oder einer Website bereitgestellt werden kann, verwenden Sie den Berichts-Designer.  
  
     Die folgende Abbildung zeigt die Entwurfsansicht für freigegebene Datasets im Berichts-Generator. Sie können die Datenverbindung, die Dataseteigenschaften, die Abfrage und Filter auswählen bzw. ändern, Filter optional als Parameter markieren und die Abfrageergebnisse anzeigen. Anschließend speichern Sie die Änderungen auf dem Server oder der Website.  
  
     ![rs_FreigegebenesDatasetEntwurfsmodus](../../reporting-services/report-builder/media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Weitere Informationen finden Sie unter [Eingebettete und freigegebene Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md) und [Eingebettete und freigegebene Datenverbindungen oder Datenquellen &#40;Berichts-Generator und SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56).  
  
 Sie können einem Bericht auch Datasets hinzufügen, indem Sie Berichtsteile mit den Datasets hinzufügen, von denen sie abhängig sind. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 Eine Anleitung zum Erstellen eines Berichts, der Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank anzeigt, finden Sie unter [Tutorial: Erstellen eines einfachen Tabellenberichts (Berichts-Generator)](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md). Informationen zum Erstellen eines Berichts, der seine eigenen Daten enthält, finden Sie unter [Tutorial: Erstellen eines Quick-Diagrammberichts offline &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Methods"></a> Hinzufügen von Berichtsdaten  
 Im Berichts-Generator stehen Ihnen folgende Möglichkeiten zum Hinzufügen von Berichtsdaten zur Verfügung.  
  
-   Fügen Sie dem Bericht Berichtsteile von einem Berichtsserver hinzu. Jeder Berichtsteil ist in sich abgeschlossen und schließt abhängige Datasets ein. Die Datasets sind vordefiniert.  
  
-   Verwenden Sie die Assistenten für Tabellen/Matrizen, Diagramme und Karten. Mithilfe der Assistenten können Sie freigegebene Datenquellen und freigegebene Datasets auswählen oder neue Datsets erstellen und mit dem Entwurf des Berichts beginnen.  
  
-   Fügen Sie freigegebene Datasets von einem Berichtsserver hinzu. Freigegebene Datasets sind vordefiniert und geben an, welche Daten aus einer vordefinierten Datenquelle verwendet werden sollen. Wenn Sie dem Bericht ein freigegebenes Dataset hinzufügen, fügen Sie einen Datasetverweis hinzu, der auf die Definition des freigegebenen Datasets verweist.  
  
 Im Berichts-Generator oder Berichts-Designer stehen Ihnen folgende Möglichkeiten zum Hinzufügen von Daten zur Verfügung.  
  
-   Fügen Sie eingebettete Datasets hinzu, die auf freigegebenen Datenquellen basieren.  
  
-   Fügen Sie eingebettete Datasets hinzu, die auf eingebetteten Datenquellen basieren.  
  
> [!NOTE]  
>  Auf einem Berichtsserver werden freigegebene Elemente einzeln oder durch Vererbung der Berechtigungen des Ordners, in dem sie veröffentlicht werden, gesichert. Damit andere Benutzer auf die von Ihnen gespeicherten freigegebenen Datasets zugreifen können, müssen Sie verstehen, wie Berechtigungen gewährt werden. Weitere Informationen finden Sie unter [Sicherheit (Berichts-Generator)](../../reporting-services/report-builder/security-report-builder.md) oder [Sichern von freigegebenen Datasetelementen](../../reporting-services/security/secure-shared-dataset-items.md).  
  
 Nachdem Sie einem Bericht Daten hinzugefügt haben, können Sie die Daten auf der Berichtsseite anhand von Datenbereichen organisieren, Berichtsteile ändern und diese Änderungen für andere freigeben sowie Benutzern das Einschränken oder Sortieren der im Bericht angezeigten Daten ermöglichen. Weitere Informationen finden Sie in folgenden verwandten Themen:  
  
-   [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
-   [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
-   [Sparklines und Datenbalken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
-   [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)  
  
-   [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
##  <a name="QuickStart"></a> Hinzufügen von Daten mit Berichtsteilen  
 Berichtsteile enthalten die Datasets, von denen sie abhängen. Diese Datasets werden basierend auf freigegebenen Datenquellen erstellt, die auf dem Berichtsserver verfügbar sind. Wenn Sie dem Bericht im Berichts-Generator einen Berichtsteil hinzufügen, werden die abhängigen Datasets dem Bericht hinzugefügt (ähnlich wie beim manuellen Hinzufügen). Ein vordefiniertes Diagramm enthält z.B. ein Dataset. Zeigen Sie eine Vorschau des Berichts an, um die Daten anzuzeigen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 Berichtsteile, freigegebene Datenquellen und freigegebene Datasets werden vorab definiert und auf einem Berichtsserver gespeichert. Für den Zugriff auf diese Elemente müssen Sie den Berichts-Generator im Servermodus öffnen, indem Sie eine Verbindung mit dem Berichtsserver herstellen. Sie können eigene neue Versionen erstellen, wenn Sie über Schreibberechtigungen für den Berichtsserver verfügen.  
  
-   Weitere Informationen finden Sie unter [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) und [Berichtsteile im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
  
##  <a name="Queries"></a> Abfragen und Abfrage-Designer  
 Zum Angeben der Daten, die Sie aus einer Datenquelle abrufen möchten, erstellen Sie einen Abfragebefehl. Jeder Datenquellentyp stellt einen zugehörigen *Abfrage-Designer* bereit, mit dessen Hilfe Sie die Abfrage erstellen können. Der Abfrage-Designer kann grafisch oder textbasiert sein. In einem grafischen Abfrage-Designer zeigen Sie Metadaten an, die die Daten in der externen Datenquelle darstellen, und erstellen durch Ziehen von Feldern oder Entitäten in die Abfrageentwurfsoberfläche interaktiv eine Abfrage. In einem textbasierten Abfrage-Designer schreiben oder importieren Sie Abfragen in der Abfragesyntax, die von der externen Datenquelle unterstützt wird.  
  
 Im Abfrage-Designer können Sie die Abfrage ausführen, um Beispieldaten anzuzeigen und die Abfragebefehlssyntax zu überprüfen. Spaltennamen im Resultset werden die Feldnamen, die im Berichtsdatenbereich angezeigt werden. Das Resultset muss ein einzelner Satz von Zeilen und Spalten sein, der die gleiche Anzahl von Werten für jede Datenzeile aufweist. Mehrere Resultsets aus einer einzelnen Abfrage werden nicht unterstützt. Unregelmäßige Hierarchien, die keine konstante Anzahl von Spalten enthalten und für jede Zeile eine andere Anzahl von Datenwerten erzeugen können, werden nicht unterstützt.  
  
 Sie benötigen Entwurfszeitanmeldeinformationen, um eine Abfrage auszuführen. Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53) und [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen (Berichts-Generator und SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Die Kommunikation zwischen einer Datenerweiterung und der externen Datenquelle wird von Datenanbietern behandelt. Die Unterstützung der Abfragebefehlssyntax, Abfrageparameter und Datentypen für Werte im Resultset wird von den einzelnen Datenanbietern bestimmt. Weitere Informationen finden Sie im Thema zum jeweiligen Datenerweiterungstyp und unter [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9).  
  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [Erstellen einer Abfrage im relationalen Abfrage-Designer &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [Anzeigen von ausgeblendeten Datasets für Parameterwerte für mehrdimensionale Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [Hinzufügen eines Filters zu einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [Festlegen einer Meldung über fehlende Daten für einen Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Zuordnen eines Abfrageparameters zu einem Berichtsparameter &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [Definieren von Parametern im MDX-Abfrage-Designer für Analysis Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  
  
  
##  <a name="Section"></a> In diesem Abschnitt  
 [Berichtsteile und Datasets in Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)  
  
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
  
 [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)  
  
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [Datasetfeld-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsentwurfsansicht &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Berichtserstellungskonzepte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
  
  
