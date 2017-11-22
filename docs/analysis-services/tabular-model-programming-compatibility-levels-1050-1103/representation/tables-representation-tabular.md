---
title: Tabellen-Darstellung (tabellarisch) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: a636fc13-4054-4cea-bce1-192ec4796063
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f658ef13ff4bcc9dd96011f3645272ff32cc4b7e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tables-representation-tabular"></a>Tabellendarstellung (tabellarisch)
  In tabellarischen Modellen ist eine Tabelle die Basisdarstellung der Daten.  
  
## <a name="tables-representation"></a>Tabellendarstellung  
  
### <a name="tables-in-amo"></a>Tabellen in AMO  
 Wenn AMO zum Verwalten einer Tabelle verwendet wird, besteht keine 1:1-Objektentsprechung. In AMO wird eine Tabelle durch dargestellt eine <xref:Microsoft.AnalysisServices.Dimension> und <xref:Microsoft.AnalysisServices.MeasureGroup>. Damit eine Measuregruppe vorhanden sein kann, muss ein <xref:Microsoft.AnalysisServices.Cube> als Host der Measuregruppe definiert werden. Damit eine Dimension, eine Measuregruppe und ein Cube vorhanden sein können, muss ein Datenquellensicht-Objekt definiert werden, das die Bindungsdefinitionen zur Datenquelle enthält.  
  
 Aus einer Verfahrensperspektive muss eine Datenquellensicht vor der Definition jedes anderen Objekts erstellt werden. Das Datenquellensicht-Objekt enthält die Zuordnung für alle relevanten Objekte in der Datenquelle. Die Zuordnung des relationalen Modells wird als .NET DataSet-Objekt in die Datenquellensicht eingebettet und in der Schema-Eigenschaft der Datenquellensicht gespeichert.  
  
 Bei folgendem Codeausschnitt wird davon ausgegangen, dass Sie über Folgendes verfügen: eine SQL-Clientverbindungszeichenfolge, ein Wörterbuch mit SELECT-Anweisungen, die allen Tabellen im relationalen Modell zugeordnet werden, das Sie im tabellarischen Modell darstellen möchten, sowie eine newDataSourceViewName-Variable mit dem Namen der Datenquellensicht (entspricht normalerweise dem Namen der relationalen Datenbank).  
  
```  
  
DataSet newDataSourceViewDataSet = new DataSet(newDataSourceViewName);  
  
Foreach( String tableName in listOfSqlStatements.Keys)  
{  
    String sqlStmt = listOfSqlStatements[tableName];  
  
    DataTable newTable = new DataTable(tableName);  
  
    using (SqlConnection SqlCnx = new SqlConnection(SqlCnxStr))  
    {  
        SqlDataAdapter dataAdapter = new SqlDataAdapter(sqlStmt, SqlCnx);  
        dataAdapter.FillSchema(newTable, SchemaType.Source);  
    }  
    newDataSourceViewDataSet.Tables.Add(newTable);  
}  
  
AMO.DataSourceView newDatasourceView = newDatabase.DataSourceViews.AddNew(newDataSourceViewName, newDataSourceViewName);  
newDatasourceView.DataSourceID = newDatasource.ID; //This is the ID of the DataSource object   
newDatasourceView.Schema = newDataSourceViewDataSet; //Here you are storing all the relational schema in the DSV  
newDatasourceView.Update();  
  
```  
  
 Sobald die Datenquellensicht erstellt und aktualisiert wurde, muss das Cubeobjekt zwar erstellt, aber erst auf dem Server aktualisiert werden, nachdem die erste Tabelle erstellt wurde. Ein Cubeobjekt kann nicht leer erstellt werden. Der folgende Codeausschnitt veranschaulicht, wie ein Cube erstellt wird. Beim Ausschnitt wird davon ausgegangen, dass Sie über die nicht leere Zeichenfolge newCubeName mit dem Namen des Cubes verfügen und dass dieser bereits auf Duplikate überprüft wurde.  
  
