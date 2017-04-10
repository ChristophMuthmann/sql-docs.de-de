---
title: "SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] stellt eine Plattform für die Entwicklung und Bereitstellung von intelligenten Anwendungen bereit, die neue Einblicke bieten. Sie können die umfassende und leistungsfähige Sprache „R“ und die zahlreichen Pakete aus der Community zum Erstellen von Modellen und Generieren von Vorhersagen mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten verwenden. Da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] die Sprache „R“ mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]integriert, können Sie die Analysen in der Nähe der Daten durchführen und den Aufwand sowie die Sicherheitsrisiken vermeiden, die mit dem Verschieben von Daten einhergehen.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] unterstützt die Open Source-Sprache „R“ mit einem umfassenden Satz an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tools und -Technologien, die eine höhere Leistung, Sicherheit, Zuverlässigkeit und Verwaltbarkeit bieten. Sie können R-Lösungen mit den geeigneten, vertrauten Tools bereitstellen, und Ihre Produktionsanwendungen können die R-Laufzeitversion aufrufen sowie Vorhersagen und visuelle Elemente mit [!INCLUDE[tsql](../../includes/tsql-md.md)]abrufen. Außerdem erhalten Sie die [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)-Bibliotheken zur Verbesserung der Skalierung und Leistung Ihrer R-Lösungen.  
  
Über das SQL Server-Setup können Sie Server- und Clientkomponenten installieren.  
  
+   **R Services (In-Database):** Installieren Sie dieses Feature während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups, um die sichere Ausführung des R-Skripts auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer zu ermöglichen.  
  
     Wenn Sie dieses Feature auswählen, werden Erweiterungen im Datenbankmodul installiert, um die Ausführung von R-Skripts zu unterstützen. Zudem wird ein neuer Dienst erstellt, der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], um die Kommunikation zwischen R-Laufzeitversion und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zu verwalten.  
  
+   **Microsoft R Server (Standalone):** eine Verteilung von Open Source-R kombiniert mit geschützten Paketen, die Parallelverarbeitung und andere Leistungssteigerungen unterstützen. R Services (In-Database) und Microsoft R Server (Standalone) enthalten beide die Basis-R-Laufzeit und -Pakete sowie die **ScaleR**-Bibliotheken für verbesserte Konnektivität und Leistung. 
  
+    [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/index#mrc) ist als separates, kostenloses Installationsprogramm verfügbar.  Sie können Microsoft R Client verwenden, um Lösungen zu entwickeln, die für R Services unter SQL Server bereitgestellt werden können oder für Microsoft R Server unter Windows, Teradata oder Hadoop. 
     

  > [!NOTE] Um Ihren R-Code unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen zu können, müssen Sie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wie [hier](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) beschrieben installieren.
  >  
  > Microsoft R Server \(Standalone\) ist eine separate Option, mit der Sie die ScaleR-Bibliotheken auf einem Windows-Computer verwenden können, auf dem SQL Server nicht ausgeführt wird. 
>   
>  Wenn Sie die Enterprise Edition besitzen, sollten Sie jedoch Microsoft R Server \(Standalone\) auf einem Laptop oder einem anderen Computer installieren, der für die R-Entwicklung verwendet wird, um R-Lösungen zu erstellen, die mühelos auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt werden können, auf der R Services \(In-Database\) ausgeführt wird.
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 Beschreibt häufige Szenarien für die Verwendung von R mit SQL Server.  
  
[Einrichten von SQL Server R Services (In-Database)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
Installieren von R und zugehörigen Komponenten als Teil des SQL Server-Setups.  
  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
Erfahren Sie, wie Sie SQL Server-Datenquellen in Ihrem R-Code erstellen und Remote Compute-Kontexte verwenden. Andere Tutorials für SQL-Entwickler veranschaulichen das Trainieren und Bereitstellen eines R-Modells in SQL Server.  
  
## <a name="see-also"></a>Siehe auch  
  
 [Erste Schritte mit Microsoft R Server &#40;eigenständig&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  