---
title: "Neues in SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 35
---
# Neues in SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ist eine Funktion in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und SQL Server vNext, die unternehmensweite Data Science unterstützt.  R ist die beliebteste Programmiersprache für die erweiterte Analyse und bietet einen äußerst umfangreichen Paketsatz sowie eine motivierte und schnell wachsende Entwicklercommunity. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] hilft Ihnen dabei, die beliebte Open Source-Sprache „R“ in Ihrem Unternehmen zu nutzen. 
  
 > [!TIP] Haben Sie bereits SQL Server 2016 R Services?
 > Jetzt können Sie die neueste Version von Microsoft R Server auf Ihre 2016-Instanzen installieren, um häufigere Updates für R-Komponenten zu erhalten. Weitere Informationen finden Sie unter [Microsoft R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new).  

## <a name="whats-new-in-sql-server-vnext"></a>Neues in SQL Server vNext
  
+ Einführung in das **MicrosoftML**-Paket

   MicrosoftML ist ein neues Machine-Learning-Paket für R von den Microsoft R Server- und Microsoft Data Science-Teams. MicrosoftML sorgt für eine verbesserte Geschwindigkeit, Leistung und Skalierung für die Handhabung großer Mengen an Textdaten und hochdimensionaler kategorischer Daten in R-Modellen mit nur wenigen Codezeilen. Darüber hinaus erhalten Kunden von Microsoft R Server Zugriff auf fünf schnelle und äußerst präzise Lernprogramme, die in Azure Machine Learning enthalten sind. 
   
   Weitere Informationen finden Sie unter [Verwenden des MicrosoftML-Pakets mit SQL Server R Services](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md).
   
