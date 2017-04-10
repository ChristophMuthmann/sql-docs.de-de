---
title: "Bereitstellen von Paketen auf dem Integration Services-Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Bereitstellen von Paketen auf dem Integration Services-Server
  Mit dem in [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] eingeführten Feature für inkrementelle Paketbereitstellung können Sie ein oder mehrere Pakete in einem vorhandenen oder neuen Projekt bereitstellen, ohne das gesamte Projekt bereitzustellen.  
  
##  <a name="DeployWizard"></a> Bereitstellen von Paketen mit dem Bereitstellungs-Assistenten für Integration Services  
  
1.  Führen Sie an der Eingabeaufforderung **isdeploymentwizard.exe** unter dem Pfad **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** aus. Auf 64-Bit-Computern steht auch eine 32-Bit-Version des Tools unter **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn** zur Verfügung.  
  
2.  Wechseln Sie auf der Seite **Quelle auswählen** zu **Paketbereitstellungsmodell**. Wählen Sie dann den Ordner aus, der die Quellpakete enthält, und konfigurieren Sie die Pakete.  
  
3.  Schließen Sie den Assistenten ab. Führen Sie die restlichen Schritte aus, die in [Paketbereitstellungsmodell](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) beschrieben werden.  
  
##  <a name="SSMS"></a> Bereitstellen von Paketen mit SQL Server Management Studio  
  
1.  Erweitern Sie in SQL Server Management Studio im Objekt-Explorer den Knoten **Integration Services-Kataloge** > **SSISDB**.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Projekte**, und klicken Sie dann auf **Projekte bereitstellen**.  
  
3.  Wenn die Seite **Einführung** angezeigt wird, klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
4.  Wechseln Sie auf der Seite **Quelle auswählen** zu **Paketbereitstellungsmodell**. Wählen Sie dann den Ordner aus, der die Quellpakete enthält, und konfigurieren Sie die Pakete.  
  
5.  Schließen Sie den Assistenten ab. Führen Sie die restlichen Schritte aus, die in [Paketbereitstellungsmodell](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) beschrieben werden.  
  
##  <a name="SSDT"></a> Bereitstellen von Paketen mit SQL Server Data Tools (Visual Studio)  
  
1.  Öffnen Sie in Visual Studio ein Integration Services-Projekt, und wählen Sie ein oder mehrere Pakete aus, die Sie bereitstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste, und wählen Sie **Paket bereitstellen** aus. Der Bereitstellung-Assistent wird geöffnet, und in diesem sind die ausgewählten Pakete als Quellpakete konfiguriert.  
  
3.  Schließen Sie den Assistenten ab. Führen Sie die restlichen Schritte aus, die in [Paketbereitstellungsmodell](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) beschrieben werden.  
  
##  <a name="StoredProcedure"></a> Bereitstellen von Paketen mithilfe der gespeicherten Prozedur „deploy_packages“  
 Sie können mithilfe der gespeicherten Prozedur **[catalog].[deploy_packages]** ein oder mehrere SSIS-Pakete im SSIS-Katalog bereitstellen. Das folgende Codebeispiel veranschaulicht die Verwendung dieser gespeicherten Prozedur zum Bereitstellen von Paketen auf einem SSIS-Server. Weitere Informationen finden Sie unter [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md).  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> Bereitstellen von Paketen mit der Management-Object Model-API  
 Das folgende Codebeispiel veranschaulicht, wie mit der Management Object Model-API Pakete auf dem Server bereitgestellt werden.  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  