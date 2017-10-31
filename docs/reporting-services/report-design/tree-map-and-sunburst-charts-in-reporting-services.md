---
title: TreeMap-Diagramm und Sunburst-Diagramme in SQL Server Reporting Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: de-de
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>TreeMap-Diagramm und Sunburst-Diagramme in Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] TreeMap-Diagramm und Sunburst-Visualisierung sind hervorragend für die visuelle Darstellung von hierarchischen Daten. Dieser Artikel bietet eine Übersicht über das Hinzufügen einer TreeMap-Diagramm oder Sunburst-Diagramm zu einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Bericht. Der Artikel umfasst auch eine AdventureWorks-Beispielabfrage, um Ihnen beim Einstieg helfen.  
  
##  <a name="bkmk_treemap_chart"></a>TreeMap-Diagramm  

Ein Treemap-Diagramm wird die Diagrammfläche in Rechtecke, die die verschiedenen Ebenen und die relative Größe der Datenhierarchie darstellen unterteilt. Die Darstellung ähnelt dem Geäst eines Baums, das am Stamm beginnt und sich in immer feinere Zweige aufspaltet. Jedes Rechteck wird in kleinere Rechtecke aufgespaltet, die die nächste Ebene in der Hierarchie darstellen. Rechtecke der obersten Ebene TreeMap-Diagramm sind mit Ihrem größten Rechteck in der oberen linken Ecke des Diagramms, um das kleinste Rechteck befindet sich in der unteren rechten Ecke angeordnet.  Innerhalb eines Rechtecks sind die Rechtecke ebenfalls der Hierarchie entsprechend von oben links nach unten rechts angeordnet.  

Beispielsweise in der folgenden Abbildung eines Beispiel-Treemap, Gebiet Südwestens ist das größte und (Deutschland) das kleinste. Innerhalb des Südwestens ist das Feld „Road Bikes“ (Rennräder) größer als das für „Mountain Bikes“.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>So fügen Sie ein Treemap-Diagramm, und richten Sie die AdventureWorks-Beispieldaten  
   
