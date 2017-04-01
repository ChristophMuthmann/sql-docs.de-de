---
title: "Lernprogramm: Kartenbericht (Berichts-Generator) | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
caps.latest.revision: 18
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 18
---
# Lernprogramm: Kartenbericht (Berichts-Generator)
In diesem [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)]-Tutorial erfahren Sie mehr über die Kartenfunktionen, mit denen Sie Daten vor einem geografischen Hintergrund in einem paginierten [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]-Bericht anzeigen können. 
  
Karten basieren auf räumlichen Daten, die in der Regel aus Punkten, Linien und Polygonen bestehen. Ein Polygon kann z. B. den Umriss eines Countys darstellen, eine Linie eine Straße und ein Punkt die Position eines Orts. Jeder räumliche Datentyp wird auf einer separaten Kartenebene als Satz von Kartenelementen angezeigt.  
  
Geben Sie zum Verändern der Darstellung von Kartenelementen ein Feld mit Werten an, durch die die Kartenelemente mit analytischen Daten aus einem Dataset verglichen werden. Sie können auch Regeln definieren, durch die Farbe, Größe oder andere Eigenschaften basierend auf Datenbereichen verändert werden.  

![Berichts-Generator-Karte-fertig-nur-Karte](../reporting-services/media/report-builder-map-final-map-only.png)
  
In diesem Tutorial erstellen Sie einen Kartenbericht, in dem Geschäftsstandorte in den Countys des Bundesstaats New York angezeigt werden.  
   
