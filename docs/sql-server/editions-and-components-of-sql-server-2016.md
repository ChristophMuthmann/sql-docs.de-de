---
title: Editionen und Komponenten von SQL Server 2016| Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 12/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
caps.latest.revision: 121
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6309d4840e29a6768347cab459c41f0b1d1d8601
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-components-of-sql-server-2016"></a>Editionen und Komponenten von SQL Server 2016
> Weitere Informationen zu Funktionen, die von den verschiedenen Editionen von SQL Server 2016 unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../sql-server/editions-and-supported-features-for-sql-server-2016.md).

  Die Installationsanforderungen variieren je nach den benötigten Anwendungen. Die verschiedenen Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tragen den individuellen Leistungs-, Laufzeit- und Preisanforderungen von Organisationen und Einzelpersonen Rechnung. Welche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Komponenten Sie installieren, hängt auch von den individuellen Anforderungen ab. In den folgenden Abschnitten erfahren Sie, wie Sie die bestmögliche Auswahl unter den in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verfügbaren Editionen und Komponenten treffen.  
  
## <a name="includesscurrentincludessscurrent-mdmd-editions"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Editionen  
 In der folgenden Tabelle werden die Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]beschrieben. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Edition|Definition|  
|---------------------------------------|----------------|  
|Enterprise|Das Premium-Angebot, [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise Edition, übermittelt umfassende hochwertige Datencenterfunktionen mit blitzschneller Performance, unbegrenzter Virtualisierung und End-to-End Business Intelligence – und bietet so hohe Servicelevel für unternehmenswichtige Arbeitslasten und Endbenutzerzugriff auf Dateneinblicke.|  
|Standard|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard Edition stellt eine grundlegende Datenverwaltungs- und Business Intelligence-Datenbank bereit, auf der Abteilungen und kleinere Unternehmen ihre Anwendungen ausführen. Diese unterstützt allgemeine Entwicklungstools für lokale und Cloudverwendung und ermöglicht eine effektive Datenbankverwaltung mit minimalen IT-Ressourcen.|  
|Web|Die[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web Edition ist eine mit geringen Anschaffungs- und Betriebskosten verbundene Option für Webhoster und Web-VAPs, die kostengünstige Skalierbarkeit und Verwaltungsfunktionen für Webpräsenzen jeder Größe bietet.|  
|Entwickler|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer Edition ermöglicht Entwicklern das Erstellen beliebiger Anwendungen auf der Basis von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sämtliche Funktionen der Enterprise Edition stehen zur Verfügung. Die Lizenz bezieht sich jedoch auf die Verwendung als Entwicklungs- und Testsystem und nicht als Produktionsserver. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer ist eine ideale Option zum Erstellen<br />                [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] und Testen von Anwendungen.|  
|Express-Editionen|Die Express Edition ist eine kostenlose Edition auf Einstiegsebene und eignet sich ideal zum Üben und zum Erstellen von datengesteuerten Anwendungen für Desktopcomputer und kleine Server. Dies ist die beste Wahl für unabhängige Softwareanbieter, Entwickler und Tüftler, die Clientanwendungen erstellen. Wenn Sie erweiterte Datenbankfunktionen benötigen, können Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express nahtlos auf höhere Endversionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aktualisieren. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB, eine neue Light-Version von Express, die sämtliche Programmierbarkeitsfunktionen besitzt, wird noch im Benutzermodus ausgeführt und bietet eine schnelle, konfigurationsfreie Installation und eine kurze Liste an Voraussetzungen.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>Verwenden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit einem Internetserver  
 Die Clienttools von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] werden normalerweise auf einem Internetserver, z. B. einem Server mit Microsoft Internetinformationsdienste (Internet Information Services, IIS), installiert. Die Clienttools enthalten die Clientkonnektivitätskomponenten, mit denen eine Anwendung eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]herstellt.  
  
> **HINWEIS:**  Die Installation einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz auf einem Computer mit IIS ist zwar möglich, in der Praxis aber nur bei kleinen Websites üblich, die einen einzigen Servercomputer haben. Bei den meisten Websites befindet sich das IIS-System mittlerer Ebene auf einem Server oder Servercluster, während die Datenbanken auf einem separaten Server oder einem vereinten System gespeichert werden.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Verwenden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit Client/Server-Anwendungen  
 Sie können auch nur die Clientkomponenten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Computer mit Client-/Serveranwendungen installieren und so eine direkte Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz herstellen. Die Installation der Clientkomponenten ist auch dann eine gute Wahl, wenn Sie eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Datenbankserver verwalten, oder wenn Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anwendungen entwickeln möchten.  
  
 Die Clienttools-Option installiert die folgenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Funktionen: Abwärtskompatibilitätskomponenten, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], Konnektivitätskomponenten, Verwaltungstools, Software Development Kit und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentations-Komponenten. Weitere Informationen finden Sie unter  [Installieren von SQL Server 2016](../database-engine/install-windows/install-sql-server.md).  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>Auswählen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Komponenten  
 Auf der Seite Funktionsauswahl des Installationsassistenten für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] können Sie die Komponenten auswählen, die mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]installiert werden sollen. Standardmäßig sind in der Struktur keine Funktionen ausgewählt.  
  
 Anhand der Informationen aus den folgenden Tabellen können Sie ermitteln, welche Gruppe von Funktionen für Ihre Anforderungen am besten geeignet ist.  
  
