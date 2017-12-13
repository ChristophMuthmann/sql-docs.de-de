---
title: Erstellen von Tabellen, Partitionen und Spalten in einem tabellarischen Modell | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: cf0e4791-ad3b-41a8-81ce-509d4cf223f8
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 94bad422a63276ad130027ea77de4734571016a8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>Erstellen von Tabellen, Partitionen und Spalten in einem tabellarischen Modell
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]In einem tabellarischen Modell besteht aus eine Tabelle Zeilen und Spalten. Zeilen sind in Partitionen unterteilt, um inkrementelle datenaktualisierung zu unterstützen. Eine tabellarische Lösung kann mehrere Typen von Tabellen, je nachdem, wo die Daten stammen unterstützen:  

* Reguläre Tabellen, in denen Daten aus einer relationalen Datenquelle über den Datenanbieter stammt. 

* Mithilfe von Push Tabellen, in denen Daten "in der Tabelle programmgesteuert wird per Push übertragen". 

* Berechnete Tabellen, woher die Daten aus einem DAX-Ausdruck stammen, die innerhalb des Modells für ihre Daten ein anderes Objekt verweist.  

Im folgenden Codebeispiel wird eine normale Tabelle definiert. 

## <a name="required-elements"></a>Erforderliche Elemente 

Eine Tabelle muss mindestens eine Partition besitzen. Eine normale Tabelle muss auch mindestens eine Spalte definiert haben. 

Jede Partition benötigen eine Quelle Ursprung der Daten angeben, aber Quelle kann festgelegt werden, auf Null. In der Regel ist die Quelle, einem Abfrageausdruck, die einen Slice von Daten in der entsprechenden Datenbank-Abfragesprache definiert. 

## <a name="code-example-create-a-table-column-parition"></a>Codebeispiel: Erstellen einer Tabelle, eine Spalte oder eine Partition

Tabellen werden durch Tabellenklasse (im Microsoft.AnalysisServices.Tabular-Namespace) dargestellt. 

Im folgenden Beispiel definieren wir eine reguläre Tabelle, die über eine Partition mit einer relationalen Datenquelle und ein paar reguläre Spalten verknüpft. Wir wird auch die Änderungen an den Server senden und eine datenaktualisierung, die die Daten in das Modell bringt ausgelöst. Dies darstellt liegt meist daran, wenn Sie Daten aus einer relationalen SQL Server-Datenbank in einer tabellarischen Lösung laden möchten. 


```
using System; 
using Microsoft.AnalysisServices; 
using Microsoft.AnalysisServices.Tabular; 
 
namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 
 
            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 
 
                // 
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithTable.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="partitions-in-a-table"></a>Partitionen in einer Tabelle 

Partitionen werden durch dargestellt eine **Partition** -Klasse (in Microsoft.AnalysisServices.Tabular-Namespace). Die **Partition** -Klasse stellt eine **Quelle** Eigenschaft P**ArtitionSource** eingeben, bietet eine Abstraktion über die verschiedenen Ansätze für das Erfassen von Daten in Partition. Ein **Partition** Instanz kann besitzen eine **Quelle** -Eigenschaft null ist, gibt an, dass Daten in die Partition verschoben werden werden, von Datensegmenten an den Server gesendet, im Rahmen des push Data-API verfügbar gemacht werden, indem Sie Analysis Services . In SQL Server 2016 **PartitionSource** -Klasse verfügt über zwei abgeleiteten Klassen, Methoden zum Binden von Daten zu einer Partition darstellen: **QueryPartitionSource** und **CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>Spalten in einer Tabelle 

Spalten werden von mehreren Klassen abgeleitet Base dargestellt **Spalte** -Klasse (in Microsoft.AnalysisServices.Tabular-Namespace): 

* **DataColumn** (bei regulären Spalten in regelmäßigen Tabellen)
* **CalculatedColumn** (für Spalten, die gesichert werden, indem Sie DAX-Ausdruck)
* **CalculatedTableColumn** (bei regulären Spalten in berechnete Tabellen)
* **RowNumberColumn** (besondere Art von Spalte, die von SSAS für jede Tabelle erstellt wurden). 

## <a name="row-numbers-in-a-table"></a>Die Zeilennummern in einer Tabelle 

Jede **Tabelle** Objekt auf einem Server hat eine **RowNumberColumn** indizieren verwendet. Sie können nicht erstellen oder explizit hinzufügen. Die Spalte wird automatisch erstellt, beim Speichern oder das Objekt zu aktualisieren: 

* **DB. SaveChanges** 

* **DB. Update(ExpandFull)** 

Beim Aufrufen einer Methode der Server wird Zeilennummernspalte automatisch erstellen, die als sichtbar sein **RowNumberColumn** der tabellenspezifischen Columns-Auflistung. 

## <a name="calculated-tables"></a>Berechnete Tabellen 

Berechnete Tabellen werden mithilfe von DAX-Ausdruck definiert, die er Daten aus vorhandenen Datenstrukturen im Modell oder Out-of-Line-Bindungen beträchtlichen. Führen Sie folgende Schritte aus, um eine berechnete Tabelle programmgesteuert zu erstellen: 

* Erstellen Sie eine generische **Tabelle**. 

* Eine Partition hinzugefügt, mit der Quelle des Typs **CalculatedPartitionSource**, wobei die Quelle eine DAX-Ausdruck ist. Quelle für die Partition ist, was eine reguläre Tabelle von einer berechneten Tabelle unterscheidet. 

Beim Speichern der Änderungen an den Server der Server der hergeleiteten Werteliste zurück **CalculatedTableColumns** (berechnete Tabellen bestehen aus berechneten Spalten), über die Auflistung für die Tabelle Spalten sichtbar. 

## <a name="next-steps"></a>Nächste Schritte

Überprüfen Sie die Klassen zur Behandlung von Ausnahmen in TOM: [Behandeln von Fehlern in TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
