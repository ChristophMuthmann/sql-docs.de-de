---
title: Editionen und unterstützte Funktionen von SQL Server 2017 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/10/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
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
ms.assetid: ''
caps.latest.revision: 121
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8f8d323562539f08ed75cb67f6b4e2aaa52a522
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="editions-and-supported-features-of-sql-server-2017"></a>Editionen und unterstützten Funktionen von SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Dieses Thema bietet detaillierte Informationen zu den von verschiedenen SQL Server 2017-Versionen unterstützten Funktionen. 

Informationen zu früheren Versionen finden Sie unter:

* [SQL Server 2016](editions-and-components-of-sql-server-2016.md).  
* [SQL Server 2014](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx).

  
Die Installationsanforderungen variieren je nach den benötigten Anwendungen. Die verschiedenen Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tragen den individuellen Leistungs-, Laufzeit- und Preisanforderungen von Organisationen und Einzelpersonen Rechnung. Welche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Komponenten Sie installieren, hängt auch von den individuellen Anforderungen ab. In den folgenden Abschnitten erfahren Sie, wie Sie die bestmögliche Auswahl unter den in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verfügbaren Editionen und Komponenten treffen.  

Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
  
Die neuesten Versionsanmerkungen und Informationen zu Neuerungen finden Sie über die folgenden Links:
- [SQL Server 2017 release notes (Versionsanmerkungen zu SQL Server 2017)](../sql-server/sql-server-2017-release-notes.md)
- [Neues in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)

### <a name="try-sql-server"></a>Testen Sie SQL Server!    
    
> [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/)**[Download SQL Server 2017 aus dem Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)**    

<!---    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**   
--->

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Editionen  
 In der folgenden Tabelle werden die Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]beschrieben. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Edition|Definition|  
|---------------------------------------|----------------|  
|Enterprise|Das Premium-Angebot, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition, übermittelt umfassende hochwertige Datencenterfunktionen mit blitzschneller Performance, unbegrenzter Virtualisierung und End-to-End Business Intelligence – und bietet so hohe Servicelevel für unternehmenswichtige Arbeitslasten und Endbenutzerzugriff auf Dateneinblicke.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition stellt eine grundlegende Datenverwaltungs- und Business Intelligence-Datenbank bereit, auf der Abteilungen und kleinere Unternehmen ihre Anwendungen ausführen. Diese unterstützt allgemeine Entwicklungstools für lokale und Cloudverwendung und ermöglicht eine effektive Datenbankverwaltung mit minimalen IT-Ressourcen.|  
|Web|Die[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition ist eine mit geringen Anschaffungs- und Betriebskosten verbundene Option für Webhoster und Web-VAPs, die kostengünstige Skalierbarkeit und Verwaltungsfunktionen für Webpräsenzen jeder Größe bietet.|  
|Entwickler|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition ermöglicht Entwicklern das Erstellen beliebiger Anwendungen auf der Basis von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sämtliche Funktionen der Enterprise Edition stehen zur Verfügung. Die Lizenz bezieht sich jedoch auf die Verwendung als Entwicklungs- und Testsystem und nicht als Produktionsserver. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer ist eine ideale Option zum Erstellen und Testen von Anwendungen.|  
|Express-Editionen|Die Express Edition ist eine kostenlose Datenbank auf Einstiegsebene und eignet sich ideal zum Üben und zum Erstellen von datengesteuerten Anwendungen für Desktopcomputer und kleine Server. Dies ist die beste Wahl für unabhängige Softwareanbieter, Entwickler und Tüftler, die Clientanwendungen erstellen. Wenn Sie erweiterte Datenbankfunktionen benötigen, können Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express nahtlos auf höhere Endversionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aktualisieren. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB, eine neue Lightweightversion von Express, die sämtliche Programmierbarkeitsfunktionen besitzt, wird im Benutzermodus ausgeführt und stellt eine schnelle, konfigurationsfreie Installation und eine kurze Liste an Voraussetzungen bereit.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>Verwenden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit einem Internetserver  
 Die Clienttools von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] werden normalerweise auf einem Internetserver, z. B. einem Server mit Microsoft Internetinformationsdienste (Internet Information Services, IIS), installiert. Die Clienttools enthalten die Clientkonnektivitätskomponenten, mit denen eine Anwendung eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]herstellt.  
  