|Serverkomponenten|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] beinhaltet das [!INCLUDE[ssDE](../includes/ssde-md.md)], den Basisdienst für Speichern, Verarbeiten und Sichern von Daten, Replikation, Volltextsuche, Tools zum Verwalten von relationalen und XML-Daten, Integration der In-Database-Analyse und Polybase-Integration für den Zugriff auf Hadoop und andere heterogene Datenquellen, sowie den [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] -Server (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] enthält Tools zum Erstellen und Verwalten der analytischen Onlineverarbeitung (OLAP, Online Analytical Processing) sowie Data Mining-Anwendungen.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] enthält Server- und Clientkomponenten, mit denen Berichte in Form einer Tabelle, Matrix, Grafik oder Freiform erstellt, verwaltet und bereitgestellt werden können. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ist gleichzeitig eine erweiterbare Plattform, die Sie zum Entwickeln von Berichtsanwendungen verwenden können.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt eine Gruppe grafischer Tools und programmierbarer Objekte zum Verschieben, Kopieren und Transformieren von Daten bereit. Es beinhaltet außerdem die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Komponente für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) ist die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Lösung für die Masterdatenverwaltung. MDS kann konfiguriert werden, um jede Domäne (Produkte, Kunden, Konten) zu verwalten und umfasst Hierarchien, präzise Sicherheit, Transaktionen, Datenversionsverwaltung und Geschäftsregeln sowie einen [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] , der verwendet werden kann, um Daten zu verwalten.|  
|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] unterstützt verteilte, skalierbare R-Lösungen auf mehreren Plattformen und verwendet mehrere Enterprise-Datenquellen einschließlich Linux, Hadoop und Teradata.|  
  
|Verwaltungstools|Description|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] bietet eine integrierte Umgebung, in der Sie auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Komponenten zugreifen sowie diese konfigurieren, verwalten und entwickeln können. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ermöglicht Entwicklern und Administratoren mit unterschiedlichen Fähigkeiten die Verwendung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Zur Installation herunterladen können Sie <br />                [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] hier:  [Herunterladen von SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Konfigurations-Manager stellt eine einfache Konfigurationsverwaltung für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Dienste, Server- und Clientprotokolle sowie Clientaliase bereit.|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] stellt eine grafische Benutzeroberfläche zum Überwachen einer Instanz von [!INCLUDE[ssDE](../includes/ssde-md.md)] oder [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]bereit.|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] -Optimierungsratgeber|Der Optimierungsratgeber für[!INCLUDE[ssDE](../includes/ssde-md.md)] unterstützt Sie beim Erstellen einer optimalen Menge von Indizes, indizierten Sichten und Partitionen.|  
|Data Quality Client|Stellt eine sehr einfache und intuitive grafische Benutzeroberfläche bereit, um eine Verbindung mit dem DQS-Server herzustellen und Datenbereinigungsvorgänge auszuführen. Diese Komponente ermöglicht außerdem die zentrale Überwachung verschiedener Aktivitäten, die während des Datenbereinigungsvorgangs ausgeführt werden.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] bietet eine IDE zum Erstellen von Lösungen für die Business Intelligence-Komponenten: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]und [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (Früher Business Intelligence Development Studio genannt).<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] schließt auch "Datenbankprojekte" ein, die eine integrierte Umgebung für Datenbankentwickler bereitstellen, die ihre ganze Datenbankentwurfsarbeit für eine beliebige [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Plattform (sowohl vor Ort als auch remote) in Visual Studio ausführen möchten. Datenbankentwickler können den verbesserten Server-Explorer in Visual Studio verwenden, um Datenbankobjekte und Daten einfach zu erstellen oder zu bearbeiten und Abfragen auszuführen.|  
|Konnektivitätskomponenten|Installiert Komponenten für die Kommunikation zwischen Clients und Servern, einschließlich Netzwerkbibliotheken für die DB-Library, ODBC und OLE DB.|  
  
|Dokumentation|Description|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation|Kerndokumentation für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
  