> [!NOTE]
> Bevor Sie dem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset.  Beispieldaten und eine Beispielabfrage finden Sie unter [AdventureWorks-Beispieldaten](#bkmk_sample_data).  
  
1.  Mit der rechten Maustaste in der Entwurfsoberfläche, und wählen Sie dann **einfügen** > **Diagramm**. Wählen Sie die **Treemap** Symbol.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  Passen Sie die Position und Größe des Diagramms an. Um mit den Beispieldaten verwenden, wird ein Diagramm, das 5 Zoll breit ist ein guter Ausgangspunkt.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  
  
    * **Werte**: "LineTotal"
    * **Kategoriegruppen** (in der folgenden Reihenfolge):
        1. Kategoriename
        2. SubcategoryName
    * **Series Groups**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Um die Seitengröße für die allgemeine Form des ein TreeMap-Diagramm zu optimieren, positionieren Sie die Legende im unteren Bereich.  
  
5.  Um QuickInfos hinzuzufügen, die die Unterkategorie und die Zeilensumme anzeigen, Maustaste **"LineTotal"**, und wählen Sie dann **Reiheneigenschaften**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Legen Sie die **QuickInfo** Eigenschaft auf den folgenden Wert:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Weitere Informationen finden Sie unter [QuickInfo anzeigen, auf eine Reihe &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Ändern Sie den standarddiagrammtitel auf **kategorisiert Sales by Territory**.  
  
7.  Die Anzahl der angezeigten Beschriftungswerte wird durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst. Um weitere Beschriftungen anzuzeigen, Ändern der **"Bezeichnungsschriftart"** Eigenschaft **"LineTotal"** auf **10 pt** vom Standardwert **8pt**.  
  
  
##  <a name="bkmk_sunburst_chart"></a>Sunburst-Diagramm  
 
Die Hierarchie wird in einem Sunburst-Diagramm durch eine Reihe von Kreisen dargestellt. Die höchste Ebene der Hierarchie ist in der Mitte und niedrigere Ebenen der Hierarchie sind Ringe außerhalb der Mitte angezeigt.  Die unterste Hierarchieebene befindet sich im äußersten Ring.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>So fügen Sie ein Sunburst-Diagramm, und richten Sie die AdventureWorks-Beispieldaten  
> [!NOTE] 
> Bevor Sie dem Bericht ein Diagramm hinzufügen, erstellen Sie eine Datenquelle und ein Dataset. Beispieldaten und eine Beispielabfrage finden Sie unter [AdventureWorks-Beispieldaten](#bkmk_sample_data).  
  
1.  Mit der rechten Maustaste in der Entwurfsoberfläche, und wählen Sie dann **einfügen** > **Diagramm**. Wählen Sie die **Sunburst** Symbol.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  Passen Sie die Position und Größe des Diagramms an. Um mit den Beispieldaten verwenden, wird ein Diagramm, das 5 Zoll breit ist ein guter Ausgangspunkt.  
  
3.  Fügen Sie die folgenden Felder aus den Beispieldaten hinzu:  

    * **Werte**: "LineTotal"
    * **Kategoriegruppen** (in der folgenden Reihenfolge):
        1. Kategoriename
        2. SubcategoryName
        3. SalesReasonName
    * **Series Groups**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Um die Seitengröße für die allgemeine Form des ein Sunburst-Diagramm zu optimieren, positionieren Sie die Legende im unteren Bereich.  
  
5.  Ändern Sie den standarddiagrammtitel auf **Sales kategorisiert nach Gebiet, mit Verkaufsgrund**.  
  
6. Um dem Sunburst-Diagramm als Bezeichnungen die Werte der Kategoriegruppen hinzuzufügen, legen Sie die Eigenschaften von **Visible = "true"** und **UseValueAsLabel = "false"**.<br /><br /> Die angezeigten Beschriftungswerte werden durch die Größe der Schriftart, die Gesamtgröße der Diagrammfläche und die Größe der jeweiligen Rechtecke beeinflusst.  Um weitere Beschriftungen anzuzeigen, Ändern der **"Bezeichnungsschriftart"** Eigenschaft **"LineTotal"** auf **10 pt** vom Standardwert **8pt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  Wenn Sie den Farbbereich ändern möchten, verändern Sie im Diagramm die Eigenschaft **Palette** .  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>AdventureWorks-Beispieldaten  
 Dieser Abschnitt enthält eine Beispielabfrage und die grundlegenden Schritte zum Erstellen einer Datenquelle und eines Datasets im [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Wenn Ihr Bericht bereits eine Datenquelle und ein Dataset enthält, können Sie diesen Abschnitt überspringen.  
  
 Die Abfrage gibt AdventureWorks sales Order Detail-Daten mit Vertriebsgebiet, Product Category, Product Subcategory und Verkaufsgrund aus.  
  
1.  **Rufen Sie Daten**.  
  
     Die Abfrage in diesem Abschnitt basiert auf der AdventureWorks-Datenbank, die zum Download von GitHub verfügbar ist: [AdventureWorks 2016 vollständige datenbanksicherung](https://github.com/Microsoft/sql-server-samples/releases).  
  
  
2.  **Erstellen einer Datenquelle**.  
  
    1.  Klicken Sie unter **Berichtsdaten**, mit der rechten Maustaste **Datenquellen**, und wählen Sie dann **Datenquelle hinzufügen**.  
  
    2.  Klicken Sie auf **In meinem Bericht eingebettete Verbindung verwenden**.  
  
    3.  Wählen Sie für den Verbindungstyp, **Microsoft SQL Server**.  
  
    4.  Geben Sie die Verbindungszeichenfolge für Ihren Server und Datenbank ein. Beispiel:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  Wählen Sie zum Überprüfen der Verbindung die **Testverbindung** Schaltfläche und wählen Sie dann **OK**.  
  
     Weitere Informationen zum Erstellen einer Datenquelle finden Sie unter [hinzufügen und überprüfen Sie, ob eine Datenverbindung mit &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Erstellen Sie ein Dataset**.  
  
    1. Klicken Sie unter **Berichtsdaten**, mit der rechten Maustaste **Datasets**, und wählen Sie dann **Dataset hinzufügen**.  
  
    2. Wählen Sie **Ein in den eigenen Bericht eingebettetes Dataset verwenden**aus.  
  
    3. Wählen Sie die Datenquelle, die Sie erstellt haben.  
  
    4. Wählen Sie die **Text** Abfragetyp, und klicken Sie dann kopieren und fügen Sie die folgende Abfrage in der **Abfrage** Textfeld:  
  
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
  
     Weitere Informationen zum Erstellen eines Datasets finden Sie unter [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Siehe auch  
* [Freigegebene datasetentwurfsansicht &#40; Berichts-Generator &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [Anzeigen von QuickInfos für eine Reihe &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [Tutorial: Treemaps in Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [Treemap: Visualisierungs-Apps von Microsoft Research Data für Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