```  
  
modelCube = newDatabase.Cubes.Add(newCubeName, newCubeName);  
modelCube.Source = new AMO.DataSourceViewBinding(newDatasourceView.ID);  
modelCube.StorageMode = AMO.StorageMode.InMemory;  
modelCube.Language = newDatabase.Language;  
modelCube.Collation = newDatabase.Collation;  
//Create initial MdxScript  
AMO.MdxScript mdxScript = modelCube.MdxScripts.Add("MdxScript", "MdxScript");  
StringBuilder initialCommand = new StringBuilder();  
initialCommand.AppendLine("CALCULATE;");  
initialCommand.AppendLine("CREATE MEMBER CURRENTCUBE.Measures.[__No measures defined] AS 1;");  
initialCommand.AppendLine("ALTER CUBE CURRENTCUBE UPDATE DIMENSION Measures, Default_Member = [__No measures defined];");  
mdxScript.Commands.Add(new AMO.Command(initialCommand.ToString()));  
  
```  
  
 Nachdem der Cube lokal definiert wurde, können Tabellen erstellt und aktualisiert werden. Im folgenden Verfahren werden die notwendigen Schritte zum Erstellen einer Tabelle veranschaulicht:  
  
1.  Erstellen der Dimension, die die Tabelle darstellt (der Server darf noch nicht aktualisiert werden)  
  
2.  Erstellen des RowNumber-Attributs und Definieren des Attributs als Schlüsselattribut der Dimension  
  
3.  Erstellen der Dimensionsattribute und Kennzeichnen der Attribute mit einer 1:n-Beziehung zu RowNumber  
  
4.  Hinzufügen einer Dimension zu den Cubedimensionen  
  
5.  Erstellen der Measuregruppe, die auch die Tabelle darstellt  
  
6.  Hinzufügen einer Dimension zur Measuregruppe  
  
7.  Erstellen eines AMO-Standardmeasureobjekts für die Measuregruppe. Beachten Sie, dass das AMO-Measureobjekt nur ein einziges Mal verwendet wird. Berechnete Measures in tabellarischen Modellen werden im AMO-Objekt MdxScripts["MdxScript"] definiert.  
  
8.  Erstellen der Standardpartition  
  
9. Aktualisieren der Datenbank  
  
 Der folgende Codeausschnitt veranschaulicht das Erstellen einer Tabelle:  
  
