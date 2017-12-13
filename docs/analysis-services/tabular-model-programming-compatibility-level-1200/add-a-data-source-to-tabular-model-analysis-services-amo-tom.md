---
title: "Hinzufügen einer Datenquelle auf tabellarische Modelle (Analysis Services AMO-TOM) | Microsoft Docs"
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
ms.assetid: e54a8a1b-b964-4b6e-9057-44d50af676c0
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8aac5145c520ac61fda5689a4ba40b882bb554da
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="add-a-data-source-to-tabular-model-analysis-services-amo-tom"></a>Hinzufügen einer Datenquelle auf tabellarische Modelle (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Die **DataSource** Klasse im Microsoft.AnalysisServices.Tabular-Namespace ist eine Abstraktion eines tabellarischen Modells-Datenquelle, die den Typ angibt und den Speicherort der importierten Daten während eines Datenaktualisierungsvorgangs. 

Sie können eine Datenquelle für das tabellarische Modell hinzufügen, indem Sie instanziieren ein Objekt einer Klasse abgeleitet **DataSource**, und fügen Sie diese der **DataSources** Auflistung des Modellobjekts. Um Änderungen an den Server zu speichern, rufen Sie entweder **Model.SaveChanges()** oder **Database.Update(UpdateOptions.ExpandFull)**. 

In SQL Server 2016 unterstützt Analysis Services importieren Sie Daten nur von relationalen Datenbanken, in denen der Datenanbieter die Daten in Form von Tabellen und Spalten verfügbar macht. Daher verwendet im tabellarischen Objektmodell die ProviderDataSource-Klasse (abgeleitet von DataSource), diese Funktion verfügbar zu machen. 

## <a name="code-example-add-a-data-source"></a>Codebeispiel: Hinzufügen einer Datenquelle 

In diesem Beispiel wird gezeigt, wie beim Instanziieren einer **ProviderDataSource** und fügen Sie es mit einem Datenmodell. 

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
                    server.Databases.GetNewName("Database with a Data Source Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithDataSource = new Database() 
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
                dbWithDataSource.Model = new Model() 
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
                dbWithDataSource.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = "SQL Server Data Source Example", 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithDataSource); 
                dbWithDataSource.Update(UpdateOptions.ExpandFull); 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithDataSource.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine("The data model includes the following data source definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (DataSource ds in dbWithDataSource.Model.DataSources) 
                { 
                    Console.WriteLine("\tData source name:\t\t{0}", ds.Name); 
                    Console.WriteLine("\tData source description:\t{0}", ds.Description); 
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

## <a name="next-step"></a>Nächster Schritt 

Innerhalb eines Modells müssen Sie zum Einrichten von datenbindungen, die in der Datenquelle Quellspalten Zielspalten im Modell zugeordnet. Sie müssen auch die Partitionen einer Länge von mindestens 1 pro Tabelle zu definieren, in denen die Daten gespeichert. Der folgende Link zeigt, wie Sie: [Erstellen von Tabellen, Partitionen und Spalten](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md) 
