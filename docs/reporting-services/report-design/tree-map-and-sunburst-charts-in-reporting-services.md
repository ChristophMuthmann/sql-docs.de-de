---
title: Treemap- und Sunburst-Diagramme in SQL Server Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/31/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1dcafd7c259a88fd57022da4e72f9e3abeb077b1
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Treemap- und Sunburst-Diagramme in Reporting Services
[!INCLUDE[feedback-stackoverflow-msdn-connect-md](../../includes/feedback-stackoverflow-msdn-connect-md.md)] Die SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Treemap- und Sunburst-Visualisierungselemente sind ausgezeichnet für die visuelle Darstellung von hierarchischen Daten geeignet. In diesem Artikel wird dargestellt, wie Sie ein Treemap- oder Sunburst-Diagramm zu einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Bericht hinzufügen. Außerdem beinhaltet er eine AdventureWorks-Beispielabfrage, um Sie bei den ersten Schritten zu unterstützen.  
  
##  <a name="bkmk_treemap_chart"></a> Treemap-Diagramm  

In einem Treemap-Diagramm wird die Diagrammfläche in Rechtecke unterteilt, die die verschiedenen Ebenen und die relative Größe der Datenhierarchie darstellen. Die Darstellung ähnelt dem Geäst eines Baums, das am Stamm beginnt und sich in immer feinere Zweige aufspaltet. Jedes Rechteck wird in kleinere Rechtecke aufgespalten, die die nächste Hierarchieebene darstellen. Die größten Rechtecke des Treemap-Diagramms werden mit dem größten Rechteck in der oberen linken Ecke des Diagramms angeordnet. Diese Rechtecke stellen die oberste Hierarchieebene dar. Die Rechtecke sind nach absteigender Hierarchie angeordnet, und das kleinste Rechteck befindet sich in der unteren rechten Ecke.  Innerhalb eines Rechtecks sind die Rechtecke ebenfalls der Hierarchie entsprechend von oben links nach unten rechts angeordnet.  

In der folgenden Abbildung eines Beispiel-Treemap-Diagramms ist das Gebiet „Southwest“ (Südwesten) das größte und „Germany“ (Deutschland) das kleinste. Innerhalb des Südwestens ist das Feld „Road Bikes“ (Rennräder) größer als das für „Mountain Bikes“.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>Einfügen eines Treemap-Diagramms und Einrichten der Adventureworks-Beispieldaten  
   
