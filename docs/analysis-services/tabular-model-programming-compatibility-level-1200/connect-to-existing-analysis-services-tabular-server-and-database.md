---
title: Herstellen einer Verbindung mit vorhandenen tabellarischen Analysis Services-Server und Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 061b37f5b0e8209f896ded915f0259c3253a1439
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>Herstellen einer Verbindung mit vorhandenen tabellarischen Analysis Services-Server und Datenbank

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In SQL Server 2016 enthält Analysis Services Management Objects (AMO) mehrere Namespaces, mit denen eine Serververbindung eingerichtet werden konnte. Dieser Artikel beschreibt die zum Herstellen eine Serververbindung mit dem Microsoft.AnalysisServices.Tabular-Namespace für Modelle und Datenbanken 1200 erstellt oder höheren Kompatibilitätsgrad. 

Zur Verbindung mit eines Analysis Services-Servers muss Code instanziieren ein Serverobjekts, und klicken Sie dann die "Connect"-Methode dafür aufrufen. Nachdem die Verbindung hergestellt ist, wider Eigenschaften des Serverobjekts die Einstellungen der aktuellen Analysis Services-Instanz. 

Die folgenden Klassen können für Verbindungen auf oberster Ebene verwendet werden: 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

Wie Sie sehen können, stellen Sie zwei Namespaces die Konnektivität zum Server- und Datenbankobjekten: der ursprünglichen Microsoft.AnalysisServices-Namespace für AMO und dem neuen Microsoft.AnalysisServices.Tabular-Namespace für TOM.

Warum zwei Namespaces für die gleichen Vorgänge? Die Antwort liegt auf der Datenbank- und modellsicherheitseinstellungen Ebene, in dem die Objekthierarchie wird modusspezifische und besteht aus der Modellstruktur mehrdimensionalen oder tabellarischen Metadaten downstream. Um in der Modellstruktur aufrufen zu können, wird das Objekt Server- oder für beide Modelltypen bereitgestellt.

> [!NOTE]  
>  Die Metadaten für die Modelldefinition und Vorgänge wird vollständig für die beiden Modi unterschiedlich. Das Aufteilen der Datendefinitionssprache (DDL) in zwei getrennte Namespaces, die Entwicklungsaufgaben durch die Präsentation der Bedarf für einen bestimmten Modelltyp API vereinfacht. 

Obwohl der DDL-Code im Detail variiert, sind Verbindungen mit einem Server identisch in allen Modi, Versionen und Editionen. Unterstützung von einem Server und die datenbankverbindung über entweder Namespace können Sie generische Tools oder Skripts, die mit Analysis Services-Instanz verbunden oder Datenbank, ohne zu wissen, welche Art von Modell wird auf dem Server gehostet.  

Diese Flexibilität wird erläutert, die Abhängigkeiten zwischen Assemblys. Um unter der Datenbank-Ebene (z. B. auf ein Modell in einem tabellarischen 1200-Datenbank oder auf einen Cube, Dimension oder MeasureGroup innerhalb einer Datenbank mit mehrdimensionalen oder tabellarischen 1050-1103) aufrufen abhängt AMO TOM. 

Im Gegensatz dazu verfügt TOM Abhängigkeit nicht auf AMO. Obwohl TOM mehrdimensionalen Metadaten (Cubes) durchsuchen können verwendet werden kann, kann AMO zum Durchsuchen von mehrdimensionalen und tabellarischen Metadaten verwendet werden. 

Aus diesem Grund ist der erste Schritt beim Einrichten Ihres Projekts Hinzufügen von Verweisen auf alle AMO-Assemblys erforderlich. Finden Sie unter [Verweis zu installieren und verteilen Sie die Clientbibliothek TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) für Details. 

> [!NOTE]  
>  Server und Datenbank-Verbindungen basieren auf älteren AMO-Klassen, die von MajorObject erben. Obwohl Haupt-und nebenobjekte nicht in einem Tabellenmodell-Struktur verwendet wird, ist die MajorObject-Klasse als Basisklasse für Server- und Datenbankobjekten, unabhängig davon, welche, die API Sie zum Einrichten der Verbindung verwenden sichtbar.  

## <a name="code-example-server-connection"></a>Codebeispiel: Server-Verbindung 

Es folgt ein C#-Codebeispiel, das zeigt, wie eine lokale Analysis Services-Instanz herstellen und dessen Eigenschaften in einem Konsolenfenster Liste. 

Dieses Beispiel zeigt nur einige der Eigenschaften eines Serverobjekts, aber es sind weitere Eigenschaften zur Verfügung, darunter ServerMode und DefaultCompatibilityLevel.  

```
using System; 
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

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
Wenn Sie dieses Programm ausführen, zeigt die Ausgabe Eigenschaften für das Serverobjekt in einem Konsolenfenster an. 

## <a name="authentication-and-authorization"></a>Authentifizierung und Autorisierung 

Ein Server oder datenbankverbindung mit Analysis Services erfordert Administratorberechtigungen für Lese-/ Schreibvorgänge und übergeben eine Verbindung mit angenommener Identität-Anforderung verwendet.  

Obwohl in den letzten Jahren, die benutzerdefinierte Authentifizierung unter sehr speziellen Bedingungen ermöglicht die Sicherheitsinfrastruktur von Analysis Services erweitert wurde, ist die einzige unterstützte externe Authentifizierung integrierte Sicherheit von Windows. Es wird angenommen, dass Sicherheitsprinzipale gültige Windows-Benutzer oder Gruppe Domänenkonten sein.  

Unter Windows 2012 und höher kann Delegierung über Domänengrenzen hinweg übergeben werden. In Analysis Services wird die Delegierung nur für DirectQuery-Modelle verwendet. Andernfalls sind die Verbindungen entweder direkt oder dessen Identität angenommen wurde. 

## <a name="next-steps"></a>Nächste Schritte 

Nach dem Herstellen einer Verbindungs, logische im nächsten Schritt wird entweder Liste vorhandener Datenbanken bereits auf dem Server oder vielleicht erstellen Sie eine neue leere Datenbank. Die folgenden Links enthalten Codebeispiele, in denen beide dieser grundlegenden Aufgaben veranschaulicht: 

- [Erstellen und Bereitstellen einer leeren Datenbank](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [Listet die vorhandene Datenbanken](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)

