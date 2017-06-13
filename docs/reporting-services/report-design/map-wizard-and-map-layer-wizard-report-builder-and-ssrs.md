---
title: Karten-Assistent und Kartenebenen-Assistent (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.mapandlayerwizard.f1
- "10542"
- MICROSOFT.REPORTDESIGNER.MAPLAYER.NAME
ms.assetid: 48cbe18b-1290-4107-8a1c-ec6acd71f73b
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8eb09925e1f1b1e1f79cc9e9b7e3fdd56d7ed165
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="map-wizard-and-map-layer-wizard-report-builder-and-ssrs"></a>Karten-Assistent und Kartenebenen-Assistent (Berichts-Generator und SSRS)
 In paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichten automatisieren der Karten-Assistent und der Kartenebenen-Assistent das Erstellen einer Karte, Hinzufügen einer Kartenebene oder Ändern der Kartenebenen auf einer vorhandenen Ebene.  
  
 Bevor Sie einem Bericht eine Karte oder einer Karte eine Kartenebene hinzufügen, sammeln Sie die folgenden Informationen:  
  
-   **Räumliche Datenquelle.** Der Speicherort oder die Verbindung zu einer Quelle, die räumliche Daten bereitstellt, z.B. der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz und einer Datenbank, die räumliche Daten enthält, oder der Name einer Shape-Datei vom Environmental Systems Research Institute, Inc. ESRI-Shape-Datei (ESRI Shapefile)  
  
-   **Spatial data.** Ein Feld aus der räumlichen Datenquelle, das Sätze von Koordinaten enthält, die Standorte angeben.  
  
-   **Analytische Daten.** Analytische Daten, die verwendet werden sollen, um die Kartenanzeige zu verändern, wie z. B. der Jahresumsatz pro Laden.  
  
-   **Übereinstimmungsfelder.** Übereinstimmungsfelder, die die Beziehung zwischen räumlichen Daten und analytischen Daten definieren, z. B. der Name eines Bereichs und einer Stadt als eindeutige Identifikation jeder Stadt.  
  
 Die folgenden Abschnitte enthalten Informationen zu Optionen, die Sie im Karten- und Kartenebenen-Assistenten angeben.  
  
-   Öffnen Sie den Berichts-Generator, und klicken Sie auf das Assistentensymbol **Karte** in der Mitte der Entwurfsoberfläche.  
  
-   Klicken Sie auf der Registerkarte **Einfügen** auf **Karte**und dann auf **Karten-Assistent**.  
  
 Um den Kartenebenen-Assistenten zu öffnen, führen Sie die folgende Aktion aus:  
  
-   Klicken Sie auf die Karte, um den Kartenbereich anzuzeigen, und klicken Sie auf der Symbolleiste auf die Schaltfläche **Assistent für neue Ebenen** .  
  
 Klicken Sie auf den Titel der Assistentenseite, um den entsprechenden Hilfeinhalt anzuzeigen. Die angezeigten Seiten hängen von der Auswahl für den Kartentyp, der Quelle der räumlichen Daten und der Quelle der analytischen Daten ab.  
  
1.  [Quelle räumlicher Daten auswählen](#SpatialDataSource). Räumliche Daten können aus dem Kartenkatalog, aus einer Shape-Datei des Environmental Systems Research Institute, Inc. (ESRI) oder aus räumlichen Daten in einer relationalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank stammen.  
  
    -   [Was sind räumliche Daten?](#SpatialData)  
  
    -   [Was ist der Kartenkatalog?](#MapGallery)  
  
    -   [Was ist eine ESRI-Shape-Datei?](#Shapefile)  
  
    -   [Wo finde ich ESRI-Shape-Dateien?](#GetShapefiles)  
  
    -   [Was ist eine SQL Server-Abfrage nach räumlichen Daten?](#SqlServerSpatial)  
  
2.  [Optionen für räumliche Daten und Kartenansicht auswählen](#MapView). Legen Sie die Kartenansicht und die Kartenauflösung fest, und geben Sie an, ob räumliche Daten in den Bericht eingebettet werden sollen sowie ob ein Kachelhintergrund aus [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing-Kartenkacheln eingeschlossen werden soll.  
  
    -   [Was ist die Kartenansicht oder der Viewport?](#Viewport)  
  
    -   [Was ist Kartenauflösung oder Optimierung?](#Resolution)  
  
    -   [Was wird bei der Einbettung räumlicher Daten ausgeführt?](#Embed)  
  
    -   [Was ist ein Hintergrund aus Bing-Kartenkacheln?](#Tiles)  
  
3.  [Kartenvisualisierung auswählen](#Visualization). Wählen Sie den Typ der Karte aus, die erstellt werden soll.  
  
    -   [Was ist der Unterschied zwischen einer Standardkarte, einer Blasendiagrammkarte und einer analytischen Karte?](#MapType)  
  
    -   Kartenvisualisierung auswählen: Polygone  
  
    -   Kartenvisualisierung auswählen: Linien  
  
    -   Kartenvisualisierung auswählen: Punkte  
  
4.  Auswählen einer Verbindung mit einer Datenquelle für „Kartenvisualisierung auswählen: Punkte“. Wählen Sie eine Datenquellenverbindung aus, oder erstellen Sie eine Verbindung zu einer externen Datenquelle mit analytischen Daten, die auf der Karte angezeigt werden sollen.  
  
5.  Entwerfen Sie eine Abfrage. Erstellen Sie eine Abfrage, die die analytischen Daten angibt.  
  
6.  [Analytisches Dataset auswählen](#AnalyticalData). Geben Sie eine Datenquelle für die analytischen Daten an.  
  
    -   [Was ist der Unterschied zwischen räumlichen Daten und analytischen Daten?](#Diff)  
  
7.  [Übereinstimmende Felder für räumliche und analytische Daten angeben](#SpecifyMatchFields). Erstellen Sie eine Beziehung zwischen den räumlichen Daten und den analytischen Daten, damit die Darstellung von Kartenelementen von den Daten abhängig gemacht werden kann.  
  
    -   [Was ist ein Übereinstimmungsfeld?](#MatchFields)  
  
8.  [Farbdesign und Datenvisualisierung auswählen](#ThemeandVisualization). Um anzugeben, wie die Daten auf dem Kartenhintergrund dargestellt werden sollen, geben Sie das Kartendesign, die darzustellenden Felder sowie die veränderlichen Eigenschaften an: Farbe, Größe und/oder Markertyp.  
  
    -   [Wozu dient das Design?](#Theme)  
  
    -   [Wozu dienen die Legenden und Skalen in der Kartenvorschau?](#Legends)  
  
    -   [Was sind Regeln?](#Rules)  
  
 Wenn Sie eine Karte oder eine Kartenebene hinzugefügt haben und den Bericht in der Vorschau anzeigen, können Sie Karten- und Kartenebenenoptionen ändern, die Sie in den Assistenten festgelegt haben. Weitere Informationen finden Sie unter [Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
 Weitere Informationen über Karten finden Sie unter [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md). Schritt-für-Schritt-Anweisungen zum Hinzufügen eines Bericht zu einer Karte finden Sie unter [Lernprogramm: Kartenbericht &#40;Berichts-Generator&#41;](../../reporting-services/tutorial-map-report-report-builder.md).  
  
##  <a name="SpatialDataSource"></a> Quelle räumlicher Daten auswählen  
 Geben Sie auf dieser Seite die räumliche Datenquelle an, und legen Sie fest, welche räumlichen Daten eingeschlossen werden sollen. Räumliche Daten können aus dem Kartenkatalog, einer ESRI-Shape-Datei oder einer Datasetabfrage stammen, die räumliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten aus einer Datenbank von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher angibt.  
  
 Sie können für jede Ebene dieselbe Quelle oder eine andere Quelle räumlicher Daten verwenden, aber Sie müssen bei jedem Hinzufügen einer Ebene die Quelle angeben. Wenn die räumlichen Daten aus dem Kartenkatalog oder aus einer ESRI-Shape-Datei stammen, ist die räumliche Datenquelle kein separates Berichtselement. Sie wird nicht im Berichtsdatenbereich angezeigt.  
  
###  <a name="SpatialData"></a> Was sind räumliche Daten?  
 Räumliche Daten enthalten Koordinaten, die geografische oder geometrische Elemente definieren. Auf einer Karte definieren räumliche Daten *Kartenelemente*: Polygone, die Bereiche oder Formen definieren, Linien, die Routen oder Pfade definieren, und Punkte, die Marker oder Ortsmarken (Pushpins) definieren. Räumliche Daten werden in einem Binärformat in der Datenquelle gespeichert und werden als Sätze von Koordinaten angegeben. Ein Punkt wird z. B. durch eine x- und y-Koordinate (X Y) dargestellt, eine Linie durch zwei Sätze von Koordinaten ((X1 Y1), (X2 Y2)) und ein Polygon durch vier oder mehr Sätze von Koordinaten, wobei der erste und letzte Satz von Koordinaten gleich sind ((X1 Y1), (X2 Y2), (X3 Y3), (X1 Y1)).  
  
 Weitere Informationen finden Sie in der Dokumentation zum verwendeten Typ räumlicher Daten.  
  
###  <a name="MapGallery"></a>Was ist der kartenkatalog?  
 Der Kartenkatalog enthält Karten aus Berichten, die sich im Kartenkatalogordner für die Berichterstellungsumgebung befinden. Karten aus dem Katalog ermöglichen es, dem Bericht schnell eine Karte hinzuzufügen. Die vordefinierten Karten im Katalog werden von einem Kartenanbieter bereitgestellt.  
  
> [!NOTE]  
>  Für diese [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Kartenfunktion werden Daten aus TIGER/Line-Shape-Dateien verwendet, die vom U.S. Census Bureau ([http://www.census.gov/](http://www.census.gov/)) bereitgestellt werden. TIGER/Line-Shape-Dateien sind ein Auszug aus ausgewählten geografischen und kartographischen Informationen aus der Census MAF/TIGER-Datenbank. TIGER/Line-Shape-Dateien sind kostenfrei vom amerikanischen Volkszählungsbüro verfügbar. Weitere Informationen zu den TIGER/Line-Shape-Dateien finden Sie unter [http://www.census.gov/geo/www/tiger](http://www.census.gov/geo/www/tiger). Die Informationen zu geografischen Grenzen in den TIGER/Line-Shape-Dateien dienen nur der Sammlung statistischer Daten und der Tabellierung. Ihre Darstellung und Verwendung zu statistischen Zwecken bedeutet keine Aussage einer Rechtsprechungsbehörde, begründet keine Eigentumsrechte oder Rechtsansprüche und stellt keine rechtsverbindlichen Landbeschreibungen dar. Census TIGER und TIGER/Line sind eingetragene Marken des U.S. Bureau of the Census.  
  
 Um den Kartenkatalog zu erweitern, können Sie Berichte im Kartenkatalogverzeichnis hinzufügen oder entfernen sowie Ordner hinzufügen, um die Karten zu verwalten. Weitere Informationen finden Sie unter [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
###  <a name="Shapefile"></a>Was ist eine esri-Shape-Datei?  
 Eine ESRI-Shape-Datei ist ein Satz von Dateien mit Daten, die dem Shape-Dateiformat des Environmental Systems Research Institute, Inc. (ESRI) für räumliche Daten entsprechen. Enthält der Satz von Dateien in der Regel die  *\<Filename >*SHP-Datei, die die räumlichen Daten und eine Unterstützungsdatei enthält * \<Filename >*DBF.  
  
 Wenn Sie eine Shape-Datei als räumliche Datenquelle angeben und sie sich auf dem lokalen Computer befindet, werden die räumlichen Daten automatisch in den Bericht eingebettet. Um räumliche Daten aus einer ESRI-Datei dynamisch zu verwenden, gehen Sie wie folgt vor:  
  
 Laden Sie in Berichts-Generator die SHP-Datei und die DBF-Datei in denselben Ordner auf einem Berichtsserver hoch, und stellen Sie dann eine Verknüpfung mit der SHP-Datei als räumlicher Datenquelle her.  
  
 Fügen Sie im Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]dem Berichtsprojekt die SHP-Datei und die DBF-Datei hinzu, und geben Sie dann den Namen der SHP-Datei als räumliche Datenquelle an.  
  
###  <a name="GetShapefiles"></a> Wo finde ich ESRI-Shape-Dateien?  
 ESRI-Shape-Dateien sind im Web verfügbar. Weitere Informationen finden Sie unter [Finding ESRI Shapefiles for a Map](http://go.microsoft.com/fwlink/?linkid=178814).  
  
###  <a name="SqlServerSpatial"></a> Was ist eine SQL Server-Abfrage nach räumlichen Daten?  
 Eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abfrage nach räumlichen Daten ist eine Datasetabfrage, in der Daten vom Datentyp "SQLGeometry" oder "SQLGeography" aus einer relationalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank angegeben werden.  
  
> [!NOTE]  
>  Wenn Sie im Assistenten eine Datenquelle definieren, werden auf der Seite "Abfrage entwerfen" abhängig vom Datenquellentyp, mit dem Sie eine Verbindung herstellen, unterschiedliche Abfrage-Designer angezeigt. Weitere Informationen finden Sie unter [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9).  
  
 Wenn Sie die Abfrage im Abfrage-Designer ausführen, enthält das Resultset eine Spalte mit räumlichen Daten, die als Text angezeigt werden. Eine Zeile kann z. B. räumliche Daten enthalten, die einen einzelnen Punkt darstellen, und die nächste Zeile kann räumliche Daten enthalten, die einen Satz von Punkten definieren. Jede Zeile wird zu einem Kartenelement. Sie können die Anzeige jedes Kartenelements als unteilbare Einheit verändern.  
  
 Weitere Informationen finden Sie unter [Räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md).  
  
##  <a name="MapView"></a> Optionen für räumliche Daten und Kartenansicht auswählen  
 Auf dieser Seite können Sie die folgenden Optionen festlegen:  
  
-   Legen Sie den Ansichtmittelpunkt und die Zoomstufe für die räumlichen Daten fest, die Sie auf der vorherigen Assistentenseite ausgewählt haben. Die Ansicht, die Sie festlegen, gilt für die gesamte Karte.  
  
-   Legen Sie die Kartenauflösung fest.  
  
-   Geben Sie an, ob die räumlichen Daten in den Bericht eingebettet werden sollen.  
  
-   Geben Sie für eingebettete Daten an, ob alle Daten oder nur die Daten in der aktuellen Ansicht eingeschlossen werden sollen.  
  
-   Geben Sie an, ob ein Hintergrund aus [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing-Kartenkacheln eingeschlossen werden soll.  
  
###  <a name="Viewport"></a> Was ist die Kartenansicht oder der Viewport?  
 Der Kartenviewport definiert den Kartenbereich, der für alle Ebenen im Bericht angezeigt werden soll.  
  
 Standardmäßig werden die Farbskala und die Entfernungsskala im Viewport angezeigt, und die Kartenlegende wird außerhalb des Viewports angezeigt. Sie können diese Optionen für den Viewport ändern, nachdem Sie den Assistenten abgeschlossen haben.  
  
###  <a name="Resolution"></a> Was sind Kartenauflösung und Optimierung?  
 Indem Sie die Auflösung für räumliche Daten ändern, die Linien oder Polygone darstellen, geben Sie an, wie ausführlich die Karte gezeichnet werden soll. Benötigen Sie beispielsweise für Luftbilder eines Bereichs eine Granularität von bis zu hundert Metern der Erdoberfläche, oder reichen anderthalb Kilometer?  
  
 Wenn räumliche Daten in den Bericht eingebettet werden, werden bei höherer Auflösung mehr Elemente benötigt, um Details zu zeichnen. Wenn die räumlichen Daten nicht in den Bericht eingebettet werden, bedeutet eine höhere Auflösung, dass der Berichtsprozessor bei jedem Anzeigen des Berichts mehr Zeit braucht, um die Linien für die Karte zu berechnen.  
  
 Wenn Sie die Auflösung herabsetzen, verwendet der Berichtsprozessor einen Algorithmus, mit dem die Anzahl der Punkte reduziert wird, die zum Zeichnen der Kartenelemente benötigt werden. Je geringer die Auflösung, desto weniger Daten sind erforderlich, um die Kartenelemente anzuzeigen. Dies kann eine bessere Anzeigeleistung bedeuten.  
  
 Wenn Sie den Schieberegler anpassen, werden die Vorschaudaten im Assistentenbereich aktualisiert, um Ihnen eine Vorstellung von den Auswirkungen zu geben. Nachdem Sie dem Bericht die Karte hinzugefügt haben, können Sie diesen Wert anpassen, indem Sie Kartenviewport-Optionen ändern.  
  
###  <a name="Embed"></a> Was wird bei der Einbettung räumlicher Daten ausgeführt?  
 Wenn Sie Kartenelemente oder Bing-Kartenkacheln in einen Bericht einbetten, werden die räumlichen Daten in der Berichtsdefinition gespeichert.  
  
 Ein Bericht mit einer Karte kann räumliche Daten oder Bing-Kartenkacheln verwenden, die entweder dynamisch bei der Berichtsverarbeitung abgerufen werden oder zur Entwurfszeit abgerufen und in die Berichtsdefinition eingebettet werden. Eingebettete Kartenelemente können die Größe der Berichtsdefinition bedeutend erhöhen, aber reduzieren die Zeit, die erforderlich ist, um die Karte im Bericht anzuzeigen. Dynamische Kartenelemente verringern die Größe der Berichtsdefinition, aber erhöhen die Zeit, die erforderlich ist, um den Kartenbericht zu verarbeiten und anzuzeigen.  
  
 Bei einem guten Berichtsentwurf müssen Sie den Zielkonflikt zwischen statischen und dynamischen Kartendaten bewerten und von Fall zu Fall das richtige Gleichgewicht suchen. Im Allgemeinen bedeuten mehr Daten, dass die Berichtsdefinition und der kompilierte Bericht mehr Speicher auf dem Berichtsserver erfordern und dass die Verarbeitungszeiten länger sind. Es ist immer eine bewährte Methode, räumliche Daten zuzuschneiden und andere Berichtsdaten einzuschränken, um nur das einzuschließen, was für den Bericht benötigt wird.  
  
###  <a name="Tiles"></a> Was ist ein Hintergrund aus Bing-Kartenkacheln?  
 Um der Karte einen geografischen Bildhintergrund hinzuzufügen, aktivieren Sie die Option für den Bing-Kartenkachelhintergrund. Der Berichtsprozessor lädt Kacheln von Bing Maps Web Services für den Kartenbereich und die Auflösung herunter, die Sie auf dieser Assistentenseite angeben. Sie können einen der folgenden Kacheltypen angeben:  
  
-   **Straße.** Zeigt ein Straßenkartenformat mit weißem Hintergrund an.  
  
-   **Luftbild.** Zeigt nur ein Luftbild an. In diesem Modus wird kein Text angezeigt.  
  
-   **Hybrid.** Zeigt die Kombination der Ansichten **Straße** und **Luftbild** an.  
  
 Weitere Informationen zu Kacheln finden Sie unter [Bing Maps Tiles System](http://go.microsoft.com/fwlink/?LinkId=147315)(möglicherweise in englischer Sprache). Weitere Informationen zur Verwendung von Bing-Kartenkacheln im Bericht finden Sie in den [zusätzlichen Nutzungsbedingungen](http://go.microsoft.com/fwlink/?LinkId=151371).  
  
 Um einen Kachelhintergrund in der Entwurfsansicht anzuzeigen, müssen Sie über Internetzugriff verfügen. Um den Kachelhintergrund in der Vorschau eines Berichts auf einem Berichtsserver anzuzeigen, muss der Berichtsserver so konfiguriert werden, dass er Bing-Kartenkacheln unterstützt. Weitere Informationen finden Sie unter [Problembehandlung bei Berichten: Kartenberichte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md) und [Planen eines Kartenberichts](../../reporting-services/report-design/plan-a-map-report-report-builder-and-ssrs.md).  
  
 Weitere Informationen zu anderen Möglichkeiten, eine Kachelebene anzupassen, finden Sie unter [Hinzufügen, Ändern oder Löschen einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="Visualization"></a> Kartenvisualisierung auswählen  
 Wählen Sie auf dieser Seite den Typ der Karte oder Kartenebene aus, den bzw. die Sie dem Bericht hinzufügen möchten. Bei der ersten Ausführung des Assistenten fügen Sie dem Bericht eine Karte und die erste Kartenebene hinzu. Eine Karte kann mehrere Kartenebenen enthalten. Jede Kartenebene zeigt einen bestimmten Typ räumlicher Daten an: Polygone, Linien oder Punkte.  
  
 Welchen Kartentyp Sie auswählen, hängt vom Zweck der Karte und von den verfügbaren Daten ab.  
  
###  <a name="MapType"></a> Was ist der Unterschied zwischen einer Standardkarte, einer Blasendiagrammkarte und einer analytischen Karte?  
 Ein **Standardkarte** zeigt nur Orte an. Sie können die Farben der Bereiche als Schattierungen auf der Karte verändern, aber die Farbe stellt keine analytischen Datenwerte dar.  
  
 Eine **Blasendiagrammkarte** stellt den relativen Wert für ein einzelnes analytisches Datenaggregat als Blasengröße dar, z. B. den Umsatz pro Laden. Sie können Blasendiagrammkarten für Polygone oder für Punkte erstellen. Legen Sie für Polygone die Polygonmittelpunkteigenschaften fest; legen Sie für Punkte die Markereigenschaften fest.  
  
 Eine **analytische Karte** stellt den relativen Wert von einem oder mehreren analytischen Datenaggregaten für jedes Kartenelement dar. Beispiele: der Umsatz pro Laden als Markergröße, die Gewinnspanne für Produktkategorien als Markerfarbe und das meistverkaufte Produkt als Markertyp.  
  
 Weitere Informationen finden Sie unter [Planen eines Kartenberichts &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/plan-a-map-report-report-builder-and-ssrs.md).  
  
##  <a name="AnalyticalData"></a> Analytisches Dataset auswählen  
 Geben Sie auf dieser Seite an, wo die analytischen Daten abgerufen werden sollen, die auf dieser Kartenebene angezeigt werden.  
  
 Um Berichtsdaten oder analytische Daten vor dem Kartenhintergrund anzuzeigen, müssen Sie angeben, wo sich die Daten befinden und wie sie mit den räumlichen Daten in Beziehung stehen. Die Daten können aus einem vorhandenen Berichtsdataset oder aus einem neuen Dataset stammen, für das Sie eine Abfrage erstellen. Vorhandene analytische Daten können in der ESRI-Shape-Datei enthalten sein, die die räumlichen Daten enthält.  
  
###  <a name="Diff"></a> Was ist der Unterschied zwischen räumlichen Daten und analytischen Daten?  
 Räumliche Daten bestehen aus Sätzen von Koordinaten, die Punkte, Linien und Polygone angeben. Kartenelemente basieren auf räumlichen Daten.  
  
 Analytische Daten sind numerische Daten oder Kategoriedaten, die Sie verwenden können, um die Darstellung der Karte zu verändern. Analytische Daten können aus einem Berichtsdataset stammen oder in die räumlichen Daten aus einer Karte im Kartenkatalog oder einer ESRI-Shape-Datei eingeschlossen sein.  
  
##  <a name="SpecifyMatchFields"></a> Angeben der Übereinstimmungsfelder  
 Erstellen Sie auf dieser Seite eine Beziehung zwischen den räumlichen Daten und analytischen Daten.  
  
###  <a name="MatchFields"></a> Was sind Übereinstimmungsfelder?  
 Mithilfe von Übereinstimmungsfeldern kann der Berichtsprozessor eine Beziehung zwischen den analytischen Daten und den räumlichen Daten erstellen. Übereinstimmungsfelder geben eindeutige Werte innerhalb der analytischen Daten an. Möglicherweise ist z. B. der Ladenname innerhalb der Daten nicht eindeutig; deshalb sollten Sie sowohl einen Ort als auch den Ladennamen angeben.  
  
##  <a name="ThemeandVisualization"></a> Farbdesign und Datenvisualisierung auswählen  
 Um anzugeben, wie die Daten auf dem Kartenhintergrund dargestellt werden sollen, geben Sie auf dieser Seite das Kartendesign, die darzustellenden Felder sowie die veränderlichen Eigenschaften an: Farbe, Größe und/oder Markertyp.  
  
###  <a name="Theme"></a> Wozu dient das Design?  
 Das Design, das Sie auswählen, legt Standardwerte für Farbe, Rahmen und Schriftart fest. Sie können diese Optionen ändern, nachdem Sie den Assistenten abgeschlossen haben.  
  
###  <a name="Legends"></a> Wozu dienen die Legenden und Skalen in der Kartenvorschau?  
 Legenden helfen dem Benutzer, die auf einer Karte angezeigten Daten zu interpretieren. Eine Karte stellt einen Farbbereich, eine Entfernungsskala und eine Legende bereit.  
  
-   **Farbbereich.** Der Farbbereich zeigt eine Farbleiste mit einer Skala an, die eine Orientierungshilfe für die Datenintervalle bietet, die vom Berichtsprozessor auf der Grundlage der für die Ebene angegebenen Regeln bestimmt werden.  
  
-   **Entfernungsskala.** Die Entfernungsskala bietet eine Orientierungshilfe für die Längenmaßeinheiten auf der Karte. Längenmaßeinheiten werden automatisch auf der Grundlage der Kartenprojektion und der Zoomstufe bestimmt.  
  
-   **Legende.** Die Legende enthält eine Orientierungshilfe für die Bedeutung von Farben, Größen und Markertypen auf einer Karte. Standardmäßig werden mit allen Regeln für alle Ebenen Datenintervalle in der ersten Legende angezeigt. Sie können diese Legende anpassen und Legenden hinzufügen, nachdem Sie dem Bericht die Karte hinzugefügt haben.  
  
###  <a name="Rules"></a> Was sind Regeln?  
 Regeln sind Berechnungen, mit denen der Berichtsprozessor analytische Daten in Bereiche unterteilt. Sie können für jede Ebene unterschiedliche Regeln angeben. Welche Art von Regeln Sie angeben können, hängt vom Typ der räumlichen Daten in der Ebene ab:  
  
-   **Polygone.** Sie können Farbregeln angeben.  
  
-   **Mittelpunkte für Polygone.** Sie können Regeln für Farbe, Größe, Breite und Markertyp angeben.  
  
-   **Linien.** Sie können Farben- und Breitenregeln angeben.  
  
-   **Punkte.** Sie können Regeln für Farbe, Größe, Breite und Markertyp angeben.  
  
 Der Berichtsprozessor wendet die festgelegten Regeln an und bestimmt automatisch die Liste der Elemente, die in einer Legende angezeigt werden sollen. Standardmäßig werden die Ergebnisse aller Regeln für alle Ebenen in der ersten Legende angezeigt. Sie können dies nach Abschließen des Assistenten anpassen. Weitere Informationen finden Sie unter [Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Problembehandlung bei Berichten: Kartenberichte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [Planen eines Kartenberichts &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/plan-a-map-report-report-builder-and-ssrs.md)   
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)  
  
  