> [!NOTE]
> Bevor Sie Ihrem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset.  Beispieldaten und eine Beispielabfrage finden Sie im Abschnitt [Sample AdventureWorks data (Adventureworks-Beispieldaten)](#bkmk_sample_data).  
  
1.  Klicken Sie mit der rechten Maustaste auf die Designoberfläche und anschließend auf **Einfügen** > **Diagramm**. Klicken Sie auf das **Treemap**-Symbol.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  Passen Sie die Position und Größe des Diagramms an. Für die Verwendung mit den Beispieldaten wird ein Diagramm mit einer Breit von 5 Zoll empfohlen.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  
  
    * **Werte**: LineTotal
    * **Kategoriegruppen** (in der folgenden Reihenfolge):
        1. CategoryName
        2. SubcategoryName
    * **Reihengruppen**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Um die Seitengröße für ein Treemap-Diagramm anzupassen, positionieren Sie die Legende ans Ende.  
  
5.  Klicken Sie mit der rechten Maustaste auf **LineTotal** und anschließend auf **Reiheneigenschaften**, um QuickInfos hinzuzufügen, die die Unterkategorie und die Zeilensumme anzeigen.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Legen Sie die Eigenschaft **QuickInfo** auf den folgenden Wert fest:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Weitere Informationen finden Sie unter [Show ToolTips on a series (Report Builder and SSRS) (Anzeigen von QuickInfos für eine Reihe (Berichts-Generator und SSRS))](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Ändern Sie den Standarddiagrammtitel in **Categorized Sales by Territory** (Verkäufe nach Kategorie und Territorium).  
  
7.  Die Anzahl der angezeigten Beschriftungswerte wird durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst. Um weitere Bezeichnungen anzuzeigen, ändern Sie die **LineTotal**-Eigenschaft **Bezeichnungsschriftart** von **8 Punkt** (standardmäßig eingestellt) in **10 Punkt**.  
  
  
##  <a name="bkmk_sunburst_chart"></a> Sunburst-Diagramm  
 
In einem Sunburst-Diagramm wird die Hierarchie durch eine Reihe von Kreisen dargestellt. Die höchste Ebene der Hierarchie liegt im Zentrum, während die niedrigsten Hierarchieebene Ringe sind, die außerhalb des Zentrums angezeigt werden.  Die unterste Hierarchieebene befindet sich im äußersten Ring.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>Einfügen eines Sunburst-Diagramms und Einrichten der Adventureworks-Beispieldaten  
> [!NOTE] 
> Bevor Sie Ihrem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset. Beispieldaten und eine Beispielabfrage finden Sie im Abschnitt [Sample AdventureWorks data (Adventureworks-Beispieldaten)](#bkmk_sample_data).  
  
1.  Klicken Sie mit der rechten Maustaste auf die Designoberfläche und anschließend auf **Einfügen** > **Diagramm**. Klicken Sie auf das **Sunburst**-Symbol.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  Passen Sie die Position und Größe des Diagramms an. Für die Verwendung mit den Beispieldaten wird ein Diagramm mit einer Breit von 5 Zoll empfohlen.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  

    * **Werte**: LineTotal
    * **Kategoriegruppen** (in der folgenden Reihenfolge):
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **Reihengruppen**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Um die Seitengröße für ein Sunburst-Diagramm zu optimieren, positionieren Sie die Legende ans Ende.  
  
5.  Ändern Sie den Standarddiagrammtitel auf **Categorized Sales by Territory, with sales reason** (Verkäufe nach Kategorie und Territorium, unter Berücksichtigung des Kaufgrunds).  
  
6. Um dem Sunburst-Diagramm die Werte der Kategoriegruppen hinzuzufügen, legen Sie die Beschriftungseigenschaften wie folgt fest: **Visible=true** und **UseValueAsLabel=false**.<br /><br /> Die angezeigten Beschriftungswerte werden durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst.  Um weitere Bezeichnungen anzuzeigen, ändern Sie die **LineTotal**-Eigenschaft **Bezeichnungsschriftart** von **8 Punkt** (standardmäßig eingestellt) in **10 Punkt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  Wenn Sie den Farbbereich ändern möchten, verändern Sie im Diagramm die Eigenschaft **Palette** .  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> AdventureWorks-Beispieldaten  
 Dieser Abschnitt enthält eine Beispielabfrage und die grundlegenden Schritte zum Erstellen einer Datenquelle und eines Datasets in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Wenn Ihr Bericht bereits eine Datenquelle und ein Dataset enthält, können Sie diesen Abschnitt überspringen.  
  
 Die Abfrage gibt detaillierte AdventureWorks-Daten zu Verkaufsaufträgen mit Daten zum Vertriebsgebiet, der Produktkategorie, der Unterkategorie des Produkts und dem Verkaufsgrund aus.  
  
1.  **Rufen Sie die Daten ab**.  
  
     Die Abfrage in diesem Abschnitt basiert auf der AdventureWorks-Datenbank, die unter [AdventureWorks 2016 full database backup (Vollständige Datenbanksicherung von AdventureWorks 2016 )](https://github.com/Microsoft/sql-server-samples/releases) auf GitHub heruntergeladen werden kann.  
  
  
2.  **Erstellen Sie eine Datenquelle**.  
  
    1.  Klicken Sie unter **Berichtsdaten** mit der rechten Maustaste auf die **Datenquellen**, und klicken Sie anschließend auf **Datenquelle hinzufügen**.  
  
    2.  Klicken Sie auf **In meinem Bericht eingebettete Verbindung verwenden**.  
  
    3.  Wählen Sie als Verbindungstyp die Option **Microsoft SQL Server** aus.  
  
    4.  Geben Sie die Verbindungszeichenfolge für Ihren Server und Ihre Datenbank ein. Zum Beispiel:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  Klicken Sie zunächst auf die Schaltfläche **Verbindung testen** und anschließend auf **OK**, um die Verbindung mit der Datenbank zu prüfen.  
  
     Weitere Informationen zum Erstellen einer Datenquelle finden Sie unter [Add and verify a data connection (Report Builder and SSRS) (Hinzufügen und Prüfen einer Datenverbindung (Berichts-Generator und SSRS))](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Erstellen Sie ein Dataset**.  
  
    1. Klicken Sie unter **Berichtsdaten** mit der rechten Maustaste auf **Datenquellen**, und klicken Sie anschließend auf **Datenquelle hinzufügen**.  
  
    2. Wählen Sie **Ein in den eigenen Bericht eingebettetes Dataset verwenden**aus.  
  
    3. Klicken Sie auf die von Ihnen erstellte Datenquelle.  
  
    4. Klicken Sie auf den Abfragetyp **Text**, kopieren Sie die folgende Abfrage, und fügen Sie sie in das Textfeld **Abfrage** ein:  
  
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
  
    5. Wählen Sie **OK**.  
  
     Weitere Informationen zum Erstellen eines Datasets finden Sie unter [Create a shared dataset or embedded dataset (Report Builder and SSRS) (Erstellen eines freigegebenen oder eingebetteten Datasets (Berichts-Generator und SSRS))](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Siehe auch  
* [Shared dataset design view (Report Builder) (Entwurfsansicht für freigegebene Datasets (Berichts-Generator))](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [Show ToolTips on a series (Report Builder and SSRS) (Anzeigen von QuickInfos für eine Reihe (Berichts-Generator und SSRS))](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [Tutorial: Treemaps in Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [Treemap: Visualisierungs-Apps von Microsoft Research Data für Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

