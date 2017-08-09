---
title: 'Lektion 8: Erstellen eines Datenfilters | Microsoft Docs'
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea0e116101c9599268b3fc2f3cd556d2149433c8
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-8-create-a-data-filter"></a>Lektion 8: Erstellen eines Datenfilters
Nachdem Sie im übergeordneten Bericht eine Drillthroughaktion hinzugefügt haben, erstellen Sie im nächsten Schritt einen Datenfilter für die Datentabelle, die Sie für den untergeordneten Bericht definiert haben.  
  
Sie können für den Drillthroughbericht einen tabellenbasierten Filter **oder** einen Abfragefilter erstellen. Diese Lektion enthält Anweisungen zum Erstellen beider Filtertypen.  
  
## <a name="table-based-filter"></a>Tabellenbasierter Filter  
Führen Sie folgende Aufgaben aus, um einen tabellenbasierten Filter zu implementieren.  
  
-   Fügen Sie der Tablix im untergeordneten Bericht einen Filterausdruck hinzu.  
  
-   Erstellen Sie eine Funktion, mit der ungefilterte Daten aus der **PurchaseOrderDetail** -Tabelle ausgewählt werden.  
  
-   Fügen Sie einen Ereignishandler hinzu, durch den die **PurchaseOrderDetail** -DataTable an den untergeordneten Bericht gebunden wird.  
  
### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>So fügen Sie der Tablix im untergeordneten Bericht einen Filterausdruck hinzu  
  
1.  Öffnen Sie den untergeordneten Bericht.  
  
2.  Wählen Sie in der Tablix eine Spaltenüberschrift aus. Klicken Sie mit der rechten Maustaste auf die graue Zelle, die oberhalb der Spaltenüberschrift angezeigt wird, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
3.  Wählen Sie die Seite **Filter** und anschließend **Hinzufügen**aus.  
  
4.  Wählen Sie im Feld **Ausdruck** aus der Dropdownliste **ProductID** aus. Dies ist die Spalte, auf die Sie den Filter anwenden.  
  
5.  Klicken Sie in der Dropdownliste**=**Operator **auf den Gleichheitsoperator (** ).  
  
6.  Wählen Sie neben dem Feld **Wert** die Ausdrucksschaltfläche aus. Wählen Sie im Bereich **Kategorie** **Parameter** aus, und doppelklicken Sie im Bereich **Werte** auf **productid** . Das Feld **Ausdruck festlegen für: Wert** sollte jetzt einen mit **=Parameters!productid.Value**vergleichbaren Ausdruck enthalten.  
  
7.  Wählen Sie **OK** aus, und klicken Sie im Dialogfeld **Tablix-Eigenschaften** ein zweites Mal auf **OK** .  
  
8.  Speichern Sie die RDLC-Datei.  
  
### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>So erstellen Sie eine Funktion, durch die ungefilterte Daten aus der PurchaseOrderDetail-Tabelle ausgewählt werden  
  
1.  Erweitern Sie im Projektmappen-Explorer Default.aspx, und doppelklicken Sie dann auf Default.aspx.cs.  
  
2.  Erstellen Sie eine neue Funktion, die den **productid**-Parameter vom Typ Integer akzeptiert, ein **datatable** -Objekt zurückgibt und folgende Schritte ausführt.  
  
    1.  Erstellt eine Instanz des Datasets **DataSet2**, das in Schritt 2 in [Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)erstellt wurde.  
  
    2.  Herstellen einer Verbindung mit der SQL Server-Datenbank, um die in **Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht**definierte Abfrage auszuführen.  
  
    3.  Die Abfrage gibt ungefilterte Daten zurück.  
  
    4.  Füllen der DataSet-Instanz mit den ungefilterten Daten, indem die Abfrage ausgeführt wird.  
  
    5.  Zurückgeben der **PurchaseOrderDetail** -DataTable.  
  
        Die Funktion sieht etwa wie folgt aus. (Sie dient nur zur Veranschaulichung. Sie können zum Abrufen der erforderlichen Daten für den untergeordneten Bericht ein beliebiges Muster verwenden.)  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>So fügen Sie einen Ereignishandler hinzu, durch den die PurchaseOrderDetail-DataTable an den untergeordneten Bericht gebunden wird  
  
1.  Öffnen Sie „Default.aspx“ in der Entwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf das ReportViewer-Steuerelement, und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie auf der Seite **Eigenschaften** das Symbol **Ereignisse** aus.  
  
