---
title: Programmieren von AMO OLAP Basic Objects | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: ad1c970e-c0cb-4687-9563-56ab62c2db5f
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bebff2d4f64f26f0f1824042512534c5459f2872
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="programming-amo-olap-basic-objects"></a>Programming AMO OLAP basic objects
  Die Erstellung komplexer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Objekte ist einfach und unkompliziert. Allerdings müssen Details genau beachtet werden. In diesem Thema werden die Programmierdetails von grundlegenden OLAP-Objekten erläutert. Dieses Thema enthält folgende Abschnitte:  
  
-   [Dimensionsobjekte](#Dim)  
  
-   [Cubeobjekte](#Cub)  
  
-   [MeasureGroup-Objekte](#MG)  
  
-   [Partitionsobjekte](#Part)  
  
-   [Aggregationsobjekte](#AD)  
  
##  <a name="Dim"></a>Dimensionsobjekte  
 Um eine Dimension zu verwalten oder zu verarbeiten, programmieren Sie das <xref:Microsoft.AnalysisServices.Dimension>-Objekt.  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>Erstellen, Löschen und Suchen einer Dimension  
 Die Erstellung eines <xref:Microsoft.AnalysisServices.Dimension>-Objekts erfolgt in vier Schritten:  
  
1.  Erstellen Sie das Dimensionsobjekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Die grundlegenden Attribute sind Name, Dimensionstyp, Speichermodus, Datenquellenbindung, Name des Alle-Elements für Attribute und andere Dimensionsattribute.  
  
     Vor dem Erstellen einer Dimension sollten Sie sicherstellen, dass die Dimension nicht bereits vorhanden ist. Wenn die Dimension vorhanden ist, wird sie gelöscht und neu erstellt.  
  
2.  Erstellen Sie die Attribute, die die Dimension definieren.  
  
     Jedes Attribut muss einzeln zum Schema hinzugefügt werden, bevor es verwendet wird (siehe CreateDataItem-Methode am Ende des Beispielcodes). Es kann dann zur Attributauflistung der Dimension hinzugefügt werden.  
  
     Die Schlüssel- und die Namensspalte müssen in allen Attributen definiert werden.  
  
     Das Primärschlüsselattribut der Dimension sollte als AttributeUsage.Key definiert werden, um zu verdeutlichen, dass es sich hierbei um den Schlüsselzugriff zur Dimension handelt.  
  
3.  Erstellen Sie die Hierarchien, auf die der Benutzer zugreift, um die Dimension zu navigieren.  
  
     Bei der Erstellung der Hierarchien wird die Ebenenreihenfolge durch die Reihenfolge definiert, in der die Ebenen von oben nach unten erstellt werden. Die höchste Ebene ist die erste, die der Ebenenauflistung der Hierarchie hinzugefügt wird.  
  
4.  Aktualisieren Sie den Server über die Updatemethode der aktuellen Dimension.  
  
 Der folgende Beispielcode erstellt die Product-Dimension aus der Tabelle in der Beispieldatenbank Adventure Works.  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>Verarbeiten einer Dimension  
 Die Verarbeitung einer Dimension ist so einfach wie die Verwendung der Process-Methode des <xref:Microsoft.AnalysisServices.Dimension>-Objekts.  
  
 Die Verarbeitung einer Dimension kann Auswirkungen auf alle Cubes haben, die die Dimension verwenden. Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Im folgenden Code wird ein inkrementelles Update in allen Dimensionen einer bereitgestellten Datenbank vorgenommen:  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a>Cubeobjekte  
 Um einen Cube zu verwalten oder zu verarbeiten, programmieren Sie das <xref:Microsoft.AnalysisServices.Cube>-Objekt.  
  
### <a name="creating-dropping-and-finding-a-cube"></a>Erstellen, Löschen und Suchen eines Cubes  
 Die Verwaltung von Cubes ähnelt der Verwaltung von Dimensionen. Die Erstellung eines <xref:Microsoft.AnalysisServices.Cube>-Objekts erfolgt in vier Schritten:  
  
1.  Erstellen Sie den Cube, und füllen Sie die grundlegenden Attribute auf.  
  
     Die grundlegenden Attribute sind Name, Speichermodus, Datenquellenbindung, Standardmeasure und andere Cubeattribute.  
  
     Vor dem Erstellen eines Cubes sollten Sie sicherstellen, dass der Cube nicht bereits vorhanden ist. Für das Beispiel gilt, dass der Cube gelöscht und neu erstellt wird, wenn er bereits vorhanden ist.  
  
2.  Fügen Sie dem Cube die Dimensionen hinzu.  
  
     Dimensionen werden zur aktuellen Cubedimensionsauflistung aus der Datenbank hinzugefügt; Dimensionen im Cube sind Verweise auf die Datenbankdimensionsauflistung. Dem Cube muss jede Dimension einzeln zugeordnet werden. Im Beispiel erfolgt die Zuordnung der Dimensionen unter Angabe von: dem internen Bezeichner der Datenbankdimension, einem Namen für die Dimension im Cube und einem ID für die benannte Dimension im Cube.  
  
     Beachten Sie im Beispiel, dass die Dimension "Date" drei Mal hinzugefügt wird, wobei bei jedem Hinzufügen ein anderer Cubedimensionsname verwendet wird: Date, Ship Date, Delivery Date. Diese Dimensionen werden als Dimensionen mit unterschiedlichen Rollen bezeichnet. Die grundlegende Dimension ist die gleiche (Date), aber in der Faktentabelle wird die Dimension in unterschiedlichen „Rollen“ gebraucht (Order Date, Ship Date, Delivery Date) – siehe „Erstellen, Löschen und Suchen einer Measuregruppe“ im späteren Teil dieses Dokuments. Hier wird erläutert, wie Dimensionen mit unterschiedlichen Rollen definiert sind.  
  
3.  Erstellen Sie die Measuregruppen, auf die der Benutzer zugreift, um die Daten des Cubes zu durchsuchen.  
  
     Die Erstellung von Measuregruppen wird unter "Erstellen, Löschen und Suchen einer Measuregruppe" im späteren Teil dieses Dokuments erläutert. Im Beispiel wird die Erstellung der Measuregruppen in unterschiedlichen Methoden umschlossen – eine für jede Measuregruppe.  
  
4.  Aktualisieren Sie den Server über die Updatemethode des aktuellen Cubes.  
  
     Die Updatemethode wird mit der Updateoption ExpandFull verwendet, um sicherzustellen, dass alle Objekte auf dem Server vollständig aktualisiert sind.  
  
 Im folgenden Codebeispiel werden die Teile des Adventure Works-Cubes erstellt. Das Codebeispiel erstellt nicht alle Dimensionen oder Measuregruppen, die im Analysis Services-Projektbeispiel für Adventure Works enthalten sind.  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>Verarbeiten eines Cube  
 Die Verarbeitung eines Cubes ist so einfach wie die Verwendung der Process-Methode des <xref:Microsoft.AnalysisServices.Cube>-Objekts. Durch die Verarbeitung eines Cubes werden auch alle Measuregruppen im Cube und alle Partitionen in der Measuregruppe verarbeitet. In einem Cube sind Partitionen die einzigen Objekte, die verarbeitet werden können. Zu Verarbeitungszwecken sind Measuregruppen nur Container für Partitionen. Der für den Cube festgelegte Verarbeitungstyp wird an die Partitionen weitergegeben. Die interne Verarbeitung von Cube und Measuregruppe wird auf die Verarbeitung von Dimensionen und Partitionen aufgelöst.  
  
 Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Processing Objects &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), und [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Im folgenden Code wird eine vollständige Verarbeitung aller Cubes in einer angegebenen Datenbank vorgenommen:  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a>MeasureGroup-Objekte  
 Um eine Measuregruppe zu verwalten oder zu verarbeiten, programmieren Sie das <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekt.  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>Erstellen, Löschen und Suchen einer Measuregruppe  
 Die Verwaltung von Measuregruppen ähnelt der Verwaltung von Dimensionen und Cubes. Die Erstellung eines <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekts wird anhand der folgenden Schritten durchgeführt:  
  
1.  Erstellen Sie das Measuregruppenobjekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Zu den grundlegenden Attributen gehören Name, Speichermodus, Verarbeitungsmodus, Standardmeasure und andere Attribute für Measuregruppen.  
  
     Stellen Sie vor der Erstellung einer Measuregruppe sicher, dass diese noch nicht vorhanden ist. Für den folgenden Beispielcode gilt, dass eine Measuregruppe gelöscht und neu erstellt wird, wenn sie bereits vorhanden ist.  
  
2.  Erstellen Sie die Measures der Measuregruppe. Jedem erstellten Measure werden die folgenden Attribute zugeordnet: Name, Aggregationsfunktion, Quellspalte, Formatzeichenfolge. Andere Attribute können auch zugewiesen werden. Beachten Sie, dass im folgenden Code die CreateDataItem-Methode dem Schema die Spalte hinzufügt.  
  
3.  Fügen Sie die Dimensionen der Measuregruppe hinzu.  
  
4.  Dimensionen werden zur aktuellen Measuregruppen-Dimensionsauflistung aus der übergeordneten Cubedimensionsauflistung hinzugefügt. Sobald die Dimension in die Measuregruppen-Dimensionsauflistung eingebunden ist, kann eine Schlüsselspalte aus der Faktentabelle einer Dimension zugeordnet werden, sodass die Measuregruppe durch die Dimension durchsucht werden kann.  
  
     Beachten Sie im folgenden Beispielcode die Zeilen unter "Mapping dimension and key column from fact table". Die Dimensionen mit unterschiedlichen Rollen werden implementiert, indem unterschiedliche Ersatzschlüssel mit der gleichen Dimension mit unterschiedlichen Namen verknüpft werden. Für jede der Dimensionen mit unterschiedlichen Rollen (Date, Ship Date, Delivery Date) erfolgt ein Link mit einem anderen Ersatzschlüssel (OrderDateKey, ShipDateKey, DueDateKey). Alle Schlüssel stammen aus der Faktentabelle FactInternetSales.  
  
5.  Fügen Sie die ausgearbeiteten Partitionen der Measuregruppe hinzu.  
  
     Im folgenden Beispielcode wird die Partitionserstellung in einer Methode umschlossen.  
  
6.  Aktualisieren Sie den Server über die Updatemethode der aktuellen Measuregruppe.  
  
     Im folgenden Beispielcode werden alle Measuregruppen aktualisiert, wenn der Cube aktualisiert wird.  
  
 Der folgende Beispielcode erstellt die InternetSales-Measuregruppe des Analysis Services-Projektbeispiels für AdventureWorks.  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>Verarbeiten einer Measuregruppe  
 Die Verarbeitung einer Measuregruppe ist so einfach wie die Verwendung der Process-Methode des <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekts. Durch die Verarbeitung einer Measuregruppe werden alle Partitionen, die zu der Measuregruppe gehören, verarbeitet. Die interne Verarbeitung einer Measuregruppe wird auf die Verarbeitung von Dimensionen und Partitionen aufgelöst. Finden Sie unter [Verarbeitung einer Partition](#ProcPart) in diesem Dokument.  
  
 Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Processing Objects &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), und [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Im folgenden Code wird eine vollständige Verarbeitung in allen Measuregruppen eines bereitgestellten Cubes vorgenommen.  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a>Partitionsobjekte  
 Um eine Partition zu verwalten oder zu verarbeiten, programmieren Sie ein <xref:Microsoft.AnalysisServices.Partition>-Objekt.  
  
### <a name="creating-dropping-and-finding-a-partition"></a>Erstellen, Löschen und Suchen einer Partition  
 Partitionen sind einfache Objekte, die in zwei Schritten erstellt werden können.  
  
1.  Erstellen Sie das Partitionsobjekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Die grundlegenden Attributen sind Name, Speichermodus, Partitionsquelle, Slice und andere Attribute für Measuregruppen. Die Partitionsquelle definiert die SQL-Select-Anweisung für die aktuelle Partition. Slice ist ein MDX-Ausdruck, der ein Tupel oder eine Menge festlegt, das/die einen Teil der Dimensionen von der übergeordneten Measuregruppe abtrennt, die in der aktuellen Partition enthalten sind. Bei MOLAP-Partitionen wird das Slicing bei jeder Verarbeitung der Partition automatisch festgelegt.  
  
     Vor dem Erstellen einer Partition sollten Sie sicherstellen, dass die Partition nicht bereits vorhanden ist. Für den folgenden Beispielcode gilt, dass eine Partition gelöscht und neu erstellt wird, wenn sie bereits vorhanden ist.  
  
2.  Aktualisieren Sie den Server über die Updatemethode der aktuellen Partition.  
  
     Im folgenden Beispielcode werden alle Partitionen aktualisiert, wenn der Cube aktualisiert wird.  
  
 Im folgenden Codebeispiel werden Partitionen für die Measuregruppe InternetSales erstellt.  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a>Verarbeiten einer Partition  
 Die Verarbeitung einer Partition ist so einfach wie die Verwendung der Process-Methode des <xref:Microsoft.AnalysisServices.Partition>-Objekts.  
  
 Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Processing Objects &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md) und [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Im folgenden Codebeispiel wird eine vollständige Verarbeitung in allen Partitionen einer festgelegten Measuregruppe vorgenommen.  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>Zusammenführen von Partitionen  
 Das Zusammenführen von Partitionen bedeutet, dass ein Vorgang durchgeführt wird, durch den aus zwei oder mehr Partitionen eine wird.  
  
 Das Zusammenführen von Partitionen ist eine Methode des <xref:Microsoft.AnalysisServices.Partition>-Objekts. Dieser Befehl führt die Daten von einer oder mehreren Quellpartitionen zu einer Zielpartition zusammen und löscht die Quellpartitionen.  
  
 Partitionen können nur zusammengeführt werden, wenn sie sämtliche der folgenden Kriterien erfüllen:  
  
-   Die Partitionen sind in der gleichen Measuregruppe.  
  
-   Die Partitionen werden im gleichen Modus (MOLAP, HOLAP und ROLAP) gespeichert.  
  
-   Die Partitionen befinden sich auf dem gleichen Server; Remotepartitionen können zusammengeführt werden, wenn sie sich auf dem gleichen Server befinden.  
  
 Im Gegensatz zu früheren Versionen in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ist nicht erforderlich, dass alle Quellpartitionen identische aggregationsentwürfe haben.  
  
 Die resultierende Menge der Aggregationen für die Zielpartition ist die gleiche Menge der Aggregationen wie vor dem Zusammenführen.  
  
 Im folgenden Codebeispiel werden alle Partitionen einer festgelegten Measuregruppe zusammengeführt. Die Partitionen werden in der ersten Partition der Measuregruppe zusammengeführt.  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a>Aggregationsobjekte  
 Um eine Aggregation zu entwerfen und diese auf ein oder mehr Partitionen anzuwenden, programmieren Sie das <xref:Microsoft.AnalysisServices.Aggregation>-Objekt.  
  
### <a name="creating-and-dropping-aggregations"></a>Erstellen und Löschen von Aggregationen  
 Aggregationen können leicht durch die DesignAggregations-Methode des <xref:Microsoft.AnalysisServices.AggregationDesign>-Objekts erstellt und Measuregruppen oder Partitionen zugewiesen werden. Das <xref:Microsoft.AnalysisServices.AggregationDesign>-Objekt ist ein Objekt, das von der Partition getrennt ist. Das <xref:Microsoft.AnalysisServices.AggregationDesign>-Objekt ist im <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekt enthalten. Aggregationen können auf eine festgelegte Optimierungsebene (0 bis 100) oder auf eine Speicherebene (Bytes) entworfen werden. Mehrere Partitionen können den gleichen Aggregationsentwurf verwenden.  
  
 Im folgenden Codebeispiel werden Aggregationen für alle Partitionen einer bereitgestellten Measuregruppe erstellt. Alle vorhandenen Aggregationen in Partitionen werden gelöscht.  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO-OLAP-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Installieren von Sample Data and Projects für Analysis Services-mehrdimensionale Modellierung-Lernprogramm](../../../analysis-services/install-sample-data-and-projects.md)  
  
  
