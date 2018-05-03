---
title: Programmieren von AMO Fundamental Objects | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bc8a2cf279f204d76e96657bfb25c0ebfe14329
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-fundamental-objects"></a>Programming AMO Fundamental objects
  Grundlegende Objekte sind im Allgemeinen einfache und unkomplizierte Objekte. Diese Objekte werden in der Regel erstellt und instanziiert, und wenn sie nicht mehr benötigt werden, trennt der Benutzer die Verbindung zu ihnen. Grundlegende Klassen beinhalten die folgenden Objekte: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource> und <xref:Microsoft.AnalysisServices.DataSourceView>. Das einzige komplexe Objekt innerhalb der grundlegenden AMO-Objekte ist <xref:Microsoft.AnalysisServices.DataSourceView>, das Details benötigt, um das abstrakte Modell zu erstellen, das die Datenquellensicht darstellt.  
  
 <xref:Microsoft.AnalysisServices.Server>- und <xref:Microsoft.AnalysisServices.Database>-Objekte sind in der Regel erforderlich, um die enthaltenen Objekte als OLAP- oder Data Mining-Objekte zu verwenden.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Serverobjekte](#ServerObjects)  
  
-   [AMOException-Ausnahmeobjekte](#AMO)  
  
-   [Datenbankobjekte](#DatabaseObjects)  
  
-   [DataSource-Objekte](#DataSource)  
  
-   [DataSourceView-Objekte](#DSV)  
  
##  <a name="ServerObjects"></a> Serverobjekte  
 Verwenden einer <xref:Microsoft.AnalysisServices.Server> Objekt erfordert die folgenden Schritte: Herstellen einer Verbindung mit dem Server, zu überprüfen, ob die <xref:Microsoft.AnalysisServices.Server> Objekt, mit dem Server verbunden ist, und wenn dies der Fall ist, Trennen der <xref:Microsoft.AnalysisServices.Server> vom Server.  
  
### <a name="connecting-to-the-server-object"></a>Herstellen einer Verbindung mit dem Serverobjekt  
 Um eine Verbindung mit dem Server herzustellen, ist die richtige Verbindungszeichenfolge erforderlich.  
  
 Im folgenden Codebeispiel Beispiel gibt eine <xref:Microsoft.AnalysisServices.Server> Objekt, wenn die Verbindung erfolgreich ist, oder gibt **null** Wenn ein Fehler auftritt. Fehler während des Verbindungsprozesses werden in einem try/catch-Konstrukt behandelt. AMO-Fehler werden mit der <xref:Microsoft.AnalysisServices.AmoException>-Ausnahmeklasse abgefangen. In diesem Beispiel wird dem Benutzer der Fehler in einem Meldungsfeld angezeigt.  
  
```  
static Server ServerConnect( String strStringConnection)  
{  
    string methodCaption = "ServerConnect method";  
    Server svr = new Server();  
    try  
    {  
        svr.Connect(strStringConnection);  
    }  
    #region ErrorHandling  
    catch (AmoException e)  
    {  
        MessageBox.Show( "AMO exception " + e.ToString());  
        svr = null;  
    }  
    catch (Exception e)  
    {  
        MessageBox.Show("General exception " + e.ToString());  
        svr = null;  
    }  
    #endregion  
  
    return svr;  
}  
```  
  
 Die Struktur der Verbindungszeichenfolge lautet wie folgt:  
  
 "**Datenquelle =**\<Servername >".  
  
 Weitere Informationen zur Verbindungszeichenfolge, finden Sie unter <xref:Microsoft.SqlServer.Management.Common.OlapConnectionInfo.ConnectionString%2A>.  
  
### <a name="validating-the-connection"></a>Überprüfen der Verbindung  
 Vor dem Programmieren der <xref:Microsoft.AnalysisServices.Server>-Objekte sollten Sie überprüfen, ob Sie immer noch mit dem Server verbunden sind. Im folgenden Codebeispiel wird dies veranschaulicht. Im Beispiel wird davon ausgegangen, dass `svr` ein <xref:Microsoft.AnalysisServices.Server>-Objekt ist, das in Ihrem Code vorhanden ist.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    // Do what it is needed if connection is good  
}  
```  
  
### <a name="disconnecting-from-the-server"></a>Trennen der Verbindung zum Server  
 Sobald Sie fertig sind, können Sie die Verbindung zum Server mit der Disconnect-Methode trennen. Im folgenden Codebeispiel wird dies veranschaulicht. Im Beispiel wird davon ausgegangen, dass `svr` ein <xref:Microsoft.AnalysisServices.Server>-Objekt ist, das in Ihrem Code vorhanden ist.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    svr.Disconnect()  
}  
```  
  
###  <a name="AMO"></a> AmoException-Ausnahmeobjekte  
 AMO löst bei verschiedenen Problemen Ausnahmen aus. Eine ausführliche Erläuterung der Ausnahmen finden Sie unter [andere AMO-Klassen und Methoden](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md). Im folgenden Beispielcode wird die richtige Methode veranschaulicht, um Ausnahmen in AMO zu erfassen:  
  
```  
try  
{  
   //... some AMO code in here  
}  
  
catch (  OutOfSynchException e)  
{  
   // error handling code for OutOfSynchException   
}  
  
catch (  OperationException e)  
{  
   // error handling code for OperationException   
}   
  
catch (  ResponseFormatException e)  
  
{  
   // error handling code for ResponseFormatException   
}   
  
catch (  ConnectionException e)  
  
{  
   // error handling code for ConnectionException   
}  
  
catch (  AMOException e)  
  
{  
   //... here is the place where you end if it is an AMO exception, but none of the previous exceptions  
   // if you start with AMOException in the first catch you will never see any one of the previous exceptions  
}  
```  
  
##  <a name="DatabaseObjects"></a> Datenbankobjekte  
 Die Verwendung eines <xref:Microsoft.AnalysisServices.Database>-Objekts ist sehr einfach und unkompliziert. Sie rufen aus der Datenbankauflistung des <xref:Microsoft.AnalysisServices.Server>-Objekts eine vorhandene Datenbank ab.  
  
### <a name="creating-dropping-and-finding-a-database"></a>Erstellen, Löschen und Suchen einer Datenbank  
 Im folgenden Codebeispiel wird gezeigt, wie eine Datenbank mithilfe eines Datenbanknamens erstellt wird. Fragen Sie vor dem Erstellen der Datenbank die <xref:Microsoft.AnalysisServices.DatabaseCollection> vom Server ab, um festzustellen, ob die Datenbank vorhanden ist. Wenn die Datenbank vorhanden ist, wird sie gelöscht und anschließend neu erstellt. Wenn die Datenbank nicht vorhanden ist, wird sie erstellt. Wenn die Datenbank gelöscht werden muss, wird sie zunächst aus der Datenbankauflistung abgerufen.  
  
```  
static Database CreateDatabase(Server svr, String DatabaseName)  
{  
    Database db = null;  
    if ( (svr != null) && ( svr.Connected))  
    {  
        // Drop the database if it already exists  
        db = svr.Databases.FindByName(DatabaseName);  
        if (db != null)  
        {  
            db.Drop();  
        }  
  
        // Create the database  
        db = svr.Databases.Add(DatabaseName);  
        db.Update();  
    }  
  
    return db;  
}  
```  
  
 Um zu bestimmen, ob eine Datenbank in der Datenbankauflistung vorhanden ist, wird die FindByName-Methode verwendet. Wenn die Datenbank vorhanden ist, gibt die Methode das gefundene Datenbankobjekt zurück. Wenn sie nicht vorhanden ist, wird ein Null-Objekt zurückgegeben.  
  
 Sobald das <xref:Microsoft.AnalysisServices.Database>-Objekt der Datenbankauflistung hinzugefügt wurde, muss der Server mithilfe der Update-Methode aktualisiert werden. Wenn der Server nicht aktualisiert wird, wird das <xref:Microsoft.AnalysisServices.Database>-Objekt nicht im Server erstellt.  
  
### <a name="processing-a-database"></a>Verarbeiten einer Datenbank  
 Das Verarbeiten einer Datenbank mit allen untergeordneten Objekten ist einfach, da das <xref:Microsoft.AnalysisServices.Database>-Objekt eine Process-Methode beinhaltet.  
  
 Die Process-Methode kann Parameter einschließen, aber sie sind nicht erforderlich. Wenn keine Parameter angegeben werden, und klicken Sie dann alle untergeordneten Objekte verarbeitet werden mit ihren **ProcessDefault** Option. Weitere Informationen zu Verarbeitungsoptionen finden Sie unter <xref:Microsoft.AnalysisServices.Database>.  
  
1.  Der folgende Beispielcode verarbeitet eine Datenbank gemäß Standardwert.  
  
```  
static Database ProcessDatabase(Database db, ProcessType pt)  
{  
    db.Process( pt);  
    return db;  
}  
```  
  
##  <a name="DataSource"></a> DataSource-Objekte  
 Ein <xref:Microsoft.AnalysisServices.DataSource>-Objekt ist der Link zwischen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und der Datenbank, in der sich die Daten befinden. Das Schema, das das zugrunde liegende Modell für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] darstellt, wird vom <xref:Microsoft.AnalysisServices.DataSourceView>-Objekt definiert. Ein <xref:Microsoft.AnalysisServices.DataSource>-Objekt kann als Verbindungszeichenfolge zur Datenbank, in der sich die Daten befinden, betrachtet werden.  
  
 Im folgenden Codebeispiel wird das Erstellen eines <xref:Microsoft.AnalysisServices.DataSource>-Objekts veranschaulicht. Das Beispiel überprüft, ob der Server immer noch vorhanden, das <xref:Microsoft.AnalysisServices.Server>-Objekt verbunden und die Datenbank vorhanden ist. Wenn das <xref:Microsoft.AnalysisServices.DataSource>-Objekt vorhanden ist, wird es gelöscht und neu erstellt. Das <xref:Microsoft.AnalysisServices.DataSource>-Objekt wird mit dem gleichen Namen und der gleichen internen ID erstellt. In diesem Beispiel wird keine Überprüfung der Verbindungszeichenfolge ausgeführt.  
  
```  
static string CreateDataSource(Database db, string strDataSourceName, string strConnectionString)  
{  
        Server svr = db.Parent;  
        DataSource ds = db.DataSources.FindByName(strDataSourceName);  
        if (ds != null)  
            ds.Drop();  
        // Create the data source  
        ds = db.DataSources.Add(strDataSourceName, strDataSourceName);  
        ds.ConnectionString = strConnectionString;  
  
        // Send the data source definition to the server.  
        ds.Update();  
  
        return ds.Name;  
}  
```  
  
##  <a name="DSV"></a> DataSourceView-Objekte  
 Das <xref:Microsoft.AnalysisServices.DataSourceView>-Objekt enthält das Schemamodell für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Damit das <xref:Microsoft.AnalysisServices.DataSourceView>-Objekt das Schema enthalten kann, muss das Schema zuerst erstellt werden. Schemas werden mithilfe des System.Data-Namespace über DataSet-Objekte erstellt.  
  
 Mit dem folgenden Beispielcode wird ein Teil des Schemas erstellt, das in dem auf AdventureWorks basierenden Analysis Services-Beispielprojekt enthalten ist. In dem Beispiel werden Schemadefinitionen für Tabellen, berechnete Spalten, Beziehungen und zusammengesetzte Beziehungen erstellt. Schemas sind persistente Datasets.  
  
 Der Beispielcode führt die folgenden Aufgaben aus:  
  
1.  Erstellen eines <xref:Microsoft.AnalysisServices.DataSourceView>-Objekts.  
  
     Überprüfen Sie zunächst, ob die <xref:Microsoft.AnalysisServices.DataSource> Objekt vorhanden ist; Wenn **"true"**, legen Sie die <xref:Microsoft.AnalysisServices.DataSource> und erstellen Sie ihn. Wenn die <xref:Microsoft.AnalysisServices.DataSource> nicht vorhanden ist, erstellen Sie sie.  
  
2.  Herstellen einer Verbindung zur Datenbank mithilfe der <xref:Microsoft.AnalysisServices.DataSource>-Verbindungszeichenfolge.  
  
3.  Erstellen des Schemas.  
  
     Das Schema umfasst Folgendes:  
  
    -   Eine Tabellendefinition, die `AddTable()`-Methode.  
  
    -   Einen optionalen Satz berechneter Spalten, die `AddComputedColumn()`-Methode.  
  
    -   Einen optionalen Satz von Beziehungen, `AddRelation`.  
  
    -   Einen optionalen Satz zusammengesetzter Beziehungen, `AddCompositeRelations`.  
  
4.  Aktualisieren des Servers.  
  
> [!NOTE]  
>  Der folgende Beispielcode wurde für eine bessere Lesbarkeit gekürzt; den vollständigen Code finden Sie am Ende dieses Themas.  
  
> [!NOTE]  
>  Die folgenden Methoden sind Teil des Beispielcodes: `AddTable`, `AddComputedColumn`, `AddRelation` und `AddCompositeRelation`.  
  
> [!NOTE]  
>  Die Klausel `'WHERE 1=0'` vermeiden Sie die Abfrage wiederkehrender Zeilen an die **DataSet** Objekt.  
  
```  
        static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
        {  
            // Create the data source view  
            DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
            if ( dsv != null)  
               dsv.Drop();  
            dsv = db.DataSourceViews.Add(strDataSourceName);  
            dsv.DataSourceID = strDataSourceName;  
            dsv.Schema = new DataSet();  
            dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
            // Open a connection to the data source  
            OleDbConnection connection  
                = new OleDbConnection(dsv.DataSource.ConnectionString);  
            connection.Open();  
  
            #region Create tables  
  
            // Add the DimTime table  
            AddTable(dsv, connection, "DimTime");  
            AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
  
            // Add the DimProductCategory table  
            AddTable(dsv, connection, "DimProductCategory");  
  
            // Add the DimProductSubcategory table  
            AddTable(dsv, connection, "DimProductSubcategory");  
            AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
            // Add the FactInternetSales table  
            AddTable(dsv, connection, "FactInternetSales");  
"DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
  
            // Add the FactInternetSalesReason table  
            AddTable(dsv, connection, "FactInternetSalesReason");  
            AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
            dsv.Update();  
  
            #endregion  
  
            // Send the data source view definition to the server  
            dsv.Update();  
  
            return dsv;  
        }  
  
        static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
        {  
            string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
            OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
            DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
  
            dataTable.ExtendedProperties.Add("TableType", "Table");  
            dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
            dataTable.ExtendedProperties.Add("DbTableName", tableName);  
            dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
        }  
  
        static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
        {  
            DataSet tmpDataSet = new DataSet();  
            tmpDataSet.Locale = CultureInfo.CurrentCulture;  
            OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
                + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
                + tableName + "] WHERE 1=0", connection);  
            DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
            DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
            dataTable.Constraints.Clear();  
            dataTable.Columns.Remove(dataColumn);  
  
            dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
            dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
                expression);  
            dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
            dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
            dataColumn = null;  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
            tmpDataSet = null;  
        }  
  
        static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
        {  
            DataColumn fkColumn  
                = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
            DataColumn pkColumn  
                = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
                + fkColumnName, pkColumn, fkColumn, true);  
        }  
  
        static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
        {  
            DataColumn[] fkColumns = new DataColumn[2];  
            fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
            fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
            DataColumn[] pkColumns = new DataColumn[2];  
            pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
            pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
                + "_" + columnName2, pkColumns, fkColumns, true);  
        }  
  
```  
  
 Im Beispielcode wird die `AddTable` und `AddComputedColumn` Methoden verwenden die `FillSchema` Methode der **"DataAdapter"** hinzuzufügende Objekt eine **DataTable** auf eine **DataSet**und so konfigurieren Sie das Schema, in der Datenquelle entsprechen. Die erweiterten Eigenschaften fügen erforderliche Informationen hinzu, um das Schema für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu konfigurieren.  
  
 Im Beispielscode fügen die `AddRelation`-Methode und die `AddCompositeRelation`-Methode abhängig vom vorhandenen Schema und den vorhandenen Spalten des Modells die Beziehungsspalten hinzu. Spalten müssen Teil der Tabellen sein, die im Schema definiert sind, damit diese Methoden funktionieren.  
  
 Dies ist das vollständige Codebeispiel:  
  
```  
static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
{  
    // Create the data source view  
    DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
    if ( dsv != null)  
       dsv.Drop();  
    dsv = db.DataSourceViews.Add(strDataSourceName);  
    dsv.DataSourceID = strDataSourceName;  
    dsv.Schema = new DataSet();  
    dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
    // Open a connection to the data source  
    OleDbConnection connection  
        = new OleDbConnection(dsv.DataSource.ConnectionString);  
    connection.Open();  
  
    #region Create tables  
  
    // Add the DimTime table  
    AddTable(dsv, connection, "DimTime");  
    AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarYearDesc", "'CY' + ' ' + CalendarYear");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarSemesterDesc", "CASE WHEN CalendarSemester = 1 THEN 'H1'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) ELSE 'H2'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarQuarterDesc", "'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "MonthName", "EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalYearDesc", "'FY' + ' ' + FiscalYear");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalSemesterDesc", "CASE WHEN FiscalSemester = 1 THEN 'H1'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) ELSE 'H2'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalQuarterDesc", "'Q' + CONVERT(CHAR (1), FiscalQuarter) +' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalMonthNumberOfYear", "CASE WHEN MonthNumberOfYear = '1'  THEN CONVERT(int,'7') WHEN MonthNumberOfYear = '2'  THEN CONVERT(int,'8') WHEN MonthNumberOfYear = '3'  THEN CONVERT(int,'9') WHEN MonthNumberOfYear = '4'  THEN CONVERT(int,'10') WHEN MonthNumberOfYear = '5'  THEN CONVERT(int,'11') WHEN MonthNumberOfYear = '6'  THEN CONVERT(int,'12') WHEN MonthNumberOfYear = '7'  THEN CONVERT(int,'1') WHEN MonthNumberOfYear = '8'  THEN CONVERT(int,'2') WHEN MonthNumberOfYear = '9'  THEN CONVERT(int,'3') WHEN MonthNumberOfYear = '10' THEN CONVERT(int,'4') WHEN MonthNumberOfYear = '11' THEN CONVERT(int,'5') WHEN MonthNumberOfYear = '12' THEN CONVERT(int,'6') END");  
    dsv.Update();  
  
    // Add the DimGeography table  
    AddTable(dsv, connection, "DimGeography");  
  
    // Add the DimProductCategory table  
    AddTable(dsv, connection, "DimProductCategory");  
  
    // Add the DimProductSubcategory table  
    AddTable(dsv, connection, "DimProductSubcategory");  
    AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
    // Add the DimProduct table  
    AddTable(dsv, connection, "DimProduct");  
    AddComputedColumn(dsv, connection, "DimProduct", "ProductLineName", "CASE ProductLine WHEN 'M' THEN 'Mountain' WHEN 'R' THEN 'Road' WHEN 'S' THEN 'Accessory' WHEN 'T' THEN 'Touring' ELSE 'Components' END");  
    AddRelation(dsv, "DimProduct", "ProductSubcategoryKey", "DimProductSubcategory", "ProductSubcategoryKey");  
    dsv.Update();  
  
    // Add the DimCustomer table  
    AddTable(dsv, connection, "DimCustomer");  
    AddComputedColumn(dsv, connection, "DimCustomer", "FullName", "CASE WHEN MiddleName IS NULL THEN FirstName + ' ' + LastName ELSE FirstName + ' ' + MiddleName + ' ' + LastName END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "GenderDesc", "CASE WHEN Gender = 'M' THEN 'Male' ELSE 'Female' END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "MaritalStatusDesc", "CASE WHEN MaritalStatus = 'S' THEN 'Single' ELSE 'Married' END");  
    AddRelation(dsv, "DimCustomer", "GeographyKey", "DimGeography", "GeographyKey");  
  
    // Add the DimReseller table  
    AddTable(dsv, connection, "DimReseller");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderFrequencyDesc", "CASE WHEN OrderFrequency = 'A' THEN 'Annual' WHEN OrderFrequency = 'S' THEN 'Bi-Annual' ELSE 'Quarterly' END");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderMonthDesc", "CASE WHEN OrderMonth = '1' THEN 'January' WHEN OrderMonth = '2' THEN 'February' WHEN OrderMonth = '3' THEN 'March' WHEN OrderMonth = '4' THEN 'April' WHEN OrderMonth = '5' THEN 'May' WHEN OrderMonth = '6' THEN 'June' WHEN OrderMonth = '7' THEN 'July' WHEN OrderMonth = '8' THEN 'August' WHEN OrderMonth = '9' THEN 'September' WHEN OrderMonth = '10' THEN 'October' WHEN OrderMonth = '11' THEN 'November' WHEN OrderMonth = '12' THEN 'December' ELSE 'Never Ordered' END");  
  
    // Add the DimCurrency table  
    AddTable(dsv, connection, "DimCurrency");  
    dsv.Update();  
  
    // Add the DimSalesReason table  
    AddTable(dsv, connection, "DimSalesReason");  
  
    // Add the FactInternetSales table  
    AddTable(dsv, connection, "FactInternetSales");  
    AddRelation(dsv, "FactInternetSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactInternetSales", "CustomerKey", "DimCustomer", "CustomerKey");  
    AddRelation(dsv, "FactInternetSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    dsv.Update();  
  
    // Add the FactResellerSales table  
    AddTable(dsv, connection, "FactResellerSales");  
    AddRelation(dsv, "FactResellerSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactResellerSales", "ResellerKey", "DimReseller", "ResellerKey");  
    AddRelation(dsv, "FactResellerSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
  
    // Add the FactInternetSalesReason table  
    AddTable(dsv, connection, "FactInternetSalesReason");  
    AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
    dsv.Update();  
  
    // Add the FactCurrencyRate table  
    AddTable(dsv, connection, "FactCurrencyRate");  
    AddRelation(dsv, "FactCurrencyRate", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    AddRelation(dsv, "FactCurrencyRate", "TimeKey", "DimTime", "TimeKey");  
  
    #endregion  
  
    // Send the data source view definition to the server  
    dsv.Update();  
  
    return dsv;  
}  
  
static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
{  
    string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
    OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
    DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
  
    dataTable.ExtendedProperties.Add("TableType", "Table");  
    dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
    dataTable.ExtendedProperties.Add("DbTableName", tableName);  
    dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
}  
  
static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
{  
    DataSet tmpDataSet = new DataSet();  
    tmpDataSet.Locale = CultureInfo.CurrentCulture;  
    OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
        + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
        + tableName + "] WHERE 1=0", connection);  
    DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
    DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
    dataTable.Constraints.Clear();  
    dataTable.Columns.Remove(dataColumn);  
  
    dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
    dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
        expression);  
    dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
    dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
    dataColumn = null;  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
    tmpDataSet = null;  
}  
  
static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
{  
    DataColumn fkColumn  
        = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
    DataColumn pkColumn  
        = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
        + fkColumnName, pkColumn, fkColumn, true);  
}  
  
static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
{  
    DataColumn[] fkColumns = new DataColumn[2];  
    fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
    fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
    DataColumn[] pkColumns = new DataColumn[2];  
    pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
    pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
        + "_" + columnName2, pkColumns, fkColumns, true);  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [Logische Architektur & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