4.  Doppelklicken Sie auf das Ereignis **Drillthrough** .  
  
    Dadurch wird dem Code ein mit folgendem Block vergleichbarer Ereignishandlerabschnitt hinzugefügt.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Vervollständigen Sie den Ereignishandler. Er sollte folgende Funktionen umfassen.  
  
    1.  Abrufen des Verweises des untergeordneten Berichtsobjekts aus dem *DrillthroughEventArgs* -Parameter.  
  
    2.  Aufrufen der **GetPurchaseOrderDetail**-Funktion.  
  
    3.  Binden der **PurchaseOrderDetail** -DataTable an die entsprechende Datenquelle des Berichts.  
  
        Der vollständige Ereignishandlercode sollte dem folgenden ähnlich sein.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Speichern Sie die Datei.  
  
## <a name="query-filter"></a>Abfragefilter  
Führen Sie folgende Aufgaben aus, um einen Abfragefilter zu implementieren.  
  
-   Erstellen Sie eine Funktion, mit der gefilterte Daten aus der **PurchaseOrderDetail** -Tabelle ausgewählt werden.  
  
-   Fügen Sie einen Ereignishandler hinzu, durch den Parameterwerte abgerufen und die **PurchaseOrdeDetail** -DataTable an den untergeordneten Bericht gebunden wird.  
  
### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>So erstellen Sie eine Funktion, durch die gefilterte Daten aus der PurchaseOrderDetail-Tabelle ausgewählt werden  
  
1.  Erweitern Sie im Projektmappen-Explorer Default.aspx, und doppelklicken Sie dann auf Default.aspx.cs.  
  
2.  Erstellen Sie eine neue Funktion, die den **productid**-Parameter vom Typ Integer akzeptiert, ein **datatable** -Objekt zurückgibt und folgende Schritte ausführt.  
  
    1.  Erstellt eine Instanz des Datasets **DataSet2**, das in Schritt 2 in [Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)erstellt wurde.  
  
    2.  Herstellen einer Verbindung mit der SQL Server-Datenbank, um die in **Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht**definierte Abfrage auszuführen.  
  
    3.  Die Abfrage enthält den **productid**-Parameter, der gewährleistet, dass die zurückgegebenen Daten auf Grundlage der im übergeordneten Bericht ausgewählten **ProductID** gefiltert werden.  
  
    4.  Füllen der DataSet-Instanz mit den gefilterten Daten, indem die Abfrage ausgeführt wird.  
  
    5.  Zurückgeben der **PurchaseOrderDetail** -DataTable.  
  
        Die Funktion sieht etwa wie folgt aus. (Sie dient nur zur Veranschaulichung. Sie können zum Abrufen der erforderlichen Daten für den untergeordneten Bericht ein beliebiges Muster verwenden.)  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlCommand cmd = new SqlCommand("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = @ProductID", sqlconn);  
                  
                        // Sets the productid parameter.  
                        cmd.Parameters.Add((new SqlParameter("@ProductID", SqlDbType.Int)).Value = productid);  
  
                        SqlDataAdapter adap = new SqlDataAdapter(cmd);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>So fügen Sie einen Ereignishandler hinzu, durch den Parameterwerte abgerufen und die PurchaseOrderDetail-DataTable an den untergeordneten Bericht gebunden wird  
  
1.  Öffnen Sie „Default.aspx“ in der Entwurfsansicht.  
  
2.  Klicken Sie mit der rechten Maustaste auf das ReportViewer-Steuerelement, und wählen Sie **Eigenschaften**aus.  
  
3.  Wählen Sie im Bereich **Eigenschaften** das Symbol **Ereignisse** aus.  
  
4.  Doppelklicken Sie auf das Ereignis **Drillthrough** .  
  
    Dadurch wird dem Code ein mit Folgendem vergleichbarer Ereignishandlerabschnitt hinzugefügt.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Vervollständigen Sie den Ereignishandler. Er sollte folgende Funktionen umfassen.  
  
    1.  Abrufen des Verweises des untergeordneten Berichtsobjekts aus dem *DrillthroughEventArgs* -Parameter.  
  
    2.  Abrufen der Parameterliste des untergeordneten Berichts aus dem abgerufenen untergeordneten Berichtsobjekt.  
  
    3.  Durchlaufen der Parameterauflistung und Abrufen des aus dem übergeordneten Bericht übergebenen Werts für den **ProductID**-Parameter.  
  
    4.  Aufrufen der **GetPurchaseOrderDetail**-Funktion und Übergeben des Werts für den **ProductID**-Parameter.  
  
    5.  Binden der **PurchaseOrderDetail** -DataTable an die entsprechende Datenquelle des Berichts.  
  
        Der vollständige Ereignishandlercode sollte dem folgenden ähnlich sein.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Speichern Sie die Datei.  
  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben erfolgreich einen Datenfilter für die Datentabelle erstellt, die Sie für den untergeordneten Bericht definiert haben. Als Nächstes werden Sie die Websiteanwendung erstellen und ausführen. Informationen hierzu finden Sie unter [Lektion 9: Erstellen und Ausführen der Anwendung](../reporting-services/lesson-9-build-and-run-the-application.md).  
  
  
  