+ Vereinfachte Paketverwaltung für Datenwissenschaftler

  Sie sind nicht mehr darauf angewiesen, dass der Datenbankadministrator die von Ihnen benötigten R-Pakete auf SQL Server installiert. Dank neuer Installations- und Deinstallationsfunktionen für Pakete in **RevoScaleR** können Sie in R Services problemlos Pakete von einem Clientcomputer aus installieren und deinstallieren. 
  
  Für den Datenbankadministrator enthält [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] neue Rollen zum Verwalten von Berechtigungen für Pakete sowohl auf der Instanz- als auch auf der Datenbankebene. 
  
  Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server R Services](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 
     
+ Neue Funktionen in **RevoScaleR** für das Lesen und Schreiben von R-Modellobjekten

  RevoScaleR enthält nun neue Serialisierungsfunktionen und ein kompakteres Modellspeicherungsformat, um das Laden und Lesen eines Modells zu beschleunigen. 
  
  Weitere Informationen finden Sie unter [Speichern und Laden von R-Objekten aus SQL Server über ODBC](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md). 

+ **Sqlrutils**-Paket für einfachere SQL-Integration

  Dieses R-Paket hilft Ihnen, den Aufruf der gespeicherten SQL-Prozedur für Ihren R-Code zu generieren. Die generierten gespeicherten SQL-Prozeduren können dann in SQL Server R Services verwendet werden. Bereitgestellte Beispiele sollen Ihnen helfen, Ihren R-Code in einer Funktion zu konsolidieren, die mit einer gespeicherten SQL-Prozedur parametrisiert werden kann.
  
  Weitere Informationen finden Sie unter [Generieren einer gespeicherten R-Prozedur für R-Code mit dem sqlrutils-Paket](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md). 
  

+ **olapR**-Paket für einfache SSAS-Konnektivität

   Dieses neue Paket bietet eine neue Dimension der Konnektivität für R und SQL Server Analysis Services und erleichtert damit die Verwendung von OLAP-Daten für die Analyse in R. Sie können vorhandene MDX-Abfragen ausführen und einen R-Datenrahmen erhalten oder einfache MDX-Anweisungen erstellen, indem Sie Cubes, Achsen und Datenschnitte in R-Code erstellen. 
   
   Weitere Informationen finden Sie unter [Verwenden von Daten aus OLAP-Cubes in R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md).
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>Funktionen in SQL Server 2016 R Services und SQL Server vNext  
  
- Das **RevoScaleR**-Paket für schnelles, parallelisierbares maschinelles Lernen mit R.

-   Unterstützt sowohl SQL-Benutzernamen als auch eine integrierte Windows-Authentifizierung.  
    
-   Beträchtliche Leistungssteigerungen, einschließlich der Optimierung der SQL-Satellitenprozesse, die R und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbinden, Unterstützung für die Auslagerung von Daten, um die Verwendung großer Datenmengen zu ermöglichen, und das Streaming, um eine schnelle Verarbeitung von Milliarden von Zeilen möglich zu machen. 
  
-   Verwenden Sie SQL Server-Ressourcenpools, um von R-Prozessen verwendeten Arbeitsspeicher zu verwalten. Weitere Informationen finden Sie unter [ERSTELLEN SIE EXTERNE RESSOURCENPOOLS &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  

### <a name="tools-and-setup"></a>Tools und Setup

-   Einfache Installation aller Komponenten. Der Setup-Assistent für SQL Server kann entweder **SQL Server R Services (In-Database)** oder **Microsoft R Server (eigenständig)** installieren.   Beim Ausführen des Setup-Assistenten wählen Sie R Services, wenn Sie eine SQL Server-Instanz einrichten. Wählen Sie R-Server (eigenständig), wenn Sie eine Data Science-Arbeitsstation einrichten.   Weitere Informationen zu Setupoptionen finden Sie unter [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) oder [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  

-   Wenn Sie keine Daten in SQL Server verwenden müssen, sollten Sie sich für [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] entscheiden, das auf einer Vielzahl von Plattformen ausgeführt wird und eine unternehmensweite Skalierung und Leistung für die beliebte Open-Source-Sprache R bietet. [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]. Weitere Informationen finden Sie unter [R-Server &#40;eigenständig&#41;](../../advanced-analytics/r-services/r-server-standalone.md) bzw. [Introducing R Server (Einführung in R Server)](https://msdn.microsoft.com/microsoft-r/rserver) auf MSDN.

- Verwenden Sie das [Hilfsprogramm SqlBindR.exe](https://msdn.microsoft.com/library/mt791781.aspx), um Ihre SQL Server 2016-Instanz upzugraden, um Microsoft R Server 9.0.1 zu verwenden.  

- [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install) ist eine kostenlose R-Umgebung, die alle Tools und Bibliotheken umfasst, die Sie zum Erstellen von R-Lösungen benötigen, welche auf R Services oder R Server ausgeführt werden.  

-   R Tools für Visual Studio ist ein kostenloses Plug-In für Visual Studio mit umfangreicher Unterstützung für R, einschließlich standardmäßiger R-interaktiver und Variablenfenster, Intellisense für R-Funktionen, Debuggen und R Markdown, inklusive Export nach Word und HTML.  Weitere Informationen finden Sie unter [R Tools for Visual Studio (R-Tools für Visual Studio)](https://www.visualstudio.com/vs/rtvs/).  

## <a name="learn-more"></a>Weitere Informationen
  
-  Ressourcen sind sowohl für Datenwissenschaftler, die mehr über die Integration von SQL Server erfahren möchten, als auch für SQL-Entwickler, die nur mit T-SQL und der vertrauten Umgebung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] R-Lösungen erstellen möchten, verfügbar. 
   + [SQL Server R Services-Tutorials](https://msdn.microsoft.com/library/mt591993.aspx)
   + [Kostenloses e-Book: Data Science mit SQL Server 2016](https://mva.microsoft.com/ebooks/)
 
+ Empfehlenswert für gebrauchsfertige Lösungen sind auch die folgenden [machine learning templates (Machine Learning-Vorlagen)](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) des Microsoft Data Science-Teams, die praktische Lösungen für allgemeine analytische Aufgaben (einschließlich der vorbeugenden Wartung und der Abwanderungsprävention) veranschaulichen.
 

  
## <a name="see-also"></a>Siehe auch  
[Neues in SQL Server vNext](../../sql-server/what-s-new-in-sql-server-vnext.md)
  