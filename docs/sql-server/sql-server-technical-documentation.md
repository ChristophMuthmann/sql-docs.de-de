---
title: Technische Dokumentation zu SQL Server | Microsoft-Dokumentation
ms.date: 07/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: 106
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b2f5d26757bd436cfd21076b2a4899376ee60c9f
ms.openlocfilehash: 56d4c398f8dc26f00e2d0dc26fb41a3089ea0ebf
ms.contentlocale: de-de
ms.lasthandoff: 08/04/2017

---
# <a name="sql-server-technical-documentation"></a>Technische Dokumentation zu SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Installation für SQL Server 2014](https://msdn.microsoft.com/en-US/library/bb500469(SQL.120).aspx).

 Dokumentation, die Sie beim Installieren, Konfigurieren und Verwenden von SQL Server unterstützt. Die Inhalte umfassen End-to-End-Beispiele, Codebeispiele und Videos. Weitere Informationen über [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] -Sprachthemen finden Sie unter [Sprachreferenz](../t-sql/language-reference.md).

 

**SQL Server 2017**

- [Versionsanmerkungen zu SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)
- [Neues in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)


**SQL Server 2016**
 
- [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Neues in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **Probieren Sie SQL Server aus!**    
 - [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  Download [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] aus dem **[Evaluation Center](http://go.microsoft.com/fwlink/?LinkID=829477)** 
 - [**Herunterladen von SQL Server 2016 aus dem Evaluierungscenter**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
 - **[Starten eines virtuellen Computers mit bereits installiertem SQL Server 2016](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
 - **[Download the latest version of SQL Server Management Studio (SSMS) (Laden Sie die neueste Version von SQL Server Management Studio (SSMS) herunter)](https://msdn.microsoft.com/library/mt238290.aspx)**   
      
## <a name="sql-server-technologies"></a>SQL Server-Technologien    
    
|||    
|-|-|    
|![SQL-Datenbankmodul](../sql-server/media/sql-database-engine.png "SQL-Datenbankmodul")|**[Datenbankmodul](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> Das Datenbankmodul ist der Kerndienst zum Speichern, Verarbeiten und Sichern von Daten. Das Datenbankmodul stellt kontrollierten Zugriff und schnelle Transaktionsverarbeitung bereit. So können Sie auch hohe Anforderungen von Daten verarbeitenden Anwendungen in Ihrem Unternehmen zu erfüllen. Das Datenbankmodul stellt darüber hinaus vielfältige Unterstützung für die Aufrechterhaltung hoher Verfügbarkeit bereit.|    
|![R Server](../sql-server/media/r-server.png "R Server")|**[Machine Learning Services (Machine Learning-Dienste)](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft Machine Learning Services unterstützt die Integration von Machine Learning in Unternehmensworkflows mithilfe der gängigen Sprachen R und Python.<br /><br /> Machine Learning-Dienste (datenbankintern) integriert R und Python in SQL Server, wodurch das Erstellen, Trainieren und Bewerten von Modellen durch das Aufrufen gespeicherter Prozeduren erleichtert wird.<br /><br /> Microsoft Machine Learning Server stellt eine unternehmensweite Unterstützung für R und Python zur Verfügung, ohne dass SQL Server erforderlich ist.|    
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) stellt eine wissensgesteuerte Datenbereinigungslösung bereit. DQS ermöglicht das Erstellen einer Knowledge Base und die anschließende Verwendung dieser Knowledge Base zum Durchführen der Datenkorrektur und Deduplizierung für Ihre Daten mithilfe von computerunterstützten und interaktiven Mitteln. Sie können Cloud-basierte Verweisdatendienste verwenden und eine Datenverwaltungslösung erstellen, die DQS in SQL Server Integration Services und Master Data Services integriert.|    
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ist eine Plattform für das Entwickeln von Hochleistungslösungen im Bereich Datenintegration, einschließlich Paketen zum Extrahieren, Transformieren und Laden (ETL) von Daten für den Data Warehouse-Betrieb.|    
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ist die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Lösung für die Masterdatenverwaltung. Eine auf [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] erstellte Lösung gewährleistet, dass Berichterstellung und Analyse auf den richtigen Informationen basieren. Mit [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]erstellen Sie ein zentrales Repository für Masterdaten und verwalten einen überwachungs- und sicherungsfähigen Datensatz dieser Daten, die sich im Laufe der Zeit ändern.|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] ist eine Plattform für analytische Daten und ein Business Intelligence-Toolset für Einzelpersonen, Teams und Unternehmen. Server- und Clientdesigner unterstützen herkömmliche OLAP-Lösungen, neue Tabellenmodellierungslösungen sowie Self-Service-Funktionen für die Analyse und Zusammenarbeit mit [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], Excel und einer SharePoint Server-Umgebung. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ermöglicht zudem Data Mining, damit Sie die Muster und Beziehungen erkennen können, die in großen Datenvolumen versteckt sind.|    
|![Replikationsdienste](../sql-server/media/replication-services.png "Replikationsdienste")|**[Replikation](../relational-databases/replication/sql-server-replication.md)**<br /><br /> Bei der Replikation handelt es sich um eine Reihe von Technologien zum Kopieren und Verteilen von Daten und Datenbankobjekten aus einer Datenbank in eine andere und das anschließende Synchronisieren der Datenbanken, um die Konsistenz der Daten sicherzustellen. Mithilfe der Replikation können Sie Daten an verschiedene Standorte, an Remotebenutzer oder mobile Benutzer über lokale Netzwerke und WANs (Wide Area Network), über DFÜ-Verbindungen, Funk-Verbindungen oder über das Internet verteilen.|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services liefert webbasierte Berichterstellungsfunktionalität für Unternehmen, sodass Sie Berichte erstellen, die Inhalte aus einer Vielzahl von Datenquellen ziehen, Berichte in verschiedenen Formaten veröffentlichen und Abonnements und Sicherheit zentral verwalten können.|    

    
## <a name="earlier-sql-server-versions"></a>Frühere SQL Server-Versionen
- [Onlinedokumentation für SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [Installieren von SQL Server 2014 Express und anderen älteren Versionen von SQL Server](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx). (**Vielen Dank an [Scott Hanselman](http://www.hanselman.com/) für das Sammeln aller Installer-Paketlinks an einem Ort!**)  
- [Technische Dokumentation zu SQL Server 2012](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [SQL Server 2008 R2-Produktdokumentation](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [Technische Dokumentation zu SQL Server 2008](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [Archivierte Dokumentation zu SQL Server 2005](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

**Beispieldatenbanken**  
- [Beispieldatenbank von Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [AdventureWorks-Beispieldatenbanken und Skripts für SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=49502) 
- [SQL Server-Beispiele bei GitHub](https://github.com/Microsoft/sql-server-samples) 
   
 ## <a name="more-information"></a>Weitere Informationen   
+ Sie finden SQL Server-Dokumentationen auch offline, indem Sie den Help Viewer verwenden. Weitere Informationen finden Sie unter [Help Viewer für SQL Server](../release-notes/sql-server-help-installation.md).
+ [SQL Server-Konfigurations-Manager](../relational-databases/sql-server-configuration-manager.md)
+ Das[SQL Server-Update Center](https://msdn.microsoft.com/library/ff803383.aspx) enthält Links und Informationen für alle unterstützten Versionen. 
+ [Installieren des SQL Server-Datenbankmoduls](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [Installieren von SQL Server-Verwaltungstools mit SSMS](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/mt186501.aspx)
+ [Videos, Beispiele und Communityressourcen](https://msdn.microsoft.com/library/dn237258.aspx)
  
##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Kontaktaufnahme mit dem SQL Server-Entwicklungsteam 
- [Stack Overflow (Tag „sql-server“): Anlaufstelle für technische Fragen](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN-Foren: Anlaufstelle für technische Fragen](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: Meldung von Programmfehlern und Vorschlagen von Features](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – allgemeine Erläuterung zu SQL Server](https://www.reddit.com/r/SQLServer/)