>[!NOTE]
>Die Installation einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz auf einem Computer mit IIS ist zwar möglich, in der Praxis aber nur bei kleinen Websites üblich, die über einen einzigen Servercomputer verfügen. Bei den meisten Websites befindet sich das IIS-System mittlerer Ebene auf einem Server oder Servercluster, während die Datenbanken auf einem separaten Server oder einem vereinten System gespeichert werden.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Verwenden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit Client-/Server-Anwendungen  
 Sie können auch nur die Clientkomponenten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Computer mit Client-/Serveranwendungen installieren und so eine direkte Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz herstellen. Die Installation der Clientkomponenten ist auch dann eine gute Wahl, wenn Sie eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Datenbankserver verwalten, oder wenn Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anwendungen entwickeln möchten.  
  
 Die Clienttools-Option installiert die folgenden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Funktionen: Abwärtskompatibilitätskomponenten, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], Konnektivitätskomponenten, Verwaltungstools, Software Development Kit und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentations-Komponenten. Weitere Informationen finden Sie unter [Install SQL Server (Installieren von SQL Server)](../database-engine/install-windows/install-sql-server.md).  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>Auswählen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Komponenten  
 Auf der Seite Funktionsauswahl des Installationsassistenten für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] können Sie die Komponenten auswählen, die mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]installiert werden sollen. Standardmäßig sind in der Struktur keine Funktionen ausgewählt.  
  
 Anhand der Informationen aus den folgenden Tabellen können Sie ermitteln, welche Gruppe von Funktionen für Ihre Anforderungen am besten geeignet ist.  
  
|Serverkomponenten|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] beinhaltet das [!INCLUDE[ssDE](../includes/ssde-md.md)], den Basisdienst für Speichern, Verarbeiten und Sichern von Daten, Replikation, Volltextsuche, Tools zum Verwalten von relationalen und XML-Daten, Integration der In-Database-Analyse und Polybase-Integration für den Zugriff auf Hadoop und andere heterogene Datenquellen, sowie den [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] -Server (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] enthält Tools zum Erstellen und Verwalten der analytischen Onlineverarbeitung (OLAP, Online Analytical Processing) sowie Data Mining-Anwendungen.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] enthält Server- und Clientkomponenten, mit denen Berichte in Form einer Tabelle, Matrix, Grafik oder Freiform erstellt, verwaltet und bereitgestellt werden können. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ist gleichzeitig eine erweiterbare Plattform, die Sie zum Entwickeln von Berichtsanwendungen verwenden können.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt eine Gruppe grafischer Tools und programmierbarer Objekte zum Verschieben, Kopieren und Transformieren von Daten bereit. Es beinhaltet außerdem die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Komponente für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) ist die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Lösung für die Masterdatenverwaltung. MDS kann konfiguriert werden, um jede Domäne (Produkte, Kunden, Konten) zu verwalten und umfasst Hierarchien, präzise Sicherheit, Transaktionen, Datenversionsverwaltung und Geschäftsregeln sowie einen [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] , der verwendet werden kann, um Daten zu verwalten.|  
|Machine Learning-Dienste (datenbankintern)|Machine Learning-Dienste (datenbankintern) unterstützt verteilte, skalierbare Machine Learning-Lösungen mithilfe von Unternehmensdatenquellen. In SQL Server 2016 wurde die R-Sprache unterstützt. SQL Server-2017 unterstützt R und Python.|
|Machine Learning-Server (eigenständig)|Machine Learning-Server (eigenständig) unterstützt die Bereitstellung von verteilten, skalierbaren Machine Learning-Lösungen auf mehreren Plattformen und verwendet mehrere Unternehmensdatenquellen, einschließlich Linux, Hadoop und Teradata. In SQL Server 2016 wurde die R-Sprache unterstützt. SQL Server-2017 unterstützt R und Python.|

  
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

**Developer und Evaluation-Editionen**  
Von den Editionen Developer und Evaluation unterstützte Funktionen finden Sie in den Funktionen der Enterprise Edition von SQL Server in den folgenden Tabellen.

