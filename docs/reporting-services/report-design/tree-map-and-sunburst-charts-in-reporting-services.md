---
title: "Treemap- und Sunburst-Diagramme in Reporting Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/31/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 16
---
# Treemap- und Sunburst-Diagramme in Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Treemap- und Sunburst-Visualisierung sind hervorragend für die visuelle Darstellung von hierarchischen Daten geeignet.   Dieses Thema bietet eine Übersicht darüber, wie Sie ein Treemap- oder Sunburst-Diagramm zu einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht hinzufügen. Dieses Thema enthält auch eine Adventureworks-Beispielabfrage, um Ihnen beim Einstieg zu helfen.  
  
##  <a name="bkmk_treemap_chart"></a> Das Treemap-Diagramm  
 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
  
 In einem Treemap-Diagramm wird die Diagrammfläche in Rechtecke unterteilt, die die verschiedenen Ebenen und die relative Größe der Datenhierarchie darstellen. Die Darstellung ähnelt dem Geäst eines Baums, das am Stamm beginnt und sich in immer feinere Zweige aufspaltet. Jedes Rechteck wird in kleinere Rechtecke aufgespaltet, die die nächste Hierarchieebene darstellen. Die größten Rechtecke des Treemap-Diagramms werden mit ihrem größten Rechteck in der oberen linken Ecke des Diagramms angeordnet. Diese Rechtecke stellen die oberste Hierarchieebene dar. Die Rechtecke sind nach absteigender Hierarchie angeordnet, und das kleinste Rechteck befindet sich in der unteren rechten Ecke.  Innerhalb eines Rechtecks sind die Rechtecke ebenfalls der Hierarchie entsprechend von oben links nach unten rechts angeordnet.  
  
 In der folgenden Abbildung eines Beispiel-Treemap-Diagramms ist das Gebiet „Southwest“ (Südwesten) das größte und „Germany“ (Deutschland) das kleinste. Innerhalb des Südwestens ist das Feld „Road Bikes“ (Rennräder) größer als das für „Mountain Bikes“.  
  
 ![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### So fügen Sie ein Treemap-Diagramm und konfigurieren es für die Adventureworks-Beispieldaten  
 **Hinweis:** Bevor Sie Ihrem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset.  Beispieldaten und eine Beispielabfrage finden Sie im Abschnitt [Adventureworks-Beispieldaten](#bkmk_sample_data) in diesem Thema.  
  
1.  Klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche, anschließend auf **Einfügen**, und klicken Sie danach auf **Diagramm**.  
  
     Wählen Sie „Treemap“ ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") aus.  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Passen Sie die Position und Größe des Diagramms an.   Für die Verwendung mit den Beispieldaten empfehlen wir ein 5 Zoll breites Diagramm.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Values (Werte):** LineTotal<br /><br /> **Category Groups (Kategoriegruppen):** Fügen Sie sie in folgender Reihenfolge hinzu:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> **Series Groups (Reihengruppen):** TerritoryName|  
  
4.  Um die Seitengröße für ein Treemap-Diagramm zu optimieren, positionieren Sie die Legende darunter.  
  
5.  Klicken Sie mit der rechten Maustaste auf **LineTotal** und anschließend auf **Series Properties ** (Reiheneigenschaften), um QuickInfos hinzuzufügen, die die Unterkategorie und die Zeilensumme anzeigen.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Legen Sie die Eigenschaft **QuickInfo** wie folgt fest:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
     Weitere Informationen finden Sie unter [Anzeigen von QuickInfos für eine Reihe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Ändern Sie den Standarddiagrammtitel auf „Categorized Sales by Territory“ (Verkäufe nach Kategorie und Territorium).  
  
7.  Die Anzahl der angezeigten Beschriftungswerte wird durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst.  Um weitere Beschriftungen anzuzeigen, ändern Sie die LineTotal-Eigenschaft „Schriftart“ von den standardmäßig eingestellten 8 Punkt auf 10 Punkt.  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [In diesem Thema](#bkmk_top)  
  
##  <a name="bkmk_sunburst_chart"></a> Sunburst-Diagramm  
 ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
 Die Hierarchie wird in einem Sunburst-Diagramm durch eine Reihe von Kreisen dargestellt. Die höchste Hierarchieebene befindet sich in der Mitte und die niedrigeren Ebenen werden in Ringen um die Mitte herum gruppiert.  Die unterste Hierarchieebene befindet sich im äußersten Ring.  
  
 ![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### So fügen Sie ein Sunburst-Diagramm ein und konfigurieren es für die Adventureworks-Beispieldaten  
 **Hinweis:** Bevor Sie Ihrem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset.  Beispieldaten und eine Beispielabfrage finden Sie im Abschnitt [Adventureworks-Beispieldaten](#bkmk_sample_data) in diesem Thema.  
  
1.  Klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche, anschließend auf **Einfügen**, und klicken Sie danach auf **Diagramm**.  
  
     Wählen Sie „Sunburst“ ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") aus.  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Passen Sie die Position und Größe des Diagramms an.   Für die Verwendung mit den Beispieldaten empfehlen wir ein 5 Zoll breites Diagramm.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Values (Werte):** LineTotal<br /><br /> **Category Groups (Kategoriegruppen):** Fügen Sie sie in folgender Reihenfolge hinzu:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> (3) SalesReasonName<br /><br /> **Series Groups (Reihengruppen):** TerritoryName|  
  
4.  Um die Seitengröße für ein Sunburst-Diagramm zu optimieren, positionieren Sie die Legende darunter.  
  
5.  Ändern Sie den Standarddiagrammtitel auf „Categorized Sales by Territory, with sales reason“ (Verkäufe nach Kategorie und Territorium, unter Berücksichtigung des Kaufgrunds).  
  
6.  |||  
    |-|-|  
    |![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")|Um dem Sunburst-Diagramm die Werte der Kategoriegruppen hinzuzufügen, legen Sie die Beschriftungseigenschaften wie folgt fest: **Visible** = TRUE und **UseValueAsLabel** = FALSE.<br /><br /> Die angezeigten Beschriftungswerte werden durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst.  Um weitere Beschriftungen anzuzeigen, ändern Sie die LineTotal-Eigenschaft „Schriftart“ von den standardmäßig eingestellten 10 Punkt auf 8 Punkt.|  
  
7.  Wenn Sie den Farbbereich ändern möchten, verändern Sie im Diagramm die Eigenschaft **Palette** .  
  
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [In diesem Thema](#bkmk_top)  
  
##  <a name="bkmk_sample_data"></a> Adventureworks-Beispieldaten  
 Der Abschnitt enthält eine Beispielabfrage und die grundlegenden Schritte zum Erstellen einer Datenquelle und eines Datasets im [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Wenn Ihr Bericht bereits eine Datenquelle und ein Dataset enthält, können Sie diesen Abschnitt überspringen.  
  
 Die Abfrage gibt detaillierte Adventureworks-Daten zu Verkaufsaufträgen mit Daten zum Vertriebsgebiet, der Produktkategorie, der Unterkategorie des Produkts und dem Verkaufsgrund aus.  
  
1.  **Abrufen der Daten:**  
  
     Die Abfrage in diesem Abschnitt basiert auf der Adventureworks-Datenbank, die unter  [Adventure Works 2014 Full Database Backup (Adventure Works 2014 vollständige Datenbanksicherung)](https://msftdbprodsamples.codeplex.com/releases/view/125550)heruntergeladen werden kann.  
  
     Weitere Informationen zum Installieren der Datenbank finden Sie unter [How to install Adventure Works 2014 Sample Databases.pdf (So installieren Sie Adventure Works 2014-Beispieldatenbanken)](https://msftdbprodsamples.codeplex.com/releases/view/125550).  
  
2.  **Erstellen einer Datenquelle:**  
  
    1.  Klicken Sie im Bereich **Berichtsdaten** mit der rechten Maustaste auf die **Datenquellen**, und klicken Sie anschließend auf **Datenquelle hinzufügen**.  
  
    2.  Klicken Sie auf **In meinem Bericht eingebettete Verbindung verwenden**.  
  
    3.  Wählen Sie den Verbindungstyp **Microsoft SQL Server**aus.  
  
    4.  Geben Sie die Verbindungszeichenfolge für Ihren Server und die Datenbank ein, z.B. die folgende:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2014  
        ```  
  
    5.  Es empfiehlt sich, das Vorgehen mithilfe der Schaltfläche **Verbindung testen** zu prüfen. Klicken Sie dann auf **OK**.  
  
     Weitere Informationen zum Erstellen einer Datenquelle finden Sie unter [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Erstellen eines Datasets:**  
  
    -   Klicken Sie im Bereich **Berichtsdaten** mit der rechten Maustaste auf **Datasets**, und klicken Sie anschließend auf **Dataset hinzufügen**.  
  
    -   Wählen Sie **Ein in den eigenen Bericht eingebettetes Dataset verwenden**aus.  
  
    -   Wählen Sie die Datenquelle aus, die Sie in den vorherigen Schritten erstellt haben.  
  
    -   Wählen Sie den Abfragetyp **Text** aus, kopieren Sie die folgende Abfrage, und fügen Sie sie in das Textfeld **Abfrage:** ein:  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    -   Klicken Sie auf **OK**.  
  
     Weitere Informationen zum Erstellen eines Datasets finden Sie unter [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [In diesem Thema](#bkmk_top)  
  
## Siehe auch  
 [Freigegebene Datasetentwurfsansicht &#40;Report Builder&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Anzeigen von QuickInfos für eine Reihe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)   
 [Tutorial: Treemaps in Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)   
 [Treemap: Microsoft Research Data-Visualisierungs-Apps für Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