> [!NOTE]  
> In diesem Lernprogramm werden die Schritte für den Assistenten in zwei Verfahren zusammengefasst: ein Verfahren zum Erstellen des Datasets und ein Verfahren zum Erstellen einer Tabelle. Im ersten Tutorial dieser Reihe erhalten Sie Schritt-für-Schritt-Anweisungen zum Navigieren zu einem Berichtsserver, Auswählen einer Datenquelle, Erstellen eines Datasets und Ausführen des Assistenten: [Tutorial: Erstellen eines einfachen Tabellenberichts &#40;Berichts-Generator&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten  
  
## Anforderungen  
Der Berichtsserver muss für dieses Tutorial für die Unterstützung von Bing Maps als Hintergrund konfiguriert werden. Weitere Informationen finden Sie unter [Planen der Unterstützung für Kartenberichte](http://msdn.microsoft.com/de-de/5ddc97a7-7ee5-475d-bc49-3b814dce7e19). 

Weitere Informationen zu weiteren Voraussetzungen finden Sie unter [Voraussetzungen für Tutorials &#40;Berichts-Generator&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Map"></a>1. Erstellen einer Karte mit einer Polygonebene im Karten-Assistenten  
In diesem Abschnitt fügen Sie dem Bericht eine Karte aus dem Kartenkatalog hinzu. Die Karte enthält eine Ebene, auf der die Countys im Bundesstaat New York angezeigt werden. Die Form jedes Countys ist ein Polygon, das auf eingebetteten räumlichen Daten in der Karte aus dem Kartenkatalog basiert.  
  
### So fügen Sie mit dem Karten-Assistenten eine Karte in einem neuen Bericht hinzu  
  
1.  [Starten Sie den Berichts-Generator](../reporting-services/report-builder/start-report-builder.md) entweder von Ihrem Computer, über das [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]-Webportal oder über den integrierten SharePoint-Modus.  
  
    Das Dialogfeld **Neuer Bericht oder neues Dataset** wird geöffnet.  
  
    Wenn das Dialogfeld **Neuer Bericht oder neues Dataset** nicht angezeigt wird, wählen Sie im Menü **Datei** die Option **Neu**.  
  
2.  Vergewissern Sie sich, dass im linken Bereich **Neuer Bericht** ausgewählt ist.  
  
3.  Klicken Sie im rechten Bereich auf **Karten-Assistent**.  
  
4.  Überprüfen Sie, ob die Option **Kartenkatalog** auf der Seite **Quelle räumlicher Daten auswählen** ausgewählt ist.  
  
6.  Erweitern Sie im Kartenkatalog unter **USA** den Bereich **States by County**, und klicken Sie auf **New York**.  
  
    Im Bereich "Kartenvorschau" wird die Karte der Countys in New York angezeigt.  
    
    ![Berichts-Generator-Karte-Countys-New York](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Übernehmen Sie auf der Seite **Optionen für räumliche Daten und Kartenansicht auswählen** die Standardwerte, und klicken Sie auf **Weiter**. 
 
    Standardmäßig werden Kartenelemente aus einem Kartenkatalog automatisch in die Berichtsdefinition eingebettet.  
  
9. Überprüfen Sie, ob auf der Seite **Kartenvisualisierung auswählen** der Eintrag **Standardkarte** ausgewählt ist, und klicken Sie auf **Weiter**.  
  
11. Aktivieren Sie auf der Seite **Farbdesign und Datenvisualisierung auswählen** die Option **Bezeichnungen anzeigen**.  
  
12. Falls aktiviert, deaktivieren Sie die Option **Einfarbige Karte**.  
  
13. Klicken Sie in der Dropdownliste **Datenfeld** auf **#COUNTYNAME**. Im Kartenvorschaubereich im Assistenten werden die folgenden Elemente angezeigt:  
  
    -   Ein Titel mit dem Text **Kartentitel**  
  
    -   Eine Karte der Countys in New York, in der jedes County mit einer anderen Farbe dargestellt und der Name des Countys angezeigt wird, sofern er über den Countybereich passt  
  
    -   Eine Legende, die einen Titel und eine Liste von Elementen von 1 bis 5 enthält.  
  
    -   Eine Farbskala, die die Werte von 0 bis 160 und keine Farbe enthält.  
  
    -   Eine Entfernungsskala, auf der Kilometer (km) und Meilen (mi) angezeigt werden  
    
    ![Berichts-Generator-Karte-Farbschema-wählen](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. Klicken Sie auf **Fertig stellen**.  
  
    Die Karte wird der Entwurfsoberfläche hinzugefügt.  
  
13. Markieren Sie den Text „Kartentitel“, geben Sie **Umsatz nach Filiale** ein, und drücken Sie die EINGABETASTE.  

15. Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Im Bereich **Kartenebenen** wird eine Polygonebene, PolygonLayer1, vom Ebenentyp **Eingebettet** angezeigt. Jedes County ist ein eingebettetes Kartenelement auf dieser Ebene.  
  
    > [!NOTE]  
    > Wenn Sie den Bereich **Kartenebenen** nicht sehen, wird er möglicherweise außerhalb der aktuellen Ansicht angezeigt. Verwenden Sie die Bildlaufleiste am unteren Rand des Entwurfsansichtsfensters, um die Ansicht zu ändern. Deaktivieren Sie alternativ auf der Registerkarte **Ansicht** die Option **Berichtsdaten**, um den Anzeigebereich für die Entwurfsoberfläche zu vergrößern.   

15. Klicken Sie auf den Pfeil neben „PolygonLayer1“ und anschließend auf **Polygoneigenschaften**.

16. Ändern Sie auf der Registerkarte **Schriftart** die Farbe zu **Mattes Grau**.

17. Klicken Sie auf der Registerkarte **Stamm** auf **Ausführen**, um eine Vorschau des Berichts anzuzeigen.  
  
    ![Berichts-Generator-Karte-erste-Vorschau](../reporting-services/media/report-builder-map-first-preview.png)
  
Im gerenderten Bericht werden der Berichtstitel, der Kartentitel, die Karte und die Entfernungsskala angezeigt. Die Countys befinden sich auf einer Polygonebene der Karte. Alle Countys werden als Polygone mit unterschiedlichen Farben aus einer Farbpalette dargestellt, die Farben sind jedoch keinen Daten zugeordnet. Auf der Entfernungsskala werden Entfernungen sowohl in Kilometern als auch in Meilen angezeigt.  
  
Die Kartenlegende und die Farbskala werden noch nicht angezeigt, da den Countys noch keine analytischen Daten zugeordnet sind. Sie fügen später in diesem Lernprogramm analytische Daten hinzu.  
  
## <a name="PointLayer"></a>2. Hinzufügen einer Kartenpunktebene, um Geschäftsstandorte anzuzeigen  
In diesem Abschnitt fügen Sie mithilfe des Kartenebenen-Assistenten eine Punktebene hinzu, die den Standort von Geschäften anzeigt.  
  
> [!NOTE]  
> In diesem Tutorial sind die Datenwerte in der Abfrage enthalten, sodass keine externe Datenquelle benötigt wird. Die Abfrage ist daher relativ lang. In einer Geschäftsumgebung wären die Daten nicht in der Abfrage enthalten. Dieses Szenario dient nur zu Lernzwecken.  
  
### So fügen Sie eine Punktebene auf Grundlage eines SQL Server-Abfrage nach räumlichen Daten hinzu  
  
1.  Klicken Sie auf die Registerkarte **Ausführen** auf **Entwurf**, um wieder zur Entwurfsansicht zurückzuwechseln.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Klicken Sie auf der Symbolleiste auf die Schaltfläche **Assistent für neue Ebenen** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.png "rs_IconMapLayerWizard"). 

    ![Berichts-Generator-Karte-Symbol-des-Assistent-für-neue-Ebene](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  Wählen Sie auf der Seite **Quelle räumlicher Daten auswählen** den Eintrag **SQL Server-Abfrage nach räumlichen Daten** aus, und klicken Sie auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Dataset mit räumlichen SQL Server-Daten auswählen** auf **Neues Dataset mit räumlichen SQL Server-Daten hinzufügen** und anschließend auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Verbindung mit einer SQL Server-Datenquelle für räumliche Daten auswählen** eine vorhandene Datenquelle aus, oder navigieren Sie zum Berichtsserver, und wählen Sie eine Datenquelle aus.  

    > [!NOTE]  
    > Welche Datenquelle Sie auswählen, ist unwichtig, solange Sie über ausreichende Berechtigungen verfügen. Aus der Datenquelle werden keine Daten abgerufen. Weitere Informationen finden Sie unter [Alternative Methoden zum Herstellen einer Datenverbindung &#40;Berichts-Generator&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**.  
  
8.  Kopieren Sie den folgenden Text, und fügen Sie ihn in den Abfragebereich ein:  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Ausführen** (**!**).  
  
    Das Resultset enthält sieben Spalten mit einem Satz von Geschäften im Bundesstaat New York, die Verbrauchsgüter verkaufen. Im Folgenden finden Sie eine Liste mit Erklärungen für die Spalten, die nicht selbsterklärend sind: 
    *   **StoreKey**: ein Geschäftsbezeichner  
    *   **StoreName**
    *   **SellingArea**: die für eine Produktauslage zur Verfügung stehende Fläche, von 455 sq ft bis hin zu 1125 sq ft
    *   **City**
    *   **County**
    *   **Vertrieb**: Gesamtvertrieb 
    *   **SpatialLocation**: Position in Längen- und Breitengraden 

    ![Berichts-Generator-Abfrage-entwerfen](../reporting-services/media/report-builder-map-design-query.png) 
  
10. Klicken Sie auf **Weiter**.  
  
    Das Berichtsdataset mit dem Namen "DataSet1" wird für Sie erstellt. Nachdem Sie den Assistenten abgeschlossen haben, wird im Bereich „Berichtsdaten“ die Feldersammlung angezeigt.  
  
11. Überprüfen Sie auf der Seite **Optionen für räumliche Daten und Kartenansicht auswählen**, ob für **Räumliches Feld** der Wert **SpatialLocation** und für **Ebenentyp** der Wert **Punkt** ausgewählt ist. Übernehmen Sie die anderen Standardwerte auf dieser Seite.  
  
    In der Kartensicht werden Kreise angezeigt, um den Standort jedes Geschäfts zu markieren.  
  
12. Klicken Sie auf **Weiter**.  
  
13. Klicken Sie auf der Seite „Kartenvisualisierung auswählen“ auf **Blasendiagrammkarte**, um einen Kartentyp zu erhalten, der Marker anzeigt, die je nach Daten in der Größe variieren. Klicken Sie auf **Weiter**.  
  
14. Klicken Sie auf der Seite **Analytisches Dataset auswählen** auf DataSet1 und anschließend auf **Weiter**. Dieses Dataset enthält sowohl analytische Daten als auch räumliche Daten, die auf der neuen Punktebene angezeigt werden.   
  
16. Aktivieren Sie auf der Seite **Farbdesign und Datenvisualisierung auswählen** die Option **Blasengrößen zum Anzeigen von Daten verwenden**.  
  
17. Wählen Sie unter **Datenfeld** `[Sum(SellingArea)]` aus, um die Blasengröße entsprechend der Größe der Ausstellfläche für die Produkte zu variieren.  
  
18. Wählen Sie **Bezeichnungen anzeigen** und unter **Datenfeld** `[City]` aus.

18. Klicken Sie auf **Fertig stellen**.  
  
    Die Kartenebene wird dem Bericht hinzugefügt. Auf der Legende werden Blasengrößen basierend auf den SellingArea-Werten angezeigt.  
  
 19. Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Im Bereich **Kartenebenen** wird eine neue Ebene PointLayer1 mit dem räumlichen Datenquellentyp **DataRegion** angezeigt.  
  
19. Fügen Sie einen Legendentitel hinzu. Wählen Sie in der Legende den Text **Titel** aus, geben Sie **Auslagefläche in Quadratfuß** ein und drücken Sie die EINGABETASTE.  
  
21. Klicken Sie im Bereich **Kartenebenen** auf den Pfeil neben PointLayer1, und klicken Sie anschließend auf **Punkteigenschaften**.  

    ![Berichts-Generator-Karte-Punkteigenschaften](../reporting-services/media/report-builder-map-point-properties.png)
  
22. Ändern Sie auf der Registerkarte **Schriftart** den Schriftschnitt auf **Fett** und die Schriftgröße auf **10 pt**.

    ![Berichts-Generator-Karte-Punkteigenschaften-Schriftart](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. Wählen Sie auf der Registerkarte **Allgemein** als **Platzierung** die Einstellung **Unten** aus.

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.  

    ![Berichts-Generator-Karte-Städtenamen](../reporting-services/media/report-builder-map-city-names.png)
  
    Auf der Karte werden die Standorte von Geschäften im Bundesstaat New York angezeigt. Die Markergröße jedes Geschäftes basiert auf der Auslagefläche. Fünf Bereiche wurden automatisch für die Aufstellfläche berechnet.


  
## <a name="LineLayer"></a>3. Hinzufügen einer Kartenlinienebene, um eine Route anzuzeigen  
Fügen Sie mithilfe des Kartenebenen-Assistenten eine Kartenebene hinzu, die eine Route zwischen zwei Geschäften anzeigt. In diesem Lernprogramm wird der Weg für drei Geschäftsstandorte erstellt. In einer Geschäftsanwendung könnte es sich bei dem Weg um die beste Route zwischen Geschäften handeln.  
  
### So fügen Sie der Karte eine Linienebene hinzu  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Klicken Sie auf der Symbolleiste auf die Schaltfläche **Assistent für neue Ebenen** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.png "rs_IconMapLayerWizard").  
  
3.  Wählen Sie auf der Seite **Quelle räumlicher Daten auswählen** den Eintrag **SQL Server-Abfrage nach räumlichen Daten** aus, und klicken Sie auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Dataset mit räumlichen SQL Server-Daten auswählen** auf **Neues Dataset mit räumlichen SQL Server-Daten hinzufügen** anschließend auf **Weiter**.  
  
5.  Wählen Sie unter **Verbindung mit einer SQL Server-Datenquelle für räumliche Daten auswählen** die Datenquelle, die Sie im ersten Verfahren verwendet haben.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Klicken Sie auf der Seite **Abfrage entwerfen** auf **Als Text bearbeiten**. Der Abfrage-Designer wechselt in den textbasierten Modus.  
  
8.  Fügen Sie den folgenden Text in den Abfragebereich ein:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Klicken Sie auf **Weiter**.  
  
    Auf der Karte wird ein Weg angezeigt, der drei Geschäfte verbindet.  
  
10. Überprüfen Sie auf der Seite **Optionen für räumliche Daten und Kartenansicht auswählen**, ob für **Räumliches Feld** der Wert **Route** und für **Ebenentyp** der Wert **Linie** ausgewählt ist. Übernehmen Sie die anderen Standardwerte.  
  
    In der Kartensicht wird ein Weg von einem Geschäft im nördlichen Teil des Bundesstaats New York zu einem Geschäft im südlichen Teil des Bundesstaats New York angezeigt.  
  
11. Klicken Sie auf **Weiter**.  
  
12. Klicken Sie auf der Seite **Kartenvisualisierung auswählen** auf **Standardkarte (Linien)** und anschließend auf **Weiter**.  
  
13. Aktivieren Sie unter **Farbdesign und Datenvisualisierung auswählen** die Option **Einfarbige Karte**. Der Weg wird mit einer einzelnen Farbe angezeigt, die auf dem ausgewählten Design basiert.  
  
14. Klicken Sie auf **Fertig stellen**.  

    ![Berichts-Generator-Karte-Linie](../reporting-services/media/report-builder-map-line.png)
  
     In der Karte wird eine neue Linienebene mit dem räumlichem Datenquellentyp **DataRegion** angezeigt. In diesem Beispiel stammen die räumlichen Daten aus einem Dataset, aber der Linie sind keine analytischen Daten zugeordnet.  

## Anpassen des Zooms
1. Sollte nicht der gesamte Bundesstaat New York angezeigt werden, können Sie den Zoom anpassen. Die **MapViewport**-Eigenschaften für die ausgewählte Karte finden Sie im Bereich „Eigenschaften“. 

15. Erweitern Sie den Abschnitt **Ansicht**, und erweitern Sie anschließend **Ansicht**, um die Eigenschaft **Zoom** anzuzeigen. Legen Sie hierfür **125** fest. 

    ![Berichts-Generator-Karte-Zoom](../reporting-services/media/report-builder-map-zoom.png)

      Dies ist der Prozentwert für den Zoom. Wenn dieser 125 % beträgt, sollte der gesamte Bundesstaat angezeigt werden.
  
## <a name="TileLayer"></a>4. Hinzufügen eines Bing Maps-Kachelhintergrunds  
In diesem Abschnitt fügen Sie eine Kartenebene hinzu, die einen Bing Maps-Kachelhintergrund anzeigt.  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Klicken Sie auf der Symbolleiste auf **Ebene hinzufügen** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.png "rs_IconMapAddLayer").  
  
3.  Klicken Sie in der Dropdownliste auf **Kachelebene**.  
  
    Die letzte Ebene im Bereich **Kartenebene** ist TileLayer1. Standardmäßig zeigt die Kachelebene das Straßenkartenformat an.  
  
    > [!NOTE]  
    > Sie können auch im Assistenten auf der Seite **Optionen für räumliche Daten und Kartenansicht auswählen** eine Kachelebene hinzufügen. Wählen Sie dazu **Bing Maps-Hintergrund für diese Kartenansicht hinzufügen** aus. In einem gerenderten Bericht zeigt der Kachelhintergrund Bing Maps-Kacheln für den aktuellen Kartenviewport-Mittelpunkt und die aktuelle Zoomstufe an.  
  
4.  Klicken Sie auf den Pfeil neben TileLayer1 und anschließend auf **Kacheleigenschaften**.  
  
5.  Wählen Sie auf der Registerkarte **Allgemein** unter **Typ** die Option **Luftbild** aus. Das Luftbild enthält keinen Text.  

    ![Berichts-Generator-Karte-Bing-Luftbild](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5. Transparente Darstellung einer Ebene  
In diesem Abschnitt passen Sie die Reihenfolge und Transparenz der Ebene an, um die Elemente auf einer anderen Ebenen durchscheinen zu lassen und den gewünschten Transparenzeffekt zu erzielen. Beginnen Sie mit PolygonLayer1, der ersten Ebene, die Sie erstellt haben. 
  
1.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen.  
  
3.  Klicken Sie auf den Pfeil neben PolygonLayer1 und auf **Ebenendaten**. Das Dialogfeld **Polygonebeneneigenschaften von Karten** wird geöffnet.  
  
4.  Geben Sie auf der Registerkarte **Sichtbarkeit** unter **Transparenz (Prozent)** **30** ein.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Auf der Entwurfsoberfläche werden die Countys halbtransparent dargestellt.  

    ![Berichts-Generator-Karte-Transparenz](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6. Verändern der Countyfarbe basierend auf Umsätzen  
Jedes County in der Polygonebene hat eine andere Farbe, da der Berichtsprozessor automatisch auf der Grundlage des Designs, das Sie auf der letzten Seite des Karten-Assistenten ausgewählt haben, einen Farbwert aus der Farbpalette zuweist.  
  
In diesem Abschnitt geben Sie eine Farbregel an, um für jedes County bestimmte Farben einem Bereich von Geschäftsumsätzen zuzuordnen. Die Farben rot, gelb und grün geben relativ hohe, mittlere bzw. niedrige Umsätze an. Formatieren Sie die Farbskala, um Währungswerte anzuzeigen. Zeigen Sie die Jahresumsatzbereiche in einer neuen Legende an. Verwenden Sie für Countys ohne Geschäfte keine Farbe, um anzuzeigen, dass keine zugeordneten Daten vorliegen.  
  
### <a name="Relationship"></a>6a. Erstellen einer Beziehung zwischen räumlichen und analytischen Daten  
Um die Countys anhand analytischer Daten farblich zu unterscheiden, müssen Sie zuerst die analytischen Daten den räumlichen Daten zuordnen. In diesem Lernprogramm verwenden Sie zu diesem Zweck den Countynamen. 
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen.  
  
3.  Klicken Sie auf den Pfeil neben PolygonLayer1 und anschließend auf **Ebenendaten**. Das Dialogfeld **Polygonebeneneigenschaften von Karten** wird geöffnet.  
  
4.  Wählen Sie auf der Registerkarte **Analytische Daten** unter **Analytisches Dataset** DataSet1 aus. Dieses Dataset wurde vom Assistenten erstellt, als Sie die Abfrage räumlicher Daten für die Countys erstellt haben.  
  
6.  Klicken Sie unter **Abzugleichende Felder** auf **Hinzufügen**. Eine neue Zeile wird hinzugefügt.  
  
7.  Klicken Sie unter **Aus räumlichem Dataset** auf COUNTYNAME.  
  
8.  Klicken Sie unter **Aus analytischem Dataset** auf [County].  

    ![Berichts-Generator-Karte-Countys-Farben](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Zeigen Sie eine Vorschau des Berichts an.  

    ![Berichts-Generator-Karte-County-hervorheben](../reporting-services/media/report-builder-map-county-highlight.png)
  
Durch die Angabe eines Übereinstimmungsfelds aus der räumlichen Datenquelle und aus dem analytischen Dataset kann der Berichtsprozessor analytische Daten auf Grundlage der Kartenelemente gruppieren. Bei einem datengebundenen Kartenelement wird eine erfolgreiche Übereinstimmung für die von Ihnen angegebenen Werte erzielt.  
  
Jedem County mit einem Geschäft ist eine Farbe zugeordnet, die auf der Farbpalette für das im Assistenten ausgewählte Format basiert. Die anderen Countys werden grau dargestellt.  
  
### <a name="ColorRules"></a>6b. Festlegen von Farbregeln für Polygone  
Zum Erstellen einer Regel, die die Farbe jedes Countys basierend auf dem Geschäftsumsatz verändert, müssen Sie die Bereichswerte, die Anzahl anzuzeigender Einteilungen innerhalb dieses Bereichs und die zu verwendenden Farben angeben.  
  
#### So geben Sie Farbregeln für alle Polygone mit zugeordneten Daten an  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Klicken Sie auf den Pfeil neben PolygonLayer1 und anschließend auf **Regel für die Polygonfarbe**. Das Dialogfeld **Farbregeleigenschaften der Karte** wird geöffnet. Beachten Sie, dass die Farbregeloption **Daten mithilfe der Farbpalette anzeigen** ausgewählt ist. Diese Option wurde vom Assistenten festgelegt.  
  
3.  Aktivieren Sie **Daten mithilfe von Farbbereichen anzeigen**. Die Palettenoption wird durch die Optionen für Startfarbe, mittlere Farbe und Endfarbe ersetzt.  
  
4.  Definieren Sie Bereichswerte für die Umsätze pro County. Wählen Sie unter **Datenfeld** den Eintrag `[Sum(Sales)]` in der Dropdownliste aus.  
  
5.  Ändern Sie den Ausdruck wie folgt, um das Format zur Anzeige der Währung in Tausendern zu ändern: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Ändern Sie **Startfarbe** in **Rot**.  
  
7.  Ändern Sie **Endfarbe** in **Grün**.  
  
    **Rot** stellt niedrige Umsatzwerte dar, **Gelb** stellt mittlere Umsatzwerte dar, und **Grün** stellt hohe Umsatzwerte dar. Der Berichtsprozessor berechnet einen Bereich von Farben auf der Grundlage dieser Werte und der Optionen, die Sie auf der Seite **Verteilung** auswählen.  
    
    ![Berichts-Generator-Karte-County-Farbregeln](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  Klicken Sie auf **Verteilung**.  
  
9. Überprüfen Sie, ob der Verteilungstyp **Optimal** lautet. Für den Ausdruck aus Schritt 5 werden die Werte durch die optimale Verteilung in Teilbereiche aufgeteilt, deren Elementanzahl und Umfang jeweils gleich sind.  
  
10. Übernehmen Sie die Standardwerte für andere Optionen auf dieser Seite. Wenn Sie den optimalen Verteilungstyp auswählen, wird die Anzahl der Teilbereiche bei der Berichtausführung berechnet.  
  
11. Klicken Sie auf **Legende**.  
  
12. Überprüfen Sie, ob unter **Farbskalaoptionen** der Wert **In Farbskala anzeigen** ausgewählt ist.  
  
13. Wählen Sie unter **In dieser Legende anzeigen** in der Dropdownliste die Leerzeile aus. Zurzeit zeigen Sie die Farbbereiche nur in der Farbskala an.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. Zeigen Sie eine Vorschau des Berichts an.

    ![Berichts-Generator-Karte-County-Farbregel-Vorschau](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    Auf der Farbskala werden vier Farben angezeigt: rot, orange, gelb und grün. Jede Farbe stellt einen Umsatzbereich dar, der automatisch auf Grundlage der Umsätze nach County berechnet wird.  
  
### <a name="ColorScale"></a>6c. Formatieren der Daten in der Farbskala als Währung  
Für Daten wird standardmäßig ein allgemeines Format verwendet. In diesem Abschnitt wenden Sie benutzerdefinierte Formate an.  
  
1. Wechseln Sie in die Entwurfsansicht.  

2. Wählen Sie die Farbskala aus. Klicken Sie auf der Registerkarte **Stamm** im Abschnitt **Zahl** auf **Währung**.  
  
4.  Klicken Sie im Abschnitt **Zahl** zweimal auf die Schaltfläche **Dezimalstelle verringern**.  
  
    Die Farbskala zeigt für jeden Bereich den Jahresumsatz im Währungsformat an.  
  
### <a name="NewLegend"></a>6d. Hinzufügen eines Legendentitels   
  
1.  Bei ausgewählter Farbskala werden im Eigenschaftenbereich die Eigenschaften für **MapColorScale** angezeigt. 
  
2. Erweitern Sie den Abschnitt „Titel“, und geben Sie die Beschriftungseigenschaft **Umsatz in Tausend** ein.

3. Ändern Sie die Eigenschaft „TextColor“ in **Weiß**.  

    ![Berichts-Generator-Karte-Farbskala-Titel](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  Zeigen Sie eine Vorschau des Berichts an.  
  
Die Countys mit zugeordneten Geschäften und Umsätzen werden entsprechend den Farbregeln angezeigt. Countys ohne Umsätze ist keine Farbe zugeordnet.  
  
### <a name="NoData"></a>6f. Ändern der Farbe für Countys ohne Daten  
Sie können die Standardanzeigeoptionen für alle Kartenelemente auf einer Ebene festlegen. Farbregeln haben Vorrang vor diesen Anzeigeoptionen.  
  
#### So legen Sie die Anzeigeeigenschaften für alle Elemente auf einer Ebene fest  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen.  
  
3.  Klicken Sie in „PolygonLayer1“ auf den Pfeil nach unten und anschließend auf **Polygoneigenschaften**. 

     ![Berichts-Generator-Karte-Polygonebeneneigenschaften](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     Das Dialogfeld **Polygoneigenschaften von Karten** wird geöffnet. Bevor regelbasierte Anzeigeoptionen angewendet werden, gelten in diesem Dialogfeld festgelegte Anzeigeoptionen für alle Polygone auf der Ebene.  
  
4.  Vergewissern Sie sich auf der Registerkarte **Ausfüllen**, dass der Füllstil **Einfarbig** lautet. festgelegt ist. Farbverläufe und Muster gelten für alle Farben.  
  
6.  Wählen Sie unter **Farbe** die Option **Helles Stahlblau** aus.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Zeigen Sie eine Vorschau des Berichts an.  
  
Countys ohne zugeordnete Daten werden graublau dargestellt. Nur Countys, denen analytische Daten zugeordnet sind, werden in den Farben im Bereich zwischen **Rot** und **Grün** der angegebenen Farbregeln angezeigt.  
  
## <a name="CustomPoint"></a>7. Hinzufügen eines benutzerdefinierten Punkts  
In diesem Abschnitt geben Sie einen Punkt an, und verwenden den Markertyp **Stern**, um ein neues, noch nicht gebautes Geschäft darzustellen.  
  
1.  Wechseln Sie in die Entwurfsansicht.  
  
2.  Doppelklicken Sie auf die Karte, um den Bereich **Kartenebenen** anzuzeigen. Klicken Sie auf der Symbolleiste auf **Ebene hinzufügen** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.png "rs_IconMapAddLayer") und anschließend auf **Punktebene**.  
  
    Der Karte wird eine neue Punktebene hinzugefügt. Standardmäßig verfügt die Punktebene über den räumlichen Datentyp **Eingebettet**.  
  
3.  Klicken Sie auf den Pfeil unter PointLayer2 und anschließend auf **Punkt hinzufügen**.  
  
4.  Bewegen Sie den Zeiger über den Kartenviewport. Der Cursor verändert sich zu einem Fadenkreuz.  
  
5.  Klicken Sie auf den Ort auf der Karte, an dem Sie einen Punkt hinzufügen möchten. Klicken Sie für dieses Tutorial auf eine Position im County Oneida. Der Ebene wird an der Stelle, auf die Sie geklickt haben, ein durch einen Kreis markierter Punkt hinzugefügt. Standardmäßig ist der Punkt ausgewählt.  

    ![Berichts-Generator-Karte-benutzerdefinierter-Punkt](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  Klicken Sie mit der rechten Maustaste auf den hinzugefügten Punkt, und klicken Sie anschließend auf **Eigenschaften für eingebettete Punkte**.  
  
7.  Wählen Sie **Punktoptionen für diese Ebene überschreiben** aus. Im Dialogfeld werden weitere Seiten angezeigt. Hier festgelegte Werte haben Vorrang vor Anzeigeoptionen für die Ebene oder für Farbregeln.  

    ![Berichts-Generator-Karte-benutzerdefinierter-Punkt-allgemein](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  Wählen Sie auf der Registerkarte **Marker** unter **Markertyp** den Wert **Stern** aus.  

10. Ändern Sie die **Markergröße** in **18 pt**.
  
3.  Geben Sie auf der Registerkarte **Bezeichnungen** unter **Bezeichnungstext** **Neues Geschäft** ein.  
  
5.  Klicken Sie unter **Platzierung** auf **Oben**.  

13. Ändern Sie auf der Registerkarte **Schriftart** die Schriftgröße in **10 pt** und den Schriftschnitt in **Fett**.

    ![Berichts-Generator-Karte-benutzerdefinierter-Punkt-Schriftart](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
Die Bezeichnung wird über dem Geschäftsstandort angezeigt.  

![Berichts-Generator-Karte-benutzerdefinierter-Punkt-neues-Geschäft](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8. Zentrieren und Skalieren der Karte   
In diesem Abschnitt erfahren Sie sowohl, wie Sie den Mittelpunkt der Karte ändern, als auch einen weiteren Weg, um den Zoomfaktor zu ändern.  
 
1.  Wechseln Sie in die Entwurfsansicht.  

1.  Klicken Sie mit der rechten Maustaste auf die Karte, und klicken Sie anschließend auf **Viewporteigenschaften**.  
  
2.  Stellen Sie auf der Registerkarte **Zentrieren und zoomen** sicher, dass die Option **Mittelpunkt und Zoomstufe für Ansicht festlegen** ausgewählt ist.  

4. Legen Sie die Einstellung **Zoomfaktor (Prozent)** auf **125** fest.
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Klicken Sie auf die Karte, und ziehen Sie sie, um sie an der gewünschten Stelle zu zentrieren.  
  
6.  Sie können den Zoomfaktor auch mithilfe des Mausrads ändern.  
  
7.  Zeigen Sie eine Vorschau des Berichts an.  
  
In der Entwurfsansicht basieren die Karte auf der Anzeigeoberfläche und die Ansicht auf Beispieldaten. Im gerenderten Bericht wird die Kartenansicht in der angegebenen Ansicht zentriert.  
  
## <a name="Title"></a>9. Hinzufügen eines Berichtstitels  
  
1.  Wechseln Sie in die Entwurfsansicht.
  
1.  Klicken Sie auf der Entwurfsoberfläche auf **Zum Hinzufügen eines Titels klicken**.  
  
2.  Geben Sie **Umsätze in den Geschäften in New York** ein, und klicken Sie anschließend auf den Bereich außerhalb des Textfelds.  
  
Dieser Titel wird am Anfang des Berichts angezeigt. Elemente über dem Berichtshauptteil entsprechen einer Berichtskopfzeile, wenn keine Seitenkopfzeile definiert ist.  
  
## <a name="Save"></a>10. Speichern des Berichts  
  
1.  Klicken Sie in der Entwurfsansicht oder in einer Vorschau auf **Datei** und anschließend auf **Speichern unter**.
 
3.  Geben Sie im Feld **Name** den Namen **Umsätze der Geschäfte in New York** ein.  

3. Speichern Sie den Bericht auf Ihrem lokalen Computer oder auf einem [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]-Server.
  
4. Klicken Sie auf **Speichern**. 

Wenn Sie den Bericht auf einem Berichtsserver speichern, können Sie ihn dort auch anzeigen.

![Berichts-Generator-Karte-im-Portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## Nächste Schritte  
Damit ist die exemplarische Vorgehensweise für das Hinzufügen einer Karte zum Bericht abgeschlossen.  
  
Weitere Informationen finden Sie unter [Karten &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
## Siehe auch  
[Tutorials (Berichts-Generator)](../reporting-services/report-builder-tutorials.md)  
[Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[Karten-Assistent und Kartenebenen-Assistent &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md)  
  