```  
  
private Boolean CreateTable(  
                       AMO.Database db      //the AMO database object where dimension are created  
                     , AMO.Cube cb          //the AMO cube where measure group is created  
                     , DataTable dataTable  //the schema of the table to be created  
                     )  
{  
    String tableID = dataTable.TableName;  
  
    if (db.Dimensions.Contains(tableID))  
    {  
        if (cb.MeasureGroups.Contains(tableID))  
        {  
            cb.MeasureGroups[tableID].Measures.Clear();  
            cb.MeasureGroups[tableID].Partitions.Clear();  
            cb.MeasureGroups.Remove(tableID, true);  
        }  
        if (cb.Dimensions.Contains(tableID))  
        {  
            cb.Dimensions.Remove(tableID, true);  
        }  
        db.Dimensions.Remove(tableID);  
    }  
  
    #region Create Dimension  
    //Define Dimension general properties  
    AMO.Dimension currentDimension = db.Dimensions.AddNew(tableID, tableID);  
    currentDimension.Source = new AMO.DataSourceViewBinding(newDatasourceView.ID);  
    currentDimension.StorageMode = AMO.DimensionStorageMode.InMemory;  
    currentDimension.UnknownMember = AMO.UnknownMemberBehavior.AutomaticNull;  
    currentDimension.UnknownMemberName = "Unknown";  
    currentDimension.ErrorConfiguration = new AMO.ErrorConfiguration();  
    currentDimension.ErrorConfiguration.KeyNotFound = AMO.ErrorOption.IgnoreError;  
    currentDimension.ErrorConfiguration.KeyDuplicate = AMO.ErrorOption.ReportAndStop;  
    currentDimension.ErrorConfiguration.NullKeyNotAllowed = AMO.ErrorOption.ReportAndStop;  
    currentDimension.Language = db.Language;  
    currentDimension.Collation = db.Collation;  
    currentDimension.ProactiveCaching = new AMO.ProactiveCaching();  
    TimeSpan defaultProactiveChachingTimeSpan = new TimeSpan(0, 0, -1);  
    currentDimension.ProactiveCaching.SilenceInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.Latency = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.SilenceOverrideInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.ForceRebuildInterval = defaultProactiveChachingTimeSpan;  
    currentDimension.ProactiveCaching.Source = new AMO.ProactiveCachingInheritedBinding();  
  
    //Manualy add a "RowNumber" attribute as the key attribute of the dimension, until a primary key is defined  
    //"RowNumber" a required column for a tabular model and has to be of type AMO.AttributeType.RowNumber and binding AMO.RowNumberBinding.  
    //The name of the "RowNumber" attribute can be any name, as long as type and binding are correctly set  
    //By default, the MS client tools set the column name and column ID of the RowNumber attribute to "RowNumber"  
    //In this sample, to avoid problems, on any customer table that contains a column named 'RowNumber'   
    //the Id value of the column (in the dimension object) will be renamed to 'RowNumber_in_<TableName>' and the Name of the column will remain "RowNumber"  
  
    AMO.DimensionAttribute currentAttribute = currentDimension.Attributes.Add("RowNumber", "RowNumber");  
    currentAttribute.Type = AMO.AttributeType.RowNumber;  
    currentAttribute.KeyUniquenessGuarantee = true;  
    currentAttribute.Usage = AMO.AttributeUsage.Key;  
    currentAttribute.KeyColumns.Add(new AMO.DataItem());  
    currentAttribute.KeyColumns[0].DataType = System.Data.OleDb.OleDbType.Integer;  
    currentAttribute.KeyColumns[0].DataSize = 4;  
    currentAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Error;  
    currentAttribute.KeyColumns[0].Source = new AMO.RowNumberBinding();  
    currentAttribute.NameColumn = new AMO.DataItem();  
    currentAttribute.NameColumn.DataType = System.Data.OleDb.OleDbType.WChar;  
    currentAttribute.NameColumn.DataSize = 4;  
    currentAttribute.NameColumn.NullProcessing = AMO.NullProcessing.ZeroOrBlank;  
    currentAttribute.NameColumn.Source = new AMO.RowNumberBinding();  
    currentAttribute.OrderBy = AMO.OrderBy.Key;  
    currentAttribute.AttributeHierarchyVisible = false;  
    //Deferring AttributeRelationships until after adding each other attribute  
    //Add each column in the table as an attribute in the dimension  
    foreach (DataColumn dataColumn in dataTable.Columns)  
    {  
        string attributeID, attributeName;  
        if (dataColumn.ColumnName != "RowNumber")  
        {  
            attributeID = dataColumn.ColumnName;  
        }  
        else  
        {  
            attributeID = string.Format("RowNumber_in_{0}", dataTable.TableName);  
        }  
        attributeName = dataColumn.ColumnName;  
        currentAttribute = currentDimension.Attributes.Add(attributeName, attributeID);  
        currentAttribute.Usage = AMO.AttributeUsage.Regular;  
        currentAttribute.KeyUniquenessGuarantee = false;  
        currentAttribute.KeyColumns.Add(new AMO.DataItem(dataTable.TableName, dataColumn.ColumnName, AMO.OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType)));  
        currentAttribute.KeyColumns[0].Source = new AMO.ColumnBinding(dataTable.TableName, dataColumn.ColumnName);  
        currentAttribute.KeyColumns[0].NullProcessing = AMO.NullProcessing.Preserve;  
        currentAttribute.NameColumn = new AMO.DataItem(dataTable.TableName, dataColumn.ColumnName, System.Data.OleDb.OleDbType.WChar);  
        currentAttribute.NameColumn.Source = new AMO.ColumnBinding(dataTable.TableName, dataColumn.ColumnName);  
        currentAttribute.NameColumn.NullProcessing = AMO.NullProcessing.ZeroOrBlank;  
        currentAttribute.OrderBy = AMO.OrderBy.Key;  
        AMO.AttributeRelationship currentAttributeRelationship = currentDimension.Attributes["RowNumber"].AttributeRelationships.Add(currentAttribute.ID);  
        currentAttributeRelationship.Cardinality = AMO.Cardinality.Many;  
        currentAttributeRelationship.OverrideBehavior = AMO.OverrideBehavior.None;  
    }  
    #endregion  
  
    #region Add Dimension to Model cube  
    cb.Dimensions.Add(tableID, tableID, tableID);  
    #endregion  
  
    #region Add MeasureGroup to Model cube  
    AMO.MeasureGroup currentMeasureGroup = cb.MeasureGroups.Add(tableID, tableID);  
    currentMeasureGroup.StorageMode = AMO.StorageMode.InMemory;  
    currentMeasureGroup.ProcessingMode = AMO.ProcessingMode.Regular;  
  
    //Adding Dimension  
    AMO.DegenerateMeasureGroupDimension currentMGDim = new AMO.DegenerateMeasureGroupDimension(tableID);  
    currentMeasureGroup.Dimensions.Add(currentMGDim);  
    currentMGDim.ShareDimensionStorage = AMO.StorageSharingMode.Shared;  
    currentMGDim.CubeDimensionID = tableID;  
    foreach (AMO.CubeAttribute ca in cb.Dimensions[tableID].Attributes)  
    {  
        AMO.MeasureGroupAttribute mga = new AMO.MeasureGroupAttribute(ca.AttributeID);  
        if (mga.AttributeID == "RowNumber")  
        {  
            mga.Type = AMO.MeasureGroupAttributeType.Granularity;  
            AMO.DataItem rowNumberKeyColumn = new AMO.DataItem(new AMO.ColumnBinding(tableID, "RowNumber"));  
            rowNumberKeyColumn.DataType = System.Data.OleDb.OleDbType.Integer;  
            mga.KeyColumns.Add(rowNumberKeyColumn);  
        }  
        else  
        {  
            foreach (AMO.DataItem di in ca.Attribute.KeyColumns)  
            {  
                AMO.DataItem keyColumn = new AMO.DataItem(new AMO.ColumnBinding(tableID, ((AMO.ColumnBinding)di.Source).ColumnID));  
                keyColumn.DataType = di.DataType;  
                keyColumn.NullProcessing = AMO.NullProcessing.Preserve;  
                keyColumn.InvalidXmlCharacters = AMO.InvalidXmlCharacters.Remove;  
                mga.KeyColumns.Add(keyColumn);  
            }  
        }  
        currentMGDim.Attributes.Add(mga);  
    }  
  
    //Adding default Measure  
    String defaultMeasureID = string.Concat("_Count ", tableID);  
    AMO.Measure currentMeasure = currentMeasureGroup.Measures.Add(defaultMeasureID, defaultMeasureID);  
    currentMeasure.AggregateFunction = AMO.AggregationFunction.Count;  
    currentMeasure.DataType = AMO.MeasureDataType.BigInt;  
    AMO.DataItem currentMeasureSource = new AMO.DataItem(new AMO.RowBinding(tableID));  
    currentMeasureSource.DataType = System.Data.OleDb.OleDbType.BigInt;  
    currentMeasure.Source = currentMeasureSource;  
  
    //Partitions  
    AMO.Partition currentPartition = new AMO.Partition(tableID, tableID);  
    currentPartition.StorageMode = AMO.StorageMode.InMemory;  
    currentPartition.ProcessingMode = AMO.ProcessingMode.Regular;  
    currentPartition.Source = new AMO.QueryBinding(newDatasource.ID, (String)dataTable.ExtendedProperties["sqlStmt"]);  
    currentMeasureGroup.Partitions.Add(currentPartition);  
  
    #endregion  
  
    #region Update new objects in database  
    db.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
    #endregion  
  
    return true;  
}  
  
```  
  
> [!CAUTION]  
>  Der oben erwähnte Codeausschnitt umfasst keine Fehlerüberprüfungs- bzw. Cleanupverfahren bei Fehlern.  
  
  