Die Developer Edition unterstützt weiterhin nur einen Client für [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Skalierungsgrenzen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne| 
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|  
|Maximaler Arbeitsspeicher für den Pufferpool pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Maximum des Betriebssystems|128 GB|64 GB|1410 MB|1410 MB|
|Maximaler Arbeitsspeicher für Columnstore-Segmentcache pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB| 16 GB| 352 MB| 352 MB|  
|Maximale speicheroptimierte Datengröße pro Datenbank in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB| 16 GB| 352 MB| 352 MB|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Maximum des Betriebssystems|Tabellarisch: 16 GB<br /><br /> MOLAP: 64 GB|–|–|–|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Maximum des Betriebssystems|64 GB|64 GB|4 GB|–|
|Maximale relationale Datenbankgröße|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> Die Enterprise Edition mit einer Lizenzierung auf der Grundlage von Serverlizenz + Clientzugriffslizenz (CAL) (für neue Verträge nicht verfügbar) ist auf maximal 20 Kerne pro SQL Server-Instanz beschränkt. Für das auf Prozessorkernen basierende Serverlizenzierungsmodell gelten keine Beschränkungen. Weitere Informationen finden Sie unter [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA">
            </a> RDBMS: Hochverfügbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core-Unterstützung <sup>1</sup>|ja|ja|ja|ja|ja|  
|Protokollversand|ja|ja|ja|nein|nein|  
|Datenbankspiegelung|ja|ja<br /><br /> Nur vollständige Sicherheit|Nur WITNESS|Nur WITNESS|Nur WITNESS| 
|Sicherungskomprimierung|ja|ja|nein|nein|nein| 
|Datenbankmomentaufnahme|ja|ja|ja|ja|ja|
|Always On-Failoverclusterinstanzen<sup>2</sup>|ja|ja|nein|nein|nein|  
|Always On-Verfügbarkeitsgruppen<sup>3</sup>|ja|nein|nein|nein|nein|
|Basis-Verfügbarkeitsgruppen<sup>4</sup>|nein|ja|nein|nein|nein|
|Onlineseiten- und Onlinedateiwiederherstellung|ja|nein|nein|nein|nein|
|Online-Indizierung|ja|nein|nein|nein|nein|
|Fortsetzbare Neuerstellung von online geschalteten Indizes|ja|nein|nein|nein|nein|
|Onlineschemaänderung|ja|nein|nein|nein|nein|
|Schnelle Wiederherstellung|ja|nein|nein|nein|nein|
|Gespiegelte Sicherungen|ja|nein|nein|nein|nein|
|Hinzufügen von Speicher im laufenden Systembetrieb und CPU|ja|nein|nein|nein|nein|
|Datenbankwiederherstellungsberater|ja|ja|ja|ja|ja|
|Verschlüsselte Sicherung|ja|ja|nein|nein|nein|
|Hybridsicherung in Windows Azure (Sicherung über URL)|ja|ja|nein|nein|nein|
|Verfügbarkeitsgruppe ohne Cluster|ja|ja|nein|nein|nein|nein|
|Mindestreplikate für Commitverfügbarkeitsgruppen|ja|ja|ja|nein|nein|nein|
  

<sup>1</sup> Weitere Informationen zum Installieren von SQL Server unter Server Core finden Sie unter [Install SQL Server on Server Core (Installieren von SQL unter Server Core)](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Bei der Enterprise Edition entspricht die Anzahl der Knoten dem Maximum des Betriebssystems. Bei der Standard Edition werden nur zwei Knoten unterstützt. 

<sup>3</sup> Bei der Enterprise Edition werden bis zu acht sekundäre Replikate unterstützt, einschließlich zwei synchronen sekundären Replikaten. 

<sup>4</sup> Bei der Standard Edition werden Basis-Verfügbarkeitsgruppen unterstützt. Eine Basis-Verfügbarkeitsgruppe unterstützt zwei Replikate mit einer Datenbank. Weitere Informationen über Basis-Verfügbarkeitsgruppen finden Sie unter [Basis-Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  


##  <a name="RDBMSSP"></a> RDBMS: Skalierbarkeit und Leistung  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|ja|ja|ja|ja|ja|  
|Große Objektbinärdateien in gruppierten Columnstore-Indizes|ja|ja|ja|ja|ja|  
|Onlineneuerstellung für nicht gruppierten Columnstore-Index|ja|nein|nein|nein|nein|
|In-Memory-OLTP <sup>1</sup>|ja|ja|ja|Ja, <sup>2</sup>|ja|
|Stretch-Datenbank|ja|ja|ja|ja|ja|
|Persistenter Hauptspeicher|ja|ja|ja|ja|ja|
|Unterstützung mehrerer Instanzen|50|50|50|50|50|
|Tabellen- und Indexpartitionierung|ja|ja|ja|ja|ja|  
|Datenkomprimierung|ja|ja|ja|ja|ja|
|Ressourcenkontrolle|ja|nein|nein|nein|nein|  
|Parallelverarbeitung für partitionierte Tabellen|ja|nein|nein|nein|nein|
|Mehrere FILESTREAM-Container|ja|ja|ja|ja|ja|
|NUMA-basierter und großer Arbeitsspeicher für umfangreiche Seiten und Zuordnung von Pufferarrays|ja|nein|nein|nein|nein|
|Pufferpoolerweiterung|ja|ja|nein|nein|nein|
|Ressourcenkontrolle für E/A-Vorgänge|ja|nein|nein|nein|nein|  
|Verzögerte Dauerhaftigkeit|ja|ja|ja|ja|ja|
|Automatische Optimierung|ja|nein|nein|nein|nein|
|Adaptive Joins im Batchmodus|ja|nein|nein|nein|nein|
|Feedback zur Speicherzuweisung im Batchmodus|ja|nein|nein|nein|nein|
|Verschachtelte Ausführung mit Tabellenwertfunktionen mit mehreren Anweisungen|ja|ja|ja|ja|ja|
|Verbesserungen beim massenhaften Einfügen|ja|ja|ja|ja|ja|


<sup>1</sup> Die Größe der In-Memory OLTP-Daten und des Columnstore-Segmentcaches sind auf die Größe des Arbeitsspeichers beschränkt, die von der Edition im Bereich Kapazitätsgrenzen festgelegt wird. Den maximale Grad an Parallelität ist beschränkt. Der Grad an Prozessparallelität (Degree of Parallelism, DOP) für eine Indexerstellung ist auf 2 DOP für die Standard Edition und auf 1 DOP für die Web und die Express Edition beschränkt. Dies gilt für Columnstore-Indizes, die über datenträgerbasierte Tabellen und speicheroptimierte Tabellen erstellt wurden.

<sup>2</sup> Diese Funktion ist in der LocalDB-Installationsoption nicht enthalten.

##  <a name="RDBMSS"></a> RDBMS: Sicherheit  
  
|Funktion|Enterprise|Standard|Web|Express|Express mit Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Sicherheit auf Zeilenebene|ja|ja|ja|ja|ja|  
|Always Encrypted|ja|ja|ja|ja|ja| 
|Dynamische Datenmaskierung|ja|ja|ja|ja|ja|   
|Allgemeine Überwachung|ja|ja|ja|ja|ja| 
|Feine Überwachung|ja|ja|ja|ja|ja| 
|Transparente Datenbankverschlüsselung|ja|nein|nein|nein|nein|   
|Erweiterbare Schlüsselverwaltung|ja|nein|nein|nein|nein| 
|Benutzerdefinierte Rollen|ja|ja|ja|ja|ja| 
|Eigenständige Datenbanken|ja|ja|ja|ja|ja| 
|Verschlüsselung von Sicherungen|ja|ja|nein|nein|nein|  

##  <a name="Replication"></a> Replication  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Heterogene Abonnenten|ja|ja|nein|nein|nein|  
|Mergereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Veröffentlichungen mit Oracle|ja|nein|nein|nein|nein| 
|Peer-zu-Peer-Transaktionsreplikation|ja|nein|nein|nein|nein|   
|Momentaufnahmereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|SQL Server-Änderungsnachverfolgung|ja|ja|ja|ja|ja| 
|Transaktionsreplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Transaktionsreplikation zu Azure|ja|ja|nein|nein|nein|   
|Aktualisierbares Abonnement für Transaktionsreplikation|ja|nein|nein|nein|nein|  
  
##  <a name="SSMS"></a> Verwaltungstools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|ja|ja|ja|ja|ja|  
|SQL-Konfigurations-Manager|ja|ja|ja|ja|ja|   
|SQL CMD (Command Prompt Tool – Eingabeaufforderungstool)|ja|ja|ja|ja|ja|      
|Distributed Replay: Administratortool|ja|ja|ja|ja|nein|  
|Distributed Replay – Client|ja|ja|ja|nein|nein|  
|Distributed Replay - Controller|Ja (bis zu 16 Clients)|Ja (1 Client)|Ja (1 Client)|nein|nein|   
|SQL Profiler|ja|ja|Nein <sup>1</sup>|Nein <sup>1</sup>|Nein <sup>1</sup>|  
|SQL Server-Agent|ja|ja|ja|nein|nein| 
|Microsoft System Center Operations Manager Management Pack|ja|ja|ja|nein|nein|  
|Datenbankoptimierungsratgeber (DTA)|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|nein|nein|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express mit Tools und SQL Server Express mit Advanced Services können mit der SQL Server Standard- und SQL Server Enterprise-Edition profiliert werden.  
  
 <sup>2</sup> Optimierung ist nur in Funktionen der Standard Edition aktiviert.  
  
##  <a name="RDBMSM"></a> RDBMS: Verwaltbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Benutzerinstanzen|nein|nein|nein|ja|ja| 
|LocalDB|nein|nein|nein|ja|nein| 
|Dedizierte Administratorverbindung|ja|ja|ja|Ja, mit Ablaufverfolgungsflag|Ja, mit Ablaufverfolgungsflag|   
|SysPrep-Unterstützung <sup>1</sup>|ja|ja|ja|ja|ja| 
|PowerShell-Skriptunterstützung<sup>2</sup>|ja|ja|ja|ja|ja| 
|Unterstützung für Komponentenvorgänge der Datenschichtanwendung: Extrahieren, Bereitstellen, Aktualisieren, Löschen|ja|ja|ja|ja|ja| 
|Richtlinienautomatisierung (Überprüfung nach Zeitplan und Änderungen)|ja|ja|ja|nein|nein|   
|Sammler von Leistungsdaten|ja|ja|ja|nein|nein| 
|Fähigkeit zur Registrierung als verwaltete Instanz in einer Mehrfachinstanzverwaltung|ja|ja|ja|nein|nein|   
|Standardleistungsberichte|ja|ja|ja|nein|nein| 
|Planhinweislisten und Planeinfrierung für Planhinweislisten|ja|ja|ja|nein|nein|   
|Direkte Abfrage von indizierten Sichten (mittels NOEXPAND-Hinweis)|ja|ja|ja|ja|ja| 
|Automatische Wartung für indizierte Sichten|ja|ja|ja|nein|nein| 
|Verteilte partitionierte Sichten|ja|nein|nein|nein|nein| 
|Parallele Indexvorgänge|ja|nein|nein|nein|nein|  
|Automatische Verwendung indizierter Sichten mittels Abfrageoptimierer|ja|nein|nein|nein|nein| 
|Parallele Konsistenzprüfung|ja|nein|nein|nein|nein| 
|SQL Server-Steuerungspunkt für das Hilfsprogramm|ja|nein|nein|nein|nein|    
|Pufferpoolerweiterung|ja|ja|nein|nein|nein| 
  
 <sup>1</sup> Weitere Informationen finden Sie unter [Überlegungen zur Installation von SQL Server mit SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
 <sup>2</sup> Unter Linux werden PowerShell-Skripts von Windows-Computern unterstützt, die SQL Server unter Linux als Ziel verwenden. 
##  <a name="DevTools"></a> Entwicklungstools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integration in Microsoft Visual Studio|ja|ja|ja|ja|ja| 
|IntelliSense (Transact-SQL und MDX)|ja|ja|ja|ja|ja| 
|SQL Server Data Tools (SSDT)|ja|ja|ja|ja|nein|    
|MDX-Bearbeitungs-, MDX-Debug- und MDX-Entwurfstools|ja|ja|nein|nein|nein|   
  
##  <a name="Programmability"></a> Programmability  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Grundlegende Integration von R|ja|ja|ja|ja|nein|   
|Erweiterte Integration von R|ja|nein|nein|nein|nein| 
|Grundlegende Integration von Python|ja|ja|ja|ja|nein|
|Erweiterte Integration von Python|ja|nein|nein|nein|nein| 
|Machine Learning-Server (eigenständig)|ja|nein|nein|nein|nein|   
|PolyBase-Computeknoten|ja|Ja <sup>1</sup>|Ja <sup>1</sup>, <sup>2</sup>|Ja <sup>1</sup>,|Ja <sup>1</sup>, | 
|PolyBase-Hauptknoten|ja|nein|nein|nein|nein| 
|JSON|ja|ja|ja|ja|ja|   
|Abfragespeicher|ja|ja|ja|ja|ja|   
|Temporal|ja|ja|ja|ja|ja|   
|Common Language Runtime (CLR)-Integration|ja|ja|ja|ja|ja|   
|Systemeigene XML-Unterstützung|ja|ja|ja|ja|ja| 
|XML-Indizierung|ja|ja|ja|ja|ja| 
|MERGE- und UPSERT-Funktionen|ja|ja|ja|ja|ja|   
|FILESTREAM-Unterstützung|ja|ja|ja|ja|ja| 
|FileTable|ja|ja|ja|ja|ja| 
|Datums- und Uhrzeitdatentypen|ja|ja|ja|ja|ja|  
|Internationalisierungsunterstützung|ja|ja|ja|ja|ja| 
|Volltextsuche und semantische Suche|ja|ja|ja|ja|nein| 
|Angabe der Sprache in einer Abfrage|ja|ja|ja|ja|nein|   
|Service Broker (Messaging)|ja|ja|Nein (nur Client)|Nein (nur Client)|Nein (nur Client)|   
|Transact-SQL-Endpunkte|ja|ja|ja|nein|nein| 
|Diagramm|ja|ja|ja|ja|ja|  


<sup>1</sup> Horizontale Skalierung mit mehreren Computeknoten erfordert einen Hauptknoten.

## <a name="IS"></a> Integration Services

Informationen zu SSIS-Features (SQL Server Integration Services), die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] unterstützt werden, finden Sie unter [Von den SQL Server-Editionen unterstützte Integration Services-Features](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="MDS"></a> Master Data Services  
 Informationen über die [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] - und Data Quality Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)]unterstützt werden, finden Sie unter [Master Data Services and Data Quality Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server 2016 unterstützte Master Data Services- und Data Quality Services-Features)](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="DW"></a> Data Warehouse  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Erstellen von Cubes ohne Datenbank|ja|ja|nein|nein|nein |   
|Automatisches Generieren von Staging- und Data Warehouse-Schemas|ja|ja|nein|nein|nein| 
|Change Data Capture|ja|ja|nein|nein|nein| 
|Optimierung von Sternjoin-Abfragen|ja|nein|nein|nein|nein| 
|Skalierbare schreibgeschützte Analysis Services-Konfiguration|ja|nein|nein|nein|nein| 
|Parallele Abfrageverarbeitung bei partitionierten Tabellen und Indizes|ja|nein|nein|nein|nein|   
|Globale Batchaggregation|ja|nein|nein|nein|nein| 

##  <a name="SSAS"></a> Analysis Services  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services-Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="BIMD"></a> BI-Semantikmodell (mehrdimensional)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services-Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="BIT"></a> BI-Semantikmodell (tabellarisch)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services-Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
Informationen über die Power Pivot for SharePoint-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services-Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="DM"></a> Data Mining  
  
Informationen über die Data Mining-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services-Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SSRS"></a> Reporting Services  
  
Informationen über die Reporting Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Reporting Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Reporting Services-Features)](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="BIC"></a> Business Intelligence-Clients  

Informationen über die Business Intelligence-Clientfeatures, die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] unterstützt werden, finden Sie unter [Analysis Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Analysis Services Features)](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) oder [Reporting Services Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Reporting Services Features)](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SLS"></a> Räumliche und ortsbezogene Dienste  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Räumlichkeitsindizes|ja|ja|ja|ja|ja|   
|Planarer und geodätischer Datentyp|ja|ja|ja|ja|ja| 
|Erweiterte räumliche Bibliotheken|ja|ja|ja|ja|ja|   
|Importieren/Exportieren räumlicher Industriestandard-Datenformate|ja|ja|ja|ja|ja|   
  
##  <a name="ADS"></a> Weitere Datenbankdienste  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|ja|ja|ja|ja|ja|   
|Datenbank-E-Mail|ja|ja|ja|nein|nein| 
  
##  <a name="Other"></a> Andere Komponenten  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium-Edition|StreamInsight Standard-Edition|StreamInsight Standard-Edition|nein|nein| 
|StreamInsight HA|StreamInsight Premium-Edition|nein|nein|nein|nein|   

> [![Herunterladen von SSMS](../analysis-services/media/download.png)](../ssms/download-sql-server-management-studio-ssms.md) Laden Sie die neueste Version von **[SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) herunter.**     
  
## <a name="next-steps"></a>Nächste Schritte 
 [Product Specifications for SQL Server (Produktspezifikationen für SQL Server 2016)](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Installation for SQL Server (Installation für SQLServer 2016)](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 
 [!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]