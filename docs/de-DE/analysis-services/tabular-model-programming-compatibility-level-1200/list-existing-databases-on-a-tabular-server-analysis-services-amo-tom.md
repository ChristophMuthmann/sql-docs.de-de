---
title: Listet die vorhandene Datenbanken auf einem tabellarischen Server (Analysis Services AMO-TOM) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ab5eb4b8-6254-442d-a42e-2372c346d260
caps.latest.revision: 2
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ec4718f826815217b13c7b27acfd3b51ec148fe4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>Listet die vorhandene Datenbanken auf einem tabellarischen Server (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Wenn Sie haben eine **Server** Objekt, mit einer Analysis Services-Instanz verbunden, Sie können eine Iteration durch **Server.Databases** -Auflistung, um die Liste aller Datenbanken, die von der Anlaysis-Services-Instanz gehostet wird. 

Die **Server.Databases** Auflistung enthält ein **Datenbank** Objekt für jede Datenbank auf dem Server, unabhängig vom Servermodus (mehrdimensional oder tabellarisch) oder Datenbanktyp (mehrdimensional, gehostet Tabellarische Pre-1200 oder tabellarischen 1200 oder höher). 

Sehen Sie sich den Typ der Datenbank über **Database.StorageEngineUsed** Eigenschaft.  

Datenbanken für tabellarische 1200 oder höhere werden eine Wert ungleich Null zurückgeben **Database.Model** -Eigenschaft, die Zugriff auf alle tabellarischen Metadatenobjekte gewährt: Tabellen, Spalten, Beziehungen und So weiter.  

Für mehrdimensionale oder tabellarische 1103 und unterhalb der Database.Model wird die Eigenschaft null sein. In diesem Fall nicht tabellarische Metadaten verfügbar, werden unter mehrdimensionale Eigenschaften (z. B. Database.Cubes und Database.Dimensions), aber diese Eigenschaften sind nur verfügbar Microsoft.AnalysisServices.Database-Klasse (von AMO), nicht durch Microsoft.AnalysisServices.Tabular.Database (für TOM). Weitere Informationen zu der Datenbank-Klasse zu verwenden, finden Sie unter [installieren, verteilen und verweisen auf die Clientbibliothek TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md).

Wenn Database.StorageEngineUsed auf "tabularmetadata" festgelegt ist, wird Sie kann nicht verwenden andere Klassen in der tabellarischen Namespace zugreifen, oder bearbeiten die Modellstruktur. 

In der folgenden Tabelle werden erwartete Verhalten zusammengefasst, wenn Sie auf einen Server oder eine Datenbank mithilfe einer Microsoft.AnalysisServices.Tabular-Klasse auf einem Server oder Datenbank verbinden. 

mode | Database.Model | Database.StorageEngineUsed
-----|----------------|---------------------------
Tabellarische 1200 1400 | Gibt den Namen des Modells zurück| StorageEngineUsed.TabularMetadata 
Tabellarische 1103 1100, 1050 | Gibt null zurück | StorageEngineUsed.InMemory 
Multidimensional | Gibt null zurück | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>Codebeispiel: Auflisten von vorhandenen Datenbanken

Der folgende Code veranschaulicht, wie die Verbindung auf die Liste und Server-Datenbanken, die vom Server gehostet werden. 

```
using System; using Microsoft.AnalysisServices; 
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
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>Rufen Sie ein Element aus einer Datenbank 

Der folgende Codeausschnitt zeigt, wie einer tabellarischen abgerufen oder eine Spalte aus einer Datenbank. 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>Nächste Schritte

Verstehen, wie [erstellen und Bereitstellen eine leere Datenbank](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md) mithilfe der TOM-API.

