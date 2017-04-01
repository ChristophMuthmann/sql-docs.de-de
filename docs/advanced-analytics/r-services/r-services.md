---
title: "R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# R Services
  Microsoft R Services verfügt über zwei Serverplattformen, um die beliebte Open-Source-Sprache R in Geschäftsanwendungen zu integrieren: **SQL Server R Services (In-Database)**, für die Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und **Microsoft R Server**.  
  
-   **R Services (In-Database)**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] soll eine schnelle Entwicklung, Bereitstellung und Operationalisierung von R-Lösungen auf Basis der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Plattform und zugehöriger Dienste ermöglichen.  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bringt den Rechenvorgang zu den Daten, da R auf demselben Computer ausgeführt werden kann wie die Datenbank. Es umfasst einen Datenbankdienst, der außerhalb des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses ausgeführt wird und sicher mit der R-Laufzeitumgebung kommuniziert. Sie können R-Modelle trainieren, R-Plots generieren, Bewertungen durchführen und Daten problemlos zwischen R und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschieben. Datenanalysten, die Lösungen testen und entwickeln, können mit dem Server von einem Remote-Entwicklungscomputer aus kommunizieren, um R-Code auf dem Server auszuführen sowie vollständige Lösungen durch Einbetten von Aufrufen an R in gespeicherten Prozeduren auf SQL Server bereitzustellen.  
  
     Dieser Download umfasst eine Verteilung der Open-Source-Sprache R sowie ScaleR, einen Satz skalierbarer, leistungsfähiger R-Pakete. Außerdem umfasst er Anbieter für eine einfachere und schnellere Verbindung mit allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Technologien.  
  
     Weitere Informationen finden Sie unter [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md). Beispielszenarien finden Sie unter [SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
-   **Microsoft R Server**  
  
     Dieses eigenständige Serversystem unterstützt verteilte, skalierbare R-Lösungen auf mehreren Plattformen und verwendet mehreren Enterprise-Datenquellen, einschließlich Linux, Hadoop und Teradata.  
  
     Weitere Informationen finden Sie unter [Microsoft R Server (MSDN)](https://msdn.microsoft.com/microsoft-r/index).  
  
## <a name="related-technologies"></a>Verwandte Technologien  
 Microsoft bietet umfassende Unterstützung für das Ökosystem der Open Source-Sprache R, einschließlich Tools, Anbieter, verbesserte R-Pakete und integrierte Entwicklungsumgebungen.  
  
-   **R-Tools für Visual Studio**  
  
     Visual Studio stellt eine vollständige Entwicklungsumgebung für die Sprache R bereit. Das Plug-In enthält einen Editor, interaktive Fenster, Zeichnen, Debugger und mehr. Sie können .NET-Sprachen von R verwenden oder R aus .NET durch Open Source-Bibliotheken wie R.NET und rClr aufrufen.  
  
     Weitere Informationen finden Sie unter [R Tools for Visual Studio (R-Tools für Visual Studio)](https://www.visualstudio.com/vs/rtvs/).  
  
-   **R in Azure Machine Learning**  
  
     Erstellen Sie Ihren eigenen Arbeitsbereich in Azure Machine Learning Studio, in dem Sie auf über 400 vorab geladene R-Pakete zugreifen können. Erstellen und trainieren Sie Modelle, um sie als Webdienst bereitzustellen, oder schreiben Sie benutzerdefinierte Skripts zum Transformieren von Daten. Erstellen Sie eigene R-Pakete und laden Sie diese in Azure hoch, um sie als benutzerdefinierte Module auszuführen. Veröffentlichen Sie auch Lösungen auf dem [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning).  
  
     Weitere Informationen finden Sie unter [Erweitern Ihres Experiments mit R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r) und [Benutzerdefinierte R-Module in Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules).  
  
-   **Data Science Virtual Machines**  
  
     Sie können eine vorinstallierte und vorkonfigurierte Version von [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] in Microsoft Azure bereitstellen. Dies erleichtert die ersten Schritte beim Auswerten und Modellieren von Daten in der Cloud, ohne ein vollständig konfiguriertes System lokal einrichten zu müssen.  
  
     Der Azure Marketplace enthält mehrere virtuelle Computer, die Data Science unterstützen:
     + Die **Microsoft Data Science Virtual Machine** wurde mit Microsoft R Server, Python (Anaconda-Verteilung), einem Jupyter Notebook-Server, Visual Studio Community Edition, Power BI Desktop, dem Azure SDK und SQL Server Express Edition konfiguriert. 
     + **Microsoft R Server 2016 für Linux** enthält die neueste Version von R Server (Version 9.0.1). Separate virtuelle Computer sind für CentOS Version 7.2 und Ubuntu Version 16.04 verfügbar. 
     + Der virtuelle Computer **R Server Only SQL Server 2016 Enterprise** umfasst ein eigenständiges Installationsprogramm für R Server 9.0.1, welches das neue Lizenzierungsmodell Modern Software Lifecycle unterstützt.
 

## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[Erste Schritte mit Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [Installieren des SQL Server-Datenbankmoduls](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  